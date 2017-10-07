---
title: aaaEnable la synchronisation hors connexion pour votre application de plateforme Windows universelle (UWP) avec des applications mobiles | Documents Microsoft
description: "Découvrez comment toouse l’application Mobile Azure toocache et la synchronisation des données hors ligne dans votre application de plateforme Windows universelle (UWP)."
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 8fe51773-90de-4014-8a38-41544446d9b5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: a9f4ad02e92c2c423f10f07b7f1a4270aafd6c6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-windows-app"></a>Activation de la synchronisation hors connexion pour votre application Windows
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel vous montre comment tooadd hors connexion prennent en charge l’application de plateforme Windows universelle (UWP) tooa à l’aide d’un serveur principal de l’application Mobile Azure. Synchronisation hors connexion permet de toointeract des utilisateurs finaux avec une application mobile--affichage, l’ajout ou la modification de données - même quand il n’existe aucune connexion réseau. Les modifications sont stockées dans une base de données locale. Une fois que l’appareil de hello est remis en ligne, ces modifications sont synchronisées avec le serveur principal à distance hello.

Dans ce didacticiel, vous mettez à jour projet d’application UWP hello de didacticiel de hello [créer une application Windows] toosupport hello des fonctions hors connexion des applications mobiles Azure. Si vous n’utilisez pas hello téléchargé le projet de démarrage rapide de serveur, vous devez ajouter projet tooyour de packages d’extension hello données access. Pour plus d’informations sur les packages d’extension de serveur, consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn en savoir plus sur la fonctionnalité de synchronisation hors connexion hello, consultez rubrique de hello [synchronisation des données hors connexion dans les applications mobiles Azure].

## <a name="requirements"></a>Configuration requise
Ce didacticiel requiert hello suivant des conditions préalables :

* Visual Studio 2013 s’exécutant sous Windows 8.1 ou version ultérieure.
* finalisation de [Créer une application Windows][Créer une application Windows].
* [Azure Mobile Services SQLite Store][sqlite store nuget]
* [SQLite pour développement sur plateforme Windows universelle](http://www.sqlite.org/downloads)

## <a name="update-hello-client-app-toosupport-offline-features"></a>Mettre à jour des fonctions hors connexion hello client application toosupport
Les fonctionnalités en mode hors connexion de l’application Mobile Azure permettent de toointeract avec une base de données local lorsque vous êtes dans un scénario hors connexion. toouse ces fonctionnalités dans votre application, vous initialisez un [SyncContext] [ synccontext] tooa les magasin local. Puis faire référence à la table via hello [IMobileServiceSyncTable][IMobileServiceSyncTable] interface. SQLite est utilisé comme magasin local hello périphérique de hello.

1. Installer hello [runtime SQLite pour hello plateforme Windows universelle](http://sqlite.org/2016/sqlite-uwp-3120200.vsix).
2. Dans Visual Studio, ouvrez le Gestionnaire de package NuGet hello pour le projet d’application UWP hello que vous avez hello [créer une application Windows] didacticiel.
    Recherchez et installez hello **Microsoft.Azure.Mobile.Client.SQLiteStore** package NuGet.
3. Dans l’Explorateur de solutions, cliquez avec le bouton droit sur **Références** > **Ajouter une référence...** >**Windows universel**>**Extensions**, puis activez **SQLite pour plateforme Windows universelle** et **Runtime Visual C++ 2015 pour applications pour plateforme Windows universelle**.

    ![Ajouter une référence SQLite UWP][1]
4. Ouvrez le fichier de MainPage.xaml.cs hello et ne commentez pas hello `#define OFFLINE_SYNC_ENABLED` définition.
5. Dans Visual Studio, appuyez sur hello **F5** toorebuild et exécution hello client application de la clé. application Hello fonctionne hello même tel qu’il le faisait avant que vous avez activé la synchronisation hors connexion. Toutefois, base de données locale hello est maintenant remplie avec les données qui peuvent être utilisées dans un scénario hors connexion.

## <a name="update-sync"></a>Mettre à jour toodisconnect d’application hello de hello principal
Dans cette section, vous rompez hello connexion tooyour Mobile application back-end toosimulate une situation hors connexion. Lorsque vous ajoutez des éléments de données, votre gestionnaire d’exception vous indique cette application hello est en mode hors connexion. Dans cet état, les nouveaux éléments ajoutés dans hello local stockent et seront synchronisées pour hello principal de l’application mobile lors de la prochaine exécution push dans l’état connecté.

1. Modifier App.xaml.cs dans un projet partagé de hello. Commentez l’initialisation de hello Hello **MobileServiceClient** et ajoutez hello ligne, qui utilise une URL d’application mobile non valide suivante :

         public static MobileServiceClient MobileService = new MobileServiceClient("https://your-service.azurewebsites.fail");

    Vous pouvez également illustrer le comportement en mode hors connexion en désactivant le Wi-Fi et les réseaux cellulaires sur l’appareil de hello ou utiliser le mode avion.
2. Appuyez sur **F5** toobuild et exécution de l’application hello. Notez que la synchronisation a échoué lors de l’actualisation lorsque hello application lancée.
3. Entrez de nouveaux éléments et notez que l’opération Push échoue avec un état [CancelledByNetworkError] chaque fois que vous cliquez sur **Enregistrer**. Toutefois, les nouveaux éléments de tâche hello existent dans le magasin local de hello jusqu'à ce que le serveur principal d’application mobile toohello elles peuvent être appliquées.  Dans une production application, si vous supprimez ces exceptions hello client application se comporte comme s’il est toujours connecté principal d’application mobile toohello.
4. Fermez l’application hello et redémarrez-le tooverify que hello nouveaux éléments que vous avez créé sont magasin local de toohello persistante.
5. (Facultatif) Dans Visual Studio, ouvrez l’ **Explorateur de serveurs**. Accédez de la base de données tooyour dans **Azure**->**bases de données SQL**. Cliquez avec le bouton droit sur votre base de données, puis sélectionnez **Ouvrir dans l’Explorateur d’objets SQL Server**. Vous pouvez maintenant rechercher table de base de données SQL tooyour et son contenu. Vérifiez que les données de salutation dans la base de données principale hello n’a pas changé.
6. (Facultatif) Utiliser un outil REST tel que Fiddler ou Postman tooquery votre serveur principal mobile, à l’aide d’une requête GET sous la forme `https://<your-mobile-app-backend-name>.azurewebsites.net/tables/TodoItem`.

## <a name="update-online-app"></a>Mettre à jour hello application tooreconnect votre serveur principal de l’application Mobile
Dans cette section, vous reconnecter hello application toohello application mobile back-end. Ces modifications simulent une reconnexion de réseau sur l’application hello.

Lorsque vous exécutez tout d’abord des application hello, hello `OnNavigatedTo` appels du Gestionnaire d’événements `InitLocalStoreAsync`. Cette méthode appelle à son tour `SyncAsync` toosync local stocker avec la base de données principale hello. application Hello tentatives toosync au démarrage.

1. Ouvrez App.xaml.cs dans un projet partagé de hello et supprimez les commentaires de l’initialisation de votre précédente de `MobileServiceClient` URL d’application mobile toouse hello hello correct.
2. Hello de presse **F5** toorebuild et application hello d’exécution de la clé. Hello application à synchroniser vos modifications locales avec le serveur principal de l’application Mobile Azure hello à l’aide d’opérations push et pull lorsque hello `OnNavigatedTo` s’exécute le Gestionnaire d’événements.
3. (Facultatif) Hello d’affichage mis à jour les données à l’aide de l’Explorateur d’objets SQL Server ou d’un outil REST, comme Fiddler. Les données de salutation avis a été synchronisées entre la base de données principale de l’application Mobile Azure hello et magasin local de hello.
4. Dans l’application hello, cliquez sur Rechercher de hello zone en regard de quelques éléments toocomplete les dans le magasin local de hello.

   `UpdateCheckedTodoItem`appels `SyncAsync` élément toosync chaque s’est terminée avec le serveur principal de l’application Mobile hello. `SyncAsync` appelle des opérations Push et Pull. Toutefois, **chaque fois que vous exécutez une extraction sur une table client hello a apporté des modifications à, une notification push est toujours exécuté automatiquement**. Ce comportement garantit la que cohérence de toutes les tables dans le magasin local de hello, ainsi que des relations. Il peut entraîner un push inattendu.  Pour plus d’informations, consultez la page [synchronisation des données hors connexion dans les applications mobiles Azure].

## <a name="api-summary"></a>Résumé de l’API
toosupport hello des fonctions hors connexion des services mobiles, nous avons utilisé hello [IMobileServiceSyncTable] de l’interface et initialisé [MobileServiceClient.SyncContext] [ synccontext] une base de données local SQLite. Lorsque hors connexion, les opérations CRUD normales hello pour les applications mobiles fonctionnent comme si l’application hello est toujours connectée pendant hello se produisent sur le magasin local de hello. Hello méthodes suivantes est magasin local de hello toosynchronize utilisé avec le serveur de hello :

* **[PushAsync]**  , car cette méthode est un membre de [IMobileServicesSyncContext], les modifications apportées dans toutes les tables sont envoyées toohello principal. Seuls les enregistrements des modifications locales sont envoyés toohello server.
* **[PullAsync]** Une extraction (pull) est démarrée à partir d’une interface [IMobileServiceSyncTable]. Lorsqu’il existe des modifications dans la table de hello, un push implicit est exécuté toomake assurer la cohérence de toutes les tables dans le magasin local de hello, ainsi que des relations. Hello *pushOtherTables* paramètre contrôle si des autres tables dans le contexte de hello sont envoyées dans une opération de push implicite. Hello *requête* accepte un [IMobileServiceTableQuery<T> ] [ IMobileServiceTableQuery] ou hello de toofilter de chaîne de requête OData a retourné des données. Hello *queryId* sert de paramètre toodefine la synchronisation incrémentielle. Pour en savoir plus, consultez [Synchronisation des données hors connexion dans Azure Mobile Apps](app-service-mobile-offline-data-sync.md#how-sync-works).
* **[PurgeAsync]**  votre application doit appeler régulièrement cette données périmées de méthode toopurge à partir du magasin local de hello. Hello d’utilisation *forcer* paramètre lorsque vous devez toopurge toutes les modifications qui n’ont pas encore été synchronisées.

Pour plus d’informations sur ces concepts, consultez la page [Synchronisation des données hors connexion dans Azure Mobile Apps](app-service-mobile-offline-data-sync.md#how-sync-works).

## <a name="more-info"></a>En savoir plus
Hello rubriques suivantes fournissent des informations générales supplémentaires sur la fonctionnalité de synchronisation hors connexion hello des applications mobiles :

* [synchronisation des données hors connexion dans les applications mobiles Azure]
* [SDK HOWTO Azure Mobile Apps .NET][8]

<!-- Anchors. -->
[Update hello app toosupport offline features]: #enable-offline-app
[Update hello sync behavior of hello app]: #update-sync
[Update hello app tooreconnect your Mobile Apps backend]: #update-online-app
[Next Steps]:#next-steps

<!-- Images -->
[1]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/app-service-mobile-add-reference-sqlite-dialog.png
[11]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/app-service-mobile-add-wp81-reference-sqlite-dialog.png
[13]: ./media/app-service-mobile-windows-store-dotnet-get-started-offline-data/cpu-architecture.png


<!-- URLs. -->
[synchronisation des données hors connexion dans les applications mobiles Azure]: app-service-mobile-offline-data-sync.md
[Créer une application Windows]: app-service-mobile-windows-store-dotnet-get-started.md
[SQLite for Windows 8.1]: http://go.microsoft.com/fwlink/?LinkID=716919
[SQLite for Windows Phone 8.1]: http://go.microsoft.com/fwlink/?LinkID=716920
[SQLite for Windows 10]: http://go.microsoft.com/fwlink/?LinkID=716921
[synccontext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient.synccontext(v=azure.10).aspx
[sqlite store nuget]: https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client.SQLiteStore/
[IMobileServiceSyncTable]: https://msdn.microsoft.com/library/azure/mt691742(v=azure.10).aspx
[IMobileServiceTableQuery]: https://msdn.microsoft.com/library/azure/dn250631(v=azure.10).aspx
[IMobileServicesSyncContext]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.imobileservicesynccontext(v=azure.10).aspx
[MobileServicePushFailedException]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushfailedexception(v=azure.10).aspx
[Status]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushcompletionresult.status(v=azure.10).aspx
[CancelledByNetworkError]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.mobileservicepushstatus(v=azure.10).aspx
[PullAsync]: https://msdn.microsoft.com/library/azure/mt667558(v=azure.10).aspx
[PushAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.mobileservicesynccontextextensions.pushasync(v=azure.10).aspx
[PurgeAsync]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mobileservices.sync.imobileservicesynctable.purgeasync(v=azure.10).aspx
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
