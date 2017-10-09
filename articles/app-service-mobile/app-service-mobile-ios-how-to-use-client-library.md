---
title: aaaHow tooUse SDK iOS pour les applications mobiles Azure
description: Comment tooUse SDK iOS pour les applications mobiles Azure
services: app-service\mobile
documentationcenter: ios
author: ysxu
manager: yochayk
editor: 
ms.assetid: 4e8e45df-c36a-4a60-9ad4-393ec10b7eb9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: yuaxu
ms.openlocfilehash: fa299ab3f152bad12d821832fa9fb5495d1fa296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ios-client-library-for-azure-mobile-apps"></a><span data-ttu-id="01146-103">Comment tooUse iOS bibliothèque cliente pour les applications mobiles Azure</span><span class="sxs-lookup"><span data-stu-id="01146-103">How tooUse iOS Client Library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="01146-104">Ce guide vous explique tooperform des scénarios courants utilisant hello dernières [e/s des applications mobiles Azure SDK][1].</span><span class="sxs-lookup"><span data-stu-id="01146-104">This guide teaches you tooperform common scenarios using hello latest [Azure Mobile Apps iOS SDK][1].</span></span> <span data-ttu-id="01146-105">Si vous êtes tooAzure Mobile de nouvelles applications, d’abord terminer [démarrage rapide d’Azure Mobile Apps] toocreate un service principal, créez une table et télécharger un projet de Xcode avant génération iOS.</span><span class="sxs-lookup"><span data-stu-id="01146-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend, create a table, and download a pre-built iOS Xcode project.</span></span> <span data-ttu-id="01146-106">Dans ce guide, nous concentrer sur hello côté client iOS SDK.</span><span class="sxs-lookup"><span data-stu-id="01146-106">In this guide, we focus on hello client-side iOS SDK.</span></span> <span data-ttu-id="01146-107">toolearn savoir plus sur hello du Kit de développement logiciel côté serveur pour hello principal, consultez hello serveur SDK la.</span><span class="sxs-lookup"><span data-stu-id="01146-107">toolearn more about hello server-side SDK for hello backend, see hello Server SDK HOWTOs.</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="01146-108">Documentation de référence</span><span class="sxs-lookup"><span data-stu-id="01146-108">Reference documentation</span></span>
<span data-ttu-id="01146-109">Hello documentation de référence pour le client d’iOS hello SDK se trouve ici : [e/s des applications mobiles Azure Client référence][2].</span><span class="sxs-lookup"><span data-stu-id="01146-109">hello reference documentation for hello iOS client SDK is located here: [Azure Mobile Apps iOS Client Reference][2].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="01146-110">Plateformes prises en charge</span><span class="sxs-lookup"><span data-stu-id="01146-110">Supported Platforms</span></span>
<span data-ttu-id="01146-111">Hello, iOS SDK prend en charge les projets Objective-C, les projets Swift 2.2 ou Swift 2.3 pour iOS version 8.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="01146-111">hello iOS SDK supports Objective-C projects, Swift 2.2 projects, and Swift 2.3 projects for iOS versions 8.0 or later.</span></span>

<span data-ttu-id="01146-112">l’authentification de « flux de serveur » Hello utilise un WebView hello affiche l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="01146-112">hello "server-flow" authentication uses a WebView for hello presented UI.</span></span>  <span data-ttu-id="01146-113">Si l’appareil de hello n’est pas en mesure de toopresent un UI WebView, une autre méthode d’authentification est requise, qui est extérieur étendue hello du produit de hello.</span><span class="sxs-lookup"><span data-stu-id="01146-113">If hello device is not able toopresent a WebView UI, then another method of authentication is required that is outside hello scope of hello product.</span></span>  
<span data-ttu-id="01146-114">Ce SDK ne convient donc pas au type Watch ou d’autres appareils restreints similaires.</span><span class="sxs-lookup"><span data-stu-id="01146-114">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="01146-115"><a name="Setup"></a>Configuration et conditions préalables</span><span class="sxs-lookup"><span data-stu-id="01146-115"><a name="Setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="01146-116">Ce guide part du principe que vous avez créé un serveur principal avec une table.</span><span class="sxs-lookup"><span data-stu-id="01146-116">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="01146-117">Ce guide part du principe que la table hello a le même schéma que les tables hello dans ces didacticiels.</span><span class="sxs-lookup"><span data-stu-id="01146-117">This guide assumes that hello table has the same schema as hello tables in those tutorials.</span></span> <span data-ttu-id="01146-118">Ce guide suppose également que dans votre code, vous référencez `MicrosoftAzureMobile.framework` et importez `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span><span class="sxs-lookup"><span data-stu-id="01146-118">This guide also assumes that in your code, you reference `MicrosoftAzureMobile.framework` and import `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span></span>

## <span data-ttu-id="01146-119"><a name="create-client"></a>Création du client</span><span class="sxs-lookup"><span data-stu-id="01146-119"><a name="create-client"></a>How to: Create Client</span></span>
<span data-ttu-id="01146-120">tooaccess un serveur d’applications mobiles Azure principal dans votre projet, créez un `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="01146-120">tooaccess an Azure Mobile Apps backend in your project, create an `MSClient`.</span></span> <span data-ttu-id="01146-121">Remplacez `AppUrl` avec l’URL de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="01146-121">Replace `AppUrl` with hello app URL.</span></span> <span data-ttu-id="01146-122">Vous pouvez laisser `gatewayURLString` et `applicationKey` vides.</span><span class="sxs-lookup"><span data-stu-id="01146-122">You may leave `gatewayURLString` and `applicationKey` empty.</span></span> <span data-ttu-id="01146-123">Si vous configurez une passerelle pour l’authentification, remplir `gatewayURLString` avec l’URL de la passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="01146-123">If you set up a gateway for authentication, populate `gatewayURLString` with hello gateway URL.</span></span>

<span data-ttu-id="01146-124">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-124">**Objective-C**:</span></span>

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

<span data-ttu-id="01146-125">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-125">**Swift**:</span></span>

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <span data-ttu-id="01146-126"><a name="table-reference"></a>Procédure : création d'une référence de table</span><span class="sxs-lookup"><span data-stu-id="01146-126"><a name="table-reference"></a>How to: Create Table Reference</span></span>
<span data-ttu-id="01146-127">tooaccess ou mise à jour des données, créez une table de serveur principal de référence toohello.</span><span class="sxs-lookup"><span data-stu-id="01146-127">tooaccess or update data, create a reference toohello backend table.</span></span> <span data-ttu-id="01146-128">Remplacez `TodoItem` par nom de hello de votre table</span><span class="sxs-lookup"><span data-stu-id="01146-128">Replace `TodoItem` with hello name of your table</span></span>

<span data-ttu-id="01146-129">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-129">**Objective-C**:</span></span>

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

<span data-ttu-id="01146-130">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-130">**Swift**:</span></span>

```
let table = client.tableWithName("TodoItem")
```


## <span data-ttu-id="01146-131"><a name="querying"></a>Procédure : interrogation des données</span><span class="sxs-lookup"><span data-stu-id="01146-131"><a name="querying"></a>How to: Query Data</span></span>
<span data-ttu-id="01146-132">toocreate une requête de base de données, hello de requête `MSTable` objet.</span><span class="sxs-lookup"><span data-stu-id="01146-132">toocreate a database query, query hello `MSTable` object.</span></span> <span data-ttu-id="01146-133">Hello requête suivante obtient tous les éléments hello dans `TodoItem` et journaux hello texte de chaque élément.</span><span class="sxs-lookup"><span data-stu-id="01146-133">hello following query gets all hello items in `TodoItem` and logs hello text of each item.</span></span>

<span data-ttu-id="01146-134">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-134">**Objective-C**:</span></span>

```
[table readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) { // error is nil if no error occured
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) { // items is NSArray of records that match query
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="01146-135">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-135">**Swift**:</span></span>

```
table.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <span data-ttu-id="01146-136"><a name="filtering"></a>Procédure : filtrage des données renvoyées</span><span class="sxs-lookup"><span data-stu-id="01146-136"><a name="filtering"></a>How to: Filter Returned Data</span></span>
<span data-ttu-id="01146-137">résultats de toofilter, il existe de nombreuses options disponibles.</span><span class="sxs-lookup"><span data-stu-id="01146-137">toofilter results, there are many available options.</span></span>

<span data-ttu-id="01146-138">toofilter à l’aide d’un prédicat, utilisez un `NSPredicate` et `readWithPredicate`.</span><span class="sxs-lookup"><span data-stu-id="01146-138">toofilter using a predicate, use an `NSPredicate` and `readWithPredicate`.</span></span> <span data-ttu-id="01146-139">suivant de Hello filtre les éléments de données retournées toofind uniquement incomplètes Todo.</span><span class="sxs-lookup"><span data-stu-id="01146-139">hello following filters returned data toofind only incomplete Todo items.</span></span>

<span data-ttu-id="01146-140">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-140">**Objective-C**:</span></span>

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query hello TodoItem table
[table readWithPredicate:predicate completion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="01146-141">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-141">**Swift**:</span></span>

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query hello TodoItem table
table.readWithPredicate(predicate) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <span data-ttu-id="01146-142"><a name="query-object"></a>Procédure : utilisation de MSQuery</span><span class="sxs-lookup"><span data-stu-id="01146-142"><a name="query-object"></a>How to: Use MSQuery</span></span>
<span data-ttu-id="01146-143">tooperform une requête complexe (y compris le tri et la pagination), créer un `MSQuery` de l’objet, directement ou à l’aide d’un prédicat :</span><span class="sxs-lookup"><span data-stu-id="01146-143">tooperform a complex query (including sorting and paging), create an `MSQuery` object, directly or by using a predicate:</span></span>

<span data-ttu-id="01146-144">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-144">**Objective-C**:</span></span>

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

<span data-ttu-id="01146-145">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-145">**Swift**:</span></span>

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

<span data-ttu-id="01146-146">`MSQuery` vous permet de contrôler plusieurs comportements de requête.</span><span class="sxs-lookup"><span data-stu-id="01146-146">`MSQuery` lets you control several query behaviors.</span></span>

* <span data-ttu-id="01146-147">Spécifier l’ordre des résultats</span><span class="sxs-lookup"><span data-stu-id="01146-147">Specify order of results</span></span>
* <span data-ttu-id="01146-148">Limite les champs tooreturn</span><span class="sxs-lookup"><span data-stu-id="01146-148">Limit which fields tooreturn</span></span>
* <span data-ttu-id="01146-149">Limiter le nombre d’enregistrements tooreturn</span><span class="sxs-lookup"><span data-stu-id="01146-149">Limit how many records tooreturn</span></span>
* <span data-ttu-id="01146-150">Spécifier le nombre total dans la réponse</span><span class="sxs-lookup"><span data-stu-id="01146-150">Specify total count in response</span></span>
* <span data-ttu-id="01146-151">Spécifier des paramètres de chaîne de requête personnalisés dans la requête</span><span class="sxs-lookup"><span data-stu-id="01146-151">Specify custom query string parameters in request</span></span>
* <span data-ttu-id="01146-152">Appliquer des fonctions supplémentaires</span><span class="sxs-lookup"><span data-stu-id="01146-152">Apply additional functions</span></span>

<span data-ttu-id="01146-153">Exécuter un `MSQuery` requête en appelant `readWithCompletion` sur l’objet de hello.</span><span class="sxs-lookup"><span data-stu-id="01146-153">Execute an `MSQuery` query by calling `readWithCompletion` on hello object.</span></span>

## <span data-ttu-id="01146-154"><a name="sorting"></a>Procédure : trier des données avec MSQuery</span><span class="sxs-lookup"><span data-stu-id="01146-154"><a name="sorting"></a>How to: Sort Data with MSQuery</span></span>
<span data-ttu-id="01146-155">résultats de toosort, examinons un exemple.</span><span class="sxs-lookup"><span data-stu-id="01146-155">toosort results, let's look at an example.</span></span> <span data-ttu-id="01146-156">toosort par ordre croissant de 'text' de champ, puis par ordre décroissant de « complète », appelez `MSQuery` comme suit :</span><span class="sxs-lookup"><span data-stu-id="01146-156">toosort by field 'text' ascending, then by 'complete' descending, invoke `MSQuery` like so:</span></span>

<span data-ttu-id="01146-157">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-157">**Objective-C**:</span></span>

```
[query orderByAscending:@"text"];
[query orderByDescending:@"complete"];
[query readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="01146-158">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-158">**Swift**:</span></span>

```
query.orderByAscending("text")
query.orderByDescending("complete")
query.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```


## <span data-ttu-id="01146-159"><a name="selecting"></a><a name="parameters"></a>Procédure : limitation des champs et développement des paramètres de chaîne de requête avec MSQuery</span><span class="sxs-lookup"><span data-stu-id="01146-159"><a name="selecting"></a><a name="parameters"></a>How to: Limit Fields and Expand Query String Parameters with MSQuery</span></span>
<span data-ttu-id="01146-160">toolimit toobe de champs renvoyé dans une requête, spécifiez les noms de champs de hello hello dans hello **selectFields** propriété.</span><span class="sxs-lookup"><span data-stu-id="01146-160">toolimit fields toobe returned in a query, specify hello names of hello fields in hello **selectFields** property.</span></span> <span data-ttu-id="01146-161">Cet exemple retourne uniquement le texte hello et champs terminés :</span><span class="sxs-lookup"><span data-stu-id="01146-161">This example returns only hello text and completed fields:</span></span>

<span data-ttu-id="01146-162">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-162">**Objective-C**:</span></span>

```
query.selectFields = @[@"text", @"complete"];
```

<span data-ttu-id="01146-163">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-163">**Swift**:</span></span>

```
query.selectFields = ["text", "complete"]
```

<span data-ttu-id="01146-164">paramètres de chaîne de requête supplémentaire de tooinclude dans hello server demande (par exemple, parce qu’un script côté serveur personnalisé utilise les), remplir `query.parameters` comme suit :</span><span class="sxs-lookup"><span data-stu-id="01146-164">tooinclude additional query string parameters in hello server request (for example, because a custom server-side script uses them), populate `query.parameters` like so:</span></span>

<span data-ttu-id="01146-165">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-165">**Objective-C**:</span></span>

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

<span data-ttu-id="01146-166">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-166">**Swift**:</span></span>

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <span data-ttu-id="01146-167"><a name="paging"></a>Procédure : configuration du format de page</span><span class="sxs-lookup"><span data-stu-id="01146-167"><a name="paging"></a>How to: Configure Page Size</span></span>
<span data-ttu-id="01146-168">Avec les applications mobiles Azure, les contrôles de taille de page hello hello nombre d’enregistrements qui sont extraites à la fois à partir des tables de back-end hello.</span><span class="sxs-lookup"><span data-stu-id="01146-168">With Azure Mobile Apps, hello page size controls hello number of records that are pulled at a time from hello backend tables.</span></span> <span data-ttu-id="01146-169">Un appel trop`pull` données puis de lots des données, en fonction de cette taille de page, jusqu'à ce qu’il n’y a aucun plus toopull d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="01146-169">A call too`pull` data would then batch up data, based on this page size, until there are no more records toopull.</span></span>

<span data-ttu-id="01146-170">Il s’agit d’une taille de page à l’aide de tooconfigure possible **MSPullSettings** comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="01146-170">It's possible tooconfigure a page size using **MSPullSettings** as shown below.</span></span> <span data-ttu-id="01146-171">taille de page Hello par défaut est 50, et exemple hello ci-dessous modifie too3.</span><span class="sxs-lookup"><span data-stu-id="01146-171">hello default page size is 50, and hello example below changes it too3.</span></span>

<span data-ttu-id="01146-172">Vous pouvez configurer un autre format de page pour des raisons de performances.</span><span class="sxs-lookup"><span data-stu-id="01146-172">You could configure a different page size for performance reasons.</span></span> <span data-ttu-id="01146-173">Si vous avez un grand nombre d’enregistrements de données de petite taille, une taille de page élevée allège hello d’allers-retours de serveur.</span><span class="sxs-lookup"><span data-stu-id="01146-173">If you have a large number of small data records, a high page size reduces hello number of server round-trips.</span></span>

<span data-ttu-id="01146-174">Ce paramètre contrôle uniquement hello taille de la page côté client de hello.</span><span class="sxs-lookup"><span data-stu-id="01146-174">This setting controls only hello page size on hello client side.</span></span> <span data-ttu-id="01146-175">Si hello client demande une plus grande taille de page que prend en charge les principaux des applications mobiles hello, taille de la page hello est limitée à hello hello maximale principal est toosupport configuré.</span><span class="sxs-lookup"><span data-stu-id="01146-175">If hello client asks for a larger page size than hello Mobile Apps backend supports, hello page size is capped at hello maximum hello backend is configured toosupport.</span></span>

<span data-ttu-id="01146-176">Ce paramètre est également hello *nombre* d’enregistrements de données, pas hello *taille en octets*.</span><span class="sxs-lookup"><span data-stu-id="01146-176">This setting is also hello *number* of data records, not hello *byte size*.</span></span>

<span data-ttu-id="01146-177">Si vous augmentez la taille de la page hello client, vous devez également augmenter la taille de page de hello sur le serveur hello.</span><span class="sxs-lookup"><span data-stu-id="01146-177">If you increase hello client page size, you should also increase hello page size on hello server.</span></span> <span data-ttu-id="01146-178">Consultez [« Comment : ajuster la taille de la pagination de table hello »](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) pour hello étapes toodo.</span><span class="sxs-lookup"><span data-stu-id="01146-178">See ["How to: Adjust hello table paging size"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for hello steps toodo this.</span></span>

<span data-ttu-id="01146-179">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-179">**Objective-C**:</span></span>

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


<span data-ttu-id="01146-180">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-180">**Swift**:</span></span>

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <span data-ttu-id="01146-181"><a name="inserting"></a>Procédure : insertion de données</span><span class="sxs-lookup"><span data-stu-id="01146-181"><a name="inserting"></a>How to: Insert Data</span></span>
<span data-ttu-id="01146-182">tooinsert une nouvelle ligne de table, créer un `NSDictionary` et appeler `table insert`.</span><span class="sxs-lookup"><span data-stu-id="01146-182">tooinsert a new table row, create a `NSDictionary` and invoke `table insert`.</span></span> <span data-ttu-id="01146-183">Si [le schéma dynamique] est activé, service principal de Service d’applications Azure mobile hello génère automatiquement de nouvelles colonnes selon hello `NSDictionary`.</span><span class="sxs-lookup"><span data-stu-id="01146-183">If [Dynamic Schema] is enabled, hello Azure App Service mobile backend automatically generates new columns based on hello `NSDictionary`.</span></span>

<span data-ttu-id="01146-184">Si `id` n’est pas fourni, hello principal génère automatiquement un nouvel ID unique.</span><span class="sxs-lookup"><span data-stu-id="01146-184">If `id` is not provided, hello backend automatically generates a new unique ID.</span></span> <span data-ttu-id="01146-185">Fournissez votre propre `id` toouse adresses de messagerie, les noms d’utilisateur ou vos propres valeurs en tant que code.</span><span class="sxs-lookup"><span data-stu-id="01146-185">Provide your own `id` toouse email addresses, usernames, or your own custom values as ID.</span></span> <span data-ttu-id="01146-186">Fournir son propre ID peut faciliter les jointures et la logique de base de données orientée métier.</span><span class="sxs-lookup"><span data-stu-id="01146-186">Providing your own ID may ease joins and business-oriented database logic.</span></span>

<span data-ttu-id="01146-187">Hello `result` contient hello nouvel élément a été inséré.</span><span class="sxs-lookup"><span data-stu-id="01146-187">hello `result` contains hello new item that was inserted.</span></span> <span data-ttu-id="01146-188">Selon la logique du serveur, peut-être supplémentaires, ou des données modifiées comparées toowhat a été transmise toohello server.</span><span class="sxs-lookup"><span data-stu-id="01146-188">Depending on your server logic, it may have additional or modified data compared toowhat was passed toohello server.</span></span>

<span data-ttu-id="01146-189">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-189">**Objective-C**:</span></span>

```
NSDictionary *newItem = @{@"id": @"custom-id", @"text": @"my new item", @"complete" : @NO};
[table insert:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="01146-190">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-190">**Swift**:</span></span>

```
let newItem = ["id": "custom-id", "text": "my new item", "complete": false]
table.insert(newItem) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

## <span data-ttu-id="01146-191"><a name="modifying"></a>Procédure : modification des données</span><span class="sxs-lookup"><span data-stu-id="01146-191"><a name="modifying"></a>How to: Modify Data</span></span>
<span data-ttu-id="01146-192">tooupdate une ligne existante, modifier un élément et l’appel `update`:</span><span class="sxs-lookup"><span data-stu-id="01146-192">tooupdate an existing row, modify an item and call `update`:</span></span>

<span data-ttu-id="01146-193">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-193">**Objective-C**:</span></span>

```
NSMutableDictionary *newItem = [oldItem mutableCopy]; // oldItem is NSDictionary
[newItem setValue:@"Updated text" forKey:@"text"];
[table update:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="01146-194">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-194">**Swift**:</span></span>

```
if let newItem = oldItem.mutableCopy() as? NSMutableDictionary {
    newItem["text"] = "Updated text"
    table2.update(newItem as [NSObject: AnyObject], completion: { (result, error) -> Void in
        if let err = error {
            print("ERROR ", err)
        } else if let item = result {
            print("Todo Item: ", item["text"])
        }
    })
}
```

<span data-ttu-id="01146-195">Vous pouvez également fournir les ID de ligne hello et champ de hello mis à jour :</span><span class="sxs-lookup"><span data-stu-id="01146-195">Alternatively, supply hello row ID and hello updated field:</span></span>

<span data-ttu-id="01146-196">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-196">**Objective-C**:</span></span>

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="01146-197">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-197">**Swift**:</span></span>

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

<span data-ttu-id="01146-198">Au minimum, hello `id` attribut doit être défini lors de la mise à jour.</span><span class="sxs-lookup"><span data-stu-id="01146-198">At minimum, hello `id` attribute must be set when making updates.</span></span>

## <span data-ttu-id="01146-199"><a name="deleting"></a>Procédure : suppression de données</span><span class="sxs-lookup"><span data-stu-id="01146-199"><a name="deleting"></a>How to: Delete Data</span></span>
<span data-ttu-id="01146-200">toodelete un élément, appelez `delete` avec l’élément de hello :</span><span class="sxs-lookup"><span data-stu-id="01146-200">toodelete an item, invoke `delete` with hello item:</span></span>

<span data-ttu-id="01146-201">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-201">**Objective-C**:</span></span>

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="01146-202">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-202">**Swift**:</span></span>

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="01146-203">Vous pouvez également effectuer la suppression en fournissant un ID de ligne :</span><span class="sxs-lookup"><span data-stu-id="01146-203">Alternatively, delete by providing a row ID:</span></span>

<span data-ttu-id="01146-204">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-204">**Objective-C**:</span></span>

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="01146-205">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-205">**Swift**:</span></span>

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="01146-206">Au minimum, hello `id` attribut doit être défini lors de la fabrication supprime.</span><span class="sxs-lookup"><span data-stu-id="01146-206">At minimum, hello `id` attribute must be set when making deletes.</span></span>

## <span data-ttu-id="01146-207"><a name="customapi"></a>Procédure : appel d’une API personnalisée</span><span class="sxs-lookup"><span data-stu-id="01146-207"><a name="customapi"></a>How to: Call Custom API</span></span>
<span data-ttu-id="01146-208">Une API personnalisée vous permet d’exposer toutes les fonctionnalités du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="01146-208">With a custom API, you can expose any backend functionality.</span></span> <span data-ttu-id="01146-209">Il n’a d’opération de table toomap tooa.</span><span class="sxs-lookup"><span data-stu-id="01146-209">It doesn't have toomap tooa table operation.</span></span> <span data-ttu-id="01146-210">Non seulement avoir davantage de contrôle sur la messagerie, vous pouvez même en lecture/jeu d’en-têtes et de modifier le format du corps de réponse hello.</span><span class="sxs-lookup"><span data-stu-id="01146-210">Not only do you gain more control over messaging, you can even read/set headers and change hello response body format.</span></span> <span data-ttu-id="01146-211">toolearn comment toocreate une API personnalisée sur le serveur principal hello, lire [API personnalisées](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span><span class="sxs-lookup"><span data-stu-id="01146-211">toolearn how toocreate a custom API on hello backend, read [Custom APIs](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span></span>

<span data-ttu-id="01146-212">toocall une API personnalisée, appelez `MSClient.invokeAPI`.</span><span class="sxs-lookup"><span data-stu-id="01146-212">toocall a custom API, call `MSClient.invokeAPI`.</span></span> <span data-ttu-id="01146-213">demande de Hello et contenu de réponse sont traités en tant que JSON.</span><span class="sxs-lookup"><span data-stu-id="01146-213">hello request and response content are treated as JSON.</span></span> <span data-ttu-id="01146-214">toouse autres types de médias, [utilisez hello autre surcharge de `invokeAPI` ] [ 5].</span><span class="sxs-lookup"><span data-stu-id="01146-214">toouse other media types, [use hello other overload of `invokeAPI`][5].</span></span>  <span data-ttu-id="01146-215">toomake un `GET` demande au lieu d’un `POST` demande, le paramètre de jeu de `HTTPMethod` trop`"GET"` et paramètre `body` trop`nil` (étant donné que les demandes GET ne disposez pas des corps de message.) Si votre API personnalisée prend en charge les autres verbes HTTP, modifiez `HTTPMethod` en conséquence.</span><span class="sxs-lookup"><span data-stu-id="01146-215">toomake a `GET` request instead of a `POST` request, set parameter `HTTPMethod` too`"GET"` and parameter `body` too`nil` (since GET requests do not have message bodies.) If your custom API supports other HTTP verbs, change `HTTPMethod` appropriately.</span></span>

<span data-ttu-id="01146-216">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-216">**Objective-C**:</span></span>

```
[self.client invokeAPI:@"sendEmail"
                  body:@{ @"contents": @"Hello world!" }
            HTTPMethod:@"POST"
            parameters:@{ @"to": @"bill@contoso.com", @"subject" : @"Hi!" }
               headers:nil
            completion: ^(NSData *result, NSHTTPURLResponse *response, NSError *error) {
                if(error) {
                    NSLog(@"ERROR %@", error);
                } else {
                    // Do something with result
                }
            }];
```

<span data-ttu-id="01146-217">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-217">**Swift**:</span></span>

```
client.invokeAPI("sendEmail",
            body: [ "contents": "Hello World" ],
            HTTPMethod: "POST",
            parameters: [ "to": "bill@contoso.com", "subject" : "Hi!" ],
            headers: nil)
            {
                (result, response, error) -> Void in
                if let err = error {
                    print("ERROR ", err)
                } else if let res = result {
                          // Do something with result
                }
        }
```

## <span data-ttu-id="01146-218"><a name="templates"></a>Comment : notifications de Registre push modèles toosend inter-plateformes</span><span class="sxs-lookup"><span data-stu-id="01146-218"><a name="templates"></a>How to: Register push templates toosend cross-platform notifications</span></span>
<span data-ttu-id="01146-219">modèles de tooregister, passer des modèles avec votre **client.push registerDeviceToken** méthode dans votre application cliente.</span><span class="sxs-lookup"><span data-stu-id="01146-219">tooregister templates, pass templates with your **client.push registerDeviceToken** method in your client app.</span></span>

<span data-ttu-id="01146-220">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-220">**Objective-C**:</span></span>

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

<span data-ttu-id="01146-221">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-221">**Swift**:</span></span>

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

<span data-ttu-id="01146-222">Vos modèles sont de type NSDictionary et peuvent contenir plusieurs modèles Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="01146-222">Your templates are of type NSDictionary and can contain multiple templates in hello following format:</span></span>

<span data-ttu-id="01146-223">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-223">**Objective-C**:</span></span>

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

<span data-ttu-id="01146-224">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-224">**Swift**:</span></span>

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

<span data-ttu-id="01146-225">Toutes les balises sont supprimés de la demande de hello pour la sécurité.</span><span class="sxs-lookup"><span data-stu-id="01146-225">All tags are stripped from hello request for security.</span></span>  <span data-ttu-id="01146-226">les balises tooadd tooinstallations ou modèles dans les installations, consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure][4].</span><span class="sxs-lookup"><span data-stu-id="01146-226">tooadd tags tooinstallations or templates within installations, see [Work with hello .NET backend server SDK for Azure Mobile Apps][4].</span></span>  <span data-ttu-id="01146-227">notifications de toosend à l’aide de ces modèles enregistrés, travailler avec [API de concentrateurs de Notification][3].</span><span class="sxs-lookup"><span data-stu-id="01146-227">toosend notifications using these registered templates, work with [Notification Hubs APIs][3].</span></span>

## <span data-ttu-id="01146-228"><a name="errors"></a>Procédure : gestion des erreurs</span><span class="sxs-lookup"><span data-stu-id="01146-228"><a name="errors"></a>How to: Handle Errors</span></span>
<span data-ttu-id="01146-229">Lorsque vous appelez un serveur principal de Service d’applications Azure mobile, bloc de fin hello contient un `NSError` paramètre.</span><span class="sxs-lookup"><span data-stu-id="01146-229">When you call an Azure App Service mobile backend, hello completion block contains an `NSError` parameter.</span></span> <span data-ttu-id="01146-230">Si une erreur se produit, ce paramètre est non-nil.</span><span class="sxs-lookup"><span data-stu-id="01146-230">When an error occurs, this parameter is non-nil.</span></span> <span data-ttu-id="01146-231">Dans votre code, vous devez vérifier ce paramètre et gérer l’erreur hello selon vos besoins, comme illustré dans hello précédant les extraits de code.</span><span class="sxs-lookup"><span data-stu-id="01146-231">In your code, you should check this parameter and handle hello error as needed, as demonstrated in hello preceding code snippets.</span></span>

<span data-ttu-id="01146-232">fichier de Hello [ `<WindowsAzureMobileServices/MSError.h>` ] [ 6] définit des constantes hello `MSErrorResponseKey`, `MSErrorRequestKey`, et `MSErrorServerItemKey`.</span><span class="sxs-lookup"><span data-stu-id="01146-232">hello file [`<WindowsAzureMobileServices/MSError.h>`][6] defines hello constants `MSErrorResponseKey`, `MSErrorRequestKey`, and `MSErrorServerItemKey`.</span></span> <span data-ttu-id="01146-233">tooget toohello erreur liée à plus de données :</span><span class="sxs-lookup"><span data-stu-id="01146-233">tooget more data related toohello error:</span></span>

<span data-ttu-id="01146-234">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-234">**Objective-C**:</span></span>

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

<span data-ttu-id="01146-235">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-235">**Swift**:</span></span>

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

<span data-ttu-id="01146-236">En outre, les fichiers hello définit des constantes pour chaque code d’erreur :</span><span class="sxs-lookup"><span data-stu-id="01146-236">In addition, hello file defines constants for each error code:</span></span>

<span data-ttu-id="01146-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-237">**Objective-C**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

<span data-ttu-id="01146-238">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-238">**Swift**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

## <span data-ttu-id="01146-239"><a name="adal"></a>Comment : authentifier les utilisateurs avec hello bibliothèque d’authentification Active Directory</span><span class="sxs-lookup"><span data-stu-id="01146-239"><a name="adal"></a>How to: Authenticate users with hello Active Directory Authentication Library</span></span>
<span data-ttu-id="01146-240">Vous pouvez utiliser les utilisateurs de toosign hello Active Directory Authentication Library (ADAL) dans votre application à l’aide d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="01146-240">You can use hello Active Directory Authentication Library (ADAL) toosign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="01146-241">L’authentification du client flux à l’aide d’un fournisseur d’identité SDK est préférable toousing hello `loginWithProvider:completion:` (méthode).</span><span class="sxs-lookup"><span data-stu-id="01146-241">Client flow authentication using an identity provider SDK is preferable toousing hello `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="01146-242">L’authentification par client flux offre une interface UX native plus simple et permet une personnalisation supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="01146-242">Client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="01146-243">Configurer le service principal de votre application mobile pour la connexion d’AAD par hello suivant [comment tooconfigure application de Service pour la connexion Active Directory] [ 7] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="01146-243">Configure your mobile app backend for AAD sign-in by following hello [How tooconfigure App Service for Active Directory login][7] tutorial.</span></span> <span data-ttu-id="01146-244">Assurez-vous qu’étape facultative toocomplete hello d’inscription d’une application cliente native.</span><span class="sxs-lookup"><span data-stu-id="01146-244">Make sure toocomplete hello optional step of registering a native client application.</span></span> <span data-ttu-id="01146-245">Pour iOS, nous vous recommandons ce hello URI de redirection est sous forme de hello `<app-scheme>://<bundle-id>`.</span><span class="sxs-lookup"><span data-stu-id="01146-245">For iOS, we recommend that hello redirect URI is of hello form `<app-scheme>://<bundle-id>`.</span></span> <span data-ttu-id="01146-246">Pour plus d’informations, consultez hello [ADAL iOS quickstart][8].</span><span class="sxs-lookup"><span data-stu-id="01146-246">For more information, see hello [ADAL iOS quickstart][8].</span></span>
2. <span data-ttu-id="01146-247">Installez la bibliothèque ADAL à l’aide de Cocoapods.</span><span class="sxs-lookup"><span data-stu-id="01146-247">Install ADAL using Cocoapods.</span></span> <span data-ttu-id="01146-248">Modifier votre hello de tooinclude Podfile définition, en remplaçant **votre projet** avec nom hello de votre projet Xcode :</span><span class="sxs-lookup"><span data-stu-id="01146-248">Edit your Podfile tooinclude hello following definition, replacing **YOUR-PROJECT** with hello name of your Xcode project:</span></span>

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   <span data-ttu-id="01146-249">et hello Pod :</span><span class="sxs-lookup"><span data-stu-id="01146-249">and hello Pod:</span></span>

        pod 'ADALiOS'
3. <span data-ttu-id="01146-250">À l’aide de hello Terminal Server, exécutez `pod install` à partir du répertoire de hello contenant votre projet, puis ouvrez espace de travail Xcode hello généré (pas le projet hello).</span><span class="sxs-lookup"><span data-stu-id="01146-250">Using hello Terminal, run `pod install` from hello directory containing your project, and then open hello generated Xcode workspace (not hello project).</span></span>
4. <span data-ttu-id="01146-251">Ajoutez hello après application de code tooyour, selon le langage toohello que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="01146-251">Add hello following code tooyour application, according toohello language you are using.</span></span> <span data-ttu-id="01146-252">Vérifiez à chaque fois ces remplacements :</span><span class="sxs-lookup"><span data-stu-id="01146-252">In each, make these replacements:</span></span>

   * <span data-ttu-id="01146-253">Remplacez **INSERT-autorité-ici** avec nom hello du client hello dans lequel vous avez configuré votre application.</span><span class="sxs-lookup"><span data-stu-id="01146-253">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="01146-254">Le format doit être https://login.microsoftonline.com/contoso.onmicrosoft.com. Cette valeur peut être copiée à partir de l’onglet du domaine hello dans Azure Active Directory Bonjour [portail Azure classic].</span><span class="sxs-lookup"><span data-stu-id="01146-254">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com. This value can be copied from hello Domain tab in your Azure Active Directory in hello [Azure classic portal].</span></span>
   * <span data-ttu-id="01146-255">Remplacez **INSERT-RESOURCE-ID-ici** avec l’ID de client hello pour le service principal de votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="01146-255">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="01146-256">Vous pouvez obtenir l’ID de client à partir de hello **avancé** onglet sous **paramètres Azure Active Directory** dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="01146-256">You can obtain the client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
   * <span data-ttu-id="01146-257">Remplacez **INSERT-CLIENT-ID-ici** avec l’ID de client hello copié à partir de l’application cliente native de hello.</span><span class="sxs-lookup"><span data-stu-id="01146-257">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
   * <span data-ttu-id="01146-258">Remplacez **INSERT-REDIRECT-URI-ici** avec de votre site */.auth/login/done* point de terminaison, à l’aide du schéma HTTPS de hello.</span><span class="sxs-lookup"><span data-stu-id="01146-258">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="01146-259">Cette valeur doit être similaire trop*https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="01146-259">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

<span data-ttu-id="01146-260">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-260">**Objective-C**:</span></span>

    #import <ADALiOS/ADAuthenticationContext.h>
    #import <ADALiOS/ADAuthenticationSettings.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*))completionBlock;
    {
        NSString *authority = @"INSERT-AUTHORITY-HERE";
        NSString *resourceId = @"INSERT-RESOURCE-ID-HERE";
        NSString *clientId = @"INSERT-CLIENT-ID-HERE";
        NSURL *redirectUri = [[NSURL alloc]initWithString:@"INSERT-REDIRECT-URI-HERE"];
        ADAuthenticationError *error;
        ADAuthenticationContext *authContext = [ADAuthenticationContext authenticationContextWithAuthority:authority error:&error];
        authContext.parentController = parent;
        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:resourceId
                                     clientId:clientId
                                  redirectUri:redirectUri
                              completionBlock:^(ADAuthenticationResult *result) {
                                  if (result.status != AD_SUCCEEDED)
                                  {
                                      completionBlock(nil, result.error);;
                                  }
                                  else
                                  {
                                      NSDictionary *payload = @{
                                                                @"access_token" : result.tokenCacheStoreItem.accessToken
                                                                };
                                      [client loginWithProvider:@"aad" token:payload completion:completionBlock];
                                  }
                              }];
    }


<span data-ttu-id="01146-261">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-261">**Swift**:</span></span>

    // add hello following imports tooyour bridging header:
    //        #import <ADALiOS/ADAuthenticationContext.h>
    //        #import <ADALiOS/ADAuthenticationSettings.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let authority = "INSERT-AUTHORITY-HERE"
        let resourceId = "INSERT-RESOURCE-ID-HERE"
        let clientId = "INSERT-CLIENT-ID-HERE"
        let redirectUri = NSURL(string: "INSERT-REDIRECT-URI-HERE")
        var error: AutoreleasingUnsafeMutablePointer<ADAuthenticationError?> = nil
        let authContext = ADAuthenticationContext(authority: authority, error: error)
        authContext.parentController = parent
        ADAuthenticationSettings.sharedInstance().enableFullScreen = true
        authContext.acquireTokenWithResource(resourceId, clientId: clientId, redirectUri: redirectUri) { (result) in
                if result.status != AD_SUCCEEDED {
                    completion(nil, result.error)
                }
                else {
                    let payload: [String: String] = ["access_token": result.tokenCacheStoreItem.accessToken]
                    client.loginWithProvider("aad", token: payload, completion: completion)
                }
            }
    }

## <span data-ttu-id="01146-262"><a name="facebook-sdk"></a>Comment : authentifier les utilisateurs avec hello SDK Facebook pour iOS</span><span class="sxs-lookup"><span data-stu-id="01146-262"><a name="facebook-sdk"></a>How to: Authenticate users with hello Facebook SDK for iOS</span></span>
<span data-ttu-id="01146-263">Vous pouvez utiliser hello SDK Facebook pour les utilisateurs iOS toosign dans votre application à l’aide de Facebook.</span><span class="sxs-lookup"><span data-stu-id="01146-263">You can use hello Facebook SDK for iOS toosign users into your application using Facebook.</span></span>  <span data-ttu-id="01146-264">À l’aide d’une authentification de flux client est préférable toousing hello `loginWithProvider:completion:` (méthode).</span><span class="sxs-lookup"><span data-stu-id="01146-264">Using a client flow authentication is preferable toousing hello `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="01146-265">l’authentification du client flux Hello fournit un aspect d’expérience utilisateur plus natif et permet une personnalisation supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="01146-265">hello client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="01146-266">Configurez votre serveur principal d’application mobile pour la connexion à Facebook à l’aide du [comment tooconfigure application de Service pour le compte de connexion Facebook] [ 9] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="01146-266">Configure your mobile app backend for Facebook sign-in by following the [How tooconfigure App Service for Facebook login][9] tutorial.</span></span>
2. <span data-ttu-id="01146-267">Installer hello SDK Facebook pour iOS en suivant hello [SDK Facebook pour iOS - mise en route] [ 10] documentation.</span><span class="sxs-lookup"><span data-stu-id="01146-267">Install hello Facebook SDK for iOS by following hello [Facebook SDK for iOS - Getting Started][10] documentation.</span></span> <span data-ttu-id="01146-268">Au lieu de créer une application, vous pouvez ajouter une inscription existante hello iOS plateforme tooyour.</span><span class="sxs-lookup"><span data-stu-id="01146-268">Instead of creating an app, you can add hello iOS platform tooyour existing registration.</span></span>
3. <span data-ttu-id="01146-269">Documentation de Facebook inclut du code Objective-C Bonjour délégué de l’application.</span><span class="sxs-lookup"><span data-stu-id="01146-269">Facebook's documentation includes some Objective-C code in hello App Delegate.</span></span> <span data-ttu-id="01146-270">Si vous utilisez **Swift**, vous pouvez utiliser hello suivant des traductions pour AppDelegate.swift :</span><span class="sxs-lookup"><span data-stu-id="01146-270">If you are using **Swift**, you can use hello following translations for AppDelegate.swift:</span></span>

        // Add hello following import tooyour bridging header:
        //        #import <FBSDKCoreKit/FBSDKCoreKit.h>

        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            FBSDKApplicationDelegate.sharedInstance().application(application, didFinishLaunchingWithOptions: launchOptions)
            // Add any custom logic here.
            return true
        }

        func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?, annotation: AnyObject?) -> Bool {
            let handled = FBSDKApplicationDelegate.sharedInstance().application(application, openURL: url, sourceApplication: sourceApplication, annotation: annotation)
            // Add any custom logic here.
            return handled
        }
4. <span data-ttu-id="01146-271">En outre tooadding `FBSDKCoreKit.framework` tooyour de projet, ajoutez également une référence de trop`FBSDKLoginKit.framework` Bonjour identique.</span><span class="sxs-lookup"><span data-stu-id="01146-271">In addition tooadding `FBSDKCoreKit.framework` tooyour project, also add a reference too`FBSDKLoginKit.framework` in hello same way.</span></span>
5. <span data-ttu-id="01146-272">Ajoutez hello après application de code tooyour, selon le langage toohello que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="01146-272">Add hello following code tooyour application, according toohello language you are using.</span></span>

<span data-ttu-id="01146-273">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-273">**Objective-C**:</span></span>

    #import <FBSDKLoginKit/FBSDKLoginKit.h>
    #import <FBSDKCoreKit/FBSDKAccessToken.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*)) completionBlock;
    {        
        FBSDKLoginManager *loginManager = [[FBSDKLoginManager alloc] init];
        [loginManager
         logInWithReadPermissions: @[@"public_profile"]
         fromViewController:parent
         handler:^(FBSDKLoginManagerLoginResult *result, NSError *error) {
             if (error) {
                 completionBlock(nil, error);
             } else if (result.isCancelled) {
                 completionBlock(nil, error);
             } else {
                 NSDictionary *payload = @{
                                           @"access_token":result.token.tokenString
                                           };
                 [client loginWithProvider:@"facebook" token:payload completion:completionBlock];
             }
         }];
    }

<span data-ttu-id="01146-274">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-274">**Swift**:</span></span>

    // Add hello following imports tooyour bridging header:
    //        #import <FBSDKLoginKit/FBSDKLoginKit.h>
    //        #import <FBSDKCoreKit/FBSDKAccessToken.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let loginManager = FBSDKLoginManager()
        loginManager.logInWithReadPermissions(["public_profile"], fromViewController: parent) { (result, error) in
            if (error != nil) {
                completion(nil, error)
            }
            else if result.isCancelled {
                completion(nil, error)
            }
            else {
                let payload: [String: String] = ["access_token": result.token.tokenString]
                client.loginWithProvider("facebook", token: payload, completion: completion)
            }
        }
    }

## <span data-ttu-id="01146-275"><a name="twitter-fabric"></a>Procédure : authentifier les utilisateurs avec Twitter Fabric pour iOS</span><span class="sxs-lookup"><span data-stu-id="01146-275"><a name="twitter-fabric"></a>How to: Authenticate users with Twitter Fabric for iOS</span></span>
<span data-ttu-id="01146-276">Vous pouvez utiliser l’infrastructure pour les utilisateurs iOS toosign dans votre application à l’aide de Twitter.</span><span class="sxs-lookup"><span data-stu-id="01146-276">You can use Fabric for iOS toosign users into your application using Twitter.</span></span> <span data-ttu-id="01146-277">Flux de l’authentification du client est préférable toousing hello `loginWithProvider:completion:` de la méthode, il fournit un aspect d’expérience utilisateur plus natif et permet la personnalisation supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="01146-277">Client Flow authentication is preferable toousing hello `loginWithProvider:completion:` method, as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="01146-278">Configurer le service principal de votre application mobile pour la connexion à Twitter en suivant les hello [comment tooconfigure application de Service pour le compte de connexion Twitter](app-service-mobile-how-to-configure-twitter-authentication.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="01146-278">Configure your mobile app backend for Twitter sign-in by following hello [How tooconfigure App Service for Twitter login](app-service-mobile-how-to-configure-twitter-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="01146-279">Ajouter l’ensemble fibre optique tooyour projet hello suivant [l’ensemble fibre optique pour iOS - mise en route] documentation et la configuration TwitterKit.</span><span class="sxs-lookup"><span data-stu-id="01146-279">Add Fabric tooyour project by following hello [Fabric for iOS - Getting Started] documentation and setting up TwitterKit.</span></span>

   > [!NOTE]
   > <span data-ttu-id="01146-280">Par défaut, Fabric crée une application Twitter pour vous.</span><span class="sxs-lookup"><span data-stu-id="01146-280">By default, Fabric creates a Twitter application for you.</span></span> <span data-ttu-id="01146-281">Vous pouvez éviter la création d’une application en enregistrant hello clé de consommateur et Secret de consommateur que vous avez créé précédemment à l’aide de hello suivant des extraits de code.</span><span class="sxs-lookup"><span data-stu-id="01146-281">You can avoid creating an application by registering hello Consumer Key and Consumer Secret you created earlier using hello following code snippets.</span></span>    <span data-ttu-id="01146-282">Sinon, vous pouvez remplacer la clé de consommateur de hello et valeurs de question secrète du client, vous devez fournir les valeurs tooApp Service avec hello que vous consultez Bonjour [tableau de bord de l’ensemble fibre optique].</span><span class="sxs-lookup"><span data-stu-id="01146-282">Alternatively, you can replace hello Consumer Key and Consumer Secret values that you provide tooApp Service with hello values you see in hello [Fabric Dashboard].</span></span> <span data-ttu-id="01146-283">Si vous choisissez cette option, être vraiment tooset hello rappel URL tooa valeur d’espace réservé, tel que `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="01146-283">If you choose this option, be sure tooset hello callback URL tooa placeholder value, such as `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span></span>
   >
   >

    <span data-ttu-id="01146-284">Si vous choisissez toouse secrets hello que vous avez créé précédemment, ajoutez hello suivant code tooyour délégué de l’application :</span><span class="sxs-lookup"><span data-stu-id="01146-284">If you choose toouse hello secrets you created earlier, add hello following code tooyour App Delegate:</span></span>

    <span data-ttu-id="01146-285">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-285">**Objective-C**:</span></span>

        #import <Fabric/Fabric.h>
        #import <TwitterKit/TwitterKit.h>
        // ...
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
            [[Twitter sharedInstance] startWithConsumerKey:@"your_key" consumerSecret:@"your_secret"];
            [Fabric with:@[[Twitter class]]];
            // Add any custom logic here.
            return YES;
        }

    <span data-ttu-id="01146-286">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-286">**Swift**:</span></span>

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. <span data-ttu-id="01146-287">Ajoutez hello après application de code tooyour, selon le langage toohello que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="01146-287">Add hello following code tooyour application, according toohello language you are using.</span></span>

<span data-ttu-id="01146-288">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-288">**Objective-C**:</span></span>

    #import <TwitterKit/TwitterKit.h>
    // ...
    - (void)authenticate:(UIViewController*)parent completion:(void (^) (MSUser*, NSError*))completionBlock
    {
        [[Twitter sharedInstance] logInWithCompletion:^(TWTRSession *session, NSError *error) {
            if (session) {
                NSDictionary *payload = @{
                                            @"access_token":session.authToken,
                                            @"access_token_secret":session.authTokenSecret
                                        };
                [client loginWithProvider:@"twitter" token:payload completion:completionBlock];
            } else {
                completionBlock(nil, error);
            }
        }];
    }

<span data-ttu-id="01146-289">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-289">**Swift**:</span></span>

    import TwitterKit
    // ...
    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let client = self.table!.client
        Twitter.sharedInstance().logInWithCompletion { session, error in
            if (session != nil) {
                let payload: [String: String] = ["access_token": session!.authToken, "access_token_secret": session!.authTokenSecret]
                client.loginWithProvider("twitter", token: payload, completion: completion)
            } else {
                completion(nil, error)
            }
        }
    }

## <span data-ttu-id="01146-290"><a name="google-sdk"></a>Comment : authentifier les utilisateurs avec hello Google connectez-vous SDK pour iOS</span><span class="sxs-lookup"><span data-stu-id="01146-290"><a name="google-sdk"></a>How to: Authenticate users with hello Google Sign-In SDK for iOS</span></span>
<span data-ttu-id="01146-291">Vous pouvez utiliser hello Google connectez-vous Kit de développement logiciel pour les utilisateurs iOS toosign dans votre application à l’aide d’un compte Google.</span><span class="sxs-lookup"><span data-stu-id="01146-291">You can use hello Google Sign-In SDK for iOS toosign users into your application using a Google account.</span></span>  <span data-ttu-id="01146-292">Google a récemment annoncé que les modifications des stratégies de sécurité tootheir OAuth.</span><span class="sxs-lookup"><span data-stu-id="01146-292">Google recently announced changes tootheir OAuth security policies.</span></span>  <span data-ttu-id="01146-293">Ces modifications de stratégie requiert utilisation hello du SDK Google Bonjour futures.</span><span class="sxs-lookup"><span data-stu-id="01146-293">These policy changes will require hello use of the Google SDK in hello future.</span></span>

1. <span data-ttu-id="01146-294">Configurer le service principal de votre application mobile pour la connexion à Google par hello suivant [comment tooconfigure application de Service pour le compte de connexion Google](app-service-mobile-how-to-configure-google-authentication.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="01146-294">Configure your mobile app backend for Google sign-in by following hello [How tooconfigure App Service for Google login](app-service-mobile-how-to-configure-google-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="01146-295">Installer hello Google SDK pour iOS en suivant hello [Google Sign-In pour iOS - démarrer l’intégration](https://developers.google.com/identity/sign-in/ios/start-integrating) documentation.</span><span class="sxs-lookup"><span data-stu-id="01146-295">Install hello Google SDK for iOS by following hello [Google Sign-In for iOS - Start integrating](https://developers.google.com/identity/sign-in/ios/start-integrating) documentation.</span></span> <span data-ttu-id="01146-296">Vous pouvez ignorer la section de hello « S’authentifier avec un serveur principal ».</span><span class="sxs-lookup"><span data-stu-id="01146-296">You may skip hello "Authenticate with a Backend Server" section.</span></span>
3. <span data-ttu-id="01146-297">Ajouter hello suivant du délégué tooyour `signIn:didSignInForUser:withError:` méthode, selon le langage de toohello vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="01146-297">Add hello following tooyour delegate's `signIn:didSignInForUser:withError:` method, according toohello language you are using.</span></span>

<span data-ttu-id="01146-298">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-298">**Objective-C**:</span></span>

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

<span data-ttu-id="01146-299">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-299">**Swift**:</span></span>

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. <span data-ttu-id="01146-300">Veillez à ajouter également hello suivant trop`application:didFinishLaunchingWithOptions:` dans votre application délégué, en remplaçant « SERVER_CLIENT_ID » avec hello même ID que vous avez utilisé tooconfigure du Service d’applications à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="01146-300">Make sure you also add hello following too`application:didFinishLaunchingWithOptions:` in your app delegate, replacing "SERVER_CLIENT_ID" with hello same ID that you used tooconfigure App Service in step 1.</span></span>

<span data-ttu-id="01146-301">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-301">**Objective-C**:</span></span>

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 <span data-ttu-id="01146-302">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-302">**Swift**:</span></span>

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. <span data-ttu-id="01146-303">Ajouter hello suite de l’application tooyour de code dans un UIViewController qui implémente hello `GIDSignInUIDelegate` protocole, selon le langage de toohello vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="01146-303">Add hello following code tooyour application in a UIViewController that implements hello `GIDSignInUIDelegate` protocol, according toohello language you are using.</span></span>  <span data-ttu-id="01146-304">Vous êtes déconnecté avant le fait d’être connecté à nouveau, et bien que vous n’avez pas besoin tooenter vos informations d’identification à nouveau, vous voyez une boîte de dialogue de consentement.</span><span class="sxs-lookup"><span data-stu-id="01146-304">You are signed out before being signed in again, and although you don't need tooenter your credentials again, you see a consent dialog.</span></span>  <span data-ttu-id="01146-305">Uniquement appeler cette méthode lorsque le jeton de session hello a expiré.</span><span class="sxs-lookup"><span data-stu-id="01146-305">Only call this method when hello session token has expired.</span></span>

   <span data-ttu-id="01146-306">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="01146-306">**Objective-C**:</span></span>

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   <span data-ttu-id="01146-307">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="01146-307">**Swift**:</span></span>

       // ...
       func authenticate() {
           GIDSignIn.sharedInstance().uiDelegate = self
           GIDSignIn.sharedInstance().signOut()
           GIDSignIn.sharedInstance().signIn()
       }

<!-- Anchors. -->

[What is Mobile Services]: #what-is
[Concepts]: #concepts
[Setup and Prerequisites]: #Setup
[How to: Create hello Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data toohello user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize hello client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
[démarrage rapide d’Azure Mobile Apps]: app-service-mobile-ios-get-started.md

[Add Mobile Services tooExisting App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts tooauthorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[le schéma dynamique]: http://go.microsoft.com/fwlink/p/?LinkId=296271
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI toomanage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

[tableau de bord de l’ensemble fibre optique]: https://www.fabric.io/home
[l’ensemble fibre optique pour iOS - mise en route]: https://docs.fabric.io/ios/fabric/getting-started.html
[1]: https://github.com/Azure/azure-mobile-apps-ios-client/blob/master/README.md#ios-client-sdk
[2]: http://azure.github.io/azure-mobile-apps-ios-client/
[3]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[4]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags
[5]: http://azure.github.io/azure-mobile-services/iOS/v3/Classes/MSClient.html#//api/name/invokeAPI:data:HTTPMethod:parameters:headers:completion:
[6]: https://github.com/Azure/azure-mobile-services/blob/master/sdk/iOS/src/MSError.h
[7]: app-service-mobile-how-to-configure-active-directory-authentication.md
[8]: ../active-directory/active-directory-devquickstarts-ios.md
[9]: app-service-mobile-how-to-configure-facebook-authentication.md
[10]: https://developers.facebook.com/docs/ios/getting-started
