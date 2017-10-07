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
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a>Activer la synchronisation hors connexion avec des applications mobiles iOS
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel couvre la synchronisation hors connexion avec fonctionnalité d’applications mobiles hello du Service d’application Azure pour iOS. Avec les utilisateurs finaux de synchronisation hors connexion peuvent interagir avec un tooview de l’application mobile, ajouter ou modifier des données, même si elles n’ont aucune connexion réseau. Les modifications sont stockées dans une base de données locale. Une fois l’appareil de hello en ligne, les modifications de hello sont synchronisées avec les principaux à distance hello.

S’il s’agit de votre première expérience avec les applications mobiles, vous devez d’abord terminer didacticiel de hello [créer une application iOS]. Si vous n’utilisez pas de projet de démarrage rapide serveur hello téléchargé, vous devez ajouter le projet tooyour de packages d’extension d’accès aux données de hello. Pour plus d’informations sur les packages d’extension de serveur, consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn en savoir plus sur la fonctionnalité de synchronisation hors connexion hello, consultez [synchronisation des données hors connexion dans les applications mobiles].

## <a name="review-sync"></a>Passez en revue le code de synchronisation hello client
projet de client Hello que vous avez téléchargé pour hello [créer une application iOS] didacticiel contient déjà du code qui prend en charge la synchronisation hors connexion à l’aide d’une base de données locale en fonction des données de base. Cette section résume ce qui est déjà inclus dans le code de didacticiel hello. Pour une vue d’ensemble conceptuelle de la fonctionnalité de hello, consultez [synchronisation des données hors connexion dans les applications mobiles].

À l’aide de la fonctionnalité de synchronisation des données hors connexion-hello des applications mobiles, les utilisateurs finaux peuvent interagir avec une base de données local même lorsque le réseau de hello n’est pas accessible. toouse ces fonctionnalités dans votre application, vous initialisez le contexte de synchronisation de hello de `MSClient` et faire référence à un magasin local. Puis vous font référence à votre table via hello **MSSyncTable** interface.

Dans **QSTodoService.m** (Objective-C) ou **ToDoTableViewController.swift** (rapide), notez que hello du type de membre de hello **syncTable** est  **MSSyncTable**. La synchronisation hors connexion utilise cette interface de table de synchronisation à la place de **MSTable**. Lorsqu’une table de synchronisation est utilisée, toutes les opérations accédez magasin local de toohello sont synchronisées avec les données hello distant back-end avec explicite push et pull des opérations.

 tooget une table de synchronisation tooa de référence, utilisez hello **syncTableWithName** méthode sur `MSClient`. la fonctionnalité de synchronisation hors connexion tooremove, utilisation **tableWithName** à la place.

Avant de pouvoir effectuer des opérations de table, le magasin local de hello doit être initialisé. Voici le code approprié de hello :

* **Objective-C**. Bonjour **QSTodoService.init** méthode :

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* **Swift**. Bonjour **ToDoTableViewController.viewDidLoad** méthode :

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of hello Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   Cette méthode crée un magasin local à l’aide de hello `MSCoreDataStore` fournit de l’interface qui hello SDK des applications mobiles. Vous pouvez également fournir un autre magasin local en implémentant hello `MSSyncContextDataSource` protocole. En outre, hello du premier paramètre de **MSSyncContext** toospecify utilisé n’est un gestionnaire de conflit. Étant donné que nous avons passé `nil`, nous obtenons le Gestionnaire de conflit hello par défaut, cette opération échoue sur tout conflit.

Maintenant, nous allons effectuer la synchronisation réel hello et obtenir des données de serveur principal à distance de hello :

* **Objective-C**. `syncData`transmet d’abord les nouvelles modifications, puis appelle **pullData** tooget des données à partir des principaux distants hello. À son tour, hello **pullData** méthode obtient de nouvelles données qui correspond à une requête :

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
* **Swift**:
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

Dans la version de hello Objective-C, dans `syncData`, nous avons tout d’abord appeler **pushWithCompletion** sur le contexte de synchronisation hello. Cette méthode est un membre de `MSSyncContext` (et pas la table synchronisation hello lui-même), car il exécute un push de modifications sur toutes les tables. Seuls les enregistrements qui ont été modifiées d’une certaine façon localement (via les opérations CUD) sont envoyées toohello server. Puis hello d’assistance **pullData** est appelée, les appels **MSSyncTable.pullWithQuery** tooretrieve des données distantes et les stocker dans la base de données locale hello.

Dans la version de Swift hello, car hello push n’a pas strictement nécessaire, il n’est pas appelée trop**pushWithCompletion**. Si des modifications sont en attente dans le contexte de synchronisation de hello pour table hello qui effectue une opération de diffusion, extraction émet toujours un push tout d’abord. Toutefois, si vous avez plusieurs tables de la synchronisation, il est meilleure tooexplicitly appel push tooensure que tout est cohérent entre les tables associées.

Dans les versions Swift et les hello Objective-C, vous pouvez utiliser hello **pullWithQuery** méthode toospecify un toofilter requête hello enregistrements que vous voulez tooretrieve. Dans cet exemple, les requêtes hello récupère tous les enregistrements de hello distant `TodoItem` table.

Hello du deuxième paramètre de **pullWithQuery** est un ID de requête qui est utilisé pour *synchronisation incrémentielle*. Synchronisation incrémentielle n’extrait que les enregistrements qui ont été modifiés depuis la dernière synchronisation hello, à l’aide de l’enregistrement hello `UpdatedAt` horodatage (appelée `updatedAt` dans le magasin local hello.) ID de requête hello doit être une chaîne descriptive est unique pour chaque requête logique dans votre application. tooopt hors synchronisation incrémentielle, passer `nil` comme hello ID de requête. Cette approche peut ne pas être très efficace, car elle récupère tous les enregistrements de chaque opération d’extraction.

application de Hello Objective-C se synchronise lorsque vous modifiez ou ajoutez des données, lorsqu’un utilisateur effectue des mouvements d’actualisation hello et au lancement.

application Swift Hello se synchronise lorsque les utilisateur hello effectue des mouvements d’actualisation hello et au lancement.

Parce que les synchronisations d’application chaque fois que les données sont hello modifiée (Objective-C) ou à chaque démarrage de l’application hello (Objective-C et Swift), application hello suppose que l’utilisateur hello est en ligne. Dans une section ultérieure, application hello met à jour afin que les utilisateurs peuvent modifier, même s’ils sont hors connexion.

## <a name="review-core-data"></a>Modèle de données de base hello de révision
Lorsque vous utilisez le stockage hors connexion de données de base hello, vous devez définir des tables et des champs dans votre modèle de données. exemple d’application Hello inclut déjà un modèle de données avec le format correct de hello. Dans cette section, nous guider tooshow de ces tables comment elles sont utilisées.

Ouvrez **QSDataModel.xcdatamodeld**. Quatre tables sont définies--trois utilisés par hello Kit de développement logiciel et qui est utilisé pour les tâches hello éléments eux-mêmes :
  * MS_TableOperations : Pistes hello éléments ayant besoin de toobe synchronisé avec le serveur de hello.
  * MS_TableOperationErrors : effectue le suivi des erreurs qui se produisent pendant la synchronisation hors connexion.
  * MS_TableConfig : Pistes hello dernière heure de mise à jour pour la dernière opération de synchronisation hello pour toutes les opérations d’extraction.
  * TodoItem : Stocke les éléments de tâche hello. Hello colonnes système **créédans**, **updatedAt**, et **version** sont des propriétés système facultatif.

> [!NOTE]
> Hello SDK des applications mobiles réserve les noms de colonne qui commencent par «**``**». N’utilisez ce préfixe qu’avec les colonnes système. Dans le cas contraire, les noms de colonnes sont modifiés lorsque vous utilisez des principaux distants hello.
>
>

Lorsque vous utilisez la fonctionnalité de synchronisation hors connexion hello, définir les tables système trois hello et une table de données de hello.

### <a name="system-tables"></a>Tables système

**MS_TableOperations**  

![Attributs de table MS_TableOperations][defining-core-data-tableoperations-entity]

| Attribut | Type |
| --- | --- |
| id | Integer 64 |
| itemId | String |
| properties | Binary Data |
| table | String |
| tableKind | Integer 16 |


**MS_TableOperationErrors**

 ![Attributs de table MS_TableOperationErrors][defining-core-data-tableoperationerrors-entity]

| Attribut | Type |
| --- | --- |
| id |Chaîne |
| operationId |Integer 64 |
| properties |Binary Data |
| tableKind |Integer 16 |

 **MS_TableConfig**

 ![][defining-core-data-tableconfig-entity]

| Attribut | Type |
| --- | --- |
| id |Chaîne |
| key |String |
| keyType |Integer 64 |
| table |String |
| value |Chaîne |

### <a name="data-table"></a>Table de données

**TodoItem**

| Attribut | Type | Remarque |
| --- | --- | --- |
| id | Chaîne, marquée requise |Clé primaire dans le magasin distant |
| terminé | Boolean | Champ d’élément de tâche |
| texte |String |Champ d’élément de tâche |
| createdAt | Date | (facultatif) Mappe trop**créédans** propriété système |
| updatedAt | Date | (facultatif) Mappe trop**updatedAt** propriété système |
| version | String | (facultatif) Conflits toodetect utilisé, maps tooversion |

## <a name="setup-sync"></a>Modifier le comportement de synchronisation de hello d’application hello
Dans cette section, vous modifiez application hello afin qu’il n’est pas synchronisée sur le démarrage de l’application ou lorsque vous insérez et mettre à jour des éléments. Il se synchronise uniquement lorsque le bouton d’actualisation du mouvement hello est effectuée.

**Objective-C**:

1. Dans **QSTodoListViewController.m**, modifiez hello **viewDidLoad** tooremove de la méthode hello appel trop`[self refresh]` à fin hello de méthode hello. Maintenant, les données de salutation ne sont pas synchronisées avec le serveur hello sur le démarrage de l’application. Au lieu de cela, il est synchronisé avec le contenu de hello du magasin local de hello.
2. Dans **QSTodoService.m**, modifiez la définition hello de `addItem` afin qu’il ne synchroniser après hello élément est inséré. Supprimer hello `self syncData` bloquer et remplacez-le par suivant de hello :

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. Modifier la définition de hello de `completeItem` comme mentionné précédemment. Supprimer le bloc hello pour `self syncData` et remplacez-la par suivant de hello :
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

**Swift**:

Dans `viewDidLoad`, dans **ToDoTableViewController.swift**, commentez les lignes de deux hello indiqués ici, toostop la synchronisation sur le démarrage de l’application. Au moment de hello de rédaction de cet article, hello Swift Todo application n’est pas actualisée service de hello lorsqu’un utilisateur ajoute ou termine un élément. Il met à jour le service hello uniquement sur le démarrage de l’application.

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <a name="test-app"></a>Application de test hello
Dans cette section, vous vous connectez toosimulate d’URL non valide tooan un scénario hors connexion. Lorsque vous ajoutez des éléments de données, ils sont maintenus dans hello stocker les données de base local, mais ils sont non synchronisés avec le serveur principal de l’application mobile hello.

1. Modifier l’URL de l’application mobile hello dans **QSTodoService.m** tooan URL non valide et l’application hello exécuter à nouveau :

   **Objective-C**. Dans QSTodoService.m :
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   **Swift**. Dans ToDoTableViewController.swift :
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. Ajoutez des éléments de tâche. Quitter le simulateur de hello (ou une application hello fermeture forcée), puis le redémarre. Vérifiez que vos modifications sont persistantes.

3. Afficher le contenu de hello Hello distant **TodoItem** table :
   * Pour un serveur principal de Node.js, consultez toohello [portail Azure](https://portal.azure.com/) et, dans votre serveur principal de l’application mobile, cliquez sur **Tables facile** > **TodoItem**.  
   * Pour un backend .NET, utilisez un outil SQL, comme SQL Server Management Studio, ou un client REST, comme Fiddler ou Postman.  

4. Vérifiez que de nouveaux éléments de hello *pas* été synchronisé avec le serveur de hello.

5. Modification hello URL arrière toohello corriger un dans **QSTodoService.m**et l’application hello réexécuter.

6. Effectuer des mouvements d’actualisation hello en les extrayant hello liste déroulante d’éléments.  
Un compteur de progression s’affiche.

7. Hello de vue **TodoItem** à nouveau les données. éléments de tâches nouvelles et modifiées Hello doivent désormais être affichés.

## <a name="summary"></a>Résumé
fonctionnalité de synchronisation hors connexion toosupport hello, nous avons utilisé hello `MSSyncTable` de l’interface et initialisé `MSClient.syncContext` avec un magasin local. Dans ce cas, le magasin local de hello était une base de données basée sur des données de base.

Lorsque vous utilisez un magasin de données de base local, vous devez définir plusieurs tables avec hello [corriger les propriétés système](#review-core-data).

Hello normal créer, lire, mettre à jour et supprimer (CRUD) des opérations pour les applications mobiles travail comme si l’application hello est toujours connectée, mais toutes les opérations de hello se produisent sur le magasin local de hello.

Lorsque nous synchronisé magasin local de hello avec serveur de hello, nous avons utilisé hello **MSSyncTable.pullWithQuery** (méthode).

## <a name="additional-resources"></a>Ressources supplémentaires
* [synchronisation des données hors connexion dans les applications mobiles]
* [Couverture du cloud : La synchronisation hors connexion dans Services mobiles Azure] \(hello vidéo concerne les Services mobiles, mais le fonctionnement de la synchronisation hors connexion des applications mobiles de la même façon.\)

<!-- URLs. -->


[créer une application iOS]: app-service-mobile-ios-get-started.md
[synchronisation des données hors connexion dans les applications mobiles]: app-service-mobile-offline-data-sync.md

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

[Couverture du cloud : La synchronisation hors connexion dans Services mobiles Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
