---
title: aaaEnable la synchronisation hors connexion pour votre application Mobile de Azure (Xamarin iOS)
description: "Découvrez comment toouse l’application Mobile App Service toocache et la synchronisation de données hors connexion dans votre application iOS de Xamarin"
documentationcenter: xamarin
author: ggailey777
manager: cfowler
editor: 
services: app-service\mobile
ms.assetid: 828a287c-5d58-4540-9527-1309ebb0f32b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 5243f2d292377d8de103a40f45d649394f11b97c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinios-mobile-app"></a>Activer la synchronisation hors connexion pour votre application mobile Xamarin.iOS
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel présente la fonctionnalité de synchronisation hors connexion hello des applications mobiles Azure pour Xamarin.iOS. Synchronisation hors connexion permet de toointeract des utilisateurs finaux avec une application mobile--affichage, l’ajout ou la modification des données, même lorsqu’il n’existe aucune connexion réseau. Les modifications sont stockées dans une base de données locale. Une fois que l’appareil de hello est remis en ligne, ces modifications sont synchronisées avec le service distant hello.

Dans ce didacticiel, mettre à jour de projet d’application hello Xamarin.iOS de [créer une application iOS de Xamarin] toosupport hello des fonctions hors connexion des applications mobiles Azure. Si vous n’utilisez pas hello téléchargé le projet de démarrage rapide de serveur, vous devez ajouter des packages d’extension hello données accès à votre projet. Pour plus d’informations sur les packages d’extension de serveur, consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn en savoir plus sur la fonctionnalité de synchronisation hors connexion hello, consultez rubrique de hello [synchronisation des données hors connexion dans les applications mobiles Azure].

## <a name="update-hello-client-app-toosupport-offline-features"></a>Mettre à jour des fonctions hors connexion hello client application toosupport
Les fonctionnalités en mode hors connexion de l’application Mobile Azure permettent de toointeract avec une base de données local lorsque vous êtes dans un scénario hors connexion. l’initialisation de ces fonctionnalités dans votre application, toouse un [SyncContext] magasin local de tooa. Faire référence à la table via l’interface de hello [IMobileServiceSyncTable]. SQLite est utilisé comme magasin local hello périphérique de hello.

1. Gestionnaire de package NuGet hello ouvert dans le projet hello que vous avez hello [créer une application iOS de Xamarin] didacticiel, puis recherchez et installez hello **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package.
2. Ouvrir le fichier de QSTodoService.cs hello et supprimez les commentaires hello `#define OFFLINE_SYNC_ENABLED` définition.
3. Regénérez et exécutez l’application cliente de hello. application Hello fonctionne hello même tel qu’il le faisait avant que vous avez activé la synchronisation hors connexion. Toutefois, base de données locale hello est maintenant remplie avec les données qui peuvent être utilisées dans un scénario hors connexion.

## <a name="update-sync"></a>Mettre à jour toodisconnect d’application hello de hello principal
Dans cette section, vous rompez hello connexion tooyour Mobile application back-end toosimulate une situation hors connexion. Lorsque vous ajoutez des éléments de données, votre gestionnaire d’exception vous indique cette application hello est en mode hors connexion. Dans cet état, les nouveaux éléments ajoutés dans hello local stockent et seront synchronisées pour hello principal de l’application mobile lors de la prochaine exécution push dans l’état connecté.

1. Modifier QSToDoService.cs dans le projet partagé de hello. Hello de modification **applicationURL** URL non valide de toopoint tooan :

         const string applicationURL = @"https://your-service.azurewebsites.fail";

    Vous pouvez également montrer le comportement en mode hors connexion en désactivant des Wi-Fi et les réseaux cellulaires sur l’appareil de hello ou à l’aide du mode avion.
2. Générez et exécutez l’application hello. Notez que la synchronisation a échoué lors de l’actualisation lorsque hello application lancée.
3. Entrez de nouveaux éléments et notez que l’opération d’envoi échoue avec un état [CancelledByNetworkError] chaque fois que vous cliquez sur **Enregistrer**. Toutefois, les nouveaux éléments de tâche hello existent dans le magasin local de hello jusqu'à ce que le serveur principal d’application mobile toohello elles peuvent être appliquées.  Dans une production application, si vous supprimez ces exceptions hello client application se comporte comme s’il est toujours connecté principal d’application mobile toohello.
4. Fermez l’application hello et redémarrez-le tooverify que hello nouveaux éléments que vous avez créé sont magasin local de toohello persistante.
5. (Facultatif) Si Visual Studio est installé sur votre PC, ouvrez l’**Explorateur de serveurs**. Accédez de la base de données tooyour dans **Azure**-> **bases de données SQL**. Cliquez avec le bouton droit sur votre base de données, puis sélectionnez **Ouvrir dans l’Explorateur d’objets SQL Server**. Vous pouvez maintenant rechercher table de base de données SQL tooyour et son contenu. Vérifiez que les données de salutation dans la base de données principale hello n’a pas changé.
6. (Facultatif) Utiliser un outil REST tel que Fiddler ou Postman tooquery votre serveur principal mobile, à l’aide d’une requête GET sous la forme `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.

## <a name="update-online-app"></a>Mettre à jour hello application tooreconnect votre serveur principal de l’application Mobile
Dans cette section, reconnectez le serveur principal d’application mobile hello application toohello. Cela simule l’application hello déplacement d’un état en ligne tooan d’état hors connexion avec le serveur principal d’application mobile hello.   Si vous simulé rupture de réseau hello en désactivant la connectivité réseau, aucune modification de code n’est nécessaires.
Réactiver les réseau hello.  Lorsque vous exécutez tout d’abord des application hello, hello `RefreshDataAsync` méthode est appelée. Cette action appelle à son tour `SyncAsync` toosync local stocker avec la base de données principale hello.

1. Ouvrez QSToDoService.cs dans le projet partagé de hello et annuler votre modification de hello **applicationURL** propriété.
2. Regénérez et exécutez l’application hello. Hello application à synchroniser vos modifications locales avec le serveur principal de l’application Mobile Azure hello à l’aide d’opérations push et pull lorsque hello `OnRefreshItemsSelected` méthode s’exécute.
3. (Facultatif) Hello d’affichage mis à jour les données à l’aide de l’Explorateur d’objets SQL Server ou d’un outil REST, comme Fiddler. Les données de salutation avis a été synchronisées entre la base de données principale de l’application Mobile Azure hello et magasin local de hello.
4. Dans l’application hello, cliquez sur Rechercher de hello zone en regard de quelques éléments toocomplete les dans le magasin local de hello.

   `CompleteItemAsync`appels `SyncAsync` élément toosync chaque s’est terminée avec le serveur principal de l’application Mobile hello. `SyncAsync` appelle des opérations Push et Pull.
   **Chaque fois que vous exécutez une extraction sur une table pour ce client hello a apporté des modifications à, un push sur le contexte de synchronisation hello client est toujours exécuté en premier automatiquement**. push implicite de Hello garantit que toutes les tables dans le magasin local de hello, ainsi que les relations restent cohérentes. Pour plus d’informations, consultez la page [synchronisation des données hors connexion dans les applications mobiles Azure].

## <a name="review-hello-client-sync-code"></a>Passez en revue le code de synchronisation hello client
projet de client Hello Xamarin que vous avez téléchargé lorsque vous terminé le didacticiel de hello [créer une application iOS de Xamarin] contient déjà du code prenant en charge la synchronisation hors connexion à l’aide d’une base de données local SQLite. Voici une brève vue d’ensemble de ce qui est déjà inclus dans le code de didacticiel hello. Pour une vue d’ensemble conceptuelle de la fonctionnalité de hello, consultez [synchronisation des données hors connexion dans les applications mobiles Azure].

* Avant de pouvoir effectuer des opérations de table, le magasin local de hello doit être initialisé. Hello base de données du magasin local est initialisé lorsque `QSTodoListViewController.ViewDidLoad()` exécute `QSTodoService.InitializeStoreAsync()`. Cette méthode crée une nouvelle base de SQLite locale à l’aide de hello `MobileServiceSQLiteStore` classe fournie par le client de l’application Mobile Azure hello SDK.

    Hello `DefineTable` méthode crée une table dans le magasin local hello qui correspond aux champs hello dans le type de hello fourni, `ToDoItem` dans ce cas. type de Hello ne tooinclude toutes les colonnes hello qui se trouvent dans la base de données distante hello. Il est possible toostore uniquement un sous-ensemble de colonnes.

        // QSTodoService.cs

        public async Task InitializeStoreAsync()
        {
            var store = new MobileServiceSQLiteStore(localDbPath);
            store.DefineTable<ToDoItem>();

            // Uses hello default conflict handler, which fails on conflict
            await client.SyncContext.InitializeAsync(store);
        }
* Hello `todoTable` membre `QSTodoService` est Hello `IMobileServiceSyncTable` de type au lieu de `IMobileServiceTable`. Hello IMobileServiceSyncTable dirige toutes les créer, lire, mettre à jour et supprimer (CRUD) opérations de table toohello magasin local de base de données.

    Vous décidez lorsque ces modifications sont envoyées principal de l’application Mobile Azure toohello en appelant `IMobileServiceSyncContext.PushAsync()`. Hello contexte de synchronisation permet de conserver les relations entre les tables en effectuant le suivi en exécutant un push des modifications dans toutes les tables, une application cliente a modifié lorsque `PushAsync` est appelée.

    appels de code Hello fourni `QSTodoService.SyncAsync()` toosync chaque fois que hello todoitem de la liste est actualisée ou un objet todoitem est ajouté ou s’est terminé. L’application se synchronise après chaque modification locale. Si une extraction est exécutée sur une table qui est en attente de mises à jour locales suivi par le contexte de hello, cette opération d’extraction déclenchera automatiquement un push de contexte tout d’abord.

    Dans le code hello fourni, tous les enregistrements hello distant `TodoItem` table sont interrogées, mais il est également possible de toofilter enregistrements en passant un id de requête et une requête trop`PushAsync`. Pour plus d’informations, consultez la section de hello *synchronisation incrémentielle* dans [synchronisation des données hors connexion dans les applications mobiles Azure].

        // QSTodoService.cs
        public async Task SyncAsync()
        {
            try
            {
                await client.SyncContext.PushAsync();
                await todoTable.PullAsync("allTodoItems", todoTable.CreateQuery()); // query ID is used for incremental sync
            }

            catch (MobileServiceInvalidOperationException e)
            {
                Console.Error.WriteLine(@"Sync Failed: {0}", e.Message);
            }
        }

## <a name="additional-resources"></a>Ressources supplémentaires
* [synchronisation des données hors connexion dans les applications mobiles Azure]
* [SDK HOWTO Azure Mobile Apps .NET][8]

<!-- Images -->

<!-- URLs. -->
[créer une application iOS de Xamarin]: app-service-mobile-xamarin-ios-get-started.md
[synchronisation des données hors connexion dans les applications mobiles Azure]: app-service-mobile-offline-data-sync.md
[SyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
