---
title: aaaEnable la synchronisation hors connexion pour votre application Mobile de Azure (Android)
description: "Découvrez comment toouse App Service Mobile Apps toocache et la synchronisation de données hors connexion dans votre application Android"
documentationcenter: android
author: ggailey777
manager: syntaxc4
services: app-service\mobile
ms.assetid: 32a8a079-9b3c-4faf-8588-ccff02097224
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 34508c7394610cf9127e1753637940826b8fd06a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-android-mobile-app"></a>Activation de la synchronisation hors connexion pour votre application mobile Android
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel décrit la fonctionnalité de synchronisation hors connexion hello des applications mobiles Azure pour Android. Synchronisation hors connexion permet toointeract des utilisateurs finaux avec une application mobile&mdash;affichage, l’ajout ou la modification des données&mdash;même quand il n’existe aucune connexion réseau. Les modifications sont stockées dans une base de données locale. Une fois que l’appareil de hello est remis en ligne, ces modifications sont synchronisées avec le serveur principal à distance hello.

S’il s’agit de votre première expérience avec les applications mobiles Azure, vous devez d’abord terminer didacticiel de hello [créer une application Android]. Si vous n’utilisez pas hello téléchargé le projet de démarrage rapide de serveur, vous devez ajouter projet tooyour de packages d’extension hello données access. Pour plus d’informations sur les packages d’extension de serveur, consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn en savoir plus sur la fonctionnalité de synchronisation hors connexion hello, consultez rubrique de hello [synchronisation des données hors connexion dans les applications mobiles Azure].

## <a name="update-hello-app-toosupport-offline-sync"></a>Mettre à jour de la synchronisation hors connexion des toosupport application hello
Avec la synchronisation hors connexion, vous lecture/écriture de tooand à partir d’un *table de synchronisation* (à l’aide de hello *IMobileServiceSyncTable* interface), qui fait partie d’un **SQLite** base de données sur votre appareil.

les modifications toopush et par extraction de données entre les périphériques hello et Azure Mobile Services, vous utilisez un *contexte de synchronisation* (*MobileServiceClient.SyncContext*), qui vous initialisez avec la base de données locale hello données toostore localement.

1. Dans `TodoActivity.java`, commentez la définition existante de hello de `mToDoTable` et supprimez les commentaires de version de la table hello synchronisation :
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. Bonjour `onCreate` méthode, commentez l’initialisation d’existant hello de `mToDoTable` et supprimez les commentaires de cette définition :
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. Dans `refreshItemsFromTable` Commentez la définition de hello de `results` et supprimez les commentaires de cette définition :
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. Commentez la définition de hello de `refreshItemsFromMobileServiceTable`.
5. Supprimez les commentaires de la définition de hello de `refreshItemsFromMobileServiceTableSyncTable`:
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync hello data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. Supprimez les commentaires de la définition de hello de `sync`:
   
        private AsyncTask<Void, Void, Void> sync() {
            AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
                @Override
                protected Void doInBackground(Void... params) {
                    try {
                        MobileServiceSyncContext syncContext = mClient.getSyncContext();
                        syncContext.push().get();
                        mToDoTable.pull(null).get();
                    } catch (final Exception e) {
                        createAndShowDialogFromTask(e, "Error");
                    }
                    return null;
                }
            };
            return runAsyncTask(task);
        }

## <a name="test-hello-app"></a>Application de test hello
Dans cette section, vous testez le comportement de hello avec Wi-Fi sur et mettez hors tension Wi-Fi toocreate un scénario hors connexion.

Lorsque vous ajoutez des éléments de données, elles sont conservées dans le magasin de SQLite hello local, mais pas synchronisés toohello des services mobiles jusqu'à ce que vous appuyez sur hello **Actualiser** bouton. Autres applications peuvent avoir des exigences différentes concernant lorsque les données doivent toobe synchronisé, mais à des fins de démonstration ce didacticiel propose hello demander explicitement.

Lorsque vous appuyez sur ce bouton, une nouvelle tâche en arrière-plan démarre. Il transmet d’abord toutes les modifications apportées toohello magasin local à l’aide du contexte de synchronisation, puis extrait tous les modifié des données à partir de la table locale de toohello Azure.

### <a name="offline-testing"></a>Test hors connexion
1. Appareil de hello sur place ou le simulateur dans *Mode avion*. Cela crée un scénario hors connexion.
2. Ajoutez des *tâches* , ou marquez-en certaines comme terminées. Quittez hello appareil ou simulateur (ou application hello fermeture forcée) et redémarrez. Vérifiez que vos modifications ont été rendues persistantes sur l’appareil de hello, car ils sont conservés dans le magasin de SQLite hello local.
3. Afficher le contenu de hello Hello Azure *TodoItem* telles que la table avec un outil SQL *SQL Server Management Studio*, ou un client REST comme *Fiddler* ou  *Postman*. Vérifiez que de nouveaux éléments de hello *pas* été synchronisés toohello server
   
       + Pour un service principal Node.js, consultez toohello [portail Azure](https://portal.azure.com/), dans votre application Mobile sur principal **Tables facile** > **TodoItem** contenu de hello tooview Hello `TodoItem` table.
       + Pour un service principal .NET, table hello d’affichage de contenu avec un outil SQL comme *SQL Server Management Studio*, ou un client REST comme *Fiddler* ou *Postman*.
4. Activer Wi-Fi dans le simulateur ou l’appareil de hello. Ensuite, appuyez sur hello **Actualiser** bouton.
5. Affichez de nouveau les données de salutation TodoItem Bonjour portail Azure. Hello que nouvelles et modifiées TodoItems doit maintenant apparaître.

## <a name="additional-resources"></a>Ressources supplémentaires
* [synchronisation des données hors connexion dans les applications mobiles Azure]
* [Couverture du cloud : La synchronisation hors connexion dans Services mobiles Azure] \(Remarque : hello vidéo se trouve sur les Services mobiles, mais la synchronisation hors connexion fonctionne de façon similaire dans les applications mobiles Azure\)

<!-- URLs. -->

[synchronisation des données hors connexion dans les applications mobiles Azure]: app-service-mobile-offline-data-sync.md

[créer une application Android]: app-service-mobile-android-get-started.md

[Couverture du cloud : La synchronisation hors connexion dans Services mobiles Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

