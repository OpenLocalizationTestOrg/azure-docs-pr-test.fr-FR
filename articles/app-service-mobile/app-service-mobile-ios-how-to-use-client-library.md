---
title: "Utilisation du Kit de développement logiciel (SDK) iOS pour Azure Mobile Apps"
description: "Utilisation du Kit de développement logiciel (SDK) iOS pour Azure Mobile Apps"
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
ms.openlocfilehash: 65817208e1b26fb5f9eb56d164f48b44d57dce56
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-ios-client-library-for-azure-mobile-apps"></a><span data-ttu-id="a7fa4-103">Utilisation de la bibliothèque cliente iOS pour Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="a7fa4-103">How to Use iOS Client Library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="a7fa4-104">Ce guide indique le déroulement de scénarios courants dans le cadre de l’utilisation du dernier [SDK iOS Azure Mobile Apps][1].</span><span class="sxs-lookup"><span data-stu-id="a7fa4-104">This guide teaches you to perform common scenarios using the latest [Azure Mobile Apps iOS SDK][1].</span></span> <span data-ttu-id="a7fa4-105">Si vous ne connaissez pas Azure Mobile Apps, consultez d’abord la section [Démarrage rapide d’Azure Mobile Apps] pour créer un backend, créer une table et télécharger un projet Xcode iOS prédéfini.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend, create a table, and download a pre-built iOS Xcode project.</span></span> <span data-ttu-id="a7fa4-106">Dans ce guide, nous nous concentrons sur le SDK iOS côté client.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-106">In this guide, we focus on the client-side iOS SDK.</span></span> <span data-ttu-id="a7fa4-107">Pour en savoir plus sur le Kit de développement logiciel (SDK) côté serveur, consultez les procédures du SDK Server.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-107">To learn more about the server-side SDK for the backend, see the Server SDK HOWTOs.</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="a7fa4-108">Documentation de référence</span><span class="sxs-lookup"><span data-stu-id="a7fa4-108">Reference documentation</span></span>
<span data-ttu-id="a7fa4-109">La documentation de référence du SDK du client iOS se trouve ici : [Référence du client iOS Azure Mobile Apps][2].</span><span class="sxs-lookup"><span data-stu-id="a7fa4-109">The reference documentation for the iOS client SDK is located here: [Azure Mobile Apps iOS Client Reference][2].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="a7fa4-110">Plateformes prises en charge</span><span class="sxs-lookup"><span data-stu-id="a7fa4-110">Supported Platforms</span></span>
<span data-ttu-id="a7fa4-111">Le Kit de développement logiciel (SDK) iOS prend en charge les projets Objective-C, Swift 2.2 et Swift 2.3 pour iOS 8.0 ou versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-111">The iOS SDK supports Objective-C projects, Swift 2.2 projects, and Swift 2.3 projects for iOS versions 8.0 or later.</span></span>

<span data-ttu-id="a7fa4-112">L’authentification « serveur flux » utilise un mode d’affichage WebView pour l’interface utilisateur présentée.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-112">The "server-flow" authentication uses a WebView for the presented UI.</span></span>  <span data-ttu-id="a7fa4-113">Si l’appareil n’est pas en mesure de présenter une interface utilisateur WebView, une autre méthode d’authentification est alors nécessaire, ce qui sort du cadre de ce produit.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-113">If the device is not able to present a WebView UI, then another method of authentication is required that is outside the scope of the product.</span></span>  
<span data-ttu-id="a7fa4-114">Ce SDK ne convient donc pas au type Watch ou d’autres appareils restreints similaires.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-114">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="a7fa4-115"><a name="Setup"></a>Configuration et conditions préalables</span><span class="sxs-lookup"><span data-stu-id="a7fa4-115"><a name="Setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="a7fa4-116">Ce guide part du principe que vous avez créé un serveur principal avec une table.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-116">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="a7fa4-117">Ce guide suppose que la table a le même schéma que les tables dans ces didacticiels.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-117">This guide assumes that the table has the same schema as the tables in those tutorials.</span></span> <span data-ttu-id="a7fa4-118">Ce guide suppose également que dans votre code, vous référencez `MicrosoftAzureMobile.framework` et importez `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-118">This guide also assumes that in your code, you reference `MicrosoftAzureMobile.framework` and import `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span></span>

## <span data-ttu-id="a7fa4-119"><a name="create-client"></a>Création du client</span><span class="sxs-lookup"><span data-stu-id="a7fa4-119"><a name="create-client"></a>How to: Create Client</span></span>
<span data-ttu-id="a7fa4-120">Pour accéder à un backend Azure Mobile Apps dans votre projet, créez un `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-120">To access an Azure Mobile Apps backend in your project, create an `MSClient`.</span></span> <span data-ttu-id="a7fa4-121">Remplacez `AppUrl` par l’URL de l’application.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-121">Replace `AppUrl` with the app URL.</span></span> <span data-ttu-id="a7fa4-122">Vous pouvez laisser `gatewayURLString` et `applicationKey` vides.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-122">You may leave `gatewayURLString` and `applicationKey` empty.</span></span> <span data-ttu-id="a7fa4-123">Si vous avez configuré une passerelle pour l’authentification, renseignez `gatewayURLString` avec l’URL de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-123">If you set up a gateway for authentication, populate `gatewayURLString` with the gateway URL.</span></span>

<span data-ttu-id="a7fa4-124">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-124">**Objective-C**:</span></span>

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

<span data-ttu-id="a7fa4-125">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-125">**Swift**:</span></span>

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <span data-ttu-id="a7fa4-126"><a name="table-reference"></a>Procédure : création d'une référence de table</span><span class="sxs-lookup"><span data-stu-id="a7fa4-126"><a name="table-reference"></a>How to: Create Table Reference</span></span>
<span data-ttu-id="a7fa4-127">Pour accéder aux données ou les mettre à jour, créez une référence à la table principale.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-127">To access or update data, create a reference to the backend table.</span></span> <span data-ttu-id="a7fa4-128">Remplacez `TodoItem` par le nom de votre table.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-128">Replace `TodoItem` with the name of your table</span></span>

<span data-ttu-id="a7fa4-129">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-129">**Objective-C**:</span></span>

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

<span data-ttu-id="a7fa4-130">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-130">**Swift**:</span></span>

```
let table = client.tableWithName("TodoItem")
```


## <span data-ttu-id="a7fa4-131"><a name="querying"></a>Procédure : interrogation des données</span><span class="sxs-lookup"><span data-stu-id="a7fa4-131"><a name="querying"></a>How to: Query Data</span></span>
<span data-ttu-id="a7fa4-132">Pour créer une requête de base de données, interrogez l'objet `MSTable` .</span><span class="sxs-lookup"><span data-stu-id="a7fa4-132">To create a database query, query the `MSTable` object.</span></span> <span data-ttu-id="a7fa4-133">La requête suivante obtient tous les éléments dans `TodoItem` et enregistre le texte de chaque élément.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-133">The following query gets all the items in `TodoItem` and logs the text of each item.</span></span>

<span data-ttu-id="a7fa4-134">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-134">**Objective-C**:</span></span>

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

<span data-ttu-id="a7fa4-135">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-135">**Swift**:</span></span>

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

## <span data-ttu-id="a7fa4-136"><a name="filtering"></a>Procédure : filtrage des données renvoyées</span><span class="sxs-lookup"><span data-stu-id="a7fa4-136"><a name="filtering"></a>How to: Filter Returned Data</span></span>
<span data-ttu-id="a7fa4-137">Pour filtrer les résultats, il existe de nombreuses options.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-137">To filter results, there are many available options.</span></span>

<span data-ttu-id="a7fa4-138">Pour filtrer à l'aide d'un prédicat, utilisez un `NSPredicate` et `readWithPredicate`.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-138">To filter using a predicate, use an `NSPredicate` and `readWithPredicate`.</span></span> <span data-ttu-id="a7fa4-139">Les filtres suivants retournent des données pour rechercher uniquement les éléments Todo incomplets.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-139">The following filters returned data to find only incomplete Todo items.</span></span>

<span data-ttu-id="a7fa4-140">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-140">**Objective-C**:</span></span>

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query the TodoItem table
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

<span data-ttu-id="a7fa4-141">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-141">**Swift**:</span></span>

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query the TodoItem table
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

## <span data-ttu-id="a7fa4-142"><a name="query-object"></a>Procédure : utilisation de MSQuery</span><span class="sxs-lookup"><span data-stu-id="a7fa4-142"><a name="query-object"></a>How to: Use MSQuery</span></span>
<span data-ttu-id="a7fa4-143">Pour effectuer une requête complexe (y compris le tri et la pagination), créez un objet `MSQuery` , directement ou en utilisant un prédicat :</span><span class="sxs-lookup"><span data-stu-id="a7fa4-143">To perform a complex query (including sorting and paging), create an `MSQuery` object, directly or by using a predicate:</span></span>

<span data-ttu-id="a7fa4-144">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-144">**Objective-C**:</span></span>

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

<span data-ttu-id="a7fa4-145">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-145">**Swift**:</span></span>

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

<span data-ttu-id="a7fa4-146">`MSQuery` vous permet de contrôler plusieurs comportements de requête.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-146">`MSQuery` lets you control several query behaviors.</span></span>

* <span data-ttu-id="a7fa4-147">Spécifier l’ordre des résultats</span><span class="sxs-lookup"><span data-stu-id="a7fa4-147">Specify order of results</span></span>
* <span data-ttu-id="a7fa4-148">Limiter les champs à renvoyer</span><span class="sxs-lookup"><span data-stu-id="a7fa4-148">Limit which fields to return</span></span>
* <span data-ttu-id="a7fa4-149">Limiter le nombre d’enregistrements à renvoyer</span><span class="sxs-lookup"><span data-stu-id="a7fa4-149">Limit how many records to return</span></span>
* <span data-ttu-id="a7fa4-150">Spécifier le nombre total dans la réponse</span><span class="sxs-lookup"><span data-stu-id="a7fa4-150">Specify total count in response</span></span>
* <span data-ttu-id="a7fa4-151">Spécifier des paramètres de chaîne de requête personnalisés dans la requête</span><span class="sxs-lookup"><span data-stu-id="a7fa4-151">Specify custom query string parameters in request</span></span>
* <span data-ttu-id="a7fa4-152">Appliquer des fonctions supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a7fa4-152">Apply additional functions</span></span>

<span data-ttu-id="a7fa4-153">Exécutez une requête `MSQuery` en appelant `readWithCompletion` sur l’objet.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-153">Execute an `MSQuery` query by calling `readWithCompletion` on the object.</span></span>

## <span data-ttu-id="a7fa4-154"><a name="sorting"></a>Procédure : trier des données avec MSQuery</span><span class="sxs-lookup"><span data-stu-id="a7fa4-154"><a name="sorting"></a>How to: Sort Data with MSQuery</span></span>
<span data-ttu-id="a7fa4-155">Pour trier les résultats, examinons un exemple.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-155">To sort results, let's look at an example.</span></span> <span data-ttu-id="a7fa4-156">Pour trier selon le champ ’text’ par ordre croissant, puis selon ’complete’ par ordre décroissant, vous devez appeler `MSQuery` , comme suit :</span><span class="sxs-lookup"><span data-stu-id="a7fa4-156">To sort by field 'text' ascending, then by 'complete' descending, invoke `MSQuery` like so:</span></span>

<span data-ttu-id="a7fa4-157">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-157">**Objective-C**:</span></span>

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

<span data-ttu-id="a7fa4-158">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-158">**Swift**:</span></span>

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


## <span data-ttu-id="a7fa4-159"><a name="selecting"></a><a name="parameters"></a>Procédure : limitation des champs et développement des paramètres de chaîne de requête avec MSQuery</span><span class="sxs-lookup"><span data-stu-id="a7fa4-159"><a name="selecting"></a><a name="parameters"></a>How to: Limit Fields and Expand Query String Parameters with MSQuery</span></span>
<span data-ttu-id="a7fa4-160">Pour limiter les champs à retourner dans une requête, spécifiez les noms des champs dans la propriété **selectFields** .</span><span class="sxs-lookup"><span data-stu-id="a7fa4-160">To limit fields to be returned in a query, specify the names of the fields in the **selectFields** property.</span></span> <span data-ttu-id="a7fa4-161">Cet exemple renvoie uniquement les champs text et completed :</span><span class="sxs-lookup"><span data-stu-id="a7fa4-161">This example returns only the text and completed fields:</span></span>

<span data-ttu-id="a7fa4-162">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-162">**Objective-C**:</span></span>

```
query.selectFields = @[@"text", @"complete"];
```

<span data-ttu-id="a7fa4-163">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-163">**Swift**:</span></span>

```
query.selectFields = ["text", "complete"]
```

<span data-ttu-id="a7fa4-164">Pour inclure des paramètres de chaîne de requête supplémentaires dans la demande serveur (par exemple, si un script côté serveur personnalisé les utilise), remplissez `query.parameters` comme suit :</span><span class="sxs-lookup"><span data-stu-id="a7fa4-164">To include additional query string parameters in the server request (for example, because a custom server-side script uses them), populate `query.parameters` like so:</span></span>

<span data-ttu-id="a7fa4-165">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-165">**Objective-C**:</span></span>

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

<span data-ttu-id="a7fa4-166">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-166">**Swift**:</span></span>

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <span data-ttu-id="a7fa4-167"><a name="paging"></a>Procédure : configuration du format de page</span><span class="sxs-lookup"><span data-stu-id="a7fa4-167"><a name="paging"></a>How to: Configure Page Size</span></span>
<span data-ttu-id="a7fa4-168">Avec Azure Mobile Apps, le format de page contrôle le nombre d’enregistrements extraits à la fois des tables du backend.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-168">With Azure Mobile Apps, the page size controls the number of records that are pulled at a time from the backend tables.</span></span> <span data-ttu-id="a7fa4-169">Un appel des données `pull` entraînerait la création de lots de données en fonction du format de page, jusqu'à ce qu’il n’y a plus aucun enregistrement à extraire.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-169">A call to `pull` data would then batch up data, based on this page size, until there are no more records to pull.</span></span>

<span data-ttu-id="a7fa4-170">Il est possible de configurer un format de page à l’aide de **MSPullSettings** comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-170">It's possible to configure a page size using **MSPullSettings** as shown below.</span></span> <span data-ttu-id="a7fa4-171">Le format de page par défaut est 50, et il est paramétré dans l’exemple ci-dessous sur 3.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-171">The default page size is 50, and the example below changes it to 3.</span></span>

<span data-ttu-id="a7fa4-172">Vous pouvez configurer un autre format de page pour des raisons de performances.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-172">You could configure a different page size for performance reasons.</span></span> <span data-ttu-id="a7fa4-173">Si vous avez un grand nombre d’enregistrements de données de petite taille, une taille de page élevée permet de réduire le nombre d’allers-retours avec le serveur.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-173">If you have a large number of small data records, a high page size reduces the number of server round-trips.</span></span>

<span data-ttu-id="a7fa4-174">Ce paramètre contrôle uniquement le format de page côté client.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-174">This setting controls only the page size on the client side.</span></span> <span data-ttu-id="a7fa4-175">Si le client demande un format de page plus grand que le backend Mobile Apps prend en charge, le format de page est limitée à la valeur maximale que configurée prise en charge par le serveur.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-175">If the client asks for a larger page size than the Mobile Apps backend supports, the page size is capped at the maximum the backend is configured to support.</span></span>

<span data-ttu-id="a7fa4-176">Ce paramètre correspond également au *nombre* d’enregistrements de données, non à la *taille en octets*.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-176">This setting is also the *number* of data records, not the *byte size*.</span></span>

<span data-ttu-id="a7fa4-177">Si vous augmentez le format de page côté client, vous devez également augmenter le format de page sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-177">If you increase the client page size, you should also increase the page size on the server.</span></span> <span data-ttu-id="a7fa4-178">Consultez [« Ajuster la taille de pagination des tables »](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) pour connaître les étapes à suivre.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-178">See ["How to: Adjust the table paging size"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for the steps to do this.</span></span>

<span data-ttu-id="a7fa4-179">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-179">**Objective-C**:</span></span>

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


<span data-ttu-id="a7fa4-180">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-180">**Swift**:</span></span>

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <span data-ttu-id="a7fa4-181"><a name="inserting"></a>Procédure : insertion de données</span><span class="sxs-lookup"><span data-stu-id="a7fa4-181"><a name="inserting"></a>How to: Insert Data</span></span>
<span data-ttu-id="a7fa4-182">Pour insérer une nouvelle ligne de table, créez un `NSDictionary` et appelez `table insert`.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-182">To insert a new table row, create a `NSDictionary` and invoke `table insert`.</span></span> <span data-ttu-id="a7fa4-183">Si le [schéma dynamique] est activé, le backend mobile Azure App Service génère automatiquement de nouvelles colonnes basées sur le `NSDictionary`.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-183">If [Dynamic Schema] is enabled, the Azure App Service mobile backend automatically generates new columns based on the `NSDictionary`.</span></span>

<span data-ttu-id="a7fa4-184">Si `id` n'est pas fourni, le backend génère automatiquement un nouvel ID unique.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-184">If `id` is not provided, the backend automatically generates a new unique ID.</span></span> <span data-ttu-id="a7fa4-185">Fournissez votre propre `id` pour utiliser les adresses de messagerie électronique, les noms d'utilisateurs, ou vos propres valeurs personnalisées sous la forme d'ID.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-185">Provide your own `id` to use email addresses, usernames, or your own custom values as ID.</span></span> <span data-ttu-id="a7fa4-186">Fournir son propre ID peut faciliter les jointures et la logique de base de données orientée métier.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-186">Providing your own ID may ease joins and business-oriented database logic.</span></span>

<span data-ttu-id="a7fa4-187">L’élément `result` contient le nouvel élément qui a été inséré.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-187">The `result` contains the new item that was inserted.</span></span> <span data-ttu-id="a7fa4-188">Selon la logique du serveur, il peut afficher des données supplémentaires ou modifiées par rapport à ce qui a été transmis au serveur.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-188">Depending on your server logic, it may have additional or modified data compared to what was passed to the server.</span></span>

<span data-ttu-id="a7fa4-189">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-189">**Objective-C**:</span></span>

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

<span data-ttu-id="a7fa4-190">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-190">**Swift**:</span></span>

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

## <span data-ttu-id="a7fa4-191"><a name="modifying"></a>Procédure : modification des données</span><span class="sxs-lookup"><span data-stu-id="a7fa4-191"><a name="modifying"></a>How to: Modify Data</span></span>
<span data-ttu-id="a7fa4-192">Pour mettre à jour une ligne existante, modifiez un élément et appelez `update`:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-192">To update an existing row, modify an item and call `update`:</span></span>

<span data-ttu-id="a7fa4-193">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-193">**Objective-C**:</span></span>

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

<span data-ttu-id="a7fa4-194">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-194">**Swift**:</span></span>

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

<span data-ttu-id="a7fa4-195">Vous pouvez également fournir l'ID de la ligne et le champ mis à jour :</span><span class="sxs-lookup"><span data-stu-id="a7fa4-195">Alternatively, supply the row ID and the updated field:</span></span>

<span data-ttu-id="a7fa4-196">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-196">**Objective-C**:</span></span>

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="a7fa4-197">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-197">**Swift**:</span></span>

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

<span data-ttu-id="a7fa4-198">Au minimum, l'attribut `id` doit être défini quand vous effectuez des mises à jour.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-198">At minimum, the `id` attribute must be set when making updates.</span></span>

## <span data-ttu-id="a7fa4-199"><a name="deleting"></a>Procédure : suppression de données</span><span class="sxs-lookup"><span data-stu-id="a7fa4-199"><a name="deleting"></a>How to: Delete Data</span></span>
<span data-ttu-id="a7fa4-200">Pour supprimer un élément, appelez `delete` avec l'élément :</span><span class="sxs-lookup"><span data-stu-id="a7fa4-200">To delete an item, invoke `delete` with the item:</span></span>

<span data-ttu-id="a7fa4-201">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-201">**Objective-C**:</span></span>

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="a7fa4-202">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-202">**Swift**:</span></span>

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="a7fa4-203">Vous pouvez également effectuer la suppression en fournissant un ID de ligne :</span><span class="sxs-lookup"><span data-stu-id="a7fa4-203">Alternatively, delete by providing a row ID:</span></span>

<span data-ttu-id="a7fa4-204">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-204">**Objective-C**:</span></span>

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="a7fa4-205">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-205">**Swift**:</span></span>

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="a7fa4-206">Au minimum, l'attribut `id` doit être défini quand vous effectuez des suppressions.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-206">At minimum, the `id` attribute must be set when making deletes.</span></span>

## <span data-ttu-id="a7fa4-207"><a name="customapi"></a>Procédure : appel d’une API personnalisée</span><span class="sxs-lookup"><span data-stu-id="a7fa4-207"><a name="customapi"></a>How to: Call Custom API</span></span>
<span data-ttu-id="a7fa4-208">Une API personnalisée vous permet d’exposer toutes les fonctionnalités du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-208">With a custom API, you can expose any backend functionality.</span></span> <span data-ttu-id="a7fa4-209">Il n’est pas nécessaire de la mapper à une opération de table.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-209">It doesn't have to map to a table operation.</span></span> <span data-ttu-id="a7fa4-210">Non seulement vous avez davantage de contrôle sur la messagerie, mais vous pouvez également lire/définir des en-têtes et modifier le format du corps de réponse.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-210">Not only do you gain more control over messaging, you can even read/set headers and change the response body format.</span></span> <span data-ttu-id="a7fa4-211">Pour savoir comment créer une API personnalisée sur le serveur principal, consultez la rubrique [API personnalisées](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span><span class="sxs-lookup"><span data-stu-id="a7fa4-211">To learn how to create a custom API on the backend, read [Custom APIs](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span></span>

<span data-ttu-id="a7fa4-212">Pour appeler une API personnalisée, appelez `MSClient.invokeAPI`.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-212">To call a custom API, call `MSClient.invokeAPI`.</span></span> <span data-ttu-id="a7fa4-213">Le contenu de la requête et de la réponse est traité au format JSON.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-213">The request and response content are treated as JSON.</span></span> <span data-ttu-id="a7fa4-214">Pour utiliser d’autres types de média, [utilisez l’autre surcharge de `invokeAPI`][5].</span><span class="sxs-lookup"><span data-stu-id="a7fa4-214">To use other media types, [use the other overload of `invokeAPI`][5].</span></span>  <span data-ttu-id="a7fa4-215">Pour exécuter une requête `GET` à la place d’une requête `POST`, définissez le paramètre `HTTPMethod` sur `"GET"` et le paramètre `body` sur `nil` (étant donné que les requêtes GET ne comportent pas de corps de message). Si votre API personnalisée prend en charge les autres verbes HTTP, modifiez `HTTPMethod` en conséquence.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-215">To make a `GET` request instead of a `POST` request, set parameter `HTTPMethod` to `"GET"` and parameter `body` to `nil` (since GET requests do not have message bodies.) If your custom API supports other HTTP verbs, change `HTTPMethod` appropriately.</span></span>

<span data-ttu-id="a7fa4-216">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-216">**Objective-C**:</span></span>

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

<span data-ttu-id="a7fa4-217">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-217">**Swift**:</span></span>

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

## <span data-ttu-id="a7fa4-218"><a name="templates"></a>Inscription de modèles de notifications Push pour envoyer des notifications multiplateforme</span><span class="sxs-lookup"><span data-stu-id="a7fa4-218"><a name="templates"></a>How to: Register push templates to send cross-platform notifications</span></span>
<span data-ttu-id="a7fa4-219">Pour inscrire des modèles, transmettez-les avec votre méthode **client.push registerDeviceToken** dans votre application cliente.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-219">To register templates, pass templates with your **client.push registerDeviceToken** method in your client app.</span></span>

<span data-ttu-id="a7fa4-220">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-220">**Objective-C**:</span></span>

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

<span data-ttu-id="a7fa4-221">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-221">**Swift**:</span></span>

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

<span data-ttu-id="a7fa4-222">Vos modèles sont de type NSDictionary et peuvent contenir plusieurs modèles au format suivant :</span><span class="sxs-lookup"><span data-stu-id="a7fa4-222">Your templates are of type NSDictionary and can contain multiple templates in the following format:</span></span>

<span data-ttu-id="a7fa4-223">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-223">**Objective-C**:</span></span>

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

<span data-ttu-id="a7fa4-224">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-224">**Swift**:</span></span>

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

<span data-ttu-id="a7fa4-225">Toutes les balises sont supprimées de la demande pour des raisons de sécurité.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-225">All tags are stripped from the request for security.</span></span>  <span data-ttu-id="a7fa4-226">Pour ajouter des balises à des installations ou à des modèles contenus dans une installation, consultez [Utiliser le Kit de développement logiciel (SDK) du serveur principal .NET pour Azure Mobile Apps][4].</span><span class="sxs-lookup"><span data-stu-id="a7fa4-226">To add tags to installations or templates within installations, see [Work with the .NET backend server SDK for Azure Mobile Apps][4].</span></span>  <span data-ttu-id="a7fa4-227">Pour envoyer des notifications à l’aide de ces modèles inscrits, utilisez les [API Notification Hubs][3].</span><span class="sxs-lookup"><span data-stu-id="a7fa4-227">To send notifications using these registered templates, work with [Notification Hubs APIs][3].</span></span>

## <span data-ttu-id="a7fa4-228"><a name="errors"></a>Procédure : gestion des erreurs</span><span class="sxs-lookup"><span data-stu-id="a7fa4-228"><a name="errors"></a>How to: Handle Errors</span></span>
<span data-ttu-id="a7fa4-229">Quand vous appelez un backend mobile Azure App Service, le bloc completion contient un paramètre `NSError` .</span><span class="sxs-lookup"><span data-stu-id="a7fa4-229">When you call an Azure App Service mobile backend, the completion block contains an `NSError` parameter.</span></span> <span data-ttu-id="a7fa4-230">Si une erreur se produit, ce paramètre est non-nil.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-230">When an error occurs, this parameter is non-nil.</span></span> <span data-ttu-id="a7fa4-231">Vous devez vérifier ce paramètre dans votre code et gérer les erreurs, le cas échéant, comme indiqué dans les extraits de code précédents.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-231">In your code, you should check this parameter and handle the error as needed, as demonstrated in the preceding code snippets.</span></span>

<span data-ttu-id="a7fa4-232">Le fichier [`<WindowsAzureMobileServices/MSError.h>`][6] définit les constantes `MSErrorResponseKey`, `MSErrorRequestKey` et `MSErrorServerItemKey`.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-232">The file [`<WindowsAzureMobileServices/MSError.h>`][6] defines the constants `MSErrorResponseKey`, `MSErrorRequestKey`, and `MSErrorServerItemKey`.</span></span> <span data-ttu-id="a7fa4-233">Pour obtenir plus d’informations sur l’erreur :</span><span class="sxs-lookup"><span data-stu-id="a7fa4-233">To get more data related to the error:</span></span>

<span data-ttu-id="a7fa4-234">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-234">**Objective-C**:</span></span>

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

<span data-ttu-id="a7fa4-235">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-235">**Swift**:</span></span>

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

<span data-ttu-id="a7fa4-236">En outre, le fichier définit des constantes pour chaque code d'erreur :</span><span class="sxs-lookup"><span data-stu-id="a7fa4-236">In addition, the file defines constants for each error code:</span></span>

<span data-ttu-id="a7fa4-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-237">**Objective-C**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

<span data-ttu-id="a7fa4-238">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-238">**Swift**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

## <span data-ttu-id="a7fa4-239"><a name="adal"></a>Procédure : authentifier des utilisateurs avec la bibliothèque Active Directory Authentication Library</span><span class="sxs-lookup"><span data-stu-id="a7fa4-239"><a name="adal"></a>How to: Authenticate users with the Active Directory Authentication Library</span></span>
<span data-ttu-id="a7fa4-240">Vous pouvez utiliser la bibliothèque d’authentification Active Directory (ADAL) pour authentifier des utilisateurs dans votre application à l’aide d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-240">You can use the Active Directory Authentication Library (ADAL) to sign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="a7fa4-241">L’authentification par flux client à l’aide d’un SDK de fournisseur d’identité est préférable à l’utilisation de la méthode `loginWithProvider:completion:` .</span><span class="sxs-lookup"><span data-stu-id="a7fa4-241">Client flow authentication using an identity provider SDK is preferable to using the `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="a7fa4-242">L’authentification par client flux offre une interface UX native plus simple et permet une personnalisation supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-242">Client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="a7fa4-243">Si vous souhaitez configurer le serveur d’applications mobiles back-end pour utiliser la connexion AAD, suivez le didacticiel [Configurer votre application App Service pour utiliser la connexion Azure Active Directory][7].</span><span class="sxs-lookup"><span data-stu-id="a7fa4-243">Configure your mobile app backend for AAD sign-in by following the [How to configure App Service for Active Directory login][7] tutorial.</span></span> <span data-ttu-id="a7fa4-244">Bien que cette étape soit facultative, veillez à inscrire une application cliente native.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-244">Make sure to complete the optional step of registering a native client application.</span></span> <span data-ttu-id="a7fa4-245">Pour iOS, il est recommandé d’utiliser une URI de redirection de type `<app-scheme>://<bundle-id>`.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-245">For iOS, we recommend that the redirect URI is of the form `<app-scheme>://<bundle-id>`.</span></span> <span data-ttu-id="a7fa4-246">Pour plus d’informations, consultez le [didacticiel de démarrage rapide d’ADAL pour iOS][8].</span><span class="sxs-lookup"><span data-stu-id="a7fa4-246">For more information, see the [ADAL iOS quickstart][8].</span></span>
2. <span data-ttu-id="a7fa4-247">Installez la bibliothèque ADAL à l’aide de Cocoapods.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-247">Install ADAL using Cocoapods.</span></span> <span data-ttu-id="a7fa4-248">Modifiez votre podfile pour inclure la définition suivante, en remplaçant **YOUR-PROJECT** par le nom de votre projet Xcode :</span><span class="sxs-lookup"><span data-stu-id="a7fa4-248">Edit your Podfile to include the following definition, replacing **YOUR-PROJECT** with the name of your Xcode project:</span></span>

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   <span data-ttu-id="a7fa4-249">et le pod :</span><span class="sxs-lookup"><span data-stu-id="a7fa4-249">and the Pod:</span></span>

        pod 'ADALiOS'
3. <span data-ttu-id="a7fa4-250">À l’aide du Terminal, exécutez `pod install` à partir du répertoire contenant votre projet, puis ouvrez l’espace de travail Xcode généré (et non le projet).</span><span class="sxs-lookup"><span data-stu-id="a7fa4-250">Using the Terminal, run `pod install` from the directory containing your project, and then open the generated Xcode workspace (not the project).</span></span>
4. <span data-ttu-id="a7fa4-251">Ajoutez le code suivant à votre application, en fonction du langage utilisé.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-251">Add the following code to your application, according to the language you are using.</span></span> <span data-ttu-id="a7fa4-252">Vérifiez à chaque fois ces remplacements :</span><span class="sxs-lookup"><span data-stu-id="a7fa4-252">In each, make these replacements:</span></span>

   * <span data-ttu-id="a7fa4-253">Remplacez **INSERT-AUTHORITY-HERE** par le nom du client dans lequel vous avez approvisionné votre application.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-253">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="a7fa4-254">Le format doit être https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-254">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span> <span data-ttu-id="a7fa4-255">Cette valeur peut être copiée depuis l’onglet Domaine de votre Azure Active Directory dans le [portail Azure Classic].</span><span class="sxs-lookup"><span data-stu-id="a7fa4-255">This value can be copied from the Domain tab in your Azure Active Directory in the [Azure classic portal].</span></span>
   * <span data-ttu-id="a7fa4-256">Remplacez **INSERT-RESOURCE-ID-HERE** par l’ID client du serveur principal de votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-256">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="a7fa4-257">Vous pouvez obtenir l’ID client sur le portail, sous l’onglet **Avancé** du menu **Paramètres Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-257">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
   * <span data-ttu-id="a7fa4-258">Remplacez **INSERT-CLIENT-ID-HERE** par l’ID client que vous avez copié depuis l’application cliente native.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-258">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
   * <span data-ttu-id="a7fa4-259">Remplacez **INSERT-REDIRECT-URI-HERE** par le point de terminaison */.auth/login/done* de votre site, en utilisant le modèle HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-259">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="a7fa4-260">Cette valeur doit être semblable à *https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-260">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

<span data-ttu-id="a7fa4-261">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-261">**Objective-C**:</span></span>

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


<span data-ttu-id="a7fa4-262">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-262">**Swift**:</span></span>

    // add the following imports to your bridging header:
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

## <span data-ttu-id="a7fa4-263"><a name="facebook-sdk"></a>Procédure : authentifier les utilisateurs avec le kit de développement logiciel (SDK) Facebook pour iOS</span><span class="sxs-lookup"><span data-stu-id="a7fa4-263"><a name="facebook-sdk"></a>How to: Authenticate users with the Facebook SDK for iOS</span></span>
<span data-ttu-id="a7fa4-264">Vous pouvez utiliser le kit de développement logiciel (SDK) Facebook pour iOS pour identifier les utilisateurs sur votre application utilisant Facebook.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-264">You can use the Facebook SDK for iOS to sign users into your application using Facebook.</span></span>  <span data-ttu-id="a7fa4-265">L’authentification par flux client est préférable à l’utilisation de la méthode `loginWithProvider:completion:` .</span><span class="sxs-lookup"><span data-stu-id="a7fa4-265">Using a client flow authentication is preferable to using the `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="a7fa4-266">L’authentification par client flux offre une interface UX native plus simple et permet une personnalisation supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-266">The client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="a7fa4-267">Si vous souhaitez configurer le serveur d’applications mobiles back-end pour utiliser la connexion Facebook, suivez le didacticiel [Configurer votre application App Service pour utiliser la connexion Facebook][9].</span><span class="sxs-lookup"><span data-stu-id="a7fa4-267">Configure your mobile app backend for Facebook sign-in by following the [How to configure App Service for Facebook login][9] tutorial.</span></span>
2. <span data-ttu-id="a7fa4-268">Installez le SDK Facebook pour iOS en suivant la documentation [Kit de développement logiciel (SDK) Facebook pour iOS : prise en main][10].</span><span class="sxs-lookup"><span data-stu-id="a7fa4-268">Install the Facebook SDK for iOS by following the [Facebook SDK for iOS - Getting Started][10] documentation.</span></span> <span data-ttu-id="a7fa4-269">Au lieu de créer une application, vous pouvez ajouter la plateforme iOS à votre inscription existante.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-269">Instead of creating an app, you can add the iOS platform to your existing registration.</span></span>
3. <span data-ttu-id="a7fa4-270">La documentation de Facebook comprend du code en Objective-C dans le délégué de l’application.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-270">Facebook's documentation includes some Objective-C code in the App Delegate.</span></span> <span data-ttu-id="a7fa4-271">Si vous utilisez **Swift**, vous pouvez vous servir des conversions suivantes pour AppDelegate.swift :</span><span class="sxs-lookup"><span data-stu-id="a7fa4-271">If you are using **Swift**, you can use the following translations for AppDelegate.swift:</span></span>

        // Add the following import to your bridging header:
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
4. <span data-ttu-id="a7fa4-272">En plus d’ajouter `FBSDKCoreKit.framework` à votre projet, ajoutez également une référence à `FBSDKLoginKit.framework` de la même façon.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-272">In addition to adding `FBSDKCoreKit.framework` to your project, also add a reference to `FBSDKLoginKit.framework` in the same way.</span></span>
5. <span data-ttu-id="a7fa4-273">Ajoutez le code suivant à votre application, en fonction du langage utilisé.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-273">Add the following code to your application, according to the language you are using.</span></span>

<span data-ttu-id="a7fa4-274">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-274">**Objective-C**:</span></span>

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

<span data-ttu-id="a7fa4-275">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-275">**Swift**:</span></span>

    // Add the following imports to your bridging header:
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

## <span data-ttu-id="a7fa4-276"><a name="twitter-fabric"></a>Procédure : authentifier les utilisateurs avec Twitter Fabric pour iOS</span><span class="sxs-lookup"><span data-stu-id="a7fa4-276"><a name="twitter-fabric"></a>How to: Authenticate users with Twitter Fabric for iOS</span></span>
<span data-ttu-id="a7fa4-277">Vous pouvez utiliser Twitter Fabric pour iOS pour identifier les utilisateurs sur votre application utilisant Twitter.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-277">You can use Fabric for iOS to sign users into your application using Twitter.</span></span> <span data-ttu-id="a7fa4-278">L’authentification par flux client est souvent préférable à l’utilisation de la méthode `loginWithProvider:completion:` , car elle offre une interface UX native plus simple et permet une personnalisation supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-278">Client Flow authentication is preferable to using the `loginWithProvider:completion:` method, as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="a7fa4-279">Si vous souhaitez configurer le backend de votre application mobile pour utiliser la connexion Twitter, suivez le didacticiel [Configurer votre application App Service pour utiliser la connexion Twitter](app-service-mobile-how-to-configure-twitter-authentication.md) .</span><span class="sxs-lookup"><span data-stu-id="a7fa4-279">Configure your mobile app backend for Twitter sign-in by following the [How to configure App Service for Twitter login](app-service-mobile-how-to-configure-twitter-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="a7fa4-280">Ajoutez Fabric à votre projet en suivant la documentation [Fabric pour iOS : prise en main] (en anglais) et en configurant TwitterKit.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-280">Add Fabric to your project by following the [Fabric for iOS - Getting Started] documentation and setting up TwitterKit.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a7fa4-281">Par défaut, Fabric crée une application Twitter pour vous.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-281">By default, Fabric creates a Twitter application for you.</span></span> <span data-ttu-id="a7fa4-282">Vous pouvez éviter de créer une application en enregistrant la clé et la clé secrète du client que vous avez créées plus tôt avec les extraits de code suivants.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-282">You can avoid creating an application by registering the Consumer Key and Consumer Secret you created earlier using the following code snippets.</span></span>    <span data-ttu-id="a7fa4-283">Vous pouvez également remplacer les valeurs de clé et de clé secrète du client que vous fournissez à App Service avec les valeurs que vous voyez dans le [Tableau de bord de Fabric].</span><span class="sxs-lookup"><span data-stu-id="a7fa4-283">Alternatively, you can replace the Consumer Key and Consumer Secret values that you provide to App Service with the values you see in the [Fabric Dashboard].</span></span> <span data-ttu-id="a7fa4-284">Si vous choisissez cette option, veillez à définir l’URL de rappel sur une valeur d’espace réservé, par exemple `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-284">If you choose this option, be sure to set the callback URL to a placeholder value, such as `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span></span>
   >
   >

    <span data-ttu-id="a7fa4-285">Si vous choisissez d’utiliser les clés secrètes que vous avez créées précédemment, ajoutez le code suivant à votre délégué d’application :</span><span class="sxs-lookup"><span data-stu-id="a7fa4-285">If you choose to use the secrets you created earlier, add the following code to your App Delegate:</span></span>

    <span data-ttu-id="a7fa4-286">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-286">**Objective-C**:</span></span>

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

    <span data-ttu-id="a7fa4-287">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-287">**Swift**:</span></span>

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. <span data-ttu-id="a7fa4-288">Ajoutez le code suivant à votre application, en fonction du langage utilisé.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-288">Add the following code to your application, according to the language you are using.</span></span>

<span data-ttu-id="a7fa4-289">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-289">**Objective-C**:</span></span>

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

<span data-ttu-id="a7fa4-290">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-290">**Swift**:</span></span>

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

## <span data-ttu-id="a7fa4-291"><a name="google-sdk"></a>Procédure : authentifier les utilisateurs avec le kit de développement logiciel (SDK) Google Sign-In pour iOS</span><span class="sxs-lookup"><span data-stu-id="a7fa4-291"><a name="google-sdk"></a>How to: Authenticate users with the Google Sign-In SDK for iOS</span></span>
<span data-ttu-id="a7fa4-292">Vous pouvez utiliser le kit de développement logiciel (SDK) Google Sign-In pour iOS pour identifier les utilisateurs sur votre application utilisant un compte Google.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-292">You can use the Google Sign-In SDK for iOS to sign users into your application using a Google account.</span></span>  <span data-ttu-id="a7fa4-293">Google a récemment annoncé que des modifications avaient été apportées à ses stratégies de sécurité OAuth.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-293">Google recently announced changes to their OAuth security policies.</span></span>  <span data-ttu-id="a7fa4-294">Ces modifications de stratégie nécessiteront l’utilisation du SDK Google à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-294">These policy changes will require the use of the Google SDK in the future.</span></span>

1. <span data-ttu-id="a7fa4-295">Si vous souhaitez configurer le backend de votre application mobile pour utiliser la connexion Google, suivez le didacticiel [Configurer votre application App Service pour utiliser la connexion Google](app-service-mobile-how-to-configure-google-authentication.md) .</span><span class="sxs-lookup"><span data-stu-id="a7fa4-295">Configure your mobile app backend for Google sign-in by following the [How to configure App Service for Google login](app-service-mobile-how-to-configure-google-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="a7fa4-296">Installez le SDK Google pour iOS en suivant les instructions figurant dans la documentation [Google Sign-In for iOS - Start integrating](https://developers.google.com/identity/sign-in/ios/start-integrating) (Google Sign-In pour iOS - Démarrer l’intégration).</span><span class="sxs-lookup"><span data-stu-id="a7fa4-296">Install the Google SDK for iOS by following the [Google Sign-In for iOS - Start integrating](https://developers.google.com/identity/sign-in/ios/start-integrating) documentation.</span></span> <span data-ttu-id="a7fa4-297">Vous pouvez ignorer la section « Authentification avec un serveur principal ».</span><span class="sxs-lookup"><span data-stu-id="a7fa4-297">You may skip the "Authenticate with a Backend Server" section.</span></span>
3. <span data-ttu-id="a7fa4-298">Ajoutez ce qui suit à la méthode `signIn:didSignInForUser:withError:` de votre délégué, en fonction du langage que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-298">Add the following to your delegate's `signIn:didSignInForUser:withError:` method, according to the language you are using.</span></span>

<span data-ttu-id="a7fa4-299">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-299">**Objective-C**:</span></span>

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

<span data-ttu-id="a7fa4-300">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-300">**Swift**:</span></span>

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. <span data-ttu-id="a7fa4-301">Assurez-vous que vous ajoutez également le code suivant à `application:didFinishLaunchingWithOptions:` dans votre délégué d’application, en remplaçant « SERVER_CLIENT_ID » par le même ID utilisé pour configurer App Service à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-301">Make sure you also add the following to `application:didFinishLaunchingWithOptions:` in your app delegate, replacing "SERVER_CLIENT_ID" with the same ID that you used to configure App Service in step 1.</span></span>

<span data-ttu-id="a7fa4-302">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-302">**Objective-C**:</span></span>

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 <span data-ttu-id="a7fa4-303">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-303">**Swift**:</span></span>

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. <span data-ttu-id="a7fa4-304">Ajoutez le code suivant à votre application dans un UIViewController qui implémente le protocole `GIDSignInUIDelegate` , en fonction du langage que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-304">Add the following code to your application in a UIViewController that implements the `GIDSignInUIDelegate` protocol, according to the language you are using.</span></span>  <span data-ttu-id="a7fa4-305">Vous êtes déconnecté avant d’être connecté à nouveau, et même si vous n’avez pas à entrer ses informations d’identification, une boîte de dialogue de consentement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-305">You are signed out before being signed in again, and although you don't need to enter your credentials again, you see a consent dialog.</span></span>  <span data-ttu-id="a7fa4-306">Appelez uniquement cette méthode lorsque le jeton de session a expiré.</span><span class="sxs-lookup"><span data-stu-id="a7fa4-306">Only call this method when the session token has expired.</span></span>

   <span data-ttu-id="a7fa4-307">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-307">**Objective-C**:</span></span>

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   <span data-ttu-id="a7fa4-308">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a7fa4-308">**Swift**:</span></span>

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
[How to: Create the Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data to the user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize the client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
<span data-ttu-id="a7fa4-309">[Démarrage rapide d’Azure Mobile Apps]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="a7fa4-309">[Azure Mobile Apps Quick Start]: app-service-mobile-ios-get-started.md</span></span>

[Add Mobile Services to Existing App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts to authorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
<span data-ttu-id="a7fa4-310">[schéma dynamique]: http://go.microsoft.com/fwlink/p/?LinkId=296271</span><span class="sxs-lookup"><span data-stu-id="a7fa4-310">[Dynamic Schema]: http://go.microsoft.com/fwlink/p/?LinkId=296271</span></span>
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI to manage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

<span data-ttu-id="a7fa4-311">[Tableau de bord de Fabric]: https://www.fabric.io/home</span><span class="sxs-lookup"><span data-stu-id="a7fa4-311">[Fabric Dashboard]: https://www.fabric.io/home</span></span>
<span data-ttu-id="a7fa4-312">[Fabric pour iOS : prise en main]: https://docs.fabric.io/ios/fabric/getting-started.html</span><span class="sxs-lookup"><span data-stu-id="a7fa4-312">[Fabric for iOS - Getting Started]: https://docs.fabric.io/ios/fabric/getting-started.html</span></span>
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
