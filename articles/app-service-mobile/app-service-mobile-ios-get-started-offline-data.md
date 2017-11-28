---
title: aaaEnable la synchronisation hors connexion des applications mobiles iOS | Documents Microsoft
description: "Découvrez comment toouse Azure App Service des applications mobiles toocache et la synchronisation de données hors connexion dans les applications iOS."
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: eb5b9520-0f39-4a09-940a-dadb6d940db8
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 570ea7cf6694ab7317c977331038929b64508ad3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a><span data-ttu-id="a3ccf-103">Activer la synchronisation hors connexion avec des applications mobiles iOS</span><span class="sxs-lookup"><span data-stu-id="a3ccf-103">Enable offline syncing with iOS mobile apps</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="a3ccf-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="a3ccf-104">Overview</span></span>
<span data-ttu-id="a3ccf-105">Ce didacticiel couvre la synchronisation hors connexion avec fonctionnalité d’applications mobiles hello du Service d’application Azure pour iOS.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-105">This tutorial covers offline syncing with hello Mobile Apps feature of Azure App Service for iOS.</span></span> <span data-ttu-id="a3ccf-106">Avec les utilisateurs finaux de synchronisation hors connexion peuvent interagir avec un tooview de l’application mobile, ajouter ou modifier des données, même si elles n’ont aucune connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-106">With offline syncing end-users can interact with a mobile app tooview, add, or modify data, even when they have no network connection.</span></span> <span data-ttu-id="a3ccf-107">Les modifications sont stockées dans une base de données locale.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-107">Changes are stored in a local database.</span></span> <span data-ttu-id="a3ccf-108">Une fois l’appareil de hello en ligne, les modifications de hello sont synchronisées avec les principaux à distance hello.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-108">After hello device is back online, hello changes are synced with hello remote back end.</span></span>

<span data-ttu-id="a3ccf-109">S’il s’agit de votre première expérience avec les applications mobiles, vous devez d’abord terminer didacticiel de hello [créer une application iOS].</span><span class="sxs-lookup"><span data-stu-id="a3ccf-109">If this is your first experience with Mobile Apps, you should first complete hello tutorial [Create an iOS App].</span></span> <span data-ttu-id="a3ccf-110">Si vous n’utilisez pas de projet de démarrage rapide serveur hello téléchargé, vous devez ajouter le projet tooyour de packages d’extension d’accès aux données de hello.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-110">If you do not use hello downloaded quick-start server project, you must add hello data-access extension packages tooyour project.</span></span> <span data-ttu-id="a3ccf-111">Pour plus d’informations sur les packages d’extension de serveur, consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="a3ccf-111">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="a3ccf-112">toolearn en savoir plus sur la fonctionnalité de synchronisation hors connexion hello, consultez [synchronisation des données hors connexion dans les applications mobiles].</span><span class="sxs-lookup"><span data-stu-id="a3ccf-112">toolearn more about hello offline sync feature, see [Offline Data Sync in Mobile Apps].</span></span>

## <span data-ttu-id="a3ccf-113"><a name="review-sync"></a>Passez en revue le code de synchronisation hello client</span><span class="sxs-lookup"><span data-stu-id="a3ccf-113"><a name="review-sync"></a>Review hello client sync code</span></span>
<span data-ttu-id="a3ccf-114">projet de client Hello que vous avez téléchargé pour hello [créer une application iOS] didacticiel contient déjà du code qui prend en charge la synchronisation hors connexion à l’aide d’une base de données locale en fonction des données de base.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-114">hello client project that you downloaded for hello [Create an iOS App] tutorial already contains code that supports offline synchronization using a local Core Data-based database.</span></span> <span data-ttu-id="a3ccf-115">Cette section résume ce qui est déjà inclus dans le code de didacticiel hello.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-115">This section summarizes what is already included in hello tutorial code.</span></span> <span data-ttu-id="a3ccf-116">Pour une vue d’ensemble conceptuelle de la fonctionnalité de hello, consultez [synchronisation des données hors connexion dans les applications mobiles].</span><span class="sxs-lookup"><span data-stu-id="a3ccf-116">For a conceptual overview of hello feature, see [Offline Data Sync in Mobile Apps].</span></span>

<span data-ttu-id="a3ccf-117">À l’aide de la fonctionnalité de synchronisation des données hors connexion-hello des applications mobiles, les utilisateurs finaux peuvent interagir avec une base de données local même lorsque le réseau de hello n’est pas accessible.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-117">Using hello offline data-sync feature of Mobile Apps, end-users can interact with a local database even when hello network is inaccessible.</span></span> <span data-ttu-id="a3ccf-118">toouse ces fonctionnalités dans votre application, vous initialisez le contexte de synchronisation de hello de `MSClient` et faire référence à un magasin local.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-118">toouse these features in your app, you initialize hello sync context of `MSClient` and reference a local store.</span></span> <span data-ttu-id="a3ccf-119">Puis vous font référence à votre table via hello **MSSyncTable** interface.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-119">Then you reference your table through hello **MSSyncTable** interface.</span></span>

<span data-ttu-id="a3ccf-120">Dans **QSTodoService.m** (Objective-C) ou **ToDoTableViewController.swift** (rapide), notez que hello du type de membre de hello **syncTable** est  **MSSyncTable**.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-120">In **QSTodoService.m** (Objective-C) or **ToDoTableViewController.swift** (Swift), notice that hello type of hello member **syncTable** is **MSSyncTable**.</span></span> <span data-ttu-id="a3ccf-121">La synchronisation hors connexion utilise cette interface de table de synchronisation à la place de **MSTable**.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-121">Offline sync uses this sync table interface instead of **MSTable**.</span></span> <span data-ttu-id="a3ccf-122">Lorsqu’une table de synchronisation est utilisée, toutes les opérations accédez magasin local de toohello sont synchronisées avec les données hello distant back-end avec explicite push et pull des opérations.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-122">When a sync table is used, all operations go toohello local store and are synchronized only with hello remote back end with explicit push and pull operations.</span></span>

 <span data-ttu-id="a3ccf-123">tooget une table de synchronisation tooa de référence, utilisez hello **syncTableWithName** méthode sur `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-123">tooget a reference tooa sync table, use hello **syncTableWithName** method on `MSClient`.</span></span> <span data-ttu-id="a3ccf-124">la fonctionnalité de synchronisation hors connexion tooremove, utilisation **tableWithName** à la place.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-124">tooremove offline sync functionality, use **tableWithName** instead.</span></span>

<span data-ttu-id="a3ccf-125">Avant de pouvoir effectuer des opérations de table, le magasin local de hello doit être initialisé.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-125">Before any table operations can be performed, hello local store must be initialized.</span></span> <span data-ttu-id="a3ccf-126">Voici le code approprié de hello :</span><span class="sxs-lookup"><span data-stu-id="a3ccf-126">Here is hello relevant code:</span></span>

* <span data-ttu-id="a3ccf-127">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-127">**Objective-C**.</span></span> <span data-ttu-id="a3ccf-128">Bonjour **QSTodoService.init** méthode :</span><span class="sxs-lookup"><span data-stu-id="a3ccf-128">In hello **QSTodoService.init** method:</span></span>

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* <span data-ttu-id="a3ccf-129">**Swift**.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-129">**Swift**.</span></span> <span data-ttu-id="a3ccf-130">Bonjour **ToDoTableViewController.viewDidLoad** méthode :</span><span class="sxs-lookup"><span data-stu-id="a3ccf-130">In hello **ToDoTableViewController.viewDidLoad** method:</span></span>

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of hello Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   <span data-ttu-id="a3ccf-131">Cette méthode crée un magasin local à l’aide de hello `MSCoreDataStore` fournit de l’interface qui hello SDK des applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-131">This method creates a local store by using hello `MSCoreDataStore` interface, which hello Mobile Apps SDK provides.</span></span> <span data-ttu-id="a3ccf-132">Vous pouvez également fournir un autre magasin local en implémentant hello `MSSyncContextDataSource` protocole.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-132">Alternatively, you can provide a different local store by implementing hello `MSSyncContextDataSource` protocol.</span></span> <span data-ttu-id="a3ccf-133">En outre, hello du premier paramètre de **MSSyncContext** toospecify utilisé n’est un gestionnaire de conflit.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-133">Also, hello first parameter of **MSSyncContext** is used toospecify a conflict handler.</span></span> <span data-ttu-id="a3ccf-134">Étant donné que nous avons passé `nil`, nous obtenons le Gestionnaire de conflit hello par défaut, cette opération échoue sur tout conflit.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-134">Because we have passed `nil`, we get hello default conflict handler, which fails on any conflict.</span></span>

<span data-ttu-id="a3ccf-135">Maintenant, nous allons effectuer la synchronisation réel hello et obtenir des données de serveur principal à distance de hello :</span><span class="sxs-lookup"><span data-stu-id="a3ccf-135">Now, let's perform hello actual sync operation, and get data from hello remote back end:</span></span>

* <span data-ttu-id="a3ccf-136">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-136">**Objective-C**.</span></span> <span data-ttu-id="a3ccf-137">`syncData`transmet d’abord les nouvelles modifications, puis appelle **pullData** tooget des données à partir des principaux distants hello.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-137">`syncData` first pushes new changes and then calls **pullData** tooget data from hello remote back end.</span></span> <span data-ttu-id="a3ccf-138">À son tour, hello **pullData** méthode obtient de nouvelles données qui correspond à une requête :</span><span class="sxs-lookup"><span data-stu-id="a3ccf-138">In turn, hello **pullData** method gets new data that matches a query:</span></span>

   ```objc
   -(void)syncData:(QSCompletionBlock)completion
   {
       // Push all changes in hello sync context, and then pull new data.
       [self.client.syncContext pushWithCompletion:^(NSError *error) {
           [self logErrorIfNotNil:error];
           [self pullData:completion];
       }];
   }

   -(void)pullData:(QSCompletionBlock)completion
   {
       MSQuery *query = [self.syncTable query];

       // Pulls data from hello remote server into hello local table.
       // We're pulling all items and filtering in hello view.
       // Query ID is used for incremental sync.
       [self.syncTable pullWithQuery:query queryId:@"allTodoItems" completion:^(NSError *error) {
           [self logErrorIfNotNil:error];

           // Lets hello caller know that we have finished.
           if (completion != nil) {
               dispatch_async(dispatch_get_main_queue(), completion);
           }
       }];
   }
   ```
* <span data-ttu-id="a3ccf-139">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a3ccf-139">**Swift**:</span></span>
   ```swift
   func onRefresh(sender: UIRefreshControl!) {
      UIApplication.sharedApplication().networkActivityIndicatorVisible = true

      self.table!.pullWithQuery(self.table?.query(), queryId: "AllRecords") {
          (error) -> Void in

          UIApplication.sharedApplication().networkActivityIndicatorVisible = false

          if error != nil {
              // A real application would handle various errors like network conditions,
              // server conflicts, etc via hello MSSyncContextDelegate
              print("Error: \(error!.description)")

              // We will discard our changes and keep hello server's copy for simplicity
              if let opErrors = error!.userInfo[MSErrorPushResultKey] as? Array<MSTableOperationError> {
                  for opError in opErrors {
                      print("Attempted operation tooitem \(opError.itemId)")
                      if (opError.operation == .Insert || opError.operation == .Delete) {
                          print("Insert/Delete, failed discarding changes")
                          opError.cancelOperationAndDiscardItemWithCompletion(nil)
                      } else {
                          print("Update failed, reverting tooserver's copy")
                          opError.cancelOperationAndUpdateItem(opError.serverItem!, completion: nil)
                      }
                  }
              }
          }
          self.refreshControl?.endRefreshing()
      }
   }
   ```

<span data-ttu-id="a3ccf-140">Dans la version de hello Objective-C, dans `syncData`, nous avons tout d’abord appeler **pushWithCompletion** sur le contexte de synchronisation hello.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-140">In hello Objective-C version, in `syncData`, we first call **pushWithCompletion** on hello sync context.</span></span> <span data-ttu-id="a3ccf-141">Cette méthode est un membre de `MSSyncContext` (et pas la table synchronisation hello lui-même), car il exécute un push de modifications sur toutes les tables.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-141">This method is a member of `MSSyncContext` (and not hello sync table itself) because it pushes changes across all tables.</span></span> <span data-ttu-id="a3ccf-142">Seuls les enregistrements qui ont été modifiées d’une certaine façon localement (via les opérations CUD) sont envoyées toohello server.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-142">Only records that have been modified in some way locally (through CUD operations) are sent toohello server.</span></span> <span data-ttu-id="a3ccf-143">Puis hello d’assistance **pullData** est appelée, les appels **MSSyncTable.pullWithQuery** tooretrieve des données distantes et les stocker dans la base de données locale hello.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-143">Then hello helper **pullData** is called, which calls **MSSyncTable.pullWithQuery** tooretrieve remote data and store it in hello local database.</span></span>

<span data-ttu-id="a3ccf-144">Dans la version de Swift hello, car hello push n’a pas strictement nécessaire, il n’est pas appelée trop**pushWithCompletion**.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-144">In hello Swift version, because hello push operation was not strictly necessary, there is no call too**pushWithCompletion**.</span></span> <span data-ttu-id="a3ccf-145">Si des modifications sont en attente dans le contexte de synchronisation de hello pour table hello qui effectue une opération de diffusion, extraction émet toujours un push tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-145">If there are any changes pending in hello sync context for hello table that is doing a push operation, pull always issues a push first.</span></span> <span data-ttu-id="a3ccf-146">Toutefois, si vous avez plusieurs tables de la synchronisation, il est meilleure tooexplicitly appel push tooensure que tout est cohérent entre les tables associées.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-146">However, if you have more than one sync table, it is best tooexplicitly call push tooensure that everything is consistent across related tables.</span></span>

<span data-ttu-id="a3ccf-147">Dans les versions Swift et les hello Objective-C, vous pouvez utiliser hello **pullWithQuery** méthode toospecify un toofilter requête hello enregistrements que vous voulez tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-147">In both hello Objective-C and Swift versions, you can use hello **pullWithQuery** method toospecify a query toofilter hello records you want tooretrieve.</span></span> <span data-ttu-id="a3ccf-148">Dans cet exemple, les requêtes hello récupère tous les enregistrements de hello distant `TodoItem` table.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-148">In this example, hello query retrieves all records in hello remote `TodoItem` table.</span></span>

<span data-ttu-id="a3ccf-149">Hello du deuxième paramètre de **pullWithQuery** est un ID de requête qui est utilisé pour *synchronisation incrémentielle*. Synchronisation incrémentielle n’extrait que les enregistrements qui ont été modifiés depuis la dernière synchronisation hello, à l’aide de l’enregistrement hello `UpdatedAt` horodatage (appelée `updatedAt` dans le magasin local hello.) ID de requête hello doit être une chaîne descriptive est unique pour chaque requête logique dans votre application.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-149">hello second parameter of **pullWithQuery** is a query ID that is used for *incremental sync*. Incremental sync retrieves only records that were modified since hello last sync, using hello record's `UpdatedAt` time stamp (called `updatedAt` in hello local store.) hello query ID should be a descriptive string that is unique for each logical query in your app.</span></span> <span data-ttu-id="a3ccf-150">tooopt hors synchronisation incrémentielle, passer `nil` comme hello ID de requête.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-150">tooopt out of incremental sync, pass `nil` as hello query ID.</span></span> <span data-ttu-id="a3ccf-151">Cette approche peut ne pas être très efficace, car elle récupère tous les enregistrements de chaque opération d’extraction.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-151">This approach can be potentially inefficient, because it retrieves all records on each pull operation.</span></span>

<span data-ttu-id="a3ccf-152">application de Hello Objective-C se synchronise lorsque vous modifiez ou ajoutez des données, lorsqu’un utilisateur effectue des mouvements d’actualisation hello et au lancement.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-152">hello Objective-C app syncs when you modify or add data, when a user performs hello refresh gesture, and on launch.</span></span>

<span data-ttu-id="a3ccf-153">application Swift Hello se synchronise lorsque les utilisateur hello effectue des mouvements d’actualisation hello et au lancement.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-153">hello Swift app syncs when hello user performs hello refresh gesture and on launch.</span></span>

<span data-ttu-id="a3ccf-154">Parce que les synchronisations d’application chaque fois que les données sont hello modifiée (Objective-C) ou à chaque démarrage de l’application hello (Objective-C et Swift), application hello suppose que l’utilisateur hello est en ligne.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-154">Because hello app syncs whenever data is modified (Objective-C) or whenever hello app starts (Objective-C and Swift), hello app assumes that hello user is online.</span></span> <span data-ttu-id="a3ccf-155">Dans une section ultérieure, application hello met à jour afin que les utilisateurs peuvent modifier, même s’ils sont hors connexion.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-155">In a later section, you will update hello app so that users can edit even when they are offline.</span></span>

## <span data-ttu-id="a3ccf-156"><a name="review-core-data"></a>Modèle de données de base hello de révision</span><span class="sxs-lookup"><span data-stu-id="a3ccf-156"><a name="review-core-data"></a>Review hello Core Data model</span></span>
<span data-ttu-id="a3ccf-157">Lorsque vous utilisez le stockage hors connexion de données de base hello, vous devez définir des tables et des champs dans votre modèle de données.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-157">When you use hello Core Data offline store, you must define particular tables and fields in your data model.</span></span> <span data-ttu-id="a3ccf-158">exemple d’application Hello inclut déjà un modèle de données avec le format correct de hello.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-158">hello sample app already includes a data model with hello right format.</span></span> <span data-ttu-id="a3ccf-159">Dans cette section, nous guider tooshow de ces tables comment elles sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-159">In this section, we walk through these tables tooshow how they are used.</span></span>

<span data-ttu-id="a3ccf-160">Ouvrez **QSDataModel.xcdatamodeld**.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-160">Open **QSDataModel.xcdatamodeld**.</span></span> <span data-ttu-id="a3ccf-161">Quatre tables sont définies--trois utilisés par hello Kit de développement logiciel et qui est utilisé pour les tâches hello éléments eux-mêmes :</span><span class="sxs-lookup"><span data-stu-id="a3ccf-161">Four tables are defined--three that are used by hello SDK and one that's used for hello to-do items themselves:</span></span>
  * <span data-ttu-id="a3ccf-162">MS_TableOperations : Pistes hello éléments ayant besoin de toobe synchronisé avec le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-162">MS_TableOperations: Tracks hello items that need toobe synchronized with hello server.</span></span>
  * <span data-ttu-id="a3ccf-163">MS_TableOperationErrors : effectue le suivi des erreurs qui se produisent pendant la synchronisation hors connexion.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-163">MS_TableOperationErrors: Tracks any errors that happen during offline synchronization.</span></span>
  * <span data-ttu-id="a3ccf-164">MS_TableConfig : Pistes hello dernière heure de mise à jour pour la dernière opération de synchronisation hello pour toutes les opérations d’extraction.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-164">MS_TableConfig: Tracks hello last updated time for hello last sync operation for all pull operations.</span></span>
  * <span data-ttu-id="a3ccf-165">TodoItem : Stocke les éléments de tâche hello.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-165">TodoItem: Stores hello to-do items.</span></span> <span data-ttu-id="a3ccf-166">Hello colonnes système **créédans**, **updatedAt**, et **version** sont des propriétés système facultatif.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-166">hello system columns **createdAt**, **updatedAt**, and **version** are optional system properties.</span></span>

> [!NOTE]
> <span data-ttu-id="a3ccf-167">Hello SDK des applications mobiles réserve les noms de colonne qui commencent par «**``**».</span><span class="sxs-lookup"><span data-stu-id="a3ccf-167">hello Mobile Apps SDK reserves column names that begin with "**``**".</span></span> <span data-ttu-id="a3ccf-168">N’utilisez ce préfixe qu’avec les colonnes système.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-168">Do not use this prefix with anything other than system columns.</span></span> <span data-ttu-id="a3ccf-169">Dans le cas contraire, les noms de colonnes sont modifiés lorsque vous utilisez des principaux distants hello.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-169">Otherwise, your column names are modified when you use hello remote back end.</span></span>
>
>

<span data-ttu-id="a3ccf-170">Lorsque vous utilisez la fonctionnalité de synchronisation hors connexion hello, définir les tables système trois hello et une table de données de hello.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-170">When you use hello offline sync feature, define hello three system tables and hello data table.</span></span>

### <a name="system-tables"></a><span data-ttu-id="a3ccf-171">Tables système</span><span class="sxs-lookup"><span data-stu-id="a3ccf-171">System tables</span></span>

<span data-ttu-id="a3ccf-172">**MS_TableOperations**</span><span class="sxs-lookup"><span data-stu-id="a3ccf-172">**MS_TableOperations**</span></span>  

![Attributs de table MS_TableOperations][defining-core-data-tableoperations-entity]

| <span data-ttu-id="a3ccf-174">Attribut</span><span class="sxs-lookup"><span data-stu-id="a3ccf-174">Attribute</span></span> | <span data-ttu-id="a3ccf-175">Type</span><span class="sxs-lookup"><span data-stu-id="a3ccf-175">Type</span></span> |
| --- | --- |
| <span data-ttu-id="a3ccf-176">id</span><span class="sxs-lookup"><span data-stu-id="a3ccf-176">id</span></span> | <span data-ttu-id="a3ccf-177">Integer 64</span><span class="sxs-lookup"><span data-stu-id="a3ccf-177">Integer 64</span></span> |
| <span data-ttu-id="a3ccf-178">itemId</span><span class="sxs-lookup"><span data-stu-id="a3ccf-178">itemId</span></span> | <span data-ttu-id="a3ccf-179">String</span><span class="sxs-lookup"><span data-stu-id="a3ccf-179">String</span></span> |
| <span data-ttu-id="a3ccf-180">properties</span><span class="sxs-lookup"><span data-stu-id="a3ccf-180">properties</span></span> | <span data-ttu-id="a3ccf-181">Binary Data</span><span class="sxs-lookup"><span data-stu-id="a3ccf-181">Binary Data</span></span> |
| <span data-ttu-id="a3ccf-182">table</span><span class="sxs-lookup"><span data-stu-id="a3ccf-182">table</span></span> | <span data-ttu-id="a3ccf-183">String</span><span class="sxs-lookup"><span data-stu-id="a3ccf-183">String</span></span> |
| <span data-ttu-id="a3ccf-184">tableKind</span><span class="sxs-lookup"><span data-stu-id="a3ccf-184">tableKind</span></span> | <span data-ttu-id="a3ccf-185">Integer 16</span><span class="sxs-lookup"><span data-stu-id="a3ccf-185">Integer 16</span></span> |


<span data-ttu-id="a3ccf-186">**MS_TableOperationErrors**</span><span class="sxs-lookup"><span data-stu-id="a3ccf-186">**MS_TableOperationErrors**</span></span>

 ![Attributs de table MS_TableOperationErrors][defining-core-data-tableoperationerrors-entity]

| <span data-ttu-id="a3ccf-188">Attribut</span><span class="sxs-lookup"><span data-stu-id="a3ccf-188">Attribute</span></span> | <span data-ttu-id="a3ccf-189">Type</span><span class="sxs-lookup"><span data-stu-id="a3ccf-189">Type</span></span> |
| --- | --- |
| <span data-ttu-id="a3ccf-190">id</span><span class="sxs-lookup"><span data-stu-id="a3ccf-190">id</span></span> |<span data-ttu-id="a3ccf-191">Chaîne</span><span class="sxs-lookup"><span data-stu-id="a3ccf-191">String</span></span> |
| <span data-ttu-id="a3ccf-192">operationId</span><span class="sxs-lookup"><span data-stu-id="a3ccf-192">operationId</span></span> |<span data-ttu-id="a3ccf-193">Integer 64</span><span class="sxs-lookup"><span data-stu-id="a3ccf-193">Integer 64</span></span> |
| <span data-ttu-id="a3ccf-194">properties</span><span class="sxs-lookup"><span data-stu-id="a3ccf-194">properties</span></span> |<span data-ttu-id="a3ccf-195">Binary Data</span><span class="sxs-lookup"><span data-stu-id="a3ccf-195">Binary Data</span></span> |
| <span data-ttu-id="a3ccf-196">tableKind</span><span class="sxs-lookup"><span data-stu-id="a3ccf-196">tableKind</span></span> |<span data-ttu-id="a3ccf-197">Integer 16</span><span class="sxs-lookup"><span data-stu-id="a3ccf-197">Integer 16</span></span> |

 <span data-ttu-id="a3ccf-198">**MS_TableConfig**</span><span class="sxs-lookup"><span data-stu-id="a3ccf-198">**MS_TableConfig**</span></span>

 ![][defining-core-data-tableconfig-entity]

| <span data-ttu-id="a3ccf-199">Attribut</span><span class="sxs-lookup"><span data-stu-id="a3ccf-199">Attribute</span></span> | <span data-ttu-id="a3ccf-200">Type</span><span class="sxs-lookup"><span data-stu-id="a3ccf-200">Type</span></span> |
| --- | --- |
| <span data-ttu-id="a3ccf-201">id</span><span class="sxs-lookup"><span data-stu-id="a3ccf-201">id</span></span> |<span data-ttu-id="a3ccf-202">Chaîne</span><span class="sxs-lookup"><span data-stu-id="a3ccf-202">String</span></span> |
| <span data-ttu-id="a3ccf-203">key</span><span class="sxs-lookup"><span data-stu-id="a3ccf-203">key</span></span> |<span data-ttu-id="a3ccf-204">String</span><span class="sxs-lookup"><span data-stu-id="a3ccf-204">String</span></span> |
| <span data-ttu-id="a3ccf-205">keyType</span><span class="sxs-lookup"><span data-stu-id="a3ccf-205">keyType</span></span> |<span data-ttu-id="a3ccf-206">Integer 64</span><span class="sxs-lookup"><span data-stu-id="a3ccf-206">Integer 64</span></span> |
| <span data-ttu-id="a3ccf-207">table</span><span class="sxs-lookup"><span data-stu-id="a3ccf-207">table</span></span> |<span data-ttu-id="a3ccf-208">String</span><span class="sxs-lookup"><span data-stu-id="a3ccf-208">String</span></span> |
| <span data-ttu-id="a3ccf-209">value</span><span class="sxs-lookup"><span data-stu-id="a3ccf-209">value</span></span> |<span data-ttu-id="a3ccf-210">Chaîne</span><span class="sxs-lookup"><span data-stu-id="a3ccf-210">String</span></span> |

### <a name="data-table"></a><span data-ttu-id="a3ccf-211">Table de données</span><span class="sxs-lookup"><span data-stu-id="a3ccf-211">Data table</span></span>

<span data-ttu-id="a3ccf-212">**TodoItem**</span><span class="sxs-lookup"><span data-stu-id="a3ccf-212">**TodoItem**</span></span>

| <span data-ttu-id="a3ccf-213">Attribut</span><span class="sxs-lookup"><span data-stu-id="a3ccf-213">Attribute</span></span> | <span data-ttu-id="a3ccf-214">Type</span><span class="sxs-lookup"><span data-stu-id="a3ccf-214">Type</span></span> | <span data-ttu-id="a3ccf-215">Remarque</span><span class="sxs-lookup"><span data-stu-id="a3ccf-215">Note</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a3ccf-216">id</span><span class="sxs-lookup"><span data-stu-id="a3ccf-216">id</span></span> | <span data-ttu-id="a3ccf-217">Chaîne, marquée requise</span><span class="sxs-lookup"><span data-stu-id="a3ccf-217">String, marked required</span></span> |<span data-ttu-id="a3ccf-218">Clé primaire dans le magasin distant</span><span class="sxs-lookup"><span data-stu-id="a3ccf-218">Primary key in remote store</span></span> |
| <span data-ttu-id="a3ccf-219">terminé</span><span class="sxs-lookup"><span data-stu-id="a3ccf-219">complete</span></span> | <span data-ttu-id="a3ccf-220">Boolean</span><span class="sxs-lookup"><span data-stu-id="a3ccf-220">Boolean</span></span> | <span data-ttu-id="a3ccf-221">Champ d’élément de tâche</span><span class="sxs-lookup"><span data-stu-id="a3ccf-221">To-do item field</span></span> |
| <span data-ttu-id="a3ccf-222">texte</span><span class="sxs-lookup"><span data-stu-id="a3ccf-222">text</span></span> |<span data-ttu-id="a3ccf-223">String</span><span class="sxs-lookup"><span data-stu-id="a3ccf-223">String</span></span> |<span data-ttu-id="a3ccf-224">Champ d’élément de tâche</span><span class="sxs-lookup"><span data-stu-id="a3ccf-224">To-do item field</span></span> |
| <span data-ttu-id="a3ccf-225">createdAt</span><span class="sxs-lookup"><span data-stu-id="a3ccf-225">createdAt</span></span> | <span data-ttu-id="a3ccf-226">Date</span><span class="sxs-lookup"><span data-stu-id="a3ccf-226">Date</span></span> | <span data-ttu-id="a3ccf-227">(facultatif) Mappe trop**créédans** propriété système</span><span class="sxs-lookup"><span data-stu-id="a3ccf-227">(optional) Maps too**createdAt** system property</span></span> |
| <span data-ttu-id="a3ccf-228">updatedAt</span><span class="sxs-lookup"><span data-stu-id="a3ccf-228">updatedAt</span></span> | <span data-ttu-id="a3ccf-229">Date</span><span class="sxs-lookup"><span data-stu-id="a3ccf-229">Date</span></span> | <span data-ttu-id="a3ccf-230">(facultatif) Mappe trop**updatedAt** propriété système</span><span class="sxs-lookup"><span data-stu-id="a3ccf-230">(optional) Maps too**updatedAt** system property</span></span> |
| <span data-ttu-id="a3ccf-231">version</span><span class="sxs-lookup"><span data-stu-id="a3ccf-231">version</span></span> | <span data-ttu-id="a3ccf-232">String</span><span class="sxs-lookup"><span data-stu-id="a3ccf-232">String</span></span> | <span data-ttu-id="a3ccf-233">(facultatif) Conflits toodetect utilisé, maps tooversion</span><span class="sxs-lookup"><span data-stu-id="a3ccf-233">(optional) Used toodetect conflicts, maps tooversion</span></span> |

## <span data-ttu-id="a3ccf-234"><a name="setup-sync"></a>Modifier le comportement de synchronisation de hello d’application hello</span><span class="sxs-lookup"><span data-stu-id="a3ccf-234"><a name="setup-sync"></a>Change hello sync behavior of hello app</span></span>
<span data-ttu-id="a3ccf-235">Dans cette section, vous modifiez application hello afin qu’il n’est pas synchronisée sur le démarrage de l’application ou lorsque vous insérez et mettre à jour des éléments.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-235">In this section, you modify hello app so that it does not sync on app start or when you insert and update items.</span></span> <span data-ttu-id="a3ccf-236">Il se synchronise uniquement lorsque le bouton d’actualisation du mouvement hello est effectuée.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-236">It syncs only when hello refresh gesture button is performed.</span></span>

<span data-ttu-id="a3ccf-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="a3ccf-237">**Objective-C**:</span></span>

1. <span data-ttu-id="a3ccf-238">Dans **QSTodoListViewController.m**, modifiez hello **viewDidLoad** tooremove de la méthode hello appel trop`[self refresh]` à fin hello de méthode hello.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-238">In **QSTodoListViewController.m**, change hello **viewDidLoad** method tooremove hello call too`[self refresh]` at hello end of hello method.</span></span> <span data-ttu-id="a3ccf-239">Maintenant, les données de salutation ne sont pas synchronisées avec le serveur hello sur le démarrage de l’application.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-239">Now hello data is not synced with hello server on app start.</span></span> <span data-ttu-id="a3ccf-240">Au lieu de cela, il est synchronisé avec le contenu de hello du magasin local de hello.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-240">Instead, it's synced with hello contents of hello local store.</span></span>
2. <span data-ttu-id="a3ccf-241">Dans **QSTodoService.m**, modifiez la définition hello de `addItem` afin qu’il ne synchroniser après hello élément est inséré.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-241">In **QSTodoService.m**, modify hello definition of `addItem` so that it doesn't sync after hello item is inserted.</span></span> <span data-ttu-id="a3ccf-242">Supprimer hello `self syncData` bloquer et remplacez-le par suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="a3ccf-242">Remove hello `self syncData` block and replace it with hello following:</span></span>

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. <span data-ttu-id="a3ccf-243">Modifier la définition de hello de `completeItem` comme mentionné précédemment.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-243">Modify hello definition of `completeItem` as mentioned previously.</span></span> <span data-ttu-id="a3ccf-244">Supprimer le bloc hello pour `self syncData` et remplacez-la par suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="a3ccf-244">Remove hello block for `self syncData` and replace it with hello following:</span></span>
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

<span data-ttu-id="a3ccf-245">**Swift**:</span><span class="sxs-lookup"><span data-stu-id="a3ccf-245">**Swift**:</span></span>

<span data-ttu-id="a3ccf-246">Dans `viewDidLoad`, dans **ToDoTableViewController.swift**, commentez les lignes de deux hello indiqués ici, toostop la synchronisation sur le démarrage de l’application.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-246">In `viewDidLoad`, in **ToDoTableViewController.swift**, comment out hello two lines shown here, toostop syncing on app start.</span></span> <span data-ttu-id="a3ccf-247">Au moment de hello de rédaction de cet article, hello Swift Todo application n’est pas actualisée service de hello lorsqu’un utilisateur ajoute ou termine un élément.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-247">At hello time of this writing, hello Swift Todo app does not update hello service when someone adds or completes an item.</span></span> <span data-ttu-id="a3ccf-248">Il met à jour le service hello uniquement sur le démarrage de l’application.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-248">It updates hello service only on app start.</span></span>

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <span data-ttu-id="a3ccf-249"><a name="test-app"></a>Application de test hello</span><span class="sxs-lookup"><span data-stu-id="a3ccf-249"><a name="test-app"></a>Test hello app</span></span>
<span data-ttu-id="a3ccf-250">Dans cette section, vous vous connectez toosimulate d’URL non valide tooan un scénario hors connexion.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-250">In this section, you connect tooan invalid URL toosimulate an offline scenario.</span></span> <span data-ttu-id="a3ccf-251">Lorsque vous ajoutez des éléments de données, ils sont maintenus dans hello stocker les données de base local, mais ils sont non synchronisés avec le serveur principal de l’application mobile hello.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-251">When you add data items, they're held in hello local Core Data store, but they're not synced with hello mobile-app back end.</span></span>

1. <span data-ttu-id="a3ccf-252">Modifier l’URL de l’application mobile hello dans **QSTodoService.m** tooan URL non valide et l’application hello exécuter à nouveau :</span><span class="sxs-lookup"><span data-stu-id="a3ccf-252">Change hello mobile-app URL in **QSTodoService.m** tooan invalid URL, and run hello app again:</span></span>

   <span data-ttu-id="a3ccf-253">**Objective-C**.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-253">**Objective-C**.</span></span> <span data-ttu-id="a3ccf-254">Dans QSTodoService.m :</span><span class="sxs-lookup"><span data-stu-id="a3ccf-254">In QSTodoService.m:</span></span>
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   <span data-ttu-id="a3ccf-255">**Swift**.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-255">**Swift**.</span></span> <span data-ttu-id="a3ccf-256">Dans ToDoTableViewController.swift :</span><span class="sxs-lookup"><span data-stu-id="a3ccf-256">In ToDoTableViewController.swift:</span></span>
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. <span data-ttu-id="a3ccf-257">Ajoutez des éléments de tâche.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-257">Add some to-do items.</span></span> <span data-ttu-id="a3ccf-258">Quitter le simulateur de hello (ou une application hello fermeture forcée), puis le redémarre.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-258">Quit hello simulator (or forcibly close hello app), and then restart it.</span></span> <span data-ttu-id="a3ccf-259">Vérifiez que vos modifications sont persistantes.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-259">Verify that your changes persist.</span></span>

3. <span data-ttu-id="a3ccf-260">Afficher le contenu de hello Hello distant **TodoItem** table :</span><span class="sxs-lookup"><span data-stu-id="a3ccf-260">View hello contents of hello remote **TodoItem** table:</span></span>
   * <span data-ttu-id="a3ccf-261">Pour un serveur principal de Node.js, consultez toohello [portail Azure](https://portal.azure.com/) et, dans votre serveur principal de l’application mobile, cliquez sur **Tables facile** > **TodoItem**.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-261">For a Node.js back end, go toohello [Azure portal](https://portal.azure.com/) and, in your mobile-app back end, click **Easy Tables** > **TodoItem**.</span></span>  
   * <span data-ttu-id="a3ccf-262">Pour un backend .NET, utilisez un outil SQL, comme SQL Server Management Studio, ou un client REST, comme Fiddler ou Postman.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-262">For a .NET back end, use either a SQL tool, such as SQL Server Management Studio, or a REST client, such as Fiddler or Postman.</span></span>  

4. <span data-ttu-id="a3ccf-263">Vérifiez que de nouveaux éléments de hello *pas* été synchronisé avec le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-263">Verify that hello new items have *not* been synced with hello server.</span></span>

5. <span data-ttu-id="a3ccf-264">Modification hello URL arrière toohello corriger un dans **QSTodoService.m**et l’application hello réexécuter.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-264">Change hello URL back toohello correct one in **QSTodoService.m**, and rerun hello app.</span></span>

6. <span data-ttu-id="a3ccf-265">Effectuer des mouvements d’actualisation hello en les extrayant hello liste déroulante d’éléments.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-265">Perform hello refresh gesture by pulling down hello list of items.</span></span>  
<span data-ttu-id="a3ccf-266">Un compteur de progression s’affiche.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-266">A progress spinner is displayed.</span></span>

7. <span data-ttu-id="a3ccf-267">Hello de vue **TodoItem** à nouveau les données.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-267">View hello **TodoItem** data again.</span></span> <span data-ttu-id="a3ccf-268">éléments de tâches nouvelles et modifiées Hello doivent désormais être affichés.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-268">hello new and changed to-do items should now be displayed.</span></span>

## <a name="summary"></a><span data-ttu-id="a3ccf-269">Résumé</span><span class="sxs-lookup"><span data-stu-id="a3ccf-269">Summary</span></span>
<span data-ttu-id="a3ccf-270">fonctionnalité de synchronisation hors connexion toosupport hello, nous avons utilisé hello `MSSyncTable` de l’interface et initialisé `MSClient.syncContext` avec un magasin local.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-270">toosupport hello offline sync feature, we used hello `MSSyncTable` interface and initialized `MSClient.syncContext` with a local store.</span></span> <span data-ttu-id="a3ccf-271">Dans ce cas, le magasin local de hello était une base de données basée sur des données de base.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-271">In this case, hello local store was a Core Data-based database.</span></span>

<span data-ttu-id="a3ccf-272">Lorsque vous utilisez un magasin de données de base local, vous devez définir plusieurs tables avec hello [corriger les propriétés système](#review-core-data).</span><span class="sxs-lookup"><span data-stu-id="a3ccf-272">When you use a Core Data local store, you must define several tables with hello [correct system properties](#review-core-data).</span></span>

<span data-ttu-id="a3ccf-273">Hello normal créer, lire, mettre à jour et supprimer (CRUD) des opérations pour les applications mobiles travail comme si l’application hello est toujours connectée, mais toutes les opérations de hello se produisent sur le magasin local de hello.</span><span class="sxs-lookup"><span data-stu-id="a3ccf-273">hello normal create, read, update, and delete (CRUD) operations for mobile apps work as if hello app is still connected, but all hello operations occur against hello local store.</span></span>

<span data-ttu-id="a3ccf-274">Lorsque nous synchronisé magasin local de hello avec serveur de hello, nous avons utilisé hello **MSSyncTable.pullWithQuery** (méthode).</span><span class="sxs-lookup"><span data-stu-id="a3ccf-274">When we synchronized hello local store with hello server, we used hello **MSSyncTable.pullWithQuery** method.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a3ccf-275">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a3ccf-275">Additional resources</span></span>
* <span data-ttu-id="a3ccf-276">[synchronisation des données hors connexion dans les applications mobiles]</span><span class="sxs-lookup"><span data-stu-id="a3ccf-276">[Offline Data Sync in Mobile Apps]</span></span>
* <span data-ttu-id="a3ccf-277">[Couverture du cloud : La synchronisation hors connexion dans Services mobiles Azure] \(hello vidéo concerne les Services mobiles, mais le fonctionnement de la synchronisation hors connexion des applications mobiles de la même façon.\)</span><span class="sxs-lookup"><span data-stu-id="a3ccf-277">[Cloud Cover: Offline Sync in Azure Mobile Services] \(hello video is about Mobile Services, but Mobile Apps offline sync works in a similar way.\)</span></span>

<!-- URLs. -->


[créer une application iOS]: app-service-mobile-ios-get-started.md
[synchronisation des données hors connexion dans les applications mobiles]: app-service-mobile-offline-data-sync.md

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

[Couverture du cloud : La synchronisation hors connexion dans Services mobiles Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
