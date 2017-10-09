---
title: "aaaHow toouse stockage de Table Azure à partir de Node.js | Documents Microsoft"
description: "Stocker des données structurées dans le cloud hello avec le stockage Table Azure, un magasin de données NoSQL."
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 21022491a9a21a5365628de93582ea3a325ed869
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-nodejs"></a><span data-ttu-id="87f85-103">Comment toouse stockage de Table Azure à partir de Node.js</span><span class="sxs-lookup"><span data-stu-id="87f85-103">How toouse Azure Table storage from Node.js</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="87f85-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="87f85-104">Overview</span></span>
<span data-ttu-id="87f85-105">Cette rubrique montre comment les scénarios courants tooperform hello Table Azure à l’aide de service dans une application Node.js.</span><span class="sxs-lookup"><span data-stu-id="87f85-105">This topic shows how tooperform common scenarios using hello Azure Table service in a Node.js application.</span></span>

<span data-ttu-id="87f85-106">les exemples de code Hello dans cette rubrique supposent que vous disposez déjà d’une application Node.js.</span><span class="sxs-lookup"><span data-stu-id="87f85-106">hello code examples in this topic assume you already have a Node.js application.</span></span> <span data-ttu-id="87f85-107">Pour plus d’informations sur la façon toocreate une application Node.js dans Azure, consultez une des rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="87f85-107">For information about how toocreate a Node.js application in Azure, see any of these topics:</span></span>

* [<span data-ttu-id="87f85-108">Créer une application web Node.js dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="87f85-108">Create a Node.js web app in Azure App Service</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="87f85-109">Créer et déployer un tooAzure d’application web Node.js à l’aide de WebMatrix</span><span class="sxs-lookup"><span data-stu-id="87f85-109">Build and deploy a Node.js web app tooAzure using WebMatrix</span></span>](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* <span data-ttu-id="87f85-110">[Créer et déployer un tooan d’application Node.js Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (à l’aide de Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="87f85-110">[Build and deploy a Node.js application tooan Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (using Windows PowerShell)</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-tooaccess-azure-storage"></a><span data-ttu-id="87f85-111">Configurer votre tooaccess application Azure Storage</span><span class="sxs-lookup"><span data-stu-id="87f85-111">Configure your application tooaccess Azure Storage</span></span>
<span data-ttu-id="87f85-112">toouse stockage Azure, vous devez hello SDK de stockage Azure pour Node.js, qui inclut un ensemble de bibliothèques de commodité qui communiquent avec les services REST de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="87f85-112">toouse Azure Storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooinstall-hello-package"></a><span data-ttu-id="87f85-113">Utiliser le Gestionnaire de Package de nœud (NPM) tooinstall hello package</span><span class="sxs-lookup"><span data-stu-id="87f85-113">Use Node Package Manager (NPM) tooinstall hello package</span></span>
1. <span data-ttu-id="87f85-114">Utiliser une interface de ligne de commande tels que **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix), puis accédez dossier toohello où vous avez créé votre application.</span><span class="sxs-lookup"><span data-stu-id="87f85-114">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), and navigate toohello folder where you created your application.</span></span>
2. <span data-ttu-id="87f85-115">Type **npm installer le stockage azure** dans la fenêtre de commande hello.</span><span class="sxs-lookup"><span data-stu-id="87f85-115">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="87f85-116">Sortie de commande hello est similaire toohello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="87f85-116">Output from hello command is similar toohello following example.</span></span>

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
3. <span data-ttu-id="87f85-117">Vous pouvez exécuter manuellement hello **ls** tooverify de commande qui un **nœud\_modules** dossier a été créé.</span><span class="sxs-lookup"><span data-stu-id="87f85-117">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="87f85-118">Dans ce dossier, vous trouverez hello **le stockage azure** package qui contient les bibliothèques hello vous avez besoin de stockage de tooaccess.</span><span class="sxs-lookup"><span data-stu-id="87f85-118">Inside that folder you will find hello **azure-storage** package, which contains hello libraries you need tooaccess storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="87f85-119">Importer un package hello</span><span class="sxs-lookup"><span data-stu-id="87f85-119">Import hello package</span></span>
<span data-ttu-id="87f85-120">Ajouter hello suivant en haut de toohello code Hello **server.js** fichier dans votre application :</span><span class="sxs-lookup"><span data-stu-id="87f85-120">Add hello following code toohello top of hello **server.js** file in your application:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="87f85-121">Configurer une connexion Azure Storage</span><span class="sxs-lookup"><span data-stu-id="87f85-121">Set up an Azure Storage connection</span></span>
<span data-ttu-id="87f85-122">module de Hello azure lira des variables d’environnement hello AZURE\_stockage\_compte et AZURE\_stockage\_accès\_clé ou AZURE\_stockage\_connexion \_Chaîne pour les informations requises tooconnect tooyour compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="87f85-122">hello azure module will read hello environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="87f85-123">Si ces variables d’environnement ne sont pas définies, vous devez spécifier les informations de compte hello lors de l’appel **TableService**.</span><span class="sxs-lookup"><span data-stu-id="87f85-123">If these environment variables are not set, you must specify hello account information when calling **TableService**.</span></span>

<span data-ttu-id="87f85-124">Pour obtenir un exemple de la définition de variables d’environnement hello Bonjour [portail Azure](https://portal.azure.com) pour un site Web Azure, consultez [à l’aide de Node.js web application hello Service de Table Azure](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="87f85-124">For an example of setting hello environment variables in hello [Azure portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using hello Azure Table Service](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-table"></a><span data-ttu-id="87f85-125">Création d’une table</span><span class="sxs-lookup"><span data-stu-id="87f85-125">Create a table</span></span>
<span data-ttu-id="87f85-126">Hello de code suivant crée un **TableService** de l’objet et l’utilise toocreate une nouvelle table.</span><span class="sxs-lookup"><span data-stu-id="87f85-126">hello following code creates a **TableService** object and uses it toocreate a new table.</span></span> <span data-ttu-id="87f85-127">Ajoutez suit hello vers haut hello de **server.js**.</span><span class="sxs-lookup"><span data-stu-id="87f85-127">Add hello following near hello top of **server.js**.</span></span>

```nodejs
var tableSvc = azure.createTableService();
```

<span data-ttu-id="87f85-128">Hello appel trop**createTableIfNotExists** créera une nouvelle table avec le nom spécifié de hello si elle n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="87f85-128">hello call too**createTableIfNotExists** will create a new table with hello specified name if it does not already exist.</span></span> <span data-ttu-id="87f85-129">Hello exemple suivant crée une nouvelle table nommée « mytable » si elle n’existe pas déjà :</span><span class="sxs-lookup"><span data-stu-id="87f85-129">hello following example creates a new table named 'mytable' if it does not already exist:</span></span>

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

<span data-ttu-id="87f85-130">Hello `result.created` sera `true` si une nouvelle table est créée, et `false` si hello table existe déjà.</span><span class="sxs-lookup"><span data-stu-id="87f85-130">hello `result.created` will be `true` if a new table is created, and `false` if hello table already exists.</span></span> <span data-ttu-id="87f85-131">Hello `response` contiennent des informations sur la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="87f85-131">hello `response` will contain information about hello request.</span></span>

### <a name="filters"></a><span data-ttu-id="87f85-132">Filtres</span><span class="sxs-lookup"><span data-stu-id="87f85-132">Filters</span></span>
<span data-ttu-id="87f85-133">Les opérations de filtrage facultatif peuvent être appliquées toooperations effectuées à l’aide **TableService**.</span><span class="sxs-lookup"><span data-stu-id="87f85-133">Optional filtering operations can be applied toooperations performed using **TableService**.</span></span> <span data-ttu-id="87f85-134">Il peut s’agir d’opérations de journalisation, de relance automatique, etc. Les filtres sont des objets qui implémentent une méthode avec la signature de hello :</span><span class="sxs-lookup"><span data-stu-id="87f85-134">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="87f85-135">Après son prétraitement sur les options de demande hello, méthode hello doit toocall « suivant », en passant un rappel avec hello après signature :</span><span class="sxs-lookup"><span data-stu-id="87f85-135">After doing its preprocessing on hello request options, hello method needs toocall "next", passing a callback with hello following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="87f85-136">Dans ce rappel et après le traitement hello returnObject (réponse hello du serveur de toohello hello demande), le rappel de hello doit tooeither appeler ensuite s’il existe des toocontinue du traitement des autres filtres ou simplement appeler finalCallback sinon tooend hello appel de service.</span><span class="sxs-lookup"><span data-stu-id="87f85-136">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback otherwise tooend hello service invocation.</span></span>

<span data-ttu-id="87f85-137">Deux filtres qui implémentent la logique de nouvelle tentative sont incluses avec hello Azure SDK pour Node.js, **ExponentialRetryPolicyFilter** et **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="87f85-137">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="87f85-138">Hello suivante permet de créer un **TableService** objet qui utilise hello **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="87f85-138">hello following creates a **TableService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="87f85-139">Ajouter une table de tooa d’entité</span><span class="sxs-lookup"><span data-stu-id="87f85-139">Add an entity tooa table</span></span>
<span data-ttu-id="87f85-140">tooadd une entité, d’abord créer un objet qui définit les propriétés de l’entité.</span><span class="sxs-lookup"><span data-stu-id="87f85-140">tooadd an entity, first create an object that defines your entity properties.</span></span> <span data-ttu-id="87f85-141">Toutes les entités doivent contenir un **PartitionKey** et **RowKey**, qui sont des identificateurs uniques pour l’entité de hello.</span><span class="sxs-lookup"><span data-stu-id="87f85-141">All entities must contain a **PartitionKey** and **RowKey**, which are unique identifiers for hello entity.</span></span>

* <span data-ttu-id="87f85-142">**PartitionKey** -détermine la partition de hello entité de hello est stockée dans</span><span class="sxs-lookup"><span data-stu-id="87f85-142">**PartitionKey** - determines hello partition that hello entity is stored in</span></span>
* <span data-ttu-id="87f85-143">**RowKey** - identifie de façon unique identifie l’entité hello au sein de la partition de hello</span><span class="sxs-lookup"><span data-stu-id="87f85-143">**RowKey** - uniquely identifies hello entity within hello partition</span></span>

<span data-ttu-id="87f85-144">**PartitionKey** et **RowKey** doivent être des valeurs de chaîne.</span><span class="sxs-lookup"><span data-stu-id="87f85-144">Both **PartitionKey** and **RowKey** must be string values.</span></span> <span data-ttu-id="87f85-145">Pour plus d’informations, consultez [hello de présentation des modèle de données de Service de Table](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="87f85-145">For more information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="87f85-146">Hello Voici un exemple de définition d’une entité.</span><span class="sxs-lookup"><span data-stu-id="87f85-146">hello following is an example of defining an entity.</span></span> <span data-ttu-id="87f85-147">Notez que **dueDate** est définie comme un type de **Edm.DateTime**.</span><span class="sxs-lookup"><span data-stu-id="87f85-147">Note that **dueDate** is defined as a type of **Edm.DateTime**.</span></span> <span data-ttu-id="87f85-148">Spécifiant le type hello est facultatif et types seront déduits si n’est pas spécifiés.</span><span class="sxs-lookup"><span data-stu-id="87f85-148">Specifying hello type is optional, and types will be inferred if not specified.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> <span data-ttu-id="87f85-149">Il existe également un champ **Timestamp** pour chaque enregistrement, qui est défini par Azure quand une entité est insérée ou mise à jour.</span><span class="sxs-lookup"><span data-stu-id="87f85-149">There is also a **Timestamp** field for each record, which is set by Azure when an entity is inserted or updated.</span></span>
>
>

<span data-ttu-id="87f85-150">Vous pouvez également utiliser hello **entityGenerator** toocreate entités.</span><span class="sxs-lookup"><span data-stu-id="87f85-150">You can also use hello **entityGenerator** toocreate entities.</span></span> <span data-ttu-id="87f85-151">exemple Hello crée hello même entité de tâche à l’aide de hello **entityGenerator**.</span><span class="sxs-lookup"><span data-stu-id="87f85-151">hello following example creates hello same task entity using hello **entityGenerator**.</span></span>

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out hello trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

<span data-ttu-id="87f85-152">tooadd une table de tooyour entité, passez hello entité objet toohello **insertEntity** (méthode).</span><span class="sxs-lookup"><span data-stu-id="87f85-152">tooadd an entity tooyour table, pass hello entity object toohello **insertEntity** method.</span></span>

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

<span data-ttu-id="87f85-153">Si l’opération de hello est réussie, `result` contiendra hello [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) Hello insérer enregistrement et `response` contiennent des informations sur l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="87f85-153">If hello operation is successful, `result` will contain hello [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) of hello inserted record and `response` will contain information about hello operation.</span></span>

<span data-ttu-id="87f85-154">Exemple de réponse :</span><span class="sxs-lookup"><span data-stu-id="87f85-154">Example response:</span></span>

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> <span data-ttu-id="87f85-155">Par défaut, **insertEntity** ne retourne pas d’entité de hello inséré dans le cadre de hello `response` plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="87f85-155">By default, **insertEntity** does not return hello inserted entity as part of hello `response` information.</span></span> <span data-ttu-id="87f85-156">Si vous prévoyez d’effectuer d’autres opérations sur cette entité, ou que vous souhaitez des informations toocache hello, il peut être utile toohave elle est retournée en tant que partie de hello `result`.</span><span class="sxs-lookup"><span data-stu-id="87f85-156">If you plan on performing other operations on this entity, or wish toocache hello information, it can be useful toohave it returned as part of hello `result`.</span></span> <span data-ttu-id="87f85-157">Pour ce faire, activez **echoContent** comme suit :</span><span class="sxs-lookup"><span data-stu-id="87f85-157">You can do this by enabling **echoContent** as follows:</span></span>
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a><span data-ttu-id="87f85-158">Mise à jour d'une entité</span><span class="sxs-lookup"><span data-stu-id="87f85-158">Update an entity</span></span>
<span data-ttu-id="87f85-159">Il existe plusieurs tooupdate de méthodes disponibles pour une entité existante :</span><span class="sxs-lookup"><span data-stu-id="87f85-159">There are multiple methods available tooupdate an existing entity:</span></span>

* <span data-ttu-id="87f85-160">**replaceEntity** : met à jour une entité existante en la remplaçant</span><span class="sxs-lookup"><span data-stu-id="87f85-160">**replaceEntity** - updates an existing entity by replacing it</span></span>
* <span data-ttu-id="87f85-161">**mergeEntity** -met à jour une entité existante en fusionnant les nouvelles valeurs de propriété dans une entité existante de hello</span><span class="sxs-lookup"><span data-stu-id="87f85-161">**mergeEntity** - updates an existing entity by merging new property values into hello existing entity</span></span>
* <span data-ttu-id="87f85-162">**insertOrReplaceEntity** : met à jour une entité existante en la remplaçant.</span><span class="sxs-lookup"><span data-stu-id="87f85-162">**insertOrReplaceEntity** - updates an existing entity by replacing it.</span></span> <span data-ttu-id="87f85-163">En l’absence d’entité, une nouvelle entité est insérée.</span><span class="sxs-lookup"><span data-stu-id="87f85-163">If no entity exists, a new one will be inserted</span></span>
* <span data-ttu-id="87f85-164">**insertOrMergeEntity** -met à jour une entité existante en fusionnant des nouvelles valeurs de propriété dans hello existant.</span><span class="sxs-lookup"><span data-stu-id="87f85-164">**insertOrMergeEntity** - updates an existing entity by merging new property values into hello existing.</span></span> <span data-ttu-id="87f85-165">En l’absence d’entité, une nouvelle entité est insérée.</span><span class="sxs-lookup"><span data-stu-id="87f85-165">If no entity exists, a new one will be inserted</span></span>

<span data-ttu-id="87f85-166">Hello exemple suivant illustre la mise à jour une entité à l’aide de **replaceEntity**:</span><span class="sxs-lookup"><span data-stu-id="87f85-166">hello following example demonstrates updating an entity using **replaceEntity**:</span></span>

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> <span data-ttu-id="87f85-167">Par défaut, la mise à jour une entité ne vérifie pas le toosee si les données de salutation mis à jour précédemment a été modifiées par un autre processus.</span><span class="sxs-lookup"><span data-stu-id="87f85-167">By default, updating an entity does not check toosee if hello data being updated has previously been modified by another process.</span></span> <span data-ttu-id="87f85-168">mises à jour simultanées toosupport :</span><span class="sxs-lookup"><span data-stu-id="87f85-168">toosupport concurrent updates:</span></span>
>
> 1. <span data-ttu-id="87f85-169">Obtenir hello ETag de l’objet hello mis à jour.</span><span class="sxs-lookup"><span data-stu-id="87f85-169">Get hello ETag of hello object being updated.</span></span> <span data-ttu-id="87f85-170">Cela est retourné en tant que partie de hello `response` pour toute opération dépendant de l’entité et peuvent être récupérées via `response['.metadata'].etag`.</span><span class="sxs-lookup"><span data-stu-id="87f85-170">This is returned as part of hello `response` for any entity-related operation and can be retrieved through `response['.metadata'].etag`.</span></span>
> 2. <span data-ttu-id="87f85-171">Lorsque vous effectuez une opération de mise à jour sur une entité, ajouter des informations d’ETag hello précédemment récupérées toohello nouvelle entité.</span><span class="sxs-lookup"><span data-stu-id="87f85-171">When performing an update operation on an entity, add hello ETag information previously retrieved toohello new entity.</span></span> <span data-ttu-id="87f85-172">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="87f85-172">For example:</span></span>
>
>       <span data-ttu-id="87f85-173">entity2['.metadata'].etag = currentEtag;</span><span class="sxs-lookup"><span data-stu-id="87f85-173">entity2['.metadata'].etag = currentEtag;</span></span>
> 3. <span data-ttu-id="87f85-174">Effectuer l’opération de mise à jour hello.</span><span class="sxs-lookup"><span data-stu-id="87f85-174">Perform hello update operation.</span></span> <span data-ttu-id="87f85-175">Si l’entité de hello a été modifiée depuis la récupération de valeur d’ETag hello, telles qu’une autre instance de votre application, un `error` s’affichera indiquant que la condition de mise à jour de hello spécifiée dans la demande de hello n’est pas remplie.</span><span class="sxs-lookup"><span data-stu-id="87f85-175">If hello entity has been modified since you retrieved hello ETag value, such as another instance of your application, an `error` will be returned stating that hello update condition specified in hello request was not satisfied.</span></span>
>
>

<span data-ttu-id="87f85-176">Avec **replaceEntity** et **mergeEntity**, si l’entité hello est en cours de mise à jour n’existe, opération de mise à jour hello échoue.</span><span class="sxs-lookup"><span data-stu-id="87f85-176">With **replaceEntity** and **mergeEntity**, if hello entity that is being updated doesn't exist, then hello update operation will fail.</span></span> <span data-ttu-id="87f85-177">Par conséquent, si vous le souhaitez toostore une entité, même si elle existe déjà, utilisez **insertOrReplaceEntity** ou **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="87f85-177">Therefore if you wish toostore an entity regardless of whether it already exists, use **insertOrReplaceEntity** or **insertOrMergeEntity**.</span></span>

<span data-ttu-id="87f85-178">Hello `result` pour la mise à jour réussie opérations contiendra hello **Etag** Hello mise à jour d’entité.</span><span class="sxs-lookup"><span data-stu-id="87f85-178">hello `result` for successful update operations will contain hello **Etag** of hello updated entity.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="87f85-179">Utilisation des groupes d'entités</span><span class="sxs-lookup"><span data-stu-id="87f85-179">Work with groups of entities</span></span>
<span data-ttu-id="87f85-180">Il est parfois sens toosubmit plusieurs opérations ensemble dans un lot tooensure atomique de traitement par le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="87f85-180">Sometimes it makes sense toosubmit multiple operations together in a batch tooensure atomic processing by hello server.</span></span> <span data-ttu-id="87f85-181">tooaccomplish qui, utilisez hello **TableBatch** toocreate un lot de la classe et ensuite utiliser hello **executeBatch** méthode **TableService** tooperform hello les opérations par lots.</span><span class="sxs-lookup"><span data-stu-id="87f85-181">tooaccomplish that, use hello **TableBatch** class toocreate a batch, and then use hello **executeBatch** method of **TableService** tooperform hello batched operations.</span></span>

 <span data-ttu-id="87f85-182">Hello l’exemple suivant illustre l’envoi de deux entités dans un lot :</span><span class="sxs-lookup"><span data-stu-id="87f85-182">hello following example demonstrates submitting two entities in a batch:</span></span>

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash hello dishes'},
  dueDate: {'_':new Date(2015, 6, 20)}
};

var batch = new azure.TableBatch();

batch.insertEntity(task1, {echoContent: true});
batch.insertEntity(task2, {echoContent: true});

tableSvc.executeBatch('mytable', batch, function (error, result, response) {
  if(!error) {
    // Batch completed
  }
});
```

<span data-ttu-id="87f85-183">Pour les opérations de traitement réussi, `result` contient des informations pour chaque opération de traitement par lots hello.</span><span class="sxs-lookup"><span data-stu-id="87f85-183">For successful batch operations, `result` will contain information for each operation in hello batch.</span></span>

### <a name="work-with-batched-operations"></a><span data-ttu-id="87f85-184">Ultiliser des opérations de traitement par lot</span><span class="sxs-lookup"><span data-stu-id="87f85-184">Work with batched operations</span></span>
<span data-ttu-id="87f85-185">Opérations ajoutées tooa lot peut être inspecté en consultant hello `operations` propriété.</span><span class="sxs-lookup"><span data-stu-id="87f85-185">Operations added tooa batch can be inspected by viewing hello `operations` property.</span></span> <span data-ttu-id="87f85-186">Vous pouvez également utiliser hello suivant toowork méthodes avec des opérations :</span><span class="sxs-lookup"><span data-stu-id="87f85-186">You can also use hello following methods toowork with operations:</span></span>

* <span data-ttu-id="87f85-187">**clear** : permet de supprimer toutes les opérations d’un lot</span><span class="sxs-lookup"><span data-stu-id="87f85-187">**clear** - clears all operations from a batch</span></span>
* <span data-ttu-id="87f85-188">**getOperations** -obtient d’une opération de traitement par lots hello</span><span class="sxs-lookup"><span data-stu-id="87f85-188">**getOperations** - gets an operation from hello batch</span></span>
* <span data-ttu-id="87f85-189">**hasOperations** -renvoie la valeur true si le traitement par lots hello contient des opérations</span><span class="sxs-lookup"><span data-stu-id="87f85-189">**hasOperations** - returns true if hello batch contains operations</span></span>
* <span data-ttu-id="87f85-190">**removeOperations** : permet de supprimer une opération</span><span class="sxs-lookup"><span data-stu-id="87f85-190">**removeOperations** - removes an operation</span></span>
* <span data-ttu-id="87f85-191">**taille** -renvoie hello nombre d’opérations de traitement par lots hello</span><span class="sxs-lookup"><span data-stu-id="87f85-191">**size** - returns hello number of operations in hello batch</span></span>

## <a name="retrieve-an-entity-by-key"></a><span data-ttu-id="87f85-192">Récupération d'une entité par clé</span><span class="sxs-lookup"><span data-stu-id="87f85-192">Retrieve an entity by key</span></span>
<span data-ttu-id="87f85-193">tooreturn une entité spécifique en fonction de hello **PartitionKey** et **RowKey**, utilisez hello **retrieveEntity** (méthode).</span><span class="sxs-lookup"><span data-stu-id="87f85-193">tooreturn a specific entity based on hello **PartitionKey** and **RowKey**, use hello **retrieveEntity** method.</span></span>

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains hello entity
  }
});
```

<span data-ttu-id="87f85-194">Une fois cette opération terminée, `result` contiendra une entité de hello.</span><span class="sxs-lookup"><span data-stu-id="87f85-194">Once this operation is complete, `result` will contain hello entity.</span></span>

## <a name="query-a-set-of-entities"></a><span data-ttu-id="87f85-195">Interrogation d’un ensemble d’entités</span><span class="sxs-lookup"><span data-stu-id="87f85-195">Query a set of entities</span></span>
<span data-ttu-id="87f85-196">tooquery une table, utilisez hello **TableQuery** toobuild d’une expression de requête à l’aide de hello après des clauses de l’objet :</span><span class="sxs-lookup"><span data-stu-id="87f85-196">tooquery a table, use hello **TableQuery** object toobuild up a query expression using hello following clauses:</span></span>

* <span data-ttu-id="87f85-197">**Sélectionnez** -hello champs toobe renvoyés par la requête de hello</span><span class="sxs-lookup"><span data-stu-id="87f85-197">**select** - hello fields toobe returned from hello query</span></span>
* <span data-ttu-id="87f85-198">**où** - hello où clause</span><span class="sxs-lookup"><span data-stu-id="87f85-198">**where** - hello where clause</span></span>

  * <span data-ttu-id="87f85-199">**and** : condition where `and`</span><span class="sxs-lookup"><span data-stu-id="87f85-199">**and** - an `and` where condition</span></span>
  * <span data-ttu-id="87f85-200">**or** : condition where `or`</span><span class="sxs-lookup"><span data-stu-id="87f85-200">**or** - an `or` where condition</span></span>
* <span data-ttu-id="87f85-201">**haut** -hello le nombre d’éléments toofetch</span><span class="sxs-lookup"><span data-stu-id="87f85-201">**top** - hello number of items toofetch</span></span>

<span data-ttu-id="87f85-202">Hello exemple suivant crée une requête qui retournera hello supérieur cinq éléments avec un PartitionKey de 'hometasks'.</span><span class="sxs-lookup"><span data-stu-id="87f85-202">hello following example builds a query that will return hello top five items with a PartitionKey of 'hometasks'.</span></span>

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

<span data-ttu-id="87f85-203">Comme **select** n'est pas utilisé, tous les champs sont renvoyés.</span><span class="sxs-lookup"><span data-stu-id="87f85-203">Since **select** is not used, all fields will be returned.</span></span> <span data-ttu-id="87f85-204">requête de hello tooperform par rapport à une table, utilisez **queryEntities**.</span><span class="sxs-lookup"><span data-stu-id="87f85-204">tooperform hello query against a table, use **queryEntities**.</span></span> <span data-ttu-id="87f85-205">Hello exemple suivant utilise cette tooreturn interroger des entités à partir de « mytable ».</span><span class="sxs-lookup"><span data-stu-id="87f85-205">hello following example uses this query tooreturn entities from 'mytable'.</span></span>

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

<span data-ttu-id="87f85-206">En cas de réussite, `result.entries` contient un tableau d’entités qui correspond à la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="87f85-206">If successful, `result.entries` will contain an array of entities that match hello query.</span></span> <span data-ttu-id="87f85-207">Si la requête de hello a été tooreturn Impossible de toutes les entités, `result.continuationToken` sera non -*null* et peut être utilisé comme hello troisième paramètre de **queryEntities** tooretrieve résultats supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="87f85-207">If hello query was unable tooreturn all entities, `result.continuationToken` will be non-*null* and can be used as hello third parameter of **queryEntities** tooretrieve more results.</span></span> <span data-ttu-id="87f85-208">Pour la requête initiale de hello, utilisez *null* pour le troisième paramètre de hello.</span><span class="sxs-lookup"><span data-stu-id="87f85-208">For hello initial query, use *null* for hello third parameter.</span></span>

### <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="87f85-209">Interrogation d’un sous-ensemble de propriétés d’entité</span><span class="sxs-lookup"><span data-stu-id="87f85-209">Query a subset of entity properties</span></span>
<span data-ttu-id="87f85-210">Une table de tooa de requête peut récupérer que quelques champs à partir d’une entité.</span><span class="sxs-lookup"><span data-stu-id="87f85-210">A query tooa table can retrieve just a few fields from an entity.</span></span>
<span data-ttu-id="87f85-211">Ceci permet de réduire la consommation de bande passante et peut améliorer les performances des requêtes, notamment pour les entités volumineuses.</span><span class="sxs-lookup"><span data-stu-id="87f85-211">This reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="87f85-212">Hello d’utilisation **sélectionnez** clause et passez les noms hello de hello champs toobe retournés.</span><span class="sxs-lookup"><span data-stu-id="87f85-212">Use hello **select** clause and pass hello names of hello fields toobe returned.</span></span> <span data-ttu-id="87f85-213">Par exemple, hello requête suivante retournera uniquement hello **description** et **dueDate** champs.</span><span class="sxs-lookup"><span data-stu-id="87f85-213">For example, hello following query will return only hello **description** and **dueDate** fields.</span></span>

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a><span data-ttu-id="87f85-214">Suppression d’une entité</span><span class="sxs-lookup"><span data-stu-id="87f85-214">Delete an entity</span></span>
<span data-ttu-id="87f85-215">Vous pouvez supprimer une entité en utilisant ses clés de partition et de ligne.</span><span class="sxs-lookup"><span data-stu-id="87f85-215">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="87f85-216">Dans cet exemple, hello **task1** objet contient hello **RowKey** et **PartitionKey** valeurs hello entité toobe est supprimé.</span><span class="sxs-lookup"><span data-stu-id="87f85-216">In this example, hello **task1** object contains hello **RowKey** and **PartitionKey** values of hello entity toobe deleted.</span></span> <span data-ttu-id="87f85-217">Objet de hello est transmis toohello **deleteEntity** (méthode).</span><span class="sxs-lookup"><span data-stu-id="87f85-217">Then hello object is passed toohello **deleteEntity** method.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'}
};

tableSvc.deleteEntity('mytable', task, function(error, response){
  if(!error) {
    // Entity deleted
  }
});
```

> [!NOTE]
> <span data-ttu-id="87f85-218">Envisagez d’utiliser les ETags lors de la suppression d’éléments, tooensure hello élément n’a pas été modifiée par un autre processus.</span><span class="sxs-lookup"><span data-stu-id="87f85-218">Consider using ETags when deleting items, tooensure that hello item hasn't been modified by another process.</span></span> <span data-ttu-id="87f85-219">Consultez [Mise à jour d’une entité](#update-an-entity) pour plus d’informations sur l’utilisation des ETags.</span><span class="sxs-lookup"><span data-stu-id="87f85-219">See [Update an entity](#update-an-entity) for information on using ETags.</span></span>
>
>

## <a name="delete-a-table"></a><span data-ttu-id="87f85-220">Suppression d’une table</span><span class="sxs-lookup"><span data-stu-id="87f85-220">Delete a table</span></span>
<span data-ttu-id="87f85-221">Hello suivant code supprime une table à partir d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="87f85-221">hello following code deletes a table from a storage account.</span></span>

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

<span data-ttu-id="87f85-222">Si vous ne savez pas si la table de hello existe, utilisez **deleteTableIfExists**.</span><span class="sxs-lookup"><span data-stu-id="87f85-222">If you are uncertain whether hello table exists, use **deleteTableIfExists**.</span></span>

## <a name="use-continuation-tokens"></a><span data-ttu-id="87f85-223">Utiliser des jetons de liaison</span><span class="sxs-lookup"><span data-stu-id="87f85-223">Use continuation tokens</span></span>
<span data-ttu-id="87f85-224">Si vous interrogez des tables et que les résultats peuvent être volumineux, recherchez des jetons de liaison.</span><span class="sxs-lookup"><span data-stu-id="87f85-224">When you are querying tables for large amounts of results, look for continuation tokens.</span></span> <span data-ttu-id="87f85-225">Grandes quantités de données peuvent être disponibles pour votre requête que vous avez ne peut-être pas réalisé si vous ne générez pas toorecognize lorsqu’un jeton de continuation est présent.</span><span class="sxs-lookup"><span data-stu-id="87f85-225">There may be large amounts of data available for your query that you might not realize if you do not build toorecognize when a continuation token is present.</span></span>

<span data-ttu-id="87f85-226">résultats de Hello de l’objet retourné lors de l’interrogation de jeux d’entités un `continuationToken` propriété lorsque ce jeton est présent.</span><span class="sxs-lookup"><span data-stu-id="87f85-226">hello results object returned during querying entities sets a `continuationToken` property when such a token is present.</span></span> <span data-ttu-id="87f85-227">Vous pouvez ensuite utiliser lors de l’exécution d’un toomove toocontinue de requête entre les entités de partition et table hello.</span><span class="sxs-lookup"><span data-stu-id="87f85-227">You can then use this when performing a query toocontinue toomove across hello partition and table entities.</span></span>

<span data-ttu-id="87f85-228">Lors de l’interrogation, un paramètre continuationToken peut être fourni entre l’instance d’objet de requête de hello et la fonction de rappel hello :</span><span class="sxs-lookup"><span data-stu-id="87f85-228">When querying, a continuationToken parameter may be provided between hello query object instance and hello callback function:</span></span>

```nodejs
var nextContinuationToken = null;
dc.table.queryEntities(tableName,
    query,
    nextContinuationToken,
    function (error, results) {
        if (error) throw error;

        // iterate through results.entries with results

        if (results.continuationToken) {
            nextContinuationToken = results.continuationToken;
        }

    });
```

<span data-ttu-id="87f85-229">Si vous Inspectez hello `continuationToken` objet, vous rechercherez propriétés telles que `nextPartitionKey`, `nextRowKey` et `targetLocation`, ce qui peut être utilisé tooiterate via tous les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="87f85-229">If you inspect hello `continuationToken` object, you will find properties such as `nextPartitionKey`, `nextRowKey` and `targetLocation`, which can be used tooiterate through all hello results.</span></span>

<span data-ttu-id="87f85-230">Il existe également un exemple de continuation dans le référentiel de Node.js de stockage Azure hello sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="87f85-230">There is also a continuation sample within hello Azure Storage Node.js repo on GitHub.</span></span> <span data-ttu-id="87f85-231">Recherchez `examples/samples/continuationsample.js`.</span><span class="sxs-lookup"><span data-stu-id="87f85-231">Look for `examples/samples/continuationsample.js`.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="87f85-232">Utilisation des signatures d'accès partagé</span><span class="sxs-lookup"><span data-stu-id="87f85-232">Work with shared access signatures</span></span>
<span data-ttu-id="87f85-233">Signatures d’accès partagé (SAS) sont un tootables d’un accès granulaire tooprovide sûre sans fournir votre nom de compte de stockage ou vos clés.</span><span class="sxs-lookup"><span data-stu-id="87f85-233">Shared access signatures (SAS) are a secure way tooprovide granular access tootables without providing your storage account name or keys.</span></span> <span data-ttu-id="87f85-234">Associations de sécurité sont souvent utilisés tooprovide limitée accès tooyour, par exemple pour autoriser une application mobile tooquery enregistrements.</span><span class="sxs-lookup"><span data-stu-id="87f85-234">SAS are often used tooprovide limited access tooyour data, such as allowing a mobile app tooquery records.</span></span>

<span data-ttu-id="87f85-235">Une application de confiance, tel qu’un service nuage génère une SAP à l’aide de hello **generateSharedAccessSignature** Hello **TableService**et il fournit tooan application non approuvée ou niveau de confiance partiel par exemple une application mobile.</span><span class="sxs-lookup"><span data-stu-id="87f85-235">A trusted application such as a cloud-based service generates a SAS using hello **generateSharedAccessSignature** of hello **TableService**, and provides it tooan untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="87f85-236">Hello SAS est générée à l’aide d’une stratégie qui décrit le démarrage de hello et fin pendant le hello SAS est valide, ainsi que hello détenteur SAS toohello accordé au niveau de l’accès.</span><span class="sxs-lookup"><span data-stu-id="87f85-236">hello SAS is generated using a policy, which describes hello start and end dates during which hello SAS is valid, as well as hello access level granted toohello SAS holder.</span></span>

<span data-ttu-id="87f85-237">Hello exemple suivant génère une nouvelle stratégie d’accès partagé qui permettra de hello de la table hello SAP titulaire tooquery (« r ») et expire 100 minutes après hello sa création.</span><span class="sxs-lookup"><span data-stu-id="87f85-237">hello following example generates a new shared access policy that will allow hello SAS holder tooquery ('r') hello table, and expires 100 minutes after hello time it is created.</span></span>

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
};

var tableSAS = tableSvc.generateSharedAccessSignature('mytable', sharedAccessPolicy);
var host = tableSvc.host;
```

<span data-ttu-id="87f85-238">Notez que les informations sur l’hôte hello doivent être fournie, comme requis lorsque détenteur SAS hello tente également table de hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="87f85-238">Note that hello host information must be provided also, as it is required when hello SAS holder attempts tooaccess hello table.</span></span>

<span data-ttu-id="87f85-239">Hello application cliente, puis utilise hello SAS avec **TableServiceWithSAS** tooperform des opérations par rapport à la table de hello.</span><span class="sxs-lookup"><span data-stu-id="87f85-239">hello client application then uses hello SAS with **TableServiceWithSAS** tooperform operations against hello table.</span></span> <span data-ttu-id="87f85-240">Bonjour à l’exemple suivant connecte toohello table et effectue une requête.</span><span class="sxs-lookup"><span data-stu-id="87f85-240">hello following example connects toohello table and performs a query.</span></span>

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains hello entities
  }
});
```

<span data-ttu-id="87f85-241">Hello SAP a été générée avec un accès de requête, si une tentative a été faite tooinsert, mettre à jour ou supprimer des entités, une erreur est retournée.</span><span class="sxs-lookup"><span data-stu-id="87f85-241">Since hello SAS was generated with only query access, if an attempt were made tooinsert, update, or delete entities, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="87f85-242">Listes de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="87f85-242">Access Control Lists</span></span>
<span data-ttu-id="87f85-243">Vous pouvez également utiliser une stratégie d’accès de liste de contrôle d’accès (ACL) tooset hello pour une SAP.</span><span class="sxs-lookup"><span data-stu-id="87f85-243">You can also use an Access Control List (ACL) tooset hello access policy for a SAS.</span></span> <span data-ttu-id="87f85-244">Cela est utile si vous souhaitez tooallow table hello de tooaccess plusieurs clients, mais fournissez des stratégies d’accès différents pour chaque client.</span><span class="sxs-lookup"><span data-stu-id="87f85-244">This is useful if you wish tooallow multiple clients tooaccess hello table, but provide different access policies for each client.</span></span>

<span data-ttu-id="87f85-245">Une liste de contrôle d'accès est implémentée à l'aide d'un tableau de stratégies d'accès, dans lequel un ID est associé à chaque stratégie.</span><span class="sxs-lookup"><span data-stu-id="87f85-245">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="87f85-246">Bonjour à l’exemple suivant définit deux stratégies, un pour « user1 » et un pour « user2 » :</span><span class="sxs-lookup"><span data-stu-id="87f85-246">hello following example defines two policies, one for 'user1' and one for 'user2':</span></span>

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="87f85-247">Hello suivant obtient de l’exemple hello ACL actuel pour hello **hometasks** de table et y ajoute hello nouvelles stratégies à l’aide de **setTableAcl**.</span><span class="sxs-lookup"><span data-stu-id="87f85-247">hello following example gets hello current ACL for hello **hometasks** table, and then adds hello new policies using **setTableAcl**.</span></span> <span data-ttu-id="87f85-248">Cette approche permet :</span><span class="sxs-lookup"><span data-stu-id="87f85-248">This approach allows:</span></span>

```nodejs
var extend = require('extend');
tableSvc.getTableAcl('hometasks', function(error, result, response) {
if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    tableSvc.setTableAcl('hometasks', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="87f85-249">Une fois hello QU'ACL a été défini, vous pouvez ensuite créer un SAS en fonction de ID hello pour une stratégie.</span><span class="sxs-lookup"><span data-stu-id="87f85-249">Once hello ACL has been set, you can then create a SAS based on hello ID for a policy.</span></span> <span data-ttu-id="87f85-250">Bonjour à l’exemple suivant crée une nouvelle SAP pour « user2 » :</span><span class="sxs-lookup"><span data-stu-id="87f85-250">hello following example creates a new SAS for 'user2':</span></span>

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="87f85-251">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="87f85-251">Next steps</span></span>
<span data-ttu-id="87f85-252">Pour plus d’informations, consultez hello suivant des ressources.</span><span class="sxs-lookup"><span data-stu-id="87f85-252">For more information, see hello following resources.</span></span>

* <span data-ttu-id="87f85-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome gratuit, à partir de Microsoft qui vous permet de toowork visuellement avec des données de stockage Azure sur Windows, Mac OS et Linux.</span><span class="sxs-lookup"><span data-stu-id="87f85-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="87f85-254">[Kit de développement logiciel (SDK) Azure Storage pour Node](https://github.com/Azure/azure-storage-node) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="87f85-254">[Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) repository on GitHub.</span></span>
* [<span data-ttu-id="87f85-255">Centre pour développeurs Node.js</span><span class="sxs-lookup"><span data-stu-id="87f85-255">Node.js Developer Center</span></span>](/develop/nodejs/)
* [<span data-ttu-id="87f85-256">Créer et déployer un tooan d’application Node.js site Web Azure</span><span class="sxs-lookup"><span data-stu-id="87f85-256">Create and deploy a Node.js application tooan Azure website</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
