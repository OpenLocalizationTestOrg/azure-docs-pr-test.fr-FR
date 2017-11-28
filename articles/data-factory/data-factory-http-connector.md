---
title: "aaaMove des données à partir d’une source HTTP - Azure | Documents Microsoft"
description: "En savoir plus sur la façon dont la source de données toomove à partir d’un site local ou un cloud HTTP à l’aide d’Azure Data Factory."
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
ms.openlocfilehash: e39b9cbff870aef4be91938cacff39a2fd12d64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a><span data-ttu-id="363e5-103">Déplacer des données à partir d’une source HTTP à l’aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="363e5-103">Move data from an HTTP source using Azure Data Factory</span></span>
<span data-ttu-id="363e5-104">Cet article décrit comment toouse hello activité de copie de données Azure Data Factory toomove un tooa de point de terminaison HTTP sur le site/cloud prises en charge le magasin de données récepteur.</span><span class="sxs-lookup"><span data-stu-id="363e5-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises/cloud HTTP endpoint tooa supported sink data store.</span></span> <span data-ttu-id="363e5-105">Cet article s’appuie sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article qui présente une vue d’ensemble du déplacement des données avec la liste des activités et hello copie de banques de données pris en charge en tant que sources/récepteurs.</span><span class="sxs-lookup"><span data-stu-id="363e5-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="363e5-106">Fabrique de données actuellement prend en charge uniquement déplacement de données à partir d’un HTTP source tooother des magasins de données, mais ne pas déplacer les données à partir d’autres données stocke tooan HTTP destination.</span><span class="sxs-lookup"><span data-stu-id="363e5-106">Data factory currently supports only moving data from an HTTP source tooother data stores, but not moving data from other data stores tooan HTTP destination.</span></span>

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="363e5-107">Scénarios et types d’authentification pris en charge</span><span class="sxs-lookup"><span data-stu-id="363e5-107">Supported scenarios and authentication types</span></span>
<span data-ttu-id="363e5-108">Vous pouvez utiliser ces données de tooretrieve du connecteur HTTP à partir de **cloud et locales point de terminaison HTTP/s** à l’aide de HTTP **obtenir** ou **POST** (méthode).</span><span class="sxs-lookup"><span data-stu-id="363e5-108">You can use this HTTP connector tooretrieve data from **both cloud and on-premises HTTP/s endpoint** by using HTTP **GET** or **POST** method.</span></span> <span data-ttu-id="363e5-109">Hello, les types d’authentification suivants est pris en charge : **anonyme**, **base**, **Digest**, **Windows**, et  **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="363e5-109">hello following authentication types are supported: **Anonymous**, **Basic**, **Digest**, **Windows**, and **ClientCertificate**.</span></span> <span data-ttu-id="363e5-110">Notez la différence de hello entre ce connecteur et le hello [connecteur de table Web](data-factory-web-table-connector.md) est : hello ce dernier est utilisé tooextract table de contenu à partir de page web HTML.</span><span class="sxs-lookup"><span data-stu-id="363e5-110">Note hello difference between this connector and hello [Web table connector](data-factory-web-table-connector.md) is: hello latter is used tooextract table content from web HTML page.</span></span>

<span data-ttu-id="363e5-111">Lors de la copie des données à partir d’un point de terminaison HTTP local, vous devez installer une passerelle de gestion des données dans hello local environnement/Azure VM.</span><span class="sxs-lookup"><span data-stu-id="363e5-111">When copying data from an on-premises HTTP endpoint, you need install a Data Management Gateway in hello on-premises environment/Azure VM.</span></span> <span data-ttu-id="363e5-112">Consultez [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn l’article sur la passerelle de gestion des données et des instructions détaillées sur la configuration de passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="363e5-112">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="363e5-113">Prise en main</span><span class="sxs-lookup"><span data-stu-id="363e5-113">Getting started</span></span>
<span data-ttu-id="363e5-114">Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’une source HTTP à l’aide de différents outils/API.</span><span class="sxs-lookup"><span data-stu-id="363e5-114">You can create a pipeline with a copy activity that moves data from an HTTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="363e5-115">toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**.</span><span class="sxs-lookup"><span data-stu-id="363e5-115">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="363e5-116">Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.</span><span class="sxs-lookup"><span data-stu-id="363e5-116">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

- <span data-ttu-id="363e5-117">Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**.</span><span class="sxs-lookup"><span data-stu-id="363e5-117">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="363e5-118">Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="363e5-118">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> <span data-ttu-id="363e5-119">Pour JSON échantillonne les données de toocopy à partir de la source HTTP tooAzure stockage d’objets Blob, consultez [exemples JSON](#json-examples) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="363e5-119">For JSON samples toocopy data from HTTP source tooAzure Blob Storage, see [JSON examples](#json-examples) section of this articles.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="363e5-120">Propriétés du service lié</span><span class="sxs-lookup"><span data-stu-id="363e5-120">Linked service properties</span></span>
<span data-ttu-id="363e5-121">Hello tableau suivant fournit la description du service de tooHTTP spécifique lié éléments JSON.</span><span class="sxs-lookup"><span data-stu-id="363e5-121">hello following table provides description for JSON elements specific tooHTTP linked service.</span></span>

| <span data-ttu-id="363e5-122">Propriété</span><span class="sxs-lookup"><span data-stu-id="363e5-122">Property</span></span> | <span data-ttu-id="363e5-123">Description</span><span class="sxs-lookup"><span data-stu-id="363e5-123">Description</span></span> | <span data-ttu-id="363e5-124">Requis</span><span class="sxs-lookup"><span data-stu-id="363e5-124">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="363e5-125">type</span><span class="sxs-lookup"><span data-stu-id="363e5-125">type</span></span> | <span data-ttu-id="363e5-126">propriété de type Hello doit indiquer : `Http`.</span><span class="sxs-lookup"><span data-stu-id="363e5-126">hello type property must be set to: `Http`.</span></span> | <span data-ttu-id="363e5-127">Oui</span><span class="sxs-lookup"><span data-stu-id="363e5-127">Yes</span></span> |
| <span data-ttu-id="363e5-128">url</span><span class="sxs-lookup"><span data-stu-id="363e5-128">url</span></span> | <span data-ttu-id="363e5-129">Toohello de l’URL du serveur Web de base</span><span class="sxs-lookup"><span data-stu-id="363e5-129">Base URL toohello Web Server</span></span> | <span data-ttu-id="363e5-130">Oui</span><span class="sxs-lookup"><span data-stu-id="363e5-130">Yes</span></span> |
| <span data-ttu-id="363e5-131">authenticationType</span><span class="sxs-lookup"><span data-stu-id="363e5-131">authenticationType</span></span> | <span data-ttu-id="363e5-132">Spécifie le type d’authentification hello.</span><span class="sxs-lookup"><span data-stu-id="363e5-132">Specifies hello authentication type.</span></span> <span data-ttu-id="363e5-133">Les valeurs autorisées sont : **Anonymous** (Anonyme), **Basic** (De base), **Digest**, **Windows**, **ClientCertificate** (Certificat client).</span><span class="sxs-lookup"><span data-stu-id="363e5-133">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="363e5-134">Font respectivement référence toosections sous ce tableau sur plus de propriétés et des exemples JSON pour ces types d’authentification.</span><span class="sxs-lookup"><span data-stu-id="363e5-134">Refer toosections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="363e5-135">Oui</span><span class="sxs-lookup"><span data-stu-id="363e5-135">Yes</span></span> |
| <span data-ttu-id="363e5-136">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="363e5-136">enableServerCertificateValidation</span></span> | <span data-ttu-id="363e5-137">Spécifiez si le serveur tooenable SSL la validation des certificats si la source est le serveur de Web HTTPS</span><span class="sxs-lookup"><span data-stu-id="363e5-137">Specify whether tooenable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="363e5-138">Non, la valeur par défaut est True.</span><span class="sxs-lookup"><span data-stu-id="363e5-138">No, default is true</span></span> |
| <span data-ttu-id="363e5-139">gatewayName</span><span class="sxs-lookup"><span data-stu-id="363e5-139">gatewayName</span></span> | <span data-ttu-id="363e5-140">Nom de tooan de tooconnect hello passerelle de gestion des données sur site source HTTP.</span><span class="sxs-lookup"><span data-stu-id="363e5-140">Name of hello Data Management Gateway tooconnect tooan on-premises HTTP source.</span></span> | <span data-ttu-id="363e5-141">Oui en cas de copie de données à partir d’une source HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="363e5-141">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="363e5-142">Encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="363e5-142">encryptedCredential</span></span> | <span data-ttu-id="363e5-143">Les informations d’identification chiffrées tooaccess hello de point de terminaison HTTP.</span><span class="sxs-lookup"><span data-stu-id="363e5-143">Encrypted credential tooaccess hello HTTP endpoint.</span></span> <span data-ttu-id="363e5-144">Généré automatiquement lorsque vous configurez des informations d’authentification hello dans copie Assistant ou hello ClickOnce boîte de dialogue contextuelle.</span><span class="sxs-lookup"><span data-stu-id="363e5-144">Auto-generated when you configure hello authentication information in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="363e5-145">Non.</span><span class="sxs-lookup"><span data-stu-id="363e5-145">No.</span></span> <span data-ttu-id="363e5-146">S’applique uniquement pour la copie de données à partir d’un serveur HTTP local.</span><span class="sxs-lookup"><span data-stu-id="363e5-146">Apply only when copying data from an on-premises HTTP server.</span></span> |

<span data-ttu-id="363e5-147">Consultez [déplacement des données entre des sources locales et cloud hello avec la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md) pour plus d’informations sur la définition des informations d’identification pour la source de données du connecteur local HTTP.</span><span class="sxs-lookup"><span data-stu-id="363e5-147">See [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for details about setting credentials for on-premises HTTP connector data source.</span></span>

### <a name="using-basic-digest-or-windows-authentication"></a><span data-ttu-id="363e5-148">Utilisation de l’authentification Basic (De base), Digest ou Windows</span><span class="sxs-lookup"><span data-stu-id="363e5-148">Using Basic, Digest, or Windows authentication</span></span>

<span data-ttu-id="363e5-149">Définissez `authenticationType` en tant que `Basic`, `Digest`, ou `Windows`et spécifiez hello propriétés suivantes en plus de hello du connecteur HTTP générique celles présentées ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="363e5-149">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="363e5-150">Propriété</span><span class="sxs-lookup"><span data-stu-id="363e5-150">Property</span></span> | <span data-ttu-id="363e5-151">Description</span><span class="sxs-lookup"><span data-stu-id="363e5-151">Description</span></span> | <span data-ttu-id="363e5-152">Requis</span><span class="sxs-lookup"><span data-stu-id="363e5-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="363e5-153">username</span><span class="sxs-lookup"><span data-stu-id="363e5-153">username</span></span> | <span data-ttu-id="363e5-154">Nom d’utilisateur tooaccess hello de point de terminaison HTTP.</span><span class="sxs-lookup"><span data-stu-id="363e5-154">Username tooaccess hello HTTP endpoint.</span></span> | <span data-ttu-id="363e5-155">Oui</span><span class="sxs-lookup"><span data-stu-id="363e5-155">Yes</span></span> |
| <span data-ttu-id="363e5-156">password</span><span class="sxs-lookup"><span data-stu-id="363e5-156">password</span></span> | <span data-ttu-id="363e5-157">Mot de passe pour l’utilisateur hello (nom d’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="363e5-157">Password for hello user (username).</span></span> | <span data-ttu-id="363e5-158">Oui</span><span class="sxs-lookup"><span data-stu-id="363e5-158">Yes</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="363e5-159">Exemple : utilisation de l’authentification Basic (De base), Digest ou Windows</span><span class="sxs-lookup"><span data-stu-id="363e5-159">Example: using Basic, Digest, or Windows authentication</span></span>

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

### <a name="using-clientcertificate-authentication"></a><span data-ttu-id="363e5-160">Utilisation de l’authentification ClientCertificate (Certificat client)</span><span class="sxs-lookup"><span data-stu-id="363e5-160">Using ClientCertificate authentication</span></span>

<span data-ttu-id="363e5-161">l’authentification de base toouse, définissez `authenticationType` comme `ClientCertificate`et spécifiez hello propriétés suivantes en plus de hello du connecteur HTTP générique celles présentées ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="363e5-161">toouse basic authentication, set `authenticationType` as `ClientCertificate`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="363e5-162">Propriété</span><span class="sxs-lookup"><span data-stu-id="363e5-162">Property</span></span> | <span data-ttu-id="363e5-163">Description</span><span class="sxs-lookup"><span data-stu-id="363e5-163">Description</span></span> | <span data-ttu-id="363e5-164">Requis</span><span class="sxs-lookup"><span data-stu-id="363e5-164">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="363e5-165">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="363e5-165">embeddedCertData</span></span> | <span data-ttu-id="363e5-166">contenu codé en Base64 Hello de données binaires du fichier d’informations Exchange PFX (Personal) hello.</span><span class="sxs-lookup"><span data-stu-id="363e5-166">hello Base64-encoded contents of binary data of hello Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="363e5-167">Spécifiez soit hello `embeddedCertData` ou `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="363e5-167">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="363e5-168">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="363e5-168">certThumbprint</span></span> | <span data-ttu-id="363e5-169">Bonjour empreinte numérique du certificat hello qui a été installé sur le magasin de certificats de l’ordinateur de votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="363e5-169">hello thumbprint of hello certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="363e5-170">S’applique uniquement pour la copie de données à partir d’une source HTTP locale.</span><span class="sxs-lookup"><span data-stu-id="363e5-170">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="363e5-171">Spécifiez soit hello `embeddedCertData` ou `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="363e5-171">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="363e5-172">password</span><span class="sxs-lookup"><span data-stu-id="363e5-172">password</span></span> | <span data-ttu-id="363e5-173">Mot de passe associé au certificat de hello.</span><span class="sxs-lookup"><span data-stu-id="363e5-173">Password associated with hello certificate.</span></span> | <span data-ttu-id="363e5-174">Non</span><span class="sxs-lookup"><span data-stu-id="363e5-174">No</span></span> |

<span data-ttu-id="363e5-175">Si vous utilisez `certThumbprint` pour l’authentification et hello du certificat est installé dans le magasin personnel de l’ordinateur local de hello de hello, vous devez le service passerelle toohello toogrant hello autorisation de lecture :</span><span class="sxs-lookup"><span data-stu-id="363e5-175">If you use `certThumbprint` for authentication and hello certificate is installed in hello personal store of hello local computer, you need toogrant hello read permission toohello gateway service:</span></span>

1. <span data-ttu-id="363e5-176">Lancez Microsoft Management Console (MMC).</span><span class="sxs-lookup"><span data-stu-id="363e5-176">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="363e5-177">Ajouter hello **certificats** que hello cibles du composant logiciel enfichable **ordinateur Local**.</span><span class="sxs-lookup"><span data-stu-id="363e5-177">Add hello **Certificates** snap-in that targets hello **Local Computer**.</span></span>
2. <span data-ttu-id="363e5-178">Développez **Certificats**, **Personnel**, puis cliquez sur **Certificats**.</span><span class="sxs-lookup"><span data-stu-id="363e5-178">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="363e5-179">Certificat hello magasin personnel de hello d’avec le bouton droit, puis sélectionnez **toutes les tâches**->**gérer les clés privées...**</span><span class="sxs-lookup"><span data-stu-id="363e5-179">Right-click hello certificate from hello personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="363e5-180">Sur hello **sécurité** onglet, ajoutez le compte d’utilisateur hello sous lequel le Service hôte de passerelle de gestion des données s’exécute avec le certificat de toohello hello accès en lecture.</span><span class="sxs-lookup"><span data-stu-id="363e5-180">On hello **Security** tab, add hello user account under which Data Management Gateway Host Service is running with hello read access toohello certificate.</span></span>  

#### <a name="example-using-client-certificate"></a><span data-ttu-id="363e5-181">Exemple : utilisation d’un certificat client</span><span class="sxs-lookup"><span data-stu-id="363e5-181">Example: using client certificate</span></span>
<span data-ttu-id="363e5-182">Cela les liaisons de service vos données fabrique tooan local HTTP web serveur lié.</span><span class="sxs-lookup"><span data-stu-id="363e5-182">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="363e5-183">Il utilise un certificat de client est installé sur l’ordinateur de hello avec la passerelle de gestion des données installé.</span><span class="sxs-lookup"><span data-stu-id="363e5-183">It uses a client certificate that is installed on hello machine with Data Management Gateway installed.</span></span>

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

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="363e5-184">Exemple : utilisation d’un certificat client dans un fichier</span><span class="sxs-lookup"><span data-stu-id="363e5-184">Example: using client certificate in a file</span></span>
<span data-ttu-id="363e5-185">Cela les liaisons de service vos données fabrique tooan local HTTP web serveur lié.</span><span class="sxs-lookup"><span data-stu-id="363e5-185">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="363e5-186">Elle utilise un fichier de certificat client sur l’ordinateur de hello avec la passerelle de gestion des données installé.</span><span class="sxs-lookup"><span data-stu-id="363e5-186">It uses a client certificate file on hello machine with Data Management Gateway installed.</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="363e5-187">Propriétés du jeu de données</span><span class="sxs-lookup"><span data-stu-id="363e5-187">Dataset properties</span></span>
<span data-ttu-id="363e5-188">Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="363e5-188">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="363e5-189">Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).</span><span class="sxs-lookup"><span data-stu-id="363e5-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="363e5-190">Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello.</span><span class="sxs-lookup"><span data-stu-id="363e5-190">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="363e5-191">jeu de données de type Hello typeProperties section **Http** a les propriétés suivantes de hello</span><span class="sxs-lookup"><span data-stu-id="363e5-191">hello typeProperties section for dataset of type **Http** has hello following properties</span></span>

| <span data-ttu-id="363e5-192">Propriété</span><span class="sxs-lookup"><span data-stu-id="363e5-192">Property</span></span> | <span data-ttu-id="363e5-193">Description</span><span class="sxs-lookup"><span data-stu-id="363e5-193">Description</span></span> | <span data-ttu-id="363e5-194">Requis</span><span class="sxs-lookup"><span data-stu-id="363e5-194">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="363e5-195">type</span><span class="sxs-lookup"><span data-stu-id="363e5-195">type</span></span> | <span data-ttu-id="363e5-196">Type hello du jeu de données hello spécifié.</span><span class="sxs-lookup"><span data-stu-id="363e5-196">Specified hello type of hello dataset.</span></span> <span data-ttu-id="363e5-197">doit être défini trop`Http`.</span><span class="sxs-lookup"><span data-stu-id="363e5-197">must be set too`Http`.</span></span> | <span data-ttu-id="363e5-198">Oui</span><span class="sxs-lookup"><span data-stu-id="363e5-198">Yes</span></span> |
| <span data-ttu-id="363e5-199">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="363e5-199">relativeUrl</span></span> | <span data-ttu-id="363e5-200">Une ressource URL toohello relative qui contient les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="363e5-200">A relative URL toohello resource that contains hello data.</span></span> <span data-ttu-id="363e5-201">Lorsque le chemin d’accès n’est pas spécifié, seul hello URL spécifiée dans la définition de service hello lié est utilisé.</span><span class="sxs-lookup"><span data-stu-id="363e5-201">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> <br><br> <span data-ttu-id="363e5-202">tooconstruct des URL dynamique, vous pouvez utiliser [les variables système et les fonctions de la fabrique de données](data-factory-functions-variables.md), par exemple, « relativeUrl » : « $$Text.Format ('/ my/rapport ? mois = {0}-{0:MM} & fmt = csv », SliceStart) ».</span><span class="sxs-lookup"><span data-stu-id="363e5-202">tooconstruct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), e.g. "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)".</span></span> | <span data-ttu-id="363e5-203">Non</span><span class="sxs-lookup"><span data-stu-id="363e5-203">No</span></span> |
| <span data-ttu-id="363e5-204">requestMethod</span><span class="sxs-lookup"><span data-stu-id="363e5-204">requestMethod</span></span> | <span data-ttu-id="363e5-205">Méthode HTTP.</span><span class="sxs-lookup"><span data-stu-id="363e5-205">Http method.</span></span> <span data-ttu-id="363e5-206">Les valeurs autorisées sont **GET** ou **POST**.</span><span class="sxs-lookup"><span data-stu-id="363e5-206">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="363e5-207">Non.</span><span class="sxs-lookup"><span data-stu-id="363e5-207">No.</span></span> <span data-ttu-id="363e5-208">La valeur par défaut est `GET`.</span><span class="sxs-lookup"><span data-stu-id="363e5-208">Default is `GET`.</span></span> |
| <span data-ttu-id="363e5-209">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="363e5-209">additionalHeaders</span></span> | <span data-ttu-id="363e5-210">En-têtes de requête HTTP supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="363e5-210">Additional HTTP request headers.</span></span> | <span data-ttu-id="363e5-211">Non</span><span class="sxs-lookup"><span data-stu-id="363e5-211">No</span></span> |
| <span data-ttu-id="363e5-212">RequestBody</span><span class="sxs-lookup"><span data-stu-id="363e5-212">requestBody</span></span> | <span data-ttu-id="363e5-213">Corps de la requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="363e5-213">Body for HTTP request.</span></span> | <span data-ttu-id="363e5-214">Non</span><span class="sxs-lookup"><span data-stu-id="363e5-214">No</span></span> |
| <span data-ttu-id="363e5-215">format</span><span class="sxs-lookup"><span data-stu-id="363e5-215">format</span></span> | <span data-ttu-id="363e5-216">Si vous souhaitez toosimply **hello de données à partir du point de terminaison HTTP en tant que-est** sans qu’il analyse, ignorer les paramètres de ce format.</span><span class="sxs-lookup"><span data-stu-id="363e5-216">If you want toosimply **retrieve hello data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="363e5-217">Si vous souhaitez la réponse de hello HTTP tooparse contenu pendant la copie, hello les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="363e5-217">If you want tooparse hello HTTP response content during copy, hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="363e5-218">Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="363e5-218">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="363e5-219">Non</span><span class="sxs-lookup"><span data-stu-id="363e5-219">No</span></span> |
| <span data-ttu-id="363e5-220">compression</span><span class="sxs-lookup"><span data-stu-id="363e5-220">compression</span></span> | <span data-ttu-id="363e5-221">Spécifiez le type de hello et le niveau de compression pour les données de salutation.</span><span class="sxs-lookup"><span data-stu-id="363e5-221">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="363e5-222">Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="363e5-222">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="363e5-223">Les niveaux pris en charge sont **Optimal** et **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="363e5-223">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="363e5-224">Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="363e5-224">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="363e5-225">Non</span><span class="sxs-lookup"><span data-stu-id="363e5-225">No</span></span> |

### <a name="example-using-hello-get-default-method"></a><span data-ttu-id="363e5-226">Exemple : utilisation de méthode GET (par défaut) de hello</span><span class="sxs-lookup"><span data-stu-id="363e5-226">Example: using hello GET (default) method</span></span>

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

### <a name="example-using-hello-post-method"></a><span data-ttu-id="363e5-227">Exemple : utilisation de méthode POST hello</span><span class="sxs-lookup"><span data-stu-id="363e5-227">Example: using hello POST method</span></span>

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

## <a name="copy-activity-properties"></a><span data-ttu-id="363e5-228">Propriétés de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="363e5-228">Copy activity properties</span></span>
<span data-ttu-id="363e5-229">Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="363e5-229">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="363e5-230">Les propriétés comme le nom, la description, les tables d’entrée et de sortie et la stratégie sont disponibles pour tous les types d’activités.</span><span class="sxs-lookup"><span data-stu-id="363e5-230">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="363e5-231">Propriétés disponibles dans hello **typeProperties** section de l’activité de hello sur hello autre part varient selon chaque type d’activité.</span><span class="sxs-lookup"><span data-stu-id="363e5-231">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="363e5-232">Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.</span><span class="sxs-lookup"><span data-stu-id="363e5-232">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="363e5-233">Actuellement, lorsque source hello dans l’activité de copie est de type **HttpSource**, hello propriétés suivantes est prises en charge.</span><span class="sxs-lookup"><span data-stu-id="363e5-233">Currently, when hello source in copy activity is of type **HttpSource**, hello following properties are supported.</span></span>

| <span data-ttu-id="363e5-234">Propriété</span><span class="sxs-lookup"><span data-stu-id="363e5-234">Property</span></span> | <span data-ttu-id="363e5-235">Description</span><span class="sxs-lookup"><span data-stu-id="363e5-235">Description</span></span> | <span data-ttu-id="363e5-236">Requis</span><span class="sxs-lookup"><span data-stu-id="363e5-236">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="363e5-237">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="363e5-237">httpRequestTimeout</span></span> | <span data-ttu-id="363e5-238">Bonjour le délai d’attente (TimeSpan) pour tooget de demande HTTP hello une réponse.</span><span class="sxs-lookup"><span data-stu-id="363e5-238">hello timeout (TimeSpan) for hello HTTP request tooget a response.</span></span> <span data-ttu-id="363e5-239">Il est tooget hello du délai d’attente de réponse, pas les données de réponse du tooread hello du délai d’attente.</span><span class="sxs-lookup"><span data-stu-id="363e5-239">It is hello timeout tooget a response, not hello timeout tooread response data.</span></span> | <span data-ttu-id="363e5-240">Non.</span><span class="sxs-lookup"><span data-stu-id="363e5-240">No.</span></span> <span data-ttu-id="363e5-241">Valeur par défaut : 00:01:40</span><span class="sxs-lookup"><span data-stu-id="363e5-241">Default value: 00:01:40</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="363e5-242">Formats de fichier et de compression pris en charge</span><span class="sxs-lookup"><span data-stu-id="363e5-242">Supported file and compression formats</span></span>
<span data-ttu-id="363e5-243">Pour plus d’informations, voir [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="363e5-243">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="363e5-244">Exemples JSON</span><span class="sxs-lookup"><span data-stu-id="363e5-244">JSON examples</span></span>
<span data-ttu-id="363e5-245">Hello exemple ci-dessous fournit des exemples de définitions de JSON que vous pouvez utiliser toocreate un pipeline à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="363e5-245">hello following example provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="363e5-246">Elles montrent comment la source de données de toocopy HTTP tooAzure stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="363e5-246">They show how toocopy data from HTTP source tooAzure Blob Storage.</span></span> <span data-ttu-id="363e5-247">Toutefois, les données peuvent être copiées **directement** de n’importe quelle tooany de sources de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="363e5-247">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-http-source-tooazure-blob-storage"></a><span data-ttu-id="363e5-248">Exemple : Copier des données à partir de la source HTTP tooAzure stockage d’objets Blob</span><span class="sxs-lookup"><span data-stu-id="363e5-248">Example: Copy data from HTTP source tooAzure Blob Storage</span></span>
<span data-ttu-id="363e5-249">Hello solution Data Factory pour cet exemple contient hello suivant des entités de fabrique de données :</span><span class="sxs-lookup"><span data-stu-id="363e5-249">hello Data Factory solution for this sample contains hello following Data Factory entities:</span></span>

1. <span data-ttu-id="363e5-250">Un service lié de type [HTTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="363e5-250">A linked service of type [HTTP](#linked-service-properties).</span></span>
2. <span data-ttu-id="363e5-251">Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="363e5-251">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="363e5-252">Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [Http](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="363e5-252">An input [dataset](data-factory-create-datasets.md) of type [Http](#dataset-properties).</span></span>
4. <span data-ttu-id="363e5-253">Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="363e5-253">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="363e5-254">Un [pipeline](data-factory-create-pipelines.md) avec une activité de copie qui utilise [ttpSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="363e5-254">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [HttpSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="363e5-255">exemple Hello copie des données à partir d’un tooan de source HTTP blob Azure toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="363e5-255">hello sample copies data from an HTTP source tooan Azure blob every hour.</span></span> <span data-ttu-id="363e5-256">propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="363e5-256">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="http-linked-service"></a><span data-ttu-id="363e5-257">Service lié HTTP</span><span class="sxs-lookup"><span data-stu-id="363e5-257">HTTP linked service</span></span>
<span data-ttu-id="363e5-258">Cet exemple utilise hello HTTP lié à service avec l’authentification anonyme.</span><span class="sxs-lookup"><span data-stu-id="363e5-258">This example uses hello HTTP linked service with anonymous authentication.</span></span> <span data-ttu-id="363e5-259">Pour connaître les différents types d’authentification que vous pouvez utiliser, consultez la section [Service lié HTTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="363e5-259">See [HTTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="363e5-260">Service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="363e5-260">Azure Storage linked service</span></span>

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

### <a name="http-input-dataset"></a><span data-ttu-id="363e5-261">Jeu de données d’entrée HTTP</span><span class="sxs-lookup"><span data-stu-id="363e5-261">HTTP input dataset</span></span>
<span data-ttu-id="363e5-262">Paramètre **externe** trop**true** informe le service de fabrique de données hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="363e5-262">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="363e5-263">Jeu de données de sortie d’objet Blob Azure</span><span class="sxs-lookup"><span data-stu-id="363e5-263">Azure Blob output dataset</span></span>

<span data-ttu-id="363e5-264">Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1).</span><span class="sxs-lookup"><span data-stu-id="363e5-264">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

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

### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="363e5-265">Pipeline avec activité de copie</span><span class="sxs-lookup"><span data-stu-id="363e5-265">Pipeline with Copy activity</span></span>

<span data-ttu-id="363e5-266">Hello pipeline contient une activité de copie qui est configuré toouse hello des jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="363e5-266">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="363e5-267">Dans la définition JSON du pipeline hello, hello **source** type est défini trop**HttpSource** et **récepteur** type est défini trop**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="363e5-267">In hello pipeline JSON definition, hello **source** type is set too**HttpSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="363e5-268">Consultez [HttpSource](#copy-activity-properties) pour la liste des propriétés prises en charge par hello HttpSource hello.</span><span class="sxs-lookup"><span data-stu-id="363e5-268">See [HttpSource](#copy-activity-properties) for hello list of properties supported by hello HttpSource.</span></span>

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
        "description": "Copy from an HTTP source tooan Azure blob",
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
> <span data-ttu-id="363e5-269">colonnes de toomap de toocolumns du jeu de données source à partir du jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="363e5-269">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="363e5-270">Performances et réglage</span><span class="sxs-lookup"><span data-stu-id="363e5-270">Performance and Tuning</span></span>
<span data-ttu-id="363e5-271">Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.</span><span class="sxs-lookup"><span data-stu-id="363e5-271">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
