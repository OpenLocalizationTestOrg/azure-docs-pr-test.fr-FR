---
title: authentification aaaAdd sur Apache Cordova avec les applications mobiles | Documents Microsoft
description: "Découvrez comment toouse applications mobiles dans les utilisateurs de tooauthenticate Azure App Service de votre application Apache Cordova via une variété de fournisseurs d’identité, y compris de Google, Facebook, Twitter et Microsoft."
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 10dd6dc9-ddf5-423d-8205-00ad74929f0d
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 61a05c5ac67fd0f0bc4c9d6920954a9b464a0a8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-apache-cordova-app"></a>Ajouter une application de l’authentification tooyour Apache Cordova
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a>Résumé
Dans ce didacticiel, vous ajoutez le projet de démarrage rapide de l’authentification toohello todolist sur Apache Cordova à l’aide d’un fournisseur d’identité pris en charge. Ce didacticiel est basé sur hello [prise en main les applications mobiles] didacticiel, vous devez effectuer en premier.

## <a name="register"></a>Inscrire votre application pour l’authentification et de configurer hello du Service d’applications
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[Regarder une vidéo montrant des étapes similaires](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <a name="permissions"></a>Restreindre les autorisations des utilisateurs tooauthenticated
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

Maintenant, vous pouvez vérifier que ce principal de tooyour l’accès anonyme a été désactivé. Dans Visual Studio :

* Projet ouvert hello que vous avez créé lorsque vous avez rempli le didacticiel de hello [prise en main les applications mobiles].
* Exécutez votre application dans hello **émulateur Android de Google**.
* Vérifiez qu’une défaillance inattendue de la connexion n’est affichée après le démarrage de l’application hello.

Ensuite, mettez à jour les utilisateurs de hello application tooauthenticate avant de demander des ressources à partir du serveur principal de l’application Mobile hello.

## <a name="add-authentication"></a>Ajouter une application de toohello d’authentification
1. Ouvrez votre projet dans **Visual Studio**, puis ouvrez hello `www/index.html` fichier pour le modifier.
2. Recherchez hello `Content-Security-Policy` balise meta de section d’en-tête hello.  Ajoutez hello OAuth hôte toohello liste de sources autorisées.

   | Fournisseur | Nom du fournisseur du Kit de développement logiciel. | Hôte OAuth |
   |:--- |:--- |:--- |
   | Azure Active Directory | aad | https://login.microsoftonline.com |
   | Facebook | Facebook | https://www.facebook.com |
   | Google | Google | https://accounts.google.com |
   | Microsoft | microsoftaccount | https://login.live.com |
   | Twitter | Twitter | https://api.twitter.com |

    Voici un exemple Content-Security-Policy (implémenté pour Azure Active Directory) :

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    Remplacez `https://login.microsoftonline.com` avec hôte OAuth hello hello tableau précédent.  Pour plus d’informations sur la balise meta de stratégie de sécurité de contenu hello, consultez hello [documentation de la stratégie de sécurité de contenu].

    Certains fournisseurs d’authentification ne requièrent aucune modification Content-Security-Policy avec des appareils mobiles appropriés.  Par exemple, aucune modification de l’approche Content-Security-Policy n’est nécessaire lorsque vous recourez à l’authentification Google sur un appareil Android.

3. Ouvrez hello `www/js/index.js` pour la modification du fichier, recherchez hello `onDeviceReady()` (méthode), et en cours de création de client hello code ajouter hello suivant de code :

        // Login toohello service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    Ce code remplace le code d’existant hello qui crée la référence de table hello et actualise hello l’interface utilisateur.

    méthode de login() Hello démarre l’authentification avec le fournisseur de hello. méthode de login() Hello est une fonction async qui retourne une promesse de JavaScript.  rest Hello de l’initialisation de hello est placé dans la réponse de promesse hello afin qu’il n’est pas exécuté tant que hello login() méthode se termine.

4. Dans le code hello que vous venez d’ajouter, remplacer `SDK_Provider_Name` par nom de hello de votre fournisseur de connexion. Par exemple, pour Azure Active Directory, utilisez `client.login('aad')`.
5. Exécutez votre projet.  Lorsque le projet de hello a terminé l’initialisation, votre application montre la page de connexion OAuth hello pour hello choisi le fournisseur d’authentification.

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus [À propos de l’authentification] avec Azure App Service.
* Continuer le didacticiel de hello en ajoutant [des Notifications Push] tooyour Apache Cordova application.

Découvrez comment toouse hello kits de développement logiciel.

* [Kit de développement logiciel (SDK) Apache Cordova]
* [Kit de développement logiciel du serveur ASP.NET]
* [Kit de développement logiciel du serveur Node.js]

<!-- URLs. -->
[prise en main les applications mobiles]: app-service-mobile-cordova-get-started.md
[documentation de la stratégie de sécurité de contenu]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html
[des Notifications Push]: app-service-mobile-cordova-get-started-push.md
[À propos de l’authentification]: app-service-mobile-auth.md
[Kit de développement logiciel (SDK) Apache Cordova]: app-service-mobile-cordova-how-to-use-client-library.md
[Kit de développement logiciel du serveur ASP.NET]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Kit de développement logiciel du serveur Node.js]: app-service-mobile-node-backend-how-to-use-server-sdk.md
