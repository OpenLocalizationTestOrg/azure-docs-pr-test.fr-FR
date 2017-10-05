---
title: "Utilisation du stockage Table Azure à partir de Node.js | Microsoft Docs"
description: "Stockez des données structurées dans le cloud à l’aide du stockage de tables Azure, un magasin de données NoSQL."
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: f004408910aecc380e20f7da54dbd155d179aaa5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-table-storage-from-nodejs"></a><span data-ttu-id="d762a-103">Utilisation du stockage de tables Azure à partir de Node.js</span><span class="sxs-lookup"><span data-stu-id="d762a-103">How to use Azure Table storage from Node.js</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="d762a-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="d762a-104">Overview</span></span>
<span data-ttu-id="d762a-105">Cette rubrique décrit le déroulement de scénarios courants dans le cadre de l’utilisation du service de Table Azure dans une application Node.js.</span><span class="sxs-lookup"><span data-stu-id="d762a-105">This topic shows how to perform common scenarios using the Azure Table service in a Node.js application.</span></span>

<span data-ttu-id="d762a-106">Les exemples de code de cette rubrique partent du principe que vous disposez déjà d'une application Node.js.</span><span class="sxs-lookup"><span data-stu-id="d762a-106">The code examples in this topic assume you already have a Node.js application.</span></span> <span data-ttu-id="d762a-107">Pour plus d’informations sur la création d’une application Node.js dans Azure, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="d762a-107">For information about how to create a Node.js application in Azure, see any of these topics:</span></span>

* [<span data-ttu-id="d762a-108">Créer une application web Node.js dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d762a-108">Create a Node.js web app in Azure App Service</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="d762a-109">Créer et déployer une application web Node.js dans Azure à l’aide de WebMatrix</span><span class="sxs-lookup"><span data-stu-id="d762a-109">Build and deploy a Node.js web app to Azure using WebMatrix</span></span>](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* <span data-ttu-id="d762a-110">[Création et déploiement d’une application Node.js dans un service cloud Azure](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (avec Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="d762a-110">[Build and deploy a Node.js application to an Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (using Windows PowerShell)</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-to-access-azure-storage"></a><span data-ttu-id="d762a-111">Configuration de votre application pour accéder à Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d762a-111">Configure your application to access Azure Storage</span></span>
<span data-ttu-id="d762a-112">Pour utiliser Azure Storage, vous avez besoin du Kit de développement logiciel (SDK) Azure Storage pour Node.js, qui inclut un ensemble de bibliothèques pratiques qui communiquent avec les services REST de stockage.</span><span class="sxs-lookup"><span data-stu-id="d762a-112">To use Azure Storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-install-the-package"></a><span data-ttu-id="d762a-113">Utilisation de Node Package Manager (NPM) pour installer le package</span><span class="sxs-lookup"><span data-stu-id="d762a-113">Use Node Package Manager (NPM) to install the package</span></span>
1. <span data-ttu-id="d762a-114">Utilisez une interface de ligne de commande telle que **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix) pour accéder au dossier dans lequel vous avez créé votre application.</span><span class="sxs-lookup"><span data-stu-id="d762a-114">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), and navigate to the folder where you created your application.</span></span>
2. <span data-ttu-id="d762a-115">Tapez **npm install azure-storage** dans la fenêtre de commande.</span><span class="sxs-lookup"><span data-stu-id="d762a-115">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="d762a-116">Le résultat de la commande ressemble à l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="d762a-116">Output from the command is similar to the following example.</span></span>

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
3. <span data-ttu-id="d762a-117">Vous pouvez exécuter manuellement la commande **ls** pour vérifier que le dossier **node\_modules** a été créé.</span><span class="sxs-lookup"><span data-stu-id="d762a-117">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="d762a-118">Dans ce dossier, recherchez le dossier **azure-storage** , qui contient les bibliothèques dont vous avez besoin pour accéder au stockage.</span><span class="sxs-lookup"><span data-stu-id="d762a-118">Inside that folder you will find the **azure-storage** package, which contains the libraries you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="d762a-119">Importation du package</span><span class="sxs-lookup"><span data-stu-id="d762a-119">Import the package</span></span>
<span data-ttu-id="d762a-120">Ajoutez le code suivant en haut du fichier **server.js** dans votre application :</span><span class="sxs-lookup"><span data-stu-id="d762a-120">Add the following code to the top of the **server.js** file in your application:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="d762a-121">Configurer une connexion Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d762a-121">Set up an Azure Storage connection</span></span>
<span data-ttu-id="d762a-122">Le module Azure lit les variables d’environnement AZURE\_STORAGE\_ACCOUNT et AZURE\_STORAGE\_ACCESS\_KEY, ou AZURE\_STORAGE\_CONNECTION\_STRING pour obtenir les informations nécessaires à la connexion à votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d762a-122">The azure module will read the environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="d762a-123">Si ces variables d'environnement ne sont pas définies, vous devez spécifier les informations de compte lors de l'appel de **TableService**.</span><span class="sxs-lookup"><span data-stu-id="d762a-123">If these environment variables are not set, you must specify the account information when calling **TableService**.</span></span>

<span data-ttu-id="d762a-124">Pour obtenir un exemple de configuration des variables d’environnement dans le [portail Azure](https://portal.azure.com) pour un site web Azure, consultez [Application web Node.js avec le service de Table Azure](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="d762a-124">For an example of setting the environment variables in the [Azure portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using the Azure Table Service](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-table"></a><span data-ttu-id="d762a-125">Création d’une table</span><span class="sxs-lookup"><span data-stu-id="d762a-125">Create a table</span></span>
<span data-ttu-id="d762a-126">Le code suivant crée un objet **TableService** et l'utilise pour créer une table.</span><span class="sxs-lookup"><span data-stu-id="d762a-126">The following code creates a **TableService** object and uses it to create a new table.</span></span> <span data-ttu-id="d762a-127">Ajoutez le code suivant vers le début du fichier **server.js**:</span><span class="sxs-lookup"><span data-stu-id="d762a-127">Add the following near the top of **server.js**.</span></span>

```nodejs
var tableSvc = azure.createTableService();
```

<span data-ttu-id="d762a-128">L’appel de **createTableIfNotExists** crée une nouvelle table avec le nom spécifié si elle n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="d762a-128">The call to **createTableIfNotExists** will create a new table with the specified name if it does not already exist.</span></span> <span data-ttu-id="d762a-129">Dans l'exemple suivant, la table 'mytable' est créée, si elle n'existe pas déjà :</span><span class="sxs-lookup"><span data-stu-id="d762a-129">The following example creates a new table named 'mytable' if it does not already exist:</span></span>

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

<span data-ttu-id="d762a-130">`result.created` est `true` si une table est créée et `false` si la table existe déjà.</span><span class="sxs-lookup"><span data-stu-id="d762a-130">The `result.created` will be `true` if a new table is created, and `false` if the table already exists.</span></span> <span data-ttu-id="d762a-131">`response` contient des informations sur la demande.</span><span class="sxs-lookup"><span data-stu-id="d762a-131">The `response` will contain information about the request.</span></span>

### <a name="filters"></a><span data-ttu-id="d762a-132">Filtres</span><span class="sxs-lookup"><span data-stu-id="d762a-132">Filters</span></span>
<span data-ttu-id="d762a-133">Des opérations facultatives de filtrage peuvent être appliquées aux opérations exécutées via **TableService**.</span><span class="sxs-lookup"><span data-stu-id="d762a-133">Optional filtering operations can be applied to operations performed using **TableService**.</span></span> <span data-ttu-id="d762a-134">Il peut s’agir d’opérations de journalisation, de relance automatique, etc. Les filtres sont des objets qui implémentent une méthode avec la signature :</span><span class="sxs-lookup"><span data-stu-id="d762a-134">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="d762a-135">Après le prétraitement des options de la requête, la méthode doit appeler « next », en passant un rappel avec la signature suivante :</span><span class="sxs-lookup"><span data-stu-id="d762a-135">After doing its preprocessing on the request options, the method needs to call "next", passing a callback with the following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="d762a-136">Dans ce rappel, et après le traitement de returnObject (la réponse de la requête au serveur), le rappel doit appeler la fonction next, si elle existe, pour continuer à traiter d’autres filtres ou simplement appeler finalCallback pour terminer l’utilisation du service.</span><span class="sxs-lookup"><span data-stu-id="d762a-136">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback otherwise to end the service invocation.</span></span>

<span data-ttu-id="d762a-137">Deux filtres qui implémentent la logique de relance sont inclus dans le Kit de développement logiciel (SDK) Azure pour Node.js : **ExponentialRetryPolicyFilter** et **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="d762a-137">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="d762a-138">Le code suivant crée un objet **TableService** qui utilise le filtre **ExponentialRetryPolicyFilter** :</span><span class="sxs-lookup"><span data-stu-id="d762a-138">The following creates a **TableService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="d762a-139">Ajout d'une entité à une table</span><span class="sxs-lookup"><span data-stu-id="d762a-139">Add an entity to a table</span></span>
<span data-ttu-id="d762a-140">Pour ajouter une entité, commencez par créer un objet qui définit les propriétés de l'entité.</span><span class="sxs-lookup"><span data-stu-id="d762a-140">To add an entity, first create an object that defines your entity properties.</span></span> <span data-ttu-id="d762a-141">Toutes les entités doivent contenir une propriété **PartitionKey** et **RowKey**, qui sont des identificateurs uniques de l’entité.</span><span class="sxs-lookup"><span data-stu-id="d762a-141">All entities must contain a **PartitionKey** and **RowKey**, which are unique identifiers for the entity.</span></span>

* <span data-ttu-id="d762a-142">**PartitionKey** : détermine la partition dans laquelle l’entité est stockée</span><span class="sxs-lookup"><span data-stu-id="d762a-142">**PartitionKey** - determines the partition that the entity is stored in</span></span>
* <span data-ttu-id="d762a-143">**RowKey** : identifie de façon unique l’entité dans la partition</span><span class="sxs-lookup"><span data-stu-id="d762a-143">**RowKey** - uniquely identifies the entity within the partition</span></span>

<span data-ttu-id="d762a-144">**PartitionKey** et **RowKey** doivent être des valeurs de chaîne.</span><span class="sxs-lookup"><span data-stu-id="d762a-144">Both **PartitionKey** and **RowKey** must be string values.</span></span> <span data-ttu-id="d762a-145">Pour plus d'informations, consultez la rubrique [Présentation du modèle de données du service de Table](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="d762a-145">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="d762a-146">Voici un exemple de définition d'une entité.</span><span class="sxs-lookup"><span data-stu-id="d762a-146">The following is an example of defining an entity.</span></span> <span data-ttu-id="d762a-147">Notez que **dueDate** est définie comme un type de **Edm.DateTime**.</span><span class="sxs-lookup"><span data-stu-id="d762a-147">Note that **dueDate** is defined as a type of **Edm.DateTime**.</span></span> <span data-ttu-id="d762a-148">L'indication du type est facultative et s'ils ne sont pas spécifiés, les types sont déduits.</span><span class="sxs-lookup"><span data-stu-id="d762a-148">Specifying the type is optional, and types will be inferred if not specified.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out the trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> <span data-ttu-id="d762a-149">Il existe également un champ **Timestamp** pour chaque enregistrement, qui est défini par Azure quand une entité est insérée ou mise à jour.</span><span class="sxs-lookup"><span data-stu-id="d762a-149">There is also a **Timestamp** field for each record, which is set by Azure when an entity is inserted or updated.</span></span>
>
>

<span data-ttu-id="d762a-150">Vous pouvez également utiliser **entityGenerator** pour créer des entités.</span><span class="sxs-lookup"><span data-stu-id="d762a-150">You can also use the **entityGenerator** to create entities.</span></span> <span data-ttu-id="d762a-151">L'exemple suivant crée la même entité de tâche en utilisant **entityGenerator**.</span><span class="sxs-lookup"><span data-stu-id="d762a-151">The following example creates the same task entity using the **entityGenerator**.</span></span>

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out the trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

<span data-ttu-id="d762a-152">Pour ajouter une entité à votre table, transmettez l'objet d'entité à la méthode **insertEntity** .</span><span class="sxs-lookup"><span data-stu-id="d762a-152">To add an entity to your table, pass the entity object to the **insertEntity** method.</span></span>

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

<span data-ttu-id="d762a-153">Si l’opération aboutit, `result` contient l’élément [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) de l’enregistrement inséré et `response` contient des informations sur l’opération.</span><span class="sxs-lookup"><span data-stu-id="d762a-153">If the operation is successful, `result` will contain the [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) of the inserted record and `response` will contain information about the operation.</span></span>

<span data-ttu-id="d762a-154">Exemple de réponse :</span><span class="sxs-lookup"><span data-stu-id="d762a-154">Example response:</span></span>

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> <span data-ttu-id="d762a-155">Par défaut, **insertEntity** ne renvoie pas l’entité insérée dans le cadre des informations `response`.</span><span class="sxs-lookup"><span data-stu-id="d762a-155">By default, **insertEntity** does not return the inserted entity as part of the `response` information.</span></span> <span data-ttu-id="d762a-156">Si vous prévoyez d’exécuter d’autres opérations sur cette entité, ou si vous voulez mettre en cache les informations, il peut être utile de la faire renvoyer dans le cadre de `result`.</span><span class="sxs-lookup"><span data-stu-id="d762a-156">If you plan on performing other operations on this entity, or wish to cache the information, it can be useful to have it returned as part of the `result`.</span></span> <span data-ttu-id="d762a-157">Pour ce faire, activez **echoContent** comme suit :</span><span class="sxs-lookup"><span data-stu-id="d762a-157">You can do this by enabling **echoContent** as follows:</span></span>
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a><span data-ttu-id="d762a-158">Mise à jour d'une entité</span><span class="sxs-lookup"><span data-stu-id="d762a-158">Update an entity</span></span>
<span data-ttu-id="d762a-159">Plusieurs méthodes permettent de mettre à jour une entité existante :</span><span class="sxs-lookup"><span data-stu-id="d762a-159">There are multiple methods available to update an existing entity:</span></span>

* <span data-ttu-id="d762a-160">**replaceEntity** : met à jour une entité existante en la remplaçant</span><span class="sxs-lookup"><span data-stu-id="d762a-160">**replaceEntity** - updates an existing entity by replacing it</span></span>
* <span data-ttu-id="d762a-161">**mergeEntity** : met à jour une entité existante en fusionnant les nouvelles valeurs des propriétés avec l’entité existante</span><span class="sxs-lookup"><span data-stu-id="d762a-161">**mergeEntity** - updates an existing entity by merging new property values into the existing entity</span></span>
* <span data-ttu-id="d762a-162">**insertOrReplaceEntity** : met à jour une entité existante en la remplaçant.</span><span class="sxs-lookup"><span data-stu-id="d762a-162">**insertOrReplaceEntity** - updates an existing entity by replacing it.</span></span> <span data-ttu-id="d762a-163">En l’absence d’entité, une nouvelle entité est insérée.</span><span class="sxs-lookup"><span data-stu-id="d762a-163">If no entity exists, a new one will be inserted</span></span>
* <span data-ttu-id="d762a-164">**insertOrMergeEntity** : met à jour une entité existante en fusionnant les nouvelles valeurs des propriétés avec l’entité existante.</span><span class="sxs-lookup"><span data-stu-id="d762a-164">**insertOrMergeEntity** - updates an existing entity by merging new property values into the existing.</span></span> <span data-ttu-id="d762a-165">En l’absence d’entité, une nouvelle entité est insérée.</span><span class="sxs-lookup"><span data-stu-id="d762a-165">If no entity exists, a new one will be inserted</span></span>

<span data-ttu-id="d762a-166">L’exemple suivant illustre la mise à jour d’une entité avec **replaceEntity**:</span><span class="sxs-lookup"><span data-stu-id="d762a-166">The following example demonstrates updating an entity using **replaceEntity**:</span></span>

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> <span data-ttu-id="d762a-167">Par défaut, la mise à jour d'une entité ne vérifie pas si les données en cours de mise à jour ont déjà été modifiées par un autre processus.</span><span class="sxs-lookup"><span data-stu-id="d762a-167">By default, updating an entity does not check to see if the data being updated has previously been modified by another process.</span></span> <span data-ttu-id="d762a-168">Pour activer la prise en charge de mises à jour simultanées :</span><span class="sxs-lookup"><span data-stu-id="d762a-168">To support concurrent updates:</span></span>
>
> 1. <span data-ttu-id="d762a-169">Obtenez l'ETag de l'objet mis à jour.</span><span class="sxs-lookup"><span data-stu-id="d762a-169">Get the ETag of the object being updated.</span></span> <span data-ttu-id="d762a-170">Il est renvoyé dans la `response` d’une opération sur une entité et peut être extrait dans `response['.metadata'].etag`.</span><span class="sxs-lookup"><span data-stu-id="d762a-170">This is returned as part of the `response` for any entity-related operation and can be retrieved through `response['.metadata'].etag`.</span></span>
> 2. <span data-ttu-id="d762a-171">Lors d'une opération de mise à jour sur une entité, ajoutez les informations ETag précédemment extraites dans la nouvelle entité.</span><span class="sxs-lookup"><span data-stu-id="d762a-171">When performing an update operation on an entity, add the ETag information previously retrieved to the new entity.</span></span> <span data-ttu-id="d762a-172">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d762a-172">For example:</span></span>
>
>       <span data-ttu-id="d762a-173">entity2['.metadata'].etag = currentEtag;</span><span class="sxs-lookup"><span data-stu-id="d762a-173">entity2['.metadata'].etag = currentEtag;</span></span>
> 3. <span data-ttu-id="d762a-174">Effectuez l'opération de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="d762a-174">Perform the update operation.</span></span> <span data-ttu-id="d762a-175">Si l’entité a été modifiée depuis que vous avez extrait la valeur ETag, par exemple avec une autre instance de votre application, une `error` est renvoyée, indiquant que la condition de mise à jour spécifiée dans la requête n’est pas remplie.</span><span class="sxs-lookup"><span data-stu-id="d762a-175">If the entity has been modified since you retrieved the ETag value, such as another instance of your application, an `error` will be returned stating that the update condition specified in the request was not satisfied.</span></span>
>
>

<span data-ttu-id="d762a-176">Avec **replaceEntity** et **mergeEntity**, l’opération échoue si l’entité mise à jour n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="d762a-176">With **replaceEntity** and **mergeEntity**, if the entity that is being updated doesn't exist, then the update operation will fail.</span></span> <span data-ttu-id="d762a-177">Si vous voulez stocker une entité, qu’elle existe déjà ou non, utilisez **insertOrReplaceEntity** ou **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="d762a-177">Therefore if you wish to store an entity regardless of whether it already exists, use **insertOrReplaceEntity** or **insertOrMergeEntity**.</span></span>

<span data-ttu-id="d762a-178">Le `result` des opérations de mise à jour réussies contient l’ **Etag** de l’entité mise à jour.</span><span class="sxs-lookup"><span data-stu-id="d762a-178">The `result` for successful update operations will contain the **Etag** of the updated entity.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="d762a-179">Utilisation des groupes d'entités</span><span class="sxs-lookup"><span data-stu-id="d762a-179">Work with groups of entities</span></span>
<span data-ttu-id="d762a-180">Il est parfois intéressant de soumettre un lot d'opérations simultanément pour assurer un traitement atomique par le serveur.</span><span class="sxs-lookup"><span data-stu-id="d762a-180">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span></span> <span data-ttu-id="d762a-181">Pour ce faire, utilisez la classe **TableBatch** pour créer un traitement par lot, puis la méthode **executeBatch** de **TableService** pour exécuter les opérations de traitement par lot.</span><span class="sxs-lookup"><span data-stu-id="d762a-181">To accomplish that, use the **TableBatch** class to create a batch, and then use the **executeBatch** method of **TableService** to perform the batched operations.</span></span>

 <span data-ttu-id="d762a-182">L'exemple suivant illustre la soumission par lot de deux entités :</span><span class="sxs-lookup"><span data-stu-id="d762a-182">The following example demonstrates submitting two entities in a batch:</span></span>

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out the trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash the dishes'},
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

<span data-ttu-id="d762a-183">Pour les opérations de traitement par lot réussies, `result` contient les informations de chaque opération du lot.</span><span class="sxs-lookup"><span data-stu-id="d762a-183">For successful batch operations, `result` will contain information for each operation in the batch.</span></span>

### <a name="work-with-batched-operations"></a><span data-ttu-id="d762a-184">Ultiliser des opérations de traitement par lot</span><span class="sxs-lookup"><span data-stu-id="d762a-184">Work with batched operations</span></span>
<span data-ttu-id="d762a-185">Les opérations ajoutées à un traitement par lot peuvent être inspectées en affichant la propriété `operations` .</span><span class="sxs-lookup"><span data-stu-id="d762a-185">Operations added to a batch can be inspected by viewing the `operations` property.</span></span> <span data-ttu-id="d762a-186">Vous pouvez également utiliser les méthodes suivantes avec les opérations :</span><span class="sxs-lookup"><span data-stu-id="d762a-186">You can also use the following methods to work with operations:</span></span>

* <span data-ttu-id="d762a-187">**clear** : permet de supprimer toutes les opérations d’un lot</span><span class="sxs-lookup"><span data-stu-id="d762a-187">**clear** - clears all operations from a batch</span></span>
* <span data-ttu-id="d762a-188">**getOperations** : permet d’obtenir une opération du lot</span><span class="sxs-lookup"><span data-stu-id="d762a-188">**getOperations** - gets an operation from the batch</span></span>
* <span data-ttu-id="d762a-189">**hasOperations** : permet de renvoyer true si le lot contient des opérations</span><span class="sxs-lookup"><span data-stu-id="d762a-189">**hasOperations** - returns true if the batch contains operations</span></span>
* <span data-ttu-id="d762a-190">**removeOperations** : permet de supprimer une opération</span><span class="sxs-lookup"><span data-stu-id="d762a-190">**removeOperations** - removes an operation</span></span>
* <span data-ttu-id="d762a-191">**size** : permet de renvoyer le nombre d’opérations du lot</span><span class="sxs-lookup"><span data-stu-id="d762a-191">**size** - returns the number of operations in the batch</span></span>

## <a name="retrieve-an-entity-by-key"></a><span data-ttu-id="d762a-192">Récupération d'une entité par clé</span><span class="sxs-lookup"><span data-stu-id="d762a-192">Retrieve an entity by key</span></span>
<span data-ttu-id="d762a-193">Pour envoyer une entité spécifique d’après la valeur **PartitionKey** et **RowKey**, utilisez la méthode **retrieveEntity**.</span><span class="sxs-lookup"><span data-stu-id="d762a-193">To return a specific entity based on the **PartitionKey** and **RowKey**, use the **retrieveEntity** method.</span></span>

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains the entity
  }
});
```

<span data-ttu-id="d762a-194">À la fin de cette opération, `result` contient l’entité.</span><span class="sxs-lookup"><span data-stu-id="d762a-194">Once this operation is complete, `result` will contain the entity.</span></span>

## <a name="query-a-set-of-entities"></a><span data-ttu-id="d762a-195">Interrogation d’un ensemble d’entités</span><span class="sxs-lookup"><span data-stu-id="d762a-195">Query a set of entities</span></span>
<span data-ttu-id="d762a-196">Pour interroger une table, utilisez l’objet **TableQuery** pour générer une expression de requête en utilisant les clauses suivantes :</span><span class="sxs-lookup"><span data-stu-id="d762a-196">To query a table, use the **TableQuery** object to build up a query expression using the following clauses:</span></span>

* <span data-ttu-id="d762a-197">**select** : champs à renvoyer par la requête</span><span class="sxs-lookup"><span data-stu-id="d762a-197">**select** - the fields to be returned from the query</span></span>
* <span data-ttu-id="d762a-198">**where** : clause where</span><span class="sxs-lookup"><span data-stu-id="d762a-198">**where** - the where clause</span></span>

  * <span data-ttu-id="d762a-199">**and** : condition where `and`</span><span class="sxs-lookup"><span data-stu-id="d762a-199">**and** - an `and` where condition</span></span>
  * <span data-ttu-id="d762a-200">**or** : condition where `or`</span><span class="sxs-lookup"><span data-stu-id="d762a-200">**or** - an `or` where condition</span></span>
* <span data-ttu-id="d762a-201">**top** : nombre d’éléments à extraire</span><span class="sxs-lookup"><span data-stu-id="d762a-201">**top** - the number of items to fetch</span></span>

<span data-ttu-id="d762a-202">L’exemple suivant crée une requête qui renvoie les cinq premiers éléments avec une PartitionKey « hometasks ».</span><span class="sxs-lookup"><span data-stu-id="d762a-202">The following example builds a query that will return the top five items with a PartitionKey of 'hometasks'.</span></span>

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

<span data-ttu-id="d762a-203">Comme **select** n'est pas utilisé, tous les champs sont renvoyés.</span><span class="sxs-lookup"><span data-stu-id="d762a-203">Since **select** is not used, all fields will be returned.</span></span> <span data-ttu-id="d762a-204">Pour exécuter la requête dans une table, utilisez **queryEntities**.</span><span class="sxs-lookup"><span data-stu-id="d762a-204">To perform the query against a table, use **queryEntities**.</span></span> <span data-ttu-id="d762a-205">L'exemple suivant utilise cette requête pour renvoyer des entités de « mytable ».</span><span class="sxs-lookup"><span data-stu-id="d762a-205">The following example uses this query to return entities from 'mytable'.</span></span>

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

<span data-ttu-id="d762a-206">En cas de réussite, `result.entries` contient un tableau d’entités qui correspondent à la requête.</span><span class="sxs-lookup"><span data-stu-id="d762a-206">If successful, `result.entries` will contain an array of entities that match the query.</span></span> <span data-ttu-id="d762a-207">Si la requête n’a pas pu renvoyer toutes les entités, `result.continuationToken` est non*null* et peut servir de troisième paramètre de **queryEntities** pour obtenir davantage de résultats.</span><span class="sxs-lookup"><span data-stu-id="d762a-207">If the query was unable to return all entities, `result.continuationToken` will be non-*null* and can be used as the third parameter of **queryEntities** to retrieve more results.</span></span> <span data-ttu-id="d762a-208">Pour la requête initiale, utilisez *null* comme troisième paramètre.</span><span class="sxs-lookup"><span data-stu-id="d762a-208">For the initial query, use *null* for the third parameter.</span></span>

### <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="d762a-209">Interrogation d’un sous-ensemble de propriétés d’entité</span><span class="sxs-lookup"><span data-stu-id="d762a-209">Query a subset of entity properties</span></span>
<span data-ttu-id="d762a-210">Vous pouvez utiliser une requête de table pour extraire uniquement quelques champs d'une entité.</span><span class="sxs-lookup"><span data-stu-id="d762a-210">A query to a table can retrieve just a few fields from an entity.</span></span>
<span data-ttu-id="d762a-211">Ceci permet de réduire la consommation de bande passante et peut améliorer les performances des requêtes, notamment pour les entités volumineuses.</span><span class="sxs-lookup"><span data-stu-id="d762a-211">This reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="d762a-212">Utilisez la clause **select** et transmettez les noms des champs à renvoyer.</span><span class="sxs-lookup"><span data-stu-id="d762a-212">Use the **select** clause and pass the names of the fields to be returned.</span></span> <span data-ttu-id="d762a-213">Par exemple, la requête suivante renvoie uniquement les champs **description** et **dueDate**.</span><span class="sxs-lookup"><span data-stu-id="d762a-213">For example, the following query will return only the **description** and **dueDate** fields.</span></span>

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a><span data-ttu-id="d762a-214">Suppression d'une entité</span><span class="sxs-lookup"><span data-stu-id="d762a-214">Delete an entity</span></span>
<span data-ttu-id="d762a-215">Vous pouvez supprimer une entité en utilisant ses clés de partition et de ligne.</span><span class="sxs-lookup"><span data-stu-id="d762a-215">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="d762a-216">Dans cet exemple, l’objet **task1** contient les valeurs **RowKey** et **PartitionKey** de l’entité à supprimer.</span><span class="sxs-lookup"><span data-stu-id="d762a-216">In this example, the **task1** object contains the **RowKey** and **PartitionKey** values of the entity to be deleted.</span></span> <span data-ttu-id="d762a-217">L'objet est transmis à la méthode **deleteEntity** .</span><span class="sxs-lookup"><span data-stu-id="d762a-217">Then the object is passed to the **deleteEntity** method.</span></span>

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
> <span data-ttu-id="d762a-218">Vous avez intérêt à utiliser les ETag pour supprimer des éléments afin de vous assurer que les éléments n'ont pas été modifiés par un autre processus.</span><span class="sxs-lookup"><span data-stu-id="d762a-218">Consider using ETags when deleting items, to ensure that the item hasn't been modified by another process.</span></span> <span data-ttu-id="d762a-219">Consultez [Mise à jour d’une entité](#update-an-entity) pour plus d’informations sur l’utilisation des ETags.</span><span class="sxs-lookup"><span data-stu-id="d762a-219">See [Update an entity](#update-an-entity) for information on using ETags.</span></span>
>
>

## <a name="delete-a-table"></a><span data-ttu-id="d762a-220">Suppression d’une table</span><span class="sxs-lookup"><span data-stu-id="d762a-220">Delete a table</span></span>
<span data-ttu-id="d762a-221">Le code suivant permet de supprimer une table d'un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="d762a-221">The following code deletes a table from a storage account.</span></span>

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

<span data-ttu-id="d762a-222">Si vous ne savez pas si la table existe, utilisez **deleteTableIfExists**.</span><span class="sxs-lookup"><span data-stu-id="d762a-222">If you are uncertain whether the table exists, use **deleteTableIfExists**.</span></span>

## <a name="use-continuation-tokens"></a><span data-ttu-id="d762a-223">Utiliser des jetons de liaison</span><span class="sxs-lookup"><span data-stu-id="d762a-223">Use continuation tokens</span></span>
<span data-ttu-id="d762a-224">Si vous interrogez des tables et que les résultats peuvent être volumineux, recherchez des jetons de liaison.</span><span class="sxs-lookup"><span data-stu-id="d762a-224">When you are querying tables for large amounts of results, look for continuation tokens.</span></span> <span data-ttu-id="d762a-225">Sans que vous en ayez vraiment conscience, de grandes quantités de données peuvent être disponibles pour votre requête si elle n’est pas en mesure de détecter la présence d’un jeton de liaison.</span><span class="sxs-lookup"><span data-stu-id="d762a-225">There may be large amounts of data available for your query that you might not realize if you do not build to recognize when a continuation token is present.</span></span>

<span data-ttu-id="d762a-226">L’objet de résultats renvoyé après l’interrogation des entités définit une propriété `continuationToken` si ce jeton est présent.</span><span class="sxs-lookup"><span data-stu-id="d762a-226">The results object returned during querying entities sets a `continuationToken` property when such a token is present.</span></span> <span data-ttu-id="d762a-227">Vous pouvez ensuite utiliser cette propriété pour exécuter une requête sur l’ensemble des entités de table et de partition.</span><span class="sxs-lookup"><span data-stu-id="d762a-227">You can then use this when performing a query to continue to move across the partition and table entities.</span></span>

<span data-ttu-id="d762a-228">Pendant l’interrogation, un paramètre continuationToken peut être fourni entre l’instance d’objet de requête et la fonction de rappel :</span><span class="sxs-lookup"><span data-stu-id="d762a-228">When querying, a continuationToken parameter may be provided between the query object instance and the callback function:</span></span>

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

<span data-ttu-id="d762a-229">L’objet `continuationToken` contient des propriétés telles que `nextPartitionKey`, `nextRowKey` et `targetLocation` que vous pouvez utiliser pour effectuer une itération dans tous les résultats.</span><span class="sxs-lookup"><span data-stu-id="d762a-229">If you inspect the `continuationToken` object, you will find properties such as `nextPartitionKey`, `nextRowKey` and `targetLocation`, which can be used to iterate through all the results.</span></span>

<span data-ttu-id="d762a-230">Un exemple de liaison est également disponible dans le référentiel Node.js Azure Storage sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="d762a-230">There is also a continuation sample within the Azure Storage Node.js repo on GitHub.</span></span> <span data-ttu-id="d762a-231">Recherchez `examples/samples/continuationsample.js`.</span><span class="sxs-lookup"><span data-stu-id="d762a-231">Look for `examples/samples/continuationsample.js`.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="d762a-232">Utilisation des signatures d'accès partagé</span><span class="sxs-lookup"><span data-stu-id="d762a-232">Work with shared access signatures</span></span>
<span data-ttu-id="d762a-233">Les signatures d’accès partagé (SAP) sont un moyen sécurisé de fournir un accès précis aux tables sans fournir le nom ni les clés de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="d762a-233">Shared access signatures (SAS) are a secure way to provide granular access to tables without providing your storage account name or keys.</span></span> <span data-ttu-id="d762a-234">Elles servent souvent à fournir un accès limité à vos données, par exemple pour autoriser une application mobile à interroger des enregistrements.</span><span class="sxs-lookup"><span data-stu-id="d762a-234">SAS are often used to provide limited access to your data, such as allowing a mobile app to query records.</span></span>

<span data-ttu-id="d762a-235">Une application approuvée, comme un service cloud, génère une SAP à l’aide de l’élément **generateSharedAccessSignature** du **TableService**, et la fournit à une application non approuvée ou semi-approuvée, comme une application mobile.</span><span class="sxs-lookup"><span data-stu-id="d762a-235">A trusted application such as a cloud-based service generates a SAS using the **generateSharedAccessSignature** of the **TableService**, and provides it to an untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="d762a-236">La signature d'accès partagé est générée à l'aide d'une stratégie, qui décrit les dates de début et de fin de validité de la signature, et le niveau d'accès accordé au détenteur de la signature.</span><span class="sxs-lookup"><span data-stu-id="d762a-236">The SAS is generated using a policy, which describes the start and end dates during which the SAS is valid, as well as the access level granted to the SAS holder.</span></span>

<span data-ttu-id="d762a-237">L'exemple suivant génère une nouvelle stratégie d'accès partagé qui autorise le détenteur de la signature d'accès partagé à interroger (« r ») la table et expire 100 minutes après son heure de création.</span><span class="sxs-lookup"><span data-stu-id="d762a-237">The following example generates a new shared access policy that will allow the SAS holder to query ('r') the table, and expires 100 minutes after the time it is created.</span></span>

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

<span data-ttu-id="d762a-238">Notez que les informations sur l'hôte doivent également être fournies, car elles sont obligatoires lorsque le détenteur de la signature d'accès partagé tente d'accéder à la table.</span><span class="sxs-lookup"><span data-stu-id="d762a-238">Note that the host information must be provided also, as it is required when the SAS holder attempts to access the table.</span></span>

<span data-ttu-id="d762a-239">L'application cliente utilise les signatures d'accès partagé avec **TableServiceWithSAS** pour effectuer les opérations sur la table.</span><span class="sxs-lookup"><span data-stu-id="d762a-239">The client application then uses the SAS with **TableServiceWithSAS** to perform operations against the table.</span></span> <span data-ttu-id="d762a-240">L'exemple suivant se connecte à la table et exécute une requête.</span><span class="sxs-lookup"><span data-stu-id="d762a-240">The following example connects to the table and performs a query.</span></span>

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains the entities
  }
});
```

<span data-ttu-id="d762a-241">Comme la signature d'accès partagé a été générée seulement avec un accès en requête, une erreur sera renvoyée en cas de tentative d'ajout, de mise à jour ou de suppression des entités.</span><span class="sxs-lookup"><span data-stu-id="d762a-241">Since the SAS was generated with only query access, if an attempt were made to insert, update, or delete entities, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="d762a-242">Listes de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="d762a-242">Access Control Lists</span></span>
<span data-ttu-id="d762a-243">Vous pouvez également utiliser une liste de contrôle d'accès (ACL) pour définir la stratégie d'accès pour une signature d'accès partagé.</span><span class="sxs-lookup"><span data-stu-id="d762a-243">You can also use an Access Control List (ACL) to set the access policy for a SAS.</span></span> <span data-ttu-id="d762a-244">Cela est utile si vous voulez autoriser plusieurs clients à accéder à la table, mais fournir des stratégies d'accès différentes à chaque client.</span><span class="sxs-lookup"><span data-stu-id="d762a-244">This is useful if you wish to allow multiple clients to access the table, but provide different access policies for each client.</span></span>

<span data-ttu-id="d762a-245">Une liste de contrôle d'accès est implémentée à l'aide d'un tableau de stratégies d'accès, dans lequel un ID est associé à chaque stratégie.</span><span class="sxs-lookup"><span data-stu-id="d762a-245">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="d762a-246">L’exemple suivant définit deux stratégies ; une pour « user1 » et une pour « user2 » :</span><span class="sxs-lookup"><span data-stu-id="d762a-246">The following example defines two policies, one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="d762a-247">L’exemple suivant obtient la liste de contrôle d’accès actuelle pour la table **hometasks**, puis ajoute les nouvelles stratégies à l’aide de **setTableAcl**.</span><span class="sxs-lookup"><span data-stu-id="d762a-247">The following example gets the current ACL for the **hometasks** table, and then adds the new policies using **setTableAcl**.</span></span> <span data-ttu-id="d762a-248">Cette approche permet :</span><span class="sxs-lookup"><span data-stu-id="d762a-248">This approach allows:</span></span>

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

<span data-ttu-id="d762a-249">Lorsque la liste de contrôle d'accès est définie, vous pouvez créer une signature d'accès partagé basée sur l'ID pour une stratégie.</span><span class="sxs-lookup"><span data-stu-id="d762a-249">Once the ACL has been set, you can then create a SAS based on the ID for a policy.</span></span> <span data-ttu-id="d762a-250">L'exemple suivant crée une signature d'accès partagé pour « user2 » :</span><span class="sxs-lookup"><span data-stu-id="d762a-250">The following example creates a new SAS for 'user2':</span></span>

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="d762a-251">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d762a-251">Next steps</span></span>
<span data-ttu-id="d762a-252">Pour plus d'informations, consultez les ressources suivantes.</span><span class="sxs-lookup"><span data-stu-id="d762a-252">For more information, see the following resources.</span></span>

* <span data-ttu-id="d762a-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome et gratuite de Microsoft qui vous permet d’exploiter visuellement les données de Stockage Azure sur Windows, macOS et Linux.</span><span class="sxs-lookup"><span data-stu-id="d762a-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="d762a-254">[Kit de développement logiciel (SDK) Azure Storage pour Node](https://github.com/Azure/azure-storage-node) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="d762a-254">[Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) repository on GitHub.</span></span>
* [<span data-ttu-id="d762a-255">Centre de développement Node.js</span><span class="sxs-lookup"><span data-stu-id="d762a-255">Node.js Developer Center</span></span>](/develop/nodejs/)
* [<span data-ttu-id="d762a-256">Création et déploiement d’une application Node.js sur un site web Azure</span><span class="sxs-lookup"><span data-stu-id="d762a-256">Create and deploy a Node.js application to an Azure website</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)