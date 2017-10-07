---
title: aaaEnable la synchronisation hors connexion pour votre application Mobile de Azure (Xamarin.Forms) | Documents Microsoft
description: "Découvrez comment toouse l’application Mobile App Service toocache et la synchronisation de données hors connexion dans votre application de Xamarin.Forms"
documentationcenter: xamarin
author: ggailey777
manager: yochayk
editor: 
services: app-service\mobile
ms.assetid: acf0f874-3ea5-4410-bd22-b0e72140f3b5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: glenga
ms.openlocfilehash: 4b41404fc9507e82068fdf8aa612d57cbeb366bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a>Activer la synchronisation hors connexion pour votre application mobile Xamarin.Forms
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel présente la fonctionnalité de synchronisation hors connexion hello des applications mobiles Azure pour Xamarin.Forms. La synchronisation hors connexion permet aux utilisateurs finaux d’interagir avec une application mobile pour afficher, ajouter ou modifier des données, même lorsqu’il n’existe aucune connexion réseau. Les modifications sont stockées dans une base de données locale. Une fois que l’appareil de hello est remis en ligne, ces modifications sont synchronisées avec le service distant hello.

Ce didacticiel est basé sur hello solution de démarrage rapide de Xamarin.Forms pour les applications mobiles que vous créez lorsque vous effectuez le didacticiel [créer une application Xamarin iOS]. solution de démarrage rapide de Hello pour Xamarin.Forms contient hello code toosupport synchronisation hors connexion, qui doit juste toobe activé. Dans ce didacticiel, vous mettez à jour tooturn de solution de démarrage rapide de hello sur des fonctions hors connexion hello des applications mobiles Azure. Nous avons également en surbrillance code hors connexion spécifiques de hello dans l’application hello. Si vous n’utilisez pas de solution de démarrage rapide de hello téléchargé, vous devez ajouter le projet tooyour de packages d’extension hello données access. Pour plus d’informations sur les packages d’extension de serveur, consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure][1].

toolearn en savoir plus sur la fonctionnalité de synchronisation hors connexion hello, consultez rubrique de hello [synchronisation des données hors connexion dans les applications mobiles Azure][2].

## <a name="enable-offline-sync-functionality-in-hello-quickstart-solution"></a>Activer la fonctionnalité de synchronisation hors connexion dans la solution de démarrage rapide de hello
code de synchronisation hors connexion Hello est inclus dans le projet de hello à l’aide de directives de préprocesseur c#. Hello lorsque **hors connexion\_synchronisation\_activé** symbole est défini, ces chemins d’accès du code sont inclus dans la génération de hello. Pour les applications Windows, vous devez également installer plateforme de SQLite hello.

1. Dans Visual Studio, cliquez sur la solution de hello > **gérer les Packages NuGet pour la Solution...** , puis recherchez et installez le **Microsoft.Azure.Mobile.Client.SQLiteStore** package NuGet pour tous les projets dans la solution de hello.
2. Bonjour l’Explorateur de solutions, ouvrez le fichier de TodoItemManager.cs de hello du projet hello avec **Portable** dans nom hello, qui est un projet de bibliothèque de classes portables, puis supprimez le commentaire hello après la directive de préprocesseur :

        #define OFFLINE_SYNC_ENABLED
3. Toosupport (facultatif) les appareils Windows, installez un de hello suivant SQLite runtime packages :

   * **Windows 8.1 Runtime :** installez [SQLite pour Windows 8.1][3].
   * **Windows Phone 8.1 :** installez [SQLite pour Windows Phone 8.1][4].
   * **Plateforme Windows universelle** installer [SQLite pour hello Universal Windows universel][5].

     Bien que le démarrage rapide de hello ne contient pas un projet Windows universel, plateforme Windows universelle de hello est pris en charge avec Xamarin Forms.
4. (Facultatif) Dans chaque projet d’application Windows, cliquez sur **références** > **ajouter une référence...** , développez hello **Windows** dossier > **Extensions**.
    Activer hello approprié **SQLite pour Windows** SDK avec hello **Visual C++ Runtime pour Windows 2013** Kit de développement logiciel.
    Hello SQLite SDK noms varient légèrement avec chaque plate-forme Windows.

## <a name="review-hello-client-sync-code"></a>Passez en revue le code de synchronisation hello client
Voici une brève vue d’ensemble de ce qui est déjà inclus dans le code hello du didacticiel à l’intérieur de hello `#if OFFLINE_SYNC_ENABLED` directives. La fonctionnalité de synchronisation hors connexion est en fichier de projet TodoItemManager.cs hello dans le projet de bibliothèque de classes portables hello. Pour une vue d’ensemble conceptuelle de la fonctionnalité de hello, consultez [synchronisation des données hors connexion dans les applications mobiles Azure][2].

* Avant de pouvoir effectuer des opérations de table, le magasin local de hello doit être initialisé. base de données du magasin local Hello est initialisé dans hello **TodoItemManager** constructeur de classe à l’aide de hello suivant de code :

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    Ce code crée une nouvelle base de SQLite locale à l’aide de hello **MobileServiceSQLiteStore** classe.

    Hello **DefineTable** méthode crée une table dans le magasin local hello qui correspond aux champs hello dans le type de hello fourni.  type de Hello ne tooinclude toutes les colonnes hello qui se trouvent dans la base de données distante hello. Il est possible de toostore un sous-ensemble de colonnes.
* Hello **todoTable** champ **TodoItemManager** est un **IMobileServiceSyncTable** de type au lieu de **IMobileServiceTable**. Cette classe utilise hello base de données locale pour tous les créer, lire, mettre à jour et supprimer (CRUD) des opérations de table. Vous décidez lorsque ces modifications sont envoyées principal de l’application Mobile toohello en appelant **PushAsync** sur hello **IMobileServiceSyncContext**. Hello contexte de synchronisation permet de conserver les relations entre les tables en effectuant le suivi en exécutant un push des modifications dans une application cliente a modifié lors de toutes les tables **PushAsync** est appelée.

    suivant de Hello **SyncAsync** méthode est appelée toosync avec le serveur principal de l’application Mobile hello :

        public async Task SyncAsync()
        {
            ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

            try
            {
                await this.client.SyncContext.PushAsync();

                await this.todoTable.PullAsync(
                    "allTodoItems",
                    this.todoTable.CreateQuery());
            }
            catch (MobileServicePushFailedException exc)
            {
                if (exc.PushResult != null)
                {
                    syncErrors = exc.PushResult.Errors;
                }
            }

            // Simple error/conflict handling.
            if (syncErrors != null)
            {
                foreach (var error in syncErrors)
                {
                    if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
                    {
                        //Update failed, reverting tooserver's copy.
                        await error.CancelAndUpdateItemAsync(error.Result);
                    }
                    else
                    {
                        // Discard local change.
                        await error.CancelAndDiscardItemAsync();
                    }

                    Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.",
                        error.TableName, error.Item["id"]);
                }
            }
        }

    Cet exemple utilise la simple gestion des erreurs avec Gestionnaire de synchronisation par défaut hello. Une application réelle traiterait hello diverses erreurs telles que les conditions du réseau et le serveur est en conflit à l’aide d’un **IMobileServiceSyncHandler** mise en œuvre.

## <a name="offline-sync-considerations"></a>Considérations relatives à la synchronisation hors connexion
Dans l’exemple hello, hello **SyncAsync** méthode est appelée uniquement sur la mise en route et lorsqu’une synchronisation est demandée.  tooinitiate une synchronisation dans une application Android ou iOS, par extraction vers le bas sur la liste des éléments hello ; pour Windows, utilisez hello **synchronisation** bouton. Dans une application réelle, vous pouvez également apporter des déclencheurs de synchronisation hello lorsque l’état hello réseau change.

Lorsqu’une extraction est exécutée sur une table qui comporte en attente mises à jour locales suivies par le contexte de hello, qui extrait les opération automatiquement les déclencheurs de push de contexte précédent. Lors de l’actualisation, l’ajout et la fin des éléments dans cet exemple, vous pouvez omettre hello explicite **PushAsync** appeler.

Dans le code hello fourni, tous les enregistrements dans la table TodoItem à distance de hello sont interrogées, mais il est également possible de toofilter enregistrements en passant un id de requête et une requête trop**PushAsync**. Pour plus d’informations, consultez la section de hello *synchronisation incrémentielle* dans [synchronisation des données hors connexion dans les applications mobiles Azure][2].

## <a name="run-hello-client-app"></a>Exécuter l’application cliente de hello
Avec la synchronisation hors connexion est maintenant activée, exécutez application cliente de hello au moins une fois sur chaque base de données de plateforme toopopulate hello magasin local. Une version ultérieure, de simuler un scénario hors connexion et de modifier des données de hello dans le magasin local de hello lors de l’application hello est hors connexion.

## <a name="update-hello-sync-behavior-of-hello-client-app"></a>Mettre à jour le comportement de synchronisation hello de hello client application
Dans cette section, modifiez hello client projet toosimulate un scénario hors connexion à l’aide d’une URL d’application non valide pour votre serveur principal. Ou bien, vous pouvez désactiver les connexions réseau en déplaçant votre appareil trop « Mode avion ».  Lorsque vous ajoutez ou modifiez des éléments de données, ces modifications sont conservées dans le magasin local de hello, mais non synchronisées du magasin de données de serveur principal toohello jusqu'à ce que la connexion de hello est rétablie.

1. Bonjour l’Explorateur de solutions, ouvrez le fichier de projet de Constants.cs de hello de hello **Portable** de projet et modifier la valeur hello `ApplicationURL` URL non valide de toopoint tooan :

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. Fichier ouvert hello TodoItemManager.cs hello **Portable** de projet, puis ajoutez un **catch** pour hello base **Exception** toohello de la classe **try... catch** bloquer **SyncAsync**. Cela **catch** bloc écrit hello exception message toohello la console, comme suit :

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. Générez et exécutez l’application cliente de hello.  Ajoutez de nouveaux éléments. Notez qu’une exception est enregistrée dans la console hello pour chaque toosync tentative avec le serveur principal hello. Ces nouveaux éléments existent uniquement dans le magasin local de hello jusqu'à ce qu’elles peuvent être appliquées backend mobile de toohello. Hello client application se comporte comme si elle était toohello connecté principal, la prise en charge que tous les créent, lire, la mise à jour, les opérations de suppression (CRUD).
4. Fermez l’application hello et redémarrez-le tooverify que hello nouveaux éléments que vous avez créé sont magasin local de toohello persistante.
5. (Facultatif) Utilisez Visual Studio tooview votre toosee de table de base de données SQL Azure données hello dans la base de données principale hello n’a pas changé.

    Dans Visual Studio, ouvrez l' **Explorateur de serveurs**. Accédez de la base de données tooyour dans **Azure**->**bases de données SQL**. Cliquez avec le bouton droit sur votre base de données, puis sélectionnez **Ouvrir dans l’Explorateur d’objets SQL Server**. Vous pouvez maintenant rechercher table de base de données SQL tooyour et son contenu.

## <a name="update-hello-client-app-tooreconnect-your-mobile-backend"></a>Mettre à jour hello client application tooreconnect votre serveur principal mobile
Dans cette section, vous reconnecter hello toohello mobile serveur principal d’application, qui simule l’application hello fidéliser tooan des état en ligne. Lorsque vous effectuez le mouvement d’actualisation hello, les données sont synchronisés tooyour les backend mobile.

1. Rouvrez Constants.cs. Hello correct `applicationURL` toopoint toohello Corrigez-la.
2. Regénérez et exécutez l’application cliente de hello. application Hello tentatives toosync avec le serveur principal d’application mobile hello après le lancement. Vérifiez qu’aucune exceptions ne sont enregistrées dans la console de débogage hello.
3. (Facultatif) Hello d’affichage mis à jour les données à l’aide de l’Explorateur d’objets SQL Server ou d’un outil REST, comme Fiddler ou [Postman][6]. Les données de salutation avis a été synchronisées entre la base de données principale hello et magasin local de hello.

    Notez que les données de salutation a été synchronisées entre la base de données hello et magasin local de hello et contient les éléments hello que vous avez ajouté pendant que votre application a été déconnectée.

## <a name="additional-resources"></a>Ressources supplémentaires
* [Synchronisation des données hors connexion dans Azure Mobile Apps][2]
* [SDK HOWTO Azure Mobile Apps .NET][8]

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
