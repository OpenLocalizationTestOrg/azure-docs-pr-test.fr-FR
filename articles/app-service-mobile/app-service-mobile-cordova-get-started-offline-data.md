---
title: aaaEnable la synchronisation hors connexion pour votre application Mobile de Azure (Cordova) | Documents Microsoft
description: "Découvrez comment toouse l’application Mobile App Service toocache et la synchronisation de données hors connexion dans votre application Cordova"
documentationcenter: cordova
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 1a3f685d-f79d-4f8b-ae11-ff96e79e9de9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-cordova-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 4e6ae96c3d96dac8ebb3749354b83a04686831b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a>Activation de la synchronisation hors connexion pour votre application mobile Cordova
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

Ce didacticiel présente la fonctionnalité de synchronisation hors connexion hello des applications mobiles Azure pour Cordova. Synchronisation hors connexion permet toointeract des utilisateurs finaux avec une application mobile&mdash;affichage, l’ajout ou la modification des données&mdash;même quand il n’existe aucune connexion réseau. Les modifications sont stockées dans une base de données locale.  Une fois que l’appareil de hello est remis en ligne, ces modifications sont synchronisées avec le service distant hello.

Ce didacticiel est basé sur hello solution de démarrage rapide de Cordova pour des applications mobiles que vous créez lorsque vous terminez hello didacticiel [démarrage rapide d’Apache Cordova]. Dans ce didacticiel, vous mettez à jour hello quickstart solution tooadd des fonctions hors connexion des applications mobiles Azure.  Nous avons également en surbrillance code hors connexion spécifiques de hello dans l’application hello.

toolearn en savoir plus sur la fonctionnalité de synchronisation hors connexion hello, consultez rubrique de hello [synchronisation des données hors connexion dans les applications mobiles Azure]. Pour plus d’informations d’utilisation de l’API, consultez hello [documentation de l’API](https://azure.github.io/azure-mobile-apps-js-client).

## <a name="add-offline-sync-toohello-quickstart-solution"></a>Ajouter la solution de démarrage rapide de toohello de synchronisation hors connexion
code de synchronisation hors connexion Hello doit être ajouté toohello application. Synchronisation hors connexion requiert un plug-in cordova-sqlite-stockage hello qui est automatiquement ajouté tooyour application lorsque le plug-in des applications mobiles Azure hello est inclus dans le projet de hello. projet de démarrage rapide de Hello inclut les deux de ces plug-ins.

1. Dans l’Explorateur de solutions de Visual Studio, ouvrez index.js et remplacez hello suivant de code

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable;      // Reference tooa table endpoint on backend

    par ce code :

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable,      // Reference tooa table endpoint on backend
           syncContext;        // Reference toooffline data sync context

2. Ensuite, remplacez hello suivant de code :

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    par ce code :

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');
        var store = new WindowsAzure.MobileServiceSqliteStore('store.db');

        store.defineTable({
          name: 'todoitem',
          columnDefinitions: {
              id: 'string',
              text: 'string',
              complete: 'boolean',
              version: 'string'
          }
        });

        // Get hello sync context from hello client
        syncContext = client.getSyncContext();

    initialiser le magasin local de hello Hello ajouts de code précédent et définir une table locale qui correspond aux valeurs de colonne hello utilisés dans votre Azure back-end. (Vous n’avez pas besoin tooinclude toutes les valeurs de colonne dans ce code.)  Hello `version` champ est géré par le service principal mobile de hello et est utilisé pour la résolution de conflit.

    Vous obtenez un contexte de synchronisation toohello référence en appelant **getSyncContext**. Hello contexte de synchronisation permet de conserver les relations entre les tables en effectuant le suivi en exécutant un push des modifications dans toutes les tables, une application cliente a modifié lorsque `.push()` est appelée.

3. Mettre à jour des URL de l’application hello application URL tooyour l’application Mobile.

4. Ensuite, remplacez ce code :

        todoItemTable = client.getTable('todoitem'); // todoitem is hello table name

    par ce code :

        // Initialize hello sync context with hello store
        syncContext.initialize(store).then(function () {

        // Get hello local table reference.
        todoItemTable = client.getSyncTable('todoitem');

        syncContext.pushHandler = {
            onConflict: function (pushError) {
                // Handle hello conflict.
                console.log("Sync conflict! " + pushError.getError().message);
                // Update failed, revert tooserver's copy.
                pushError.cancelAndDiscard();
              },
              onError: function (pushError) {
                  // Handle hello error
                  // In hello simulated offline state, you get "Sync error! Unexpected connection failure."
                  console.log("Sync error! " + pushError.getError().message);
              }
        };

        // Call a function tooperform hello actual sync
        syncBackend();

        // Refresh hello todoItems
        refreshDisplay();

        // Wire up hello UI Event Handler for hello Add Item
        $('#add-item').submit(addItemHandler);
        $('#refresh').on('click', refreshDisplay);

    Hello précédent code initialise le contexte de synchronisation hello, puis appelle getSyncTable (au lieu de getTable) tooget une table locale toohello de référence.

    Ce code utilise hello base de données locale pour tous les créer, lire, mettre à jour et supprimer (CRUD) des opérations de table.

    Cet exemple effectue une simple gestion des erreurs sur les conflits de synchronisation. Une application réelle traiterait hello diverses erreurs telles que les conditions du réseau, le serveur est en conflit et d’autres. Pour des exemples de code, consultez hello [exemple de synchronisation hors connexion].

5. Ensuite, ajoutez cette synchronisation réels de fonction tooperform hello.

        function syncBackend() {

          // Sync local store tooAzure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from hello Azure table after syncing tooAzure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    Vous décidez lorsque toopush devient le principal de l’application Mobile toohello en appelant **syncContext.push()**. Par exemple, vous pouvez appeler **syncBackend** dans un bouton synchronisation tooa liée du Gestionnaire d’événements bouton.

## <a name="offline-sync-considerations"></a>Considérations relatives à la synchronisation hors connexion

Dans l’exemple hello, hello **push** méthode **syncContext** est appelée uniquement sur le démarrage de l’application dans la fonction de rappel hello pour la connexion.  Dans une application réelle, vous pouvez également apporter cette fonctionnalité de synchronisation déclenchée manuellement ou que hello réseau état change.

Lorsqu’une extraction est exécutée sur une table qui comporte en attente mises à jour locales suivies par le contexte de hello, qui extrait les opération automatiquement les déclencheurs de push. Lors de l’actualisation, l’ajout et la fin des éléments dans cet exemple, vous pouvez omettre hello explicite **push** appeler, dans la mesure où il peut être redondant.

Dans le code hello fourni, tous les enregistrements dans la table todoItem à distance de hello sont interrogées, mais il est également possible de toofilter enregistrements en passant un id de requête et une requête trop**push**. Pour plus d’informations, consultez la section de hello *synchronisation incrémentielle* dans [synchronisation des données hors connexion dans les applications mobiles Azure].

## <a name="optional-disable-authentication"></a>(Facultatif) Désactiver l’authentification

Si vous ne souhaitez tooset une authentification avant de tester la synchronisation hors connexion, commentez la fonction de rappel hello pour la connexion, mais laissez code hello à l’intérieur de la fonction de rappel hello pas commentée.  Après avoir commenté de lignes de connexion hello, code de hello suit :

      // Login toohello service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave hello rest of hello code in this callback function  uncommented.
                ...
        });
      // }, handleError);

Maintenant, hello application se synchronise avec hello Azure principal lorsque vous exécutez l’application hello.

## <a name="run-hello-client-app"></a>Exécuter l’application cliente de hello
La synchronisation hors connexion est maintenant activée, vous pouvez exécuter application cliente de hello au moins une fois sur chaque plateforme pour remplir la base de données du magasin local hello. Une version ultérieure, de simuler un scénario hors connexion et de modifier des données de hello dans le magasin local de hello lors de l’application hello est hors connexion.

## <a name="optional-test-hello-sync-behavior"></a>(Facultatif) Tester le comportement de synchronisation hello
Dans cette section, vous modifiez hello client projet toosimulate un scénario hors connexion à l’aide d’une URL d’application non valide pour votre serveur principal. Lorsque vous ajoutez ou modifiez des éléments de données, ces modifications sont conservées dans le magasin local, mais ne sont pas synchronisés toohello magasin de données principal jusqu'à ce que la connexion de hello est rétablie.

1. Dans l’Explorateur de solutions de hello, ouvrir le fichier de projet index.js hello et modifiez les hello application URL toopoint vers une URL non valide, comme hello suivant de code :

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. Dans index.html, mettre à jour de hello CSP `<meta>` élément avec hello même URL non valide.

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. Générer et exécuter l’application cliente de hello et notez qu’une exception est enregistrée dans la console hello lors de l’application hello tente de se synchroniser avec le serveur principal hello après la connexion. Les nouveaux éléments que vous ajoutez existent uniquement dans le magasin local de hello jusqu'à ce qu’elles sont appliquées backend mobile de toohello. Hello client application se comporte comme si elle était connectée toohello principal.

4. Fermez l’application hello et redémarrez-le tooverify que hello nouveaux éléments que vous avez créé sont magasin local de toohello persistante.

5. (Facultatif) Utilisez Visual Studio tooview votre toosee de table de base de données SQL Azure données hello dans la base de données principale hello n’a pas changé.

    Dans Visual Studio, ouvrez l' **Explorateur de serveurs**. Accédez de la base de données tooyour dans **Azure**->**bases de données SQL**. Cliquez avec le bouton droit sur votre base de données, puis sélectionnez **Ouvrir dans l’Explorateur d’objets SQL Server**. Vous pouvez maintenant rechercher table de base de données SQL tooyour et son contenu.

## <a name="optional-test-hello-reconnection-tooyour-mobile-backend"></a>(Facultatif) Test hello reconnexion tooyour backend mobile

Dans cette section, vous reconnecter hello toohello mobile serveur principal d’application, ce qui simule l’application hello revenir à un état en ligne. Lors de la connexion, les données sont synchronisés tooyour les backend mobile.

1. Rouvrez index.js et de restauration des URL de l’application hello.
2. Rouvrez index.html et corriger les URL de l’application hello Bonjour CSP `<meta>` élément.
3. Regénérez et exécutez l’application cliente de hello. application Hello tentatives toosync avec le serveur principal d’application mobile hello après la connexion. Vérifiez qu’aucune exceptions ne sont enregistrées dans la console de débogage hello.
4. (Facultatif) Hello d’affichage mis à jour les données à l’aide de l’Explorateur d’objets SQL Server ou d’un outil REST, comme Fiddler. Les données de salutation avis a été synchronisées entre la base de données principale hello et magasin local de hello.

    Notez que les données de salutation a été synchronisées entre la base de données hello et magasin local de hello et contient les éléments hello que vous avez ajouté pendant que votre application a été déconnectée.

## <a name="additional-resources"></a>Ressources supplémentaires
* [synchronisation des données hors connexion dans les applications mobiles Azure]
* [Visual Studio Tools pour Apache Cordova]

## <a name="next-steps"></a>Étapes suivantes
* Vérification des fonctionnalités de synchronisation hors connexion tels que la résolution de conflit Bonjour avancées supplémentaires [exemple de synchronisation hors connexion]
* Passez en revue la synchronisation hors connexion hello référence d’API Bonjour [documentation de l’API](https://azure.github.io/azure-mobile-apps-js-client).

<!-- ##Summary -->

<!-- Images -->

<!-- URLs. -->
[démarrage rapide d’Apache Cordova]: app-service-mobile-cordova-get-started.md
[exemple de synchronisation hors connexion]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling
[synchronisation des données hors connexion dans les applications mobiles Azure]: app-service-mobile-offline-data-sync.md
[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Adding Authentication]: app-service-mobile-cordova-get-started-users.md
[authentication]: app-service-mobile-cordova-get-started-users.md
[Work with hello .NET backend server SDK for Azure Mobile Apps]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Visual Studio Community 2015]: http://www.visualstudio.com/
[Visual Studio Tools pour Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
