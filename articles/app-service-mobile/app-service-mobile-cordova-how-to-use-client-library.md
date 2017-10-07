---
title: "aaaHow tooUse plug-in d’Apache Cordova pour les applications mobiles Azure"
description: "Comment tooUse plug-in d’Apache Cordova pour les applications mobiles Azure"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: a56a1ce4-de0c-4f3c-8763-66252c52aa59
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: d3e0639e6478c409132af25304a2fb0f28401e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-apache-cordova-client-library-for-azure-mobile-apps"></a>La bibliothèque cliente de toouse Apache Cordova pour les applications mobiles Azure
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

Ce guide vous explique tooperform des scénarios courants utilisant hello dernières [plug-in d’Apache Cordova pour les applications mobiles Azure]. Si vous êtes tooAzure Mobile de nouvelles applications, d’abord terminer [démarrage rapide d’Azure Mobile Apps] toocreate un service principal, créez une table et télécharger un projet Apache Cordova avant génération. Dans ce guide, nous nous concentrer sur le côté client hello plug-in de Apache Cordova.

## <a name="supported-platforms"></a>Plateformes prises en charge
Ce kit de développement logiciel (SDK) prend en charge Apache Cordova 6.0.0 et version ultérieure sur les appareils iOS, Android et Windows.  prise en charge de la plateforme Hello est comme suit :

* Android API 19-24 (KitKat à Nougat).
* iOS 8.0 et versions ultérieures.
* Windows Phone 8.1.
* Plateforme Windows universelle.

## <a name="Setup"></a>Configuration et conditions préalables
Ce guide part du principe que vous avez créé un serveur principal avec une table. Ce guide part du principe que la table hello a hello même schéma en tant que tables hello dans ces didacticiels. Ce guide suppose également que vous avez ajouté le code de tooyour hello plug-in de Apache Cordova.  Si vous n'avez pas fait, vous pouvez ajouter le projet de tooyour hello Apache Cordova plug-in sur la ligne de commande hello :

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

Pour plus d’informations sur la création de [votre première application Apache Cordova], consultez la documentation officielle.

## <a name="ionic"></a>Configuration d’une application Ionic v2

configurer un projet Ionic v2 tooproperly, tout d’abord créer une application de base et ajouter le plug-in de hello Cordova :

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

Ajouter hello lignes suivantes trop`app.component.ts` objet de client toocreate hello :

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

Vous pouvez maintenant générer et exécuter des projets de hello dans le navigateur de hello :

```
ionic platform add browser
ionic run browser
```

le plug-in de Hello Azure Mobile Apps Cordova prend en charge les deux applications v1 et v2 Ionic.  Uniquement les applications de hello Ionic v2 nécessitent la déclaration supplémentaire pour hello `WindowsAzure` objet.

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <a name="auth"></a>Procédure : authentification des utilisateurs
Azure App Service prend en charge l’authentification et l’autorisation des utilisateurs d’applications par le biais de divers fournisseurs d’identité externes : Facebook, Google, compte Microsoft et Twitter. Vous pouvez définir des autorisations sur l’accès aux toorestrict de tables pour des opérations spécifiques aux utilisateurs de tooonly authentifié. Vous pouvez également utiliser l’identité hello des règles d’autorisation de tooimplement utilisateurs authentifiés dans les scripts de serveur. Pour plus d’informations, consultez hello [prise en main d’authentification] didacticiel.

Lorsque vous utilisez l’authentification dans une application Apache Cordova, hello suivant plug-ins Cordova doit être disponible :

* [cordova-plugin-device]
* [cordova-plugin-inappbrowser]

Deux flux d’authentification sont pris en charge : un flux serveur et un flux client.  flux de serveur Hello fournit expérience d’authentification la plus simple hello, car il repose sur l’interface d’authentification web du fournisseur hello. Hello flux client permet une intégration plus étroite avec des fonctionnalités spécifiques à l’appareil comme single-sign-on comme il s’appuie sur les kits de développement logiciel spécifique au fournisseur spécifique à l’appareil.

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <a name="configure-external-redirect-urls"></a>Configurer votre Mobile App Service pour les URL de redirection externes.
Plusieurs types d’applications Apache Cordova utilisent un toohandle de la fonctionnalité de bouclage Qu'oauth UI flux.  Flux OAuth UI sur localhost provoquent des problèmes, étant donné que le service d’authentification hello uniquement sait comment tooutilize votre service par défaut.  Voici quelques exemples de problèmes causés par les flux d’interface utilisateur OAuth :

* émulateur Ripple de Hello.
* Live recharger avec Ionic.
* En cours d’exécution hello backend mobile localement
* En cours d’exécution backend mobile de hello dans un autre Service d’application Azure à l’authentification en fournissant un hello.

Suivez ces tooadd instructions votre configuration de toohello paramètres locaux :

1. Connectez-vous à toohello [portail Azure]
2. Sélectionnez **toutes les ressources** ou **des Services d’application** puis cliquez sur nom hello de votre application Mobile.
3. Cliquez sur **Outils**
4. Cliquez sur **l’Explorateur de ressources** dans le menu d’observer hello, puis cliquez sur **accédez**.  Une nouvelle fenêtre ou un nouvel onglet s’ouvre.
5. Développez hello **config**, **authsettings** nœuds pour votre site de navigation de gauche hello.
6. Cliquez sur **Modifier**
7. Recherchez l’élément de « allowedExternalRedirectUrls » hello.  Elle peut être définie toonull ou un tableau de valeurs.  Modifiez toohello de valeur hello valeur suivante :

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    Remplacer les URL hello hello les URL de votre service.  Exemples « http://localhost:3000 » (pour hello Node.js exemple de service) ou « http://localhost:4400 » (pour le service d’ondulation hello).  Toutefois, ces URL est exemples - votre situation, y compris pour les services hello mentionnés dans les exemples hello, peuvent être différents.
8. Cliquez sur hello **en lecture/écriture** bouton hello en haut à droite de l’écran hello.
9. Cliquez sur hello verte **PUT** bouton.

les paramètres de Hello sont enregistrés à ce stade.  Ne fermez pas de fenêtre de navigateur hello jusqu'à la fin de paramètres de hello l’enregistrement.
Également ajouter ces paramètres CORS de bouclage URL toohello pour votre application de Service :

1. Connectez-vous à toohello [portail Azure]
2. Sélectionnez **toutes les ressources** ou **des Services d’application** puis cliquez sur nom hello de votre application Mobile.
3. Panneau de paramètres Hello s’ouvre automatiquement.  Si ce n’est pas le cas, cliquez sur **Tous les paramètres**.
4. Cliquez sur **CORS** sous le menu de hello API.
5. Entrez les URL hello que vous souhaitez tooadd dans zone de hello et appuyez sur ENTRÉE.
6. Entrez des URL supplémentaires, si nécessaire.
7. Cliquez sur **enregistrer** toosave les paramètres hello.

Il prend environ 10 à 15 secondes pour effet de tootake hello nouveaux paramètres.

## <a name="register-for-push"></a>Procédure : inscription aux notifications Push
Installer hello [push de plug-in de phonegap] toohandle les notifications push.  Ce plug-in peut être aisément ajouté à l’aide de la `cordova plugin add` commande sur la ligne de commande hello ou via le programme d’installation du plug-in Git hello dans Visual Studio.  Le code suivant dans votre application Apache Cordova inscrit votre appareil aux notifications Push :

```
var pushOptions = {
    android: {
        senderId: '<from-gcm-console>'
    },
    ios: {
        alert: true,
        badge: true,
        sound: true
    },
    windows: {
    }
};
pushHandler = PushNotification.init(pushOptions);

pushHandler.on('registration', function (data) {
    registrationId = data.registrationId;
    // For cross-platform, you can use hello device plugin toodetermine hello device
    // Best is toouse device.platform
    var name = 'gcm'; // For android - default
    if (device.platform.toLowerCase() === 'ios')
        name = 'apns';
    if (device.platform.toLowerCase().substring(0, 3) === 'win')
        name = 'wns';
    client.push.register(name, registrationId);
});

pushHandler.on('notification', function (data) {
    // data is an object and is whatever is sent by hello PNS - check hello format
    // for your particular PNS
});

pushHandler.on('error', function (error) {
    // Handle errors
});
```

Utiliser des notifications push toosend de hello Notification Hubs SDK à partir du serveur de hello.  N’envoyez jamais de notifications Push directement depuis les clients. Cette opération donc pourrait être tootrigger utilisé une attaque par déni de service par rapport aux concentrateurs de Notification ou hello PNS.  Hello PNS peut interdire le trafic de votre suite à telles attaques.

## <a name="more-information"></a>Plus d’informations

Vous pouvez trouver des informations sur les API dans notre [documentation sur les API](http://azure.github.io/azure-mobile-apps-js-client/).

<!-- URLs. -->
[portail Azure]: https://portal.azure.com
[démarrage rapide d’Azure Mobile Apps]: app-service-mobile-cordova-get-started.md
[prise en main d’authentification]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[plug-in d’Apache Cordova pour les applications mobiles Azure]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps
[votre première application Apache Cordova]: http://cordova.apache.org/#getstarted
[phonegap-facebook-plugin]: https://github.com/wizcorp/phonegap-facebook-plugin
[push de plug-in de phonegap]: https://www.npmjs.com/package/phonegap-plugin-push
[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device
[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
