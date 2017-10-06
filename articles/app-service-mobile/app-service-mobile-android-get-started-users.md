---
title: authentification aaaAdd sur Android avec des applications mobiles | Documents Microsoft
description: "Découvrez comment toouse hello fonctionnalité des applications mobiles des utilisateurs de tooauthenticate Azure App Service de votre application Android via une variété de fournisseurs d’identité, y compris de Google, Facebook, Twitter et Microsoft."
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 1fc8e7c1-6c3c-40f4-9967-9cf5e21fc4e1
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 01f608f996c931c643790ed2778df11cf590c903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-android-app"></a>Ajouter une application Android de l’authentification tooyour
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a>Résumé
Dans ce didacticiel, vous ajoutez le projet de démarrage rapide de l’authentification toohello todolist sur Android à l’aide d’un fournisseur d’identité pris en charge. Ce didacticiel est basé sur hello [prise en main les applications mobiles] didacticiel, vous devez effectuer en premier.

## <a name="register"></a>Inscription de votre application pour l’authentification et configuration d’Azure App Service
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Ajouter votre URL de redirection externe d’autorisé toohello application

L’authentification sécurisée nécessite de définir un nouveau schéma d’URL pour votre application. Cela permet de hello authentification système tooredirect tooyour arrière application une fois le processus d’authentification hello est terminée. Dans ce didacticiel, nous utilisons le modèle d’URL hello _appname_ dans l’ensemble. Toutefois, vous pouvez utiliser le schéma d’URL de votre choix. Il doit être unique tooyour des applications mobiles. redirection de hello tooenable côté serveur de hello :

1. Bonjour [Azure portal], sélectionnez votre application de Service.

2. Cliquez sur hello **l’authentification / autorisation** option de menu.

3. Bonjour **autorisé des URL de redirection externe**, entrez `appname://easyauth.callback`.  Hello _appname_ dans cette chaîne est hello le modèle d’URL pour votre application mobile.  Elle doit être conforme à la spécification d’URL normale pour un protocole (utiliser des lettres et des chiffres uniquement et commencer par une lettre).  Vous devez vous note de la chaîne hello que vous choisissez car vous en aurez besoin tooadjust votre code d’application mobile avec hello modèle d’URL à plusieurs endroits.

4. Cliquez sur **OK**.

5. Cliquez sur **Enregistrer**.

## <a name="permissions"></a>Restreindre les autorisations des utilisateurs tooauthenticated
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* Dans Android Studio, ouvrez le projet hello avec le didacticiel de hello [prise en main les applications mobiles]. À partir de hello **exécuter** menu, cliquez sur **exécuter application**et vérifiez qu’une exception non gérée avec un code d’état de 401 (non autorisé) est déclenchée après le démarrage de l’application hello.

     Cette exception se produit, car les tentatives d’application hello tooaccess hello retour comme un utilisateur non authentifié, mais hello *TodoItem* table requiert l’authentification.

Ensuite, vous mettre à jour les utilisateurs de hello application tooauthenticate avant de demander des ressources à partir de hello de fin dans les applications mobiles. 

## <a name="add-authentication-toohello-app"></a>Ajouter une application de toohello d’authentification
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <a name="cache-tokens"></a>Mettre en cache des jetons d’authentification sur le client de hello
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous terminé ce didacticiel de l’authentification de base, pensez à poursuivre sur tooone Hello suivant didacticiels :

* [Ajouter une application Android de push notifications tooyour](app-service-mobile-android-get-started-push.md).
  Découvrez comment tooconfigure vos applications mobiles sauvegarder terminer les notifications push toosend toouse Azure notification hubs.
* [Activation de la synchronisation hors connexion pour votre application Android](app-service-mobile-android-get-started-offline-data.md).
  Découvrez comment tooadd hors connexion prennent en charge tooyour application à l’aide d’un principal des applications mobiles. La synchronisation hors connexion permet aux utilisateurs d’interagir avec une application mobile &mdash;pour afficher, ajouter ou modifier des données&mdash;, même lorsqu’il n’existe aucune connexion réseau.

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions tooauthenticated users]: #permissions
[Add authentication toohello app]: #add-authentication
[Store authentication tokens on hello client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
[prise en main les applications mobiles]: app-service-mobile-android-get-started.md
