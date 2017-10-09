---
title: "aaaHow toouse stockage d’objets Blob à partir de Node.js | Documents Microsoft"
description: "Stocker des données non structurées dans le cloud hello avec le stockage d’objets Blob Azure (stockage d’objets)."
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 8b0df222-1ca8-4967-8248-6d6d720947b8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 572e7fc9f7b19ff01720a7cadd495c809ed49fb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-nodejs"></a><span data-ttu-id="5cbaf-103">Comment toouse stockage d’objets Blob à partir de Node.js</span><span class="sxs-lookup"><span data-stu-id="5cbaf-103">How toouse Blob storage from Node.js</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="5cbaf-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="5cbaf-104">Overview</span></span>
<span data-ttu-id="5cbaf-105">Cet article vous montre comment les scénarios courants tooperform à l’aide du stockage d’objets Blob.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-105">This article shows you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="5cbaf-106">exemples de Hello sont écrites via hello Node.js API.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-106">hello samples are written via hello Node.js API.</span></span> <span data-ttu-id="5cbaf-107">scénarios de Hello couvertes incluent comment tooupload, répertorier, télécharger et supprimer des objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-107">hello scenarios covered include how tooupload, list, download, and delete blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="5cbaf-108">Création d’une application Node.js</span><span class="sxs-lookup"><span data-stu-id="5cbaf-108">Create a Node.js application</span></span>
<span data-ttu-id="5cbaf-109">Pour obtenir des instructions sur la façon de toocreate une application Node.js, consultez [créer une application web de Node.js dans Azure App Service], [générer et déployer un tooan d’application Node.js Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) --à l’aide de Windows PowerShell, ou [générer et déployer un tooAzure d’application web Node.js à l’aide de Web Matrix](https://www.microsoft.com/web/webmatrix/).</span><span class="sxs-lookup"><span data-stu-id="5cbaf-109">For instructions on how toocreate a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) -- using Windows PowerShell, or [Build and deploy a Node.js web app tooAzure using Web Matrix](https://www.microsoft.com/web/webmatrix/).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="5cbaf-110">Configurer votre stockage tooaccess d’application</span><span class="sxs-lookup"><span data-stu-id="5cbaf-110">Configure your application tooaccess storage</span></span>
<span data-ttu-id="5cbaf-111">toouse stockage Azure, vous devez hello SDK de stockage Azure pour Node.js, qui inclut un ensemble de bibliothèques de commodité qui communiquent avec les services REST de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-111">toouse Azure storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="5cbaf-112">Utiliser le Gestionnaire de Package de nœud (NPM) tooobtain hello package</span><span class="sxs-lookup"><span data-stu-id="5cbaf-112">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="5cbaf-113">Utiliser une interface de ligne de commande comme **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix), dossier de toohello toonavigate où vous avez créé votre exemple application.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), toonavigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="5cbaf-114">Type **npm installer le stockage azure** dans la fenêtre de commande hello.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-114">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="5cbaf-115">Sortie de commande hello est similaire toohello exemple de code suivant.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-115">Output from hello command is similar toohello following code example.</span></span>

        azure-storage@0.5.0 node_modules\azure-storage
        +-- extend@1.2.1
        +-- xmlbuilder@0.4.3
        +-- mime@1.2.11
        +-- node-uuid@1.4.3
        +-- validator@3.22.2
        +-- underscore@1.4.4
        +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
        +-- xml2js@0.2.7 (sax@0.5.2)
        +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
3. <span data-ttu-id="5cbaf-116">Vous pouvez exécuter manuellement hello **ls** tooverify de commande qui un **nœud\_modules** dossier a été créé.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-116">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="5cbaf-117">Dans ce dossier, recherche hello **le stockage azure** package qui contient les bibliothèques hello que vous avez besoin de stockage de tooaccess.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-117">Inside that folder, find hello **azure-storage** package, which contains hello libraries that you need tooaccess storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="5cbaf-118">Importer un package hello</span><span class="sxs-lookup"><span data-stu-id="5cbaf-118">Import hello package</span></span>
<span data-ttu-id="5cbaf-119">Utilisez le bloc-notes ou un autre éditeur de texte, ajoutez hello suivant en haut de toohello de hello **server.js** fichier de l’application hello où vous avez l’intention toouse stockage :</span><span class="sxs-lookup"><span data-stu-id="5cbaf-119">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application where you intend toouse storage:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="5cbaf-120">Configurer une connexion Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5cbaf-120">Set up an Azure Storage connection</span></span>
<span data-ttu-id="5cbaf-121">Bonjour Azure module lit les variables d’environnement hello `AZURE_STORAGE_ACCOUNT` et `AZURE_STORAGE_ACCESS_KEY`, ou `AZURE_STORAGE_CONNECTION_STRING`, pour plus d’informations requises au compte de stockage Azure tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-121">hello Azure module will read hello environment variables `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY`, or `AZURE_STORAGE_CONNECTION_STRING`, for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="5cbaf-122">Si ces variables d’environnement ne sont pas définies, vous devez spécifier les informations de compte hello lors de l’appel **createBlobService**.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-122">If these environment variables are not set, you must specify hello account information when calling **createBlobService**.</span></span>

<span data-ttu-id="5cbaf-123">Pour obtenir un exemple de la définition de variables d’environnement hello Bonjour [portail Azure](https://portal.azure.com) pour une application web Azure, consultez [à l’aide de Node.js web application hello Service de Table Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="5cbaf-123">For an example of setting hello environment variables in hello [Azure portal](https://portal.azure.com) for an Azure web app, see [Node.js web app using hello Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-container"></a><span data-ttu-id="5cbaf-124">Créez un conteneur.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-124">Create a container</span></span>
<span data-ttu-id="5cbaf-125">Hello **BlobService** objet vous permet de travailler avec les conteneurs et objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-125">hello **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="5cbaf-126">Hello de code suivant crée un **BlobService** objet.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-126">hello following code creates a **BlobService** object.</span></span> <span data-ttu-id="5cbaf-127">Ajoutez suit hello vers haut hello de **server.js**:</span><span class="sxs-lookup"><span data-stu-id="5cbaf-127">Add hello following near hello top of **server.js**:</span></span>

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> <span data-ttu-id="5cbaf-128">Vous pouvez accéder à un objet blob de manière anonyme à l’aide de **createBlobServiceAnonymous** et de fournir l’adresse de l’hôte hello.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-128">You can access a blob anonymously by using **createBlobServiceAnonymous** and providing hello host address.</span></span> <span data-ttu-id="5cbaf-129">Par exemple, utilisez `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-129">For example, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="5cbaf-130">toocreate un nouveau conteneur, utilisez **createContainerIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-130">toocreate a new container, use **createContainerIfNotExists**.</span></span> <span data-ttu-id="5cbaf-131">Hello exemple de code suivant crée un nouveau conteneur nommé « mycontainer » :</span><span class="sxs-lookup"><span data-stu-id="5cbaf-131">hello following code example creates a new container named 'mycontainer':</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

<span data-ttu-id="5cbaf-132">Si le conteneur de hello a été créé récemment, `result.created` a la valeur true.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-132">If hello container is newly created, `result.created` is true.</span></span> <span data-ttu-id="5cbaf-133">Si le conteneur de hello existe déjà, `result.created` a la valeur false.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-133">If hello container already exists, `result.created` is false.</span></span> <span data-ttu-id="5cbaf-134">`response`contient des informations sur les opération hello, y compris les informations d’ETag hello pour le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-134">`response` contains information about hello operation, including hello ETag information for hello container.</span></span>

### <a name="container-security"></a><span data-ttu-id="5cbaf-135">Sécurité du conteneur</span><span class="sxs-lookup"><span data-stu-id="5cbaf-135">Container security</span></span>
<span data-ttu-id="5cbaf-136">Par défaut, les nouveaux conteneurs sont privés et ne sont pas accessibles de façon anonyme.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-136">By default, new containers are private and cannot be accessed anonymously.</span></span> <span data-ttu-id="5cbaf-137">conteneur de hello toomake public afin que vous pouvez y accéder anonymement, vous pouvez définir niveau d’accès du conteneur hello trop**blob** ou **conteneur**.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-137">toomake hello container public so that you can access it anonymously, you can set hello container's access level too**blob** or **container**.</span></span>

* <span data-ttu-id="5cbaf-138">**objet BLOB** -permet l’accès en lecture anonyme tooblob contenu et les métadonnées de ce conteneur, mais pas toocontainer métadonnées telles que la liste de tous les objets BLOB dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="5cbaf-138">**blob** - allows anonymous read access tooblob content and metadata within this container, but not toocontainer metadata such as listing all blobs within a container</span></span>
* <span data-ttu-id="5cbaf-139">**conteneur** -permet l’accès en lecture anonyme tooblob contenu et les métadonnées ainsi que les métadonnées de conteneur</span><span class="sxs-lookup"><span data-stu-id="5cbaf-139">**container** - allows anonymous read access tooblob content and metadata as well as container metadata</span></span>

<span data-ttu-id="5cbaf-140">Hello exemple de code suivant illustre le niveau de l’accès paramètre hello trop**blob**:</span><span class="sxs-lookup"><span data-stu-id="5cbaf-140">hello following code example demonstrates setting hello access level too**blob**:</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access tooblob
      // content and metadata within this container
    }
});
```

<span data-ttu-id="5cbaf-141">Ou bien, vous pouvez modifier le niveau d’accès hello d’un conteneur à l’aide de **setContainerAcl** niveau d’accès toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-141">Alternatively, you can modify hello access level of a container by using **setContainerAcl** toospecify hello access level.</span></span> <span data-ttu-id="5cbaf-142">exemple modifications hello accès niveau toocontainer de code suivant de Hello :</span><span class="sxs-lookup"><span data-stu-id="5cbaf-142">hello following code example changes hello access level toocontainer:</span></span>

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set too'container'
  }
});
```

<span data-ttu-id="5cbaf-143">Hello résultat contient plus d’informations sur l’opération hello, y compris le courant de hello **ETag** pour le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-143">hello result contains information about hello operation, including hello current **ETag** for hello container.</span></span>

### <a name="filters"></a><span data-ttu-id="5cbaf-144">Filtres</span><span class="sxs-lookup"><span data-stu-id="5cbaf-144">Filters</span></span>
<span data-ttu-id="5cbaf-145">Vous pouvez appliquer l’option filtrage operations toooperations effectuées à l’aide de **BlobService**.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-145">You can apply optional filtering operations toooperations performed using **BlobService**.</span></span> <span data-ttu-id="5cbaf-146">Il peut s’agir d’opérations de journalisation, de relance automatique, etc. Les filtres sont des objets qui implémentent une méthode avec la signature de hello :</span><span class="sxs-lookup"><span data-stu-id="5cbaf-146">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="5cbaf-147">Après son prétraitement sur les options de demande hello, méthode hello doit toocall « suivant », en passant un rappel avec hello après signature :</span><span class="sxs-lookup"><span data-stu-id="5cbaf-147">After doing its preprocessing on hello request options, hello method needs toocall "next", passing a callback with hello following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="5cbaf-148">Dans ce rappel et après le traitement hello returnObject (réponse hello du serveur de toohello hello demande), le rappel de hello doit tooeither appeler ensuite s’il existe des toocontinue du traitement des autres filtres ou simplement appeler le service de hello finalCallback tooend appel.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-148">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback tooend hello service invocation.</span></span>

<span data-ttu-id="5cbaf-149">Deux filtres qui implémentent la logique de nouvelle tentative sont incluses avec hello Azure SDK pour Node.js, **ExponentialRetryPolicyFilter** et **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-149">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="5cbaf-150">Hello suivante permet de créer un **BlobService** objet qui utilise hello **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="5cbaf-150">hello following creates a **BlobService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="5cbaf-151">Charger un objet blob dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="5cbaf-151">Upload a blob into a container</span></span>
<span data-ttu-id="5cbaf-152">Il existe trois types d’objets blob : les objets blob de blocs, les objets blob d’ajouts et les objets blob de pages.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-152">There are three types of blobs: block blobs, page blobs and append blobs.</span></span> <span data-ttu-id="5cbaf-153">Objets BLOB de blocs permettre de toomore efficacement télécharger des données de grande taille.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-153">Block blobs allow you toomore efficiently upload large data.</span></span> <span data-ttu-id="5cbaf-154">Les objets blob d’ajout sont optimisés pour les opérations d’ajout.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-154">Append blobs are optimized for append operations.</span></span> <span data-ttu-id="5cbaf-155">Les objets blob de pages sont optimisés pour les opérations de lecture/écriture.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-155">Page blobs are optimized for read/write operations.</span></span> <span data-ttu-id="5cbaf-156">Pour plus d’informations, consultez [Présentation des objets blob de blocs, des objets blob d’ajout et des objets blob de pages](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="5cbaf-156">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

### <a name="block-blobs"></a><span data-ttu-id="5cbaf-157">Objets blob de blocs</span><span class="sxs-lookup"><span data-stu-id="5cbaf-157">Block blobs</span></span>
<span data-ttu-id="5cbaf-158">tooupload données tooa objet blob de blocs, hello utilisation suivant :</span><span class="sxs-lookup"><span data-stu-id="5cbaf-158">tooupload data tooa block blob, use hello following:</span></span>

* <span data-ttu-id="5cbaf-159">**createBlockBlobFromLocalFile** - crée un nouvel objet blob et télécharge le contenu hello d’un fichier</span><span class="sxs-lookup"><span data-stu-id="5cbaf-159">**createBlockBlobFromLocalFile** - creates a new block blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="5cbaf-160">**createBlockBlobFromStream** - crée un nouvel objet blob et télécharge le contenu hello d’un flux</span><span class="sxs-lookup"><span data-stu-id="5cbaf-160">**createBlockBlobFromStream** - creates a new block blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="5cbaf-161">**createBlockBlobFromText** - crée un nouvel objet blob et télécharge le contenu hello d’une chaîne</span><span class="sxs-lookup"><span data-stu-id="5cbaf-161">**createBlockBlobFromText** - creates a new block blob and uploads hello contents of a string</span></span>
* <span data-ttu-id="5cbaf-162">**createWriteStreamToBlockBlob** -fournit un objet blob de blocs écriture flux tooa</span><span class="sxs-lookup"><span data-stu-id="5cbaf-162">**createWriteStreamToBlockBlob** - provides a write stream tooa block blob</span></span>

<span data-ttu-id="5cbaf-163">exemple de code suivant Hello télécharge contenu hello Hello **test.txt** fichier dans **myblob**.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-163">hello following code example uploads hello contents of hello **test.txt** file into **myblob**.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="5cbaf-164">Hello `result` retournés par ces méthodes contient des informations sur l’opération de hello, par exemple hello **ETag** d’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-164">hello `result` returned by these methods contains information on hello operation, such as hello **ETag** of hello blob.</span></span>

### <a name="append-blobs"></a><span data-ttu-id="5cbaf-165">Objets blob d’ajout</span><span class="sxs-lookup"><span data-stu-id="5cbaf-165">Append blobs</span></span>
<span data-ttu-id="5cbaf-166">tooa de données tooupload nouveau ajouter l’objet blob, utilisez hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="5cbaf-166">tooupload data tooa new append blob, use hello following:</span></span>

* <span data-ttu-id="5cbaf-167">**createAppendBlobFromLocalFile** - crée un nouvel objet blob d’ajout et télécharge le contenu hello d’un fichier</span><span class="sxs-lookup"><span data-stu-id="5cbaf-167">**createAppendBlobFromLocalFile** - creates a new append blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="5cbaf-168">**createAppendBlobFromStream** - crée un nouvel objet blob d’ajout et télécharge le contenu hello d’un flux</span><span class="sxs-lookup"><span data-stu-id="5cbaf-168">**createAppendBlobFromStream** - creates a new append blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="5cbaf-169">**createAppendBlobFromText** - crée un nouvel objet blob d’ajout et télécharge le contenu hello d’une chaîne</span><span class="sxs-lookup"><span data-stu-id="5cbaf-169">**createAppendBlobFromText** - creates a new append blob and uploads hello contents of a string</span></span>
* <span data-ttu-id="5cbaf-170">**createWriteStreamToNewAppendBlob** - crée un nouvel objet blob d’ajout et fournit un tooit toowrite de flux de données</span><span class="sxs-lookup"><span data-stu-id="5cbaf-170">**createWriteStreamToNewAppendBlob** - creates a new append blob and then provides a stream toowrite tooit</span></span>

<span data-ttu-id="5cbaf-171">exemple de code suivant Hello télécharge contenu hello Hello **test.txt** fichier dans **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-171">hello following code example uploads hello contents of hello **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="5cbaf-172">tooappend un tooan de bloc existant ajouter blob, hello utilisation suivant :</span><span class="sxs-lookup"><span data-stu-id="5cbaf-172">tooappend a block tooan existing append blob, use hello following:</span></span>

* <span data-ttu-id="5cbaf-173">**appendFromLocalFile** -ajouter hello contenu d’un fichier tooan existant ajouter des objets blob</span><span class="sxs-lookup"><span data-stu-id="5cbaf-173">**appendFromLocalFile** - append hello contents of a file tooan existing append blob</span></span>
* <span data-ttu-id="5cbaf-174">**appendFromStream** -ajouter hello contenu d’un flux tooan existant ajouter blob</span><span class="sxs-lookup"><span data-stu-id="5cbaf-174">**appendFromStream** - append hello contents of a stream tooan existing append blob</span></span>
* <span data-ttu-id="5cbaf-175">**appendFromText** -ajouter hello contenu d’une chaîne de tooan existant ajouter des objets blob</span><span class="sxs-lookup"><span data-stu-id="5cbaf-175">**appendFromText** - append hello contents of a string tooan existing append blob</span></span>
* <span data-ttu-id="5cbaf-176">**appendBlockFromStream** -ajouter hello contenu d’un flux tooan existant ajouter blob</span><span class="sxs-lookup"><span data-stu-id="5cbaf-176">**appendBlockFromStream** - append hello contents of a stream tooan existing append blob</span></span>
* <span data-ttu-id="5cbaf-177">**appendBlockFromText** -ajouter hello contenu d’une chaîne de tooan existant ajouter des objets blob</span><span class="sxs-lookup"><span data-stu-id="5cbaf-177">**appendBlockFromText** - append hello contents of a string tooan existing append blob</span></span>

> [!NOTE]
> <span data-ttu-id="5cbaf-178">appendFromXXX API effectuera des appels de validation côté client toofail tooavoid rapide inutile du serveur.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-178">appendFromXXX APIs will do some client-side validation toofail fast tooavoid unnecessary server calls.</span></span> <span data-ttu-id="5cbaf-179">Ce n’est pas le cas des API appendBlockFromXXX.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-179">appendBlockFromXXX won't.</span></span>
>
>

<span data-ttu-id="5cbaf-180">exemple de code suivant Hello télécharge contenu hello Hello **test.txt** fichier dans **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-180">hello following code example uploads hello contents of hello **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text toobe appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a><span data-ttu-id="5cbaf-181">Objets blob de pages</span><span class="sxs-lookup"><span data-stu-id="5cbaf-181">Page blobs</span></span>
<span data-ttu-id="5cbaf-182">tooupload données tooa objet blob de pages, hello utilisation suivant :</span><span class="sxs-lookup"><span data-stu-id="5cbaf-182">tooupload data tooa page blob, use hello following:</span></span>

* <span data-ttu-id="5cbaf-183">**createPageBlob** : permet de créer un objet blob de pages d’une longueur spécifique</span><span class="sxs-lookup"><span data-stu-id="5cbaf-183">**createPageBlob** - creates a new page blob of a specific length</span></span>
* <span data-ttu-id="5cbaf-184">**createPageBlobFromLocalFile** - crée un nouvel objet blob de page et télécharge le contenu hello d’un fichier</span><span class="sxs-lookup"><span data-stu-id="5cbaf-184">**createPageBlobFromLocalFile** - creates a new page blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="5cbaf-185">**createPageBlobFromStream** - crée un nouvel objet blob de page et télécharge le contenu hello d’un flux</span><span class="sxs-lookup"><span data-stu-id="5cbaf-185">**createPageBlobFromStream** - creates a new page blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="5cbaf-186">**createWriteStreamToExistingPageBlob** -fournit un blob de pages écriture flux tooan existant</span><span class="sxs-lookup"><span data-stu-id="5cbaf-186">**createWriteStreamToExistingPageBlob** - provides a write stream tooan existing page blob</span></span>
* <span data-ttu-id="5cbaf-187">**createWriteStreamToNewPageBlob** - crée un nouvel objet blob de page et fournit un tooit toowrite de flux de données</span><span class="sxs-lookup"><span data-stu-id="5cbaf-187">**createWriteStreamToNewPageBlob** - creates a new page blob and then provides a stream toowrite tooit</span></span>

<span data-ttu-id="5cbaf-188">exemple de code suivant Hello télécharge contenu hello Hello **test.txt** fichier dans **mypageblob**.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-188">hello following code example uploads hello contents of hello **test.txt** file into **mypageblob**.</span></span>

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> <span data-ttu-id="5cbaf-189">Les objets blob de pages sont constitués de « pages » de 512 octets.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-189">Page blobs consist of 512-byte 'pages'.</span></span> <span data-ttu-id="5cbaf-190">Une erreur se produit lors du téléchargement de données lorsque leur taille n’est pas un multiple de 512.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-190">You will receive an error when uploading data with a size that is not a multiple of 512.</span></span>
>
>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="5cbaf-191">Répertorier les objets BLOB hello dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="5cbaf-191">List hello blobs in a container</span></span>
<span data-ttu-id="5cbaf-192">objets BLOB de hello toolist dans un conteneur, utilisez hello **listBlobsSegmented** (méthode).</span><span class="sxs-lookup"><span data-stu-id="5cbaf-192">toolist hello blobs in a container, use hello **listBlobsSegmented** method.</span></span> <span data-ttu-id="5cbaf-193">Si vous souhaitez que les objets BLOB de tooreturn avec un préfixe spécifique, utilisez **listBlobsSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-193">If you'd like tooreturn blobs with a specific prefix, use **listBlobsSegmentedWithPrefix**.</span></span>

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains hello entries
      // If not all blobs were returned, result.continuationToken has hello continuation token.
  }
});
```

<span data-ttu-id="5cbaf-194">Hello `result` contient un `entries` collection, qui est un tableau d’objets qui décrivent chaque objet blob.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-194">hello `result` contains an `entries` collection, which is an array of objects that describe each blob.</span></span> <span data-ttu-id="5cbaf-195">Si tous les objets BLOB ne peut pas être retournés, hello `result` fournit également un `continuationToken`, que vous pouvez utiliser comme hello deuxième paramètre tooretrieve des entrées supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-195">If all blobs cannot be returned, hello `result` also provides a `continuationToken`, which you may use as hello second parameter tooretrieve additional entries.</span></span>

## <a name="download-blobs"></a><span data-ttu-id="5cbaf-196">Télécharger des objets blob</span><span class="sxs-lookup"><span data-stu-id="5cbaf-196">Download blobs</span></span>
<span data-ttu-id="5cbaf-197">données toodownload à partir d’un objet blob, utilisez hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="5cbaf-197">toodownload data from a blob, use hello following:</span></span>

* <span data-ttu-id="5cbaf-198">**getBlobToLocalFile** -écrit hello blob contenu toofile</span><span class="sxs-lookup"><span data-stu-id="5cbaf-198">**getBlobToLocalFile** - writes hello blob contents toofile</span></span>
* <span data-ttu-id="5cbaf-199">**getBlobToStream** -écrit hello blob contenu tooa flux</span><span class="sxs-lookup"><span data-stu-id="5cbaf-199">**getBlobToStream** - writes hello blob contents tooa stream</span></span>
* <span data-ttu-id="5cbaf-200">**getBlobToText** -écrit contenu d’objet blob hello tooa chaîne</span><span class="sxs-lookup"><span data-stu-id="5cbaf-200">**getBlobToText** - writes hello blob contents tooa string</span></span>
* <span data-ttu-id="5cbaf-201">**createReadStream** -fournit une tooread de flux de données à partir de l’objet blob de hello</span><span class="sxs-lookup"><span data-stu-id="5cbaf-201">**createReadStream** - provides a stream tooread from hello blob</span></span>

<span data-ttu-id="5cbaf-202">Hello exemple de code suivant montre comment utiliser **getBlobToStream** contenu de hello toodownload Hello **myblob** d’objets blob et le stocker toohello **output.txt** fichier à l’aide un flux de données :</span><span class="sxs-lookup"><span data-stu-id="5cbaf-202">hello following code example demonstrates using **getBlobToStream** toodownload hello contents of hello **myblob** blob and store it toohello **output.txt** file by using a stream:</span></span>

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

<span data-ttu-id="5cbaf-203">Hello `result` contient des informations sur les objets blob hello, y compris **ETag** plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-203">hello `result` contains information about hello blob, including **ETag** information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="5cbaf-204">Supprimer un objet blob</span><span class="sxs-lookup"><span data-stu-id="5cbaf-204">Delete a blob</span></span>
<span data-ttu-id="5cbaf-205">Enfin, toodelete un objet blob, appelez **deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-205">Finally, toodelete a blob, call **deleteBlob**.</span></span> <span data-ttu-id="5cbaf-206">Hello l’exemple de code supprime hello objet blob nommé suivant **myblob**.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-206">hello following code example deletes hello blob named **myblob**.</span></span>

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a><span data-ttu-id="5cbaf-207">Accès simultané</span><span class="sxs-lookup"><span data-stu-id="5cbaf-207">Concurrent access</span></span>
<span data-ttu-id="5cbaf-208">toosupport le blob tooa accès simultanés à partir de plusieurs clients ou de plusieurs instances de processus, vous pouvez utiliser **ETags** ou **baux**.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-208">toosupport concurrent access tooa blob from multiple clients or multiple process instances, you can use **ETags** or **leases**.</span></span>

* <span data-ttu-id="5cbaf-209">**ETag** -fournit un toodetect de façon que hello blob ou conteneur a été modifié par un autre processus</span><span class="sxs-lookup"><span data-stu-id="5cbaf-209">**Etag** - provides a way toodetect that hello blob or container has been modified by another process</span></span>
* <span data-ttu-id="5cbaf-210">**Bail** - fournit une manière tooobtain exclusif, renouvelables, d’écriture ou de supprimer l’accès tooa objet blob pour une période donnée</span><span class="sxs-lookup"><span data-stu-id="5cbaf-210">**Lease** - provides a way tooobtain exclusive, renewable, write or delete access tooa blob for a period of time</span></span>

### <a name="etag"></a><span data-ttu-id="5cbaf-211">ETag</span><span class="sxs-lookup"><span data-stu-id="5cbaf-211">ETag</span></span>
<span data-ttu-id="5cbaf-212">Utilisez les ETags si vous avez besoin tooallow plusieurs clients ou instances toowrite toohello bloc Blob ou page d’objets Blob simultanément.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-212">Use ETags if you need tooallow multiple clients or instances toowrite toohello block Blob or page Blob simultaneously.</span></span> <span data-ttu-id="5cbaf-213">Hello ETag vous permet de toodetermine si hello conteneur ou un objet blob a été modifié depuis lecture initiale ou créé, ce qui vous permet de tooavoid remplacer les modifications validées par un autre client ou processus.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-213">hello ETag allows you toodetermine if hello container or blob was modified since you initially read or created it, which allows you tooavoid overwriting changes committed by another client or process.</span></span>

<span data-ttu-id="5cbaf-214">Vous pouvez définir des conditions de l’ETag à l’aide de hello facultatif `options.accessConditions` paramètre.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-214">You can set ETag conditions by using hello optional `options.accessConditions` parameter.</span></span> <span data-ttu-id="5cbaf-215">Hello exemple de code suivant télécharge uniquement les hello **test.txt** fichier si l’objet blob de hello existe déjà et a la valeur d’ETag hello contenus par `etagToMatch`.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-215">hello following code example only uploads hello **test.txt** file if hello blob already exists and has hello ETag value contained by `etagToMatch`.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="5cbaf-216">Lorsque vous utilisez l’ETag, le modèle général de hello est :</span><span class="sxs-lookup"><span data-stu-id="5cbaf-216">When you're using ETags, hello general pattern is:</span></span>

1. <span data-ttu-id="5cbaf-217">Obtenir hello ETag en tant que résultat de hello de créer, de liste ou d’opération get.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-217">Obtain hello ETag as hello result of a create, list, or get operation.</span></span>
2. <span data-ttu-id="5cbaf-218">Exécuter une action, la vérification de cette valeur ETag hello n’a pas été modifiée.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-218">Perform an action, checking that hello ETag value has not been modified.</span></span>

<span data-ttu-id="5cbaf-219">Si la valeur de hello a été modifié, cela indique que client ou une autre instance modifiée blob de hello ou un conteneur dans la mesure où vous avez obtenu la valeur de l’ETag hello.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-219">If hello value was modified, this indicates that another client or instance modified hello blob or container since you obtained hello ETag value.</span></span>

### <a name="lease"></a><span data-ttu-id="5cbaf-220">Lease</span><span class="sxs-lookup"><span data-stu-id="5cbaf-220">Lease</span></span>
<span data-ttu-id="5cbaf-221">Vous pouvez acquérir un nouveau bail à l’aide de hello **acquireLease** méthode, en spécifiant l’objet blob de hello ou un conteneur que vous souhaitez tooobtain un bail sur.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-221">You can acquire a new lease by using hello **acquireLease** method, specifying hello blob or container that you wish tooobtain a lease on.</span></span> <span data-ttu-id="5cbaf-222">Par exemple, hello suivant code acquiert un bail sur **myblob**.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-222">For example, hello following code acquires a lease on **myblob**.</span></span>

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

<span data-ttu-id="5cbaf-223">Les opérations suivantes sur **myblob** doit fournir hello `options.leaseId` paramètre.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-223">Subsequent operations on **myblob** must provide hello `options.leaseId` parameter.</span></span> <span data-ttu-id="5cbaf-224">bail Hello ID est retourné en tant que `result.id` de **acquireLease**.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-224">hello lease ID is returned as `result.id` from **acquireLease**.</span></span>

> [!NOTE]
> <span data-ttu-id="5cbaf-225">Par défaut, la durée du bail hello est infinie.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-225">By default, hello lease duration is infinite.</span></span> <span data-ttu-id="5cbaf-226">Vous pouvez spécifier une durée non infini (entre 15 et 60 secondes) en fournissant hello `options.leaseDuration` paramètre.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-226">You can specify a non-infinite duration (between 15 and 60 seconds) by providing hello `options.leaseDuration` parameter.</span></span>
>
>

<span data-ttu-id="5cbaf-227">tooremove un bail, utilisez **releaseLease**.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-227">tooremove a lease, use **releaseLease**.</span></span> <span data-ttu-id="5cbaf-228">toobreak un bail, mais empêcher les autres utilisateurs d’obtenir un nouveau bail tant que la durée d’origine du hello a expiré, utilisez **breakLease**.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-228">toobreak a lease, but prevent others from obtaining a new lease until hello original duration has expired, use **breakLease**.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="5cbaf-229">Utilisation des signatures d'accès partagé</span><span class="sxs-lookup"><span data-stu-id="5cbaf-229">Work with shared access signatures</span></span>
<span data-ttu-id="5cbaf-230">Signatures d’accès partagé (SAS) sont un tooblobs d’un accès granulaire de tooprovide sûre et conteneurs sans fournir votre nom de compte de stockage ou vos clés.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-230">Shared access signatures (SAS) are a secure way tooprovide granular access tooblobs and containers without providing your storage account name or keys.</span></span> <span data-ttu-id="5cbaf-231">Signatures d’accès partagé sont souvent utilisés tooprovide limitée accès tooyour, par exemple pour autoriser une application mobile tooaccess BLOB.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-231">Shared access signatures are often used tooprovide limited access tooyour data, such as allowing a mobile app tooaccess blobs.</span></span>

> [!NOTE]
> <span data-ttu-id="5cbaf-232">Pendant que vous pouvez également autoriser l’accès anonyme tooblobs, signatures d’accès partagé permettent l’accès tooprovide plus contrôlé, que vous devez générer hello SAS.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-232">While you can also allow anonymous access tooblobs, shared access signatures allow you tooprovide more controlled access, as you must generate hello SAS.</span></span>
>
>

<span data-ttu-id="5cbaf-233">Une application de confiance, tel qu’un service nuage génère des signatures d’accès partagé à l’aide de hello **generateSharedAccessSignature** Hello **BlobService**et il fournit tooan non fiable ou niveau de confiance partiel d’application comme une application mobile.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-233">A trusted application such as a cloud-based service generates shared access signatures using hello **generateSharedAccessSignature** of hello **BlobService**, and provides it tooan untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="5cbaf-234">Accès partagé sont générées à l’aide d’une stratégie qui décrit le démarrage de hello et les dates de fin pendant le hello signatures d’accès partagé sont valides, mais aussi hello détenteur de signatures d’accès partagé de toohello accordé au niveau d’accès.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-234">Shared access signatures are generated using a policy, which describes hello start and end dates during which hello shared access signatures are valid, as well as hello access level granted toohello shared access signatures holder.</span></span>

<span data-ttu-id="5cbaf-235">exemple de code suivant Hello génère une nouvelle stratégie d’accès partagé qui permet de hello partagé accès signatures titulaire tooperform opérations de lecture sur hello **myblob** d’objets blob et 100 minutes après hello sa création n’expire.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-235">hello following code example generates a new shared access policy that allows hello shared access signatures holder tooperform read operations on hello **myblob** blob, and expires 100 minutes after hello time it is created.</span></span>

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
};

var blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', 'myblob', sharedAccessPolicy);
var host = blobSvc.host;
```

<span data-ttu-id="5cbaf-236">Notez que les informations sur l’hôte hello doivent être fournie, comme requis lorsque détenteur de signatures d’accès partagé hello tente également conteneur de hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-236">Note that hello host information must be provided also, as it is required when hello shared access signatures holder attempts tooaccess hello container.</span></span>

<span data-ttu-id="5cbaf-237">Hello client application utilise ensuite les signatures d’accès partagé avec **BlobServiceWithSAS** tooperform des opérations par rapport à l’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-237">hello client application then uses shared access signatures with **BlobServiceWithSAS** tooperform operations against hello blob.</span></span> <span data-ttu-id="5cbaf-238">Hello suivante obtient des informations sur **myblob**.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-238">hello following gets information about **myblob**.</span></span>

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

<span data-ttu-id="5cbaf-239">Étant donné que les signatures d’accès hello partagé a été générés avec un accès en lecture seule, si une tentative d’objet blob de hello toomodify, une erreur est renvoyée.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-239">Since hello shared access signatures were generated with read-only access, if an attempt is made toomodify hello blob, an error will be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="5cbaf-240">Listes de contrôle d'accès</span><span class="sxs-lookup"><span data-stu-id="5cbaf-240">Access control lists</span></span>
<span data-ttu-id="5cbaf-241">Vous pouvez également utiliser une stratégie d’accès hello tooset accès contrôle liste (ACL) pour les associations de sécurité.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-241">You can also use an access control list (ACL) tooset hello access policy for SAS.</span></span> <span data-ttu-id="5cbaf-242">Cela est utile si vous souhaitez tooallow plusieurs clients tooaccess un conteneur, mais fournissez des stratégies d’accès différents pour chaque client.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-242">This is useful if you wish tooallow multiple clients tooaccess a container but provide different access policies for each client.</span></span>

<span data-ttu-id="5cbaf-243">Une liste de contrôle d'accès est implémentée à l'aide d'un tableau de stratégies d'accès, dans lequel un ID est associé à chaque stratégie.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-243">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="5cbaf-244">Hello, exemple de code suivant définit deux stratégies, un pour « user1 » et un pour « user2 » :</span><span class="sxs-lookup"><span data-stu-id="5cbaf-244">hello following code example defines two policies, one for 'user1' and one for 'user2':</span></span>

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.WRITE,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="5cbaf-245">Hello suivant obtient d’exemple de code hello ACL actuel pour **mycontainer**, puis ajoute hello nouvelles stratégies à l’aide de **setBlobAcl**.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-245">hello following code example gets hello current ACL for **mycontainer**, and then adds hello new policies using **setBlobAcl**.</span></span> <span data-ttu-id="5cbaf-246">Cette approche permet :</span><span class="sxs-lookup"><span data-stu-id="5cbaf-246">This approach allows:</span></span>

```nodejs
var extend = require('extend');
blobSvc.getBlobAcl('mycontainer', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    blobSvc.setBlobAcl('mycontainer', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="5cbaf-247">Une fois hello QU'ACL est définie, vous pouvez ensuite créer des signatures d’accès partagé en fonction de ID hello pour une stratégie.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-247">Once hello ACL is set, you can then create shared access signatures based on hello ID for a policy.</span></span> <span data-ttu-id="5cbaf-248">Hello, exemple de code suivant crée les nouvelles signatures d’accès partagé pour « user2 » :</span><span class="sxs-lookup"><span data-stu-id="5cbaf-248">hello following code example creates new shared access signatures for 'user2':</span></span>

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="5cbaf-249">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5cbaf-249">Next steps</span></span>
<span data-ttu-id="5cbaf-250">Pour plus d’informations, consultez hello suivant des ressources.</span><span class="sxs-lookup"><span data-stu-id="5cbaf-250">For more information, see hello following resources.</span></span>

* <span data-ttu-id="5cbaf-251">[Kit de développement logiciel (SDK) Stockage Azure pour la référence de l’API Node][Kit de développement logiciel (SDK) Stockage Azure pour la référence de l'API Node]</span><span class="sxs-lookup"><span data-stu-id="5cbaf-251">[Azure Storage SDK for Node API Reference][Azure Storage SDK for Node API Reference]</span></span>
* <span data-ttu-id="5cbaf-252">[Blog de l’équipe Stockage Azure] [Blog de l’équipe Stockage Azure]</span><span class="sxs-lookup"><span data-stu-id="5cbaf-252">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>
* <span data-ttu-id="5cbaf-253">Référentiel [Kit de développement logiciel (SDK) Stockage Azure pour Node][Azure Storage SDK for Node] sur GitHub</span><span class="sxs-lookup"><span data-stu-id="5cbaf-253">[Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="5cbaf-254">Centre pour développeurs Node.js</span><span class="sxs-lookup"><span data-stu-id="5cbaf-254">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)
* [<span data-ttu-id="5cbaf-255">Transfert de données avec hello utilitaire de ligne de commande AzCopy</span><span class="sxs-lookup"><span data-stu-id="5cbaf-255">Transfer data with hello AzCopy command-line utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

<span data-ttu-id="5cbaf-256">[Application web Node.js à l’aide de hello Service de Table Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)  </span><span class="sxs-lookup"><span data-stu-id="5cbaf-256">[Node.js web app using hello Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)  </span></span>  
<span data-ttu-id="5cbaf-257">[Générer et déployer un tooAzure d’application web Node.js à l’aide de Web Matrix] : https://www.microsoft.com/web/webmatrix/</span><span class="sxs-lookup"><span data-stu-id="5cbaf-257">[Build and deploy a Node.js web app tooAzure using Web Matrix]: https://www.microsoft.com/web/webmatrix/</span></span>  
<span data-ttu-id="5cbaf-258">[À l’aide de hello API REST] : http://msdn.microsoft.com/library/azure/hh264518.aspx [Azure portal] : https://portal.azure.com [générer et déployer un tooan d’application Node.js Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Blog de l’équipe stockage Azure] : http:// blogs.msdn.com/b/windowsazurestorage/ [Azure SDK pour le nœud référence de l’API de stockage] : http://dl.windowsazure.com/nodestoragedocs/index.html</span><span class="sxs-lookup"><span data-stu-id="5cbaf-258">[Using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx [Azure portal]: https://portal.azure.com [Build and deploy a Node.js application tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/ [Azure Storage SDK for Node API Reference]: http://dl.windowsazure.com/nodestoragedocs/index.html</span></span>
