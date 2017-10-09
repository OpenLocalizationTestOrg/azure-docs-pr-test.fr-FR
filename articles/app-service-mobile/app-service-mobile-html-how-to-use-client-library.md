---
title: aaaHow tooUse hello JavaScript SDK pour les applications mobiles Azure
description: Comment v tooUse pour les applications mobiles Azure
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 53b78965-caa3-4b22-bb67-5bd5c19d03c4
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 3fcbb0c5bd6918a285bdafa1946ba0bd47bb21b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-javascript-client-library-for-azure-mobile-apps"></a>Comment tooUse hello bibliothèque cliente JavaScript pour les applications mobiles Azure
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

Ce guide vous explique tooperform des scénarios courants utilisant hello dernières [JavaScript SDK pour les applications mobiles Azure]. Si vous êtes tooAzure Mobile de nouvelles applications, d’abord terminer [démarrage rapide d’Azure Mobile Apps] toocreate un serveur principal et créez une table. Dans ce guide, nous concentrer sur l’utilisation du service principal mobile de hello dans les applications Web HTML/JavaScript.

## <a name="supported-platforms"></a>Plateformes prises en charge
Nous limiter toohello en cours de la prise en charge de navigateur et le dernier versions Hello principaux navigateurs : Google Chrome, Microsoft Edge, Microsoft Internet Explorer et Mozilla Firefox.  Nous pensons que toofunction du Kit de développement logiciel hello avec n’importe quel navigateur relativement moderne.

package de Hello est distribué comme un JavaScript Module universel, afin qu’il prend en charge les variables globales, AMD, et met en forme CommonJS.

## <a name="Setup"></a>Configuration et conditions préalables
Ce guide part du principe que vous avez créé un serveur principal avec une table. Ce guide part du principe que la table hello a hello même schéma en tant que tables hello dans ces didacticiels.

L’installation Bonjour Azure Mobile Apps JavaScript SDK peut être effectuée via hello `npm` commande :

```
npm install azure-mobile-apps-client --save
```

Hello bibliothèque peut également être utilisée comme un module ES2015, au sein d’environnements CommonJS tels que Browserify et Webpack et comme une bibliothèque AMD.  Par exemple :

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

Vous pouvez également utiliser une version prégénérée de hello SDK en téléchargeant directement à partir de notre CDN :

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <a name="auth"></a>Procédure : authentification des utilisateurs
Azure App Service prend en charge l’authentification et l’autorisation des utilisateurs d’applications par le biais de divers fournisseurs d’identité externes : Facebook, Google, compte Microsoft et Twitter. Vous pouvez définir des autorisations sur l’accès aux toorestrict de tables pour des opérations spécifiques aux utilisateurs de tooonly authentifié. Vous pouvez également utiliser l’identité hello des règles d’autorisation de tooimplement utilisateurs authentifiés dans les scripts de serveur. Pour plus d’informations, consultez hello [prise en main d’authentification] didacticiel.

Deux flux d’authentification sont pris en charge : un flux serveur et un flux client.  flux de serveur Hello fournit expérience d’authentification la plus simple hello, car il repose sur l’interface d’authentification web du fournisseur hello. Hello flux client permet une intégration plus étroite avec des fonctionnalités spécifiques à l’appareil comme single-sign-on comme il s’appuie sur les kits de développement logiciel spécifique au fournisseur.

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <a name="configure-external-redirect-urls"></a>Configurer votre Mobile App Service pour les URL de redirection externes.
Plusieurs types d’applications JavaScript utilisent un toohandle de la fonctionnalité de bouclage Qu'oauth UI flux.  Ces fonctionnalités sont les suivantes :

* Exécuter votre service en local
* À l’aide de rechargement de Live avec hello infrastructure Ionic
* Redirection tooApp Service pour l’authentification.

En cours d’exécution localement peut entraîner des problèmes étant donné que, par défaut, l’authentification est uniquement du Service d’applications accès tooallow à partir de votre serveur principal de l’application Mobile. Utilisez hello suivant les étapes toochange hello d’authentification tooenable de paramètres du Service d’applications lors de l’exécution de serveur de hello localement :

1. Connectez-vous à toohello [portail Azure]
2. Accédez principal de l’application Mobile tooyour.
3. Sélectionnez **l’Explorateur de ressources** Bonjour **outils de développement** menu.
4. Cliquez sur **accédez** tooopen l’Explorateur de ressources hello pour votre serveur principal de l’application Mobile dans une fenêtre ou un nouvel onglet.
5. Développez hello **config** > **authsettings** nœud pour votre application.
6. Cliquez sur hello **modifier** bouton tooenable modification de ressource de hello.
7. Recherche hello **allowedExternalRedirectUrls** élément, qui doit être null. Ajoutez vos URL dans un tableau :

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    Remplacez l’URL hello dans le tableau de hello avec des URL de votre service, qui est dans cet exemple hello `http://localhost:3000` pour hello local Node.js exemple de service. Vous pouvez également utiliser `http://localhost:4400` pour hello Ripple URL de service ou des autres, en fonction de la configuration de votre application.
8. En hello haut hello, cliquez sur **en lecture/écriture**, puis cliquez sur **PUT** toosave vos mises à jour.

Vous devez également tooadd hello même bouclage URL toohello paramètres CORS de l’autorisation :

1. Accédez arrière toohello [portail Azure].
2. Accédez principal de l’application Mobile tooyour.
3. Cliquez sur **CORS** Bonjour **API** menu.
4. Entrez chaque URL Bonjour vide **autorisé les origines** zone de texte.  Une zone de texte est créée.
5. Cliquez sur **ENREGISTRER**

Après que hello principales mises à jour, vous serez en mesure de toouse hello nouvelles bouclage URL dans votre application.

<!-- URLs. -->
[démarrage rapide d’Azure Mobile Apps]: app-service-mobile-cordova-get-started.md
[prise en main d’authentification]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[portail Azure]: https://portal.azure.com/
[JavaScript SDK pour les applications mobiles Azure]: https://www.npmjs.com/package/azure-mobile-apps-client
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
