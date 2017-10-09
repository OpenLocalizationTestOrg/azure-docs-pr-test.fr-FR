---
title: "aaaUpgrade à partir des Services mobiles tooAzure du Service d’applications - Node.js"
description: "Découvrez comment tooeasily mettre à niveau votre tooan d’application Mobile Services application de Service d’applications mobiles"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: c58f6df0-5aad-40a3-bddc-319c378218e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 722cda244d4f633247827f58ea6f1397137ea600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-nodejs-azure-mobile-service-tooapp-service"></a>Mettre à niveau votre tooApp Node.js Azure Mobile Service existant Service
Service d’application Mobile est une nouvelle façon toobuild applications mobiles à l’aide de Microsoft Azure. toolearn, voir [quelles sont les applications mobiles ?].

Cette rubrique décrit comment tooupgrade une application de serveur principal Node.js existante à partir d’Azure Mobile Services tooa nouvelle App Service Mobile Apps. Lorsque vous exécutez cette mise à niveau, votre application Mobile Services existante peut continuer toooperate.  Si vous devez tooupgrade une application principale de Node.js, consultez trop[la mise à niveau des Services mobiles .NET votre](app-service-mobile-net-upgrading-from-mobile-services.md).

Une fois un service principal mobile tooAzure mis à niveau du Service d’applications, il a tooall d’accès aux fonctionnalités du Service de l’application et sont facturés en fonction de trop[tarification du Service d’applications], pas les Services mobiles de tarification.

## <a name="migrate-vs-upgrade"></a>Migration et mise à niveau
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> Il est recommandé d’ [effectuer une migration](app-service-mobile-migrating-from-mobile-services.md) avant une mise à niveau. De cette manière, vous pouvez placer les deux versions de votre application hello même un Plan App Service et entraîner une baisse sans coût supplémentaire.
>
>

### <a name="improvements-in-mobile-apps-nodejs-server-sdk"></a>Améliorations du Kit de développement logiciel (SDK) serveur Node.js Mobile Apps
La mise à niveau toohello nouvelle [SDK des applications mobiles](https://www.npmjs.com/package/azure-mobile-apps) fournit de nombreuses améliorations, notamment :

* En fonction de hello [Express framework](http://expressjs.com/en/index.html), nouveau nœud SDK hello est léger et conçu tookeep configuration avec les nouvelles versions de nœud de leur. Vous pouvez personnaliser le comportement de l’application hello avec Express intergiciel (middleware).
* Améliorations significatives des performances par rapport à toohello Kit de développement logiciel de Mobile Services.
* Vous pouvez maintenant héberger un site Web avec votre serveur principal mobile ; de même, il s’agit de tooany-application de express.v4 existant tooadd facile hello Mobile Azure SDK.
* Conçu pour le développement multiplateforme et local, hello SDK des applications mobiles peut être développé et exécuté localement sur les plateformes Windows, Linux et OS x. Il est désormais facile toouse nœud développement des techniques courantes comme en cours d’exécution [Mocha](https://mochajs.org/) toodeployment préalable des tests.

## <a name="overview"></a>Présentation de la mise à niveau de base
tooaid la mise à niveau d’un service principal Node.js, Azure App Service a fourni un package de compatibilité.  Après la mise à niveau, vous aurez un site niew qui peut être déployé tooa nouveau site de Service d’applications.

sont des kits de développement logiciel client des Services mobiles Hello **pas** compatibles avec les serveurs d’applications mobiles nouvelle hello Kit de développement logiciel. Dans la continuité des activités tooprovide de commande de service pour votre application, vous ne devez pas publier site tooa de modifications actuellement le clients publiées. Vous devez plutôt créer une application mobile qui sert de doublon. Vous pouvez placer cette application sur hello du Service d’applications plan tooavoid encourir le coût financier supplémentaire.

Vous aurez alors deux versions de l’application hello : qui reste hello même et sert des applications publiées dans hello générique et autres dont vous pouvez ensuite mettre à niveau et cible avec un nouveau client mise à jour. Vous pouvez déplacer et tester votre code à votre rythme, mais vous devez vous assurer que tous les correctifs de bogue que vous apportez obtenir tooboth appliqué. Une fois que vous pensez qu’un nombre souhaité d’applications de client dans la nature ont mis à jour la version la plus récente toohello, vous pouvez supprimer l’application hello de migrées d’origine si vous le souhaitez. Elle n’entraîne des coûts supplémentaires monétaires, si hébergé dans hello du Service d’applications plan en tant que votre application Mobile.

structure complète de Hello pour le processus de mise à niveau hello est la suivante :

1. Téléchargez votre projet Azure Mobile Service existant (migré).
2. Convertir hello projet tooan l’application Mobile Azure à l’aide du package de compatibilité hello.
3. Corrigez les éventuelles différences (par exemple les paramètres d’authentification).
4. Déployer votre tooa de projet converti de l’application Mobile Azure nouveau Service d’application.
5. Diffuse une nouvelle version de votre application cliente qu’utilisation hello nouvelle application Mobile.
6. (Facultatif) Supprimez l’application de service mobile d’origine migrée.

La suppression peut se produire si vous ne voyez pas de trafic sur votre service mobile d’origine migré.

## <a name="install-npm-package"></a>Installer les composants requis pour hello
Vous devez installer [Node] sur votre ordinateur local  Vous devez également installer le package de compatibilité hello.  Une fois que le nœud est installé, vous pouvez exécuter hello de commande suivante à partir d’un nouveau cmd ou d’une invite de PowerShell :

```npm i -g azure-mobile-apps-compatibility```

## <a name="obtain-ams-scripts"></a> Obtenir vos scripts Azure Mobile Services
* Connectez-vous à toohello [Azure Portal].
* Dans **Toutes les ressources** ou **App Services**, recherchez votre site Mobile Services.
* Au sein du site de hello, cliquez sur **outils** -> **Kudu** -> **accédez** site de Kudu tooopen hello.
* Cliquez sur **Console de débogage** -> **PowerShell** console de débogage tooopen hello.
* Accédez trop`site/wwwroot/App_Data/config` en cliquant sur chaque répertoire à son tour
* Cliquez sur hello téléchargement icône suivant toohello `scripts` active.

Cela télécharge les scripts hello au format ZIP.  Créer un répertoire sur votre ordinateur local et décompressez hello `scripts.ZIP` fichier dans le répertoire de hello.  Le répertoire `scripts` est alors créé.

## <a name="scaffold-app"></a>Une vue de structure hello nouvelles applications mobiles Azure principal
Exécutez hello de commande suivante à partir du répertoire hello contenant le répertoire de scripts hello :

```scaffold-mobile-app scripts out```

Cette opération crée un serveur d’applications mobiles Azure avec génération de modèles principal Bonjour `out` active.  Mais non obligatoire, il s’agit d’un Bonjour de toocheck conseillé `out` répertoire dans un référentiel de code source de votre choix.

## <a name="deploy-ama-app"></a> Déployer votre backend Azure Mobile Apps
Pendant le déploiement, vous devrez suivant de hello toodo :

1. Créer une application Mobile Bonjour [Azure Portal].
2. Exécutez hello `createViews.sql` script sur votre base de données connectée.
3. Lien hello base de données qui est lié tooyour Service Mobile tooyour nouveau Service d’application.
4. Lier n’importe quel autre toohello de ressources (telles que des concentrateurs de Notification) nouveau Service d’application.
5. Déployer le nouveau site hello généré code tooyour.

### <a name="create-a-new-mobile-app"></a>Créer une application Mobile App
1. Connectez-vous à l’adresse hello [Azure Portal].
2. Cliquez sur **+NOUVEAU** > **Web + Mobile** > **Application mobile**, puis indiquez le nom de votre serveur principal Mobile App.
3. Pourquoi **groupe de ressources**, sélectionnez un groupe de ressources existant ou créez-en un nouveau (à l’aide de hello même nom que votre application).

    Sélectionnez un autre plan App Service ou créez-en un. Pour plus d’informations sur les plans de Services d’application et comment toocreate un nouveau plan dans différents tarifs de couche et dans l’emplacement souhaité, consultez [vue d’ensemble approfondie des plans de Service d’applications Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
4. Pourquoi **plan App Service**, plan par défaut de hello (Bonjour [niveau Standard](https://azure.microsoft.com/pricing/details/app-service/)) est sélectionné. Vous pouvez sélectionner un autre plan ou en [créer un](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan). les paramètres du plan App Service Hello déterminent hello [emplacement, fonctionnalités, de coût et des ressources de calcul](https://azure.microsoft.com/pricing/details/app-service/) associé à votre application.

    Après avoir choisi le plan de hello, cliquez sur **créer**. Cela crée le principal de l’application Mobile hello.

### <a name="run-createviewssql"></a>Exécuter CreateViews.SQL
application de modèle généré automatiquement Hello contient un fichier appelé `createViews.sql`.  Ce script doit être exécuté sur la base de données cible.  chaîne de connexion Hello pour la base de données cible hello peut être obtenu à partir de votre service mobile migré à partir de hello **paramètres** panneau sous **les chaînes de connexion**.  Elle est nommée `MS_TableConnectionString`.

Vous pouvez exécuter ce script à partir de SQL Server Management Studio ou de Visual Studio.

### <a name="link-hello-database-tooyour-app-service"></a>Lien hello tooyour de base de données du Service d’applications
Hello de lien existant tooyour de base de données du Service d’applications :

* Bonjour [Azure Portal], ouvrez votre application de Service.
* Sélectionnez **Tous les paramètres** -> **Connexions de données**.
* Cliquez sur **+ Ajouter**.
* Dans la liste déroulante de hello, sélectionnez **base de données SQL**
* Sous **Base de données SQL**, sélectionnez votre base de données existante, puis cliquez sur **Sélectionner**.
* Sous **chaîne de connexion**, entrez hello username et password pour la base de données hello, puis cliquez sur **OK**.
* Bonjour **ajouter des connexions de données** panneau, cliquez sur **OK**.

mot de passe et le nom d’utilisateur hello sont accessibles en consultant hello chaîne de connexion pour la base de données cible hello dans votre Service Mobile migrés.

### <a name="set-up-authentication"></a>Configurer l’authentification
Azure Mobile Apps permet l’authentification Azure Active Directory, Facebook, Google, Microsoft et Twitter tooconfigure au sein du service de hello.  Authentification personnalisée devez toobe développée séparément.  Reportez-vous aux messages hello [Concepts d’authentification] documentation et [démarrage rapide de l’authentification] documentation pour plus d’informations.  

## <a name="updating-clients"></a>Mettre à jour les clients mobiles
Une fois que vous avez un serveur principal Mobile App opérationnel, vous pouvez travailler sur une nouvelle version de votre application cliente qui la consomme. Applications mobiles inclut également une nouvelle version du client de hello kits de développement logiciel et similaires toohello mise à niveau server ci-dessus, vous devez tooremove toutes les références des kits de développement de toohello Mobile Services avant d’installer les versions des applications mobiles.

Une des principales modifications de hello entre les versions de hello est que les constructeurs hello ne nécessitent plus une clé d’application.
Vous maintenant transmettez simplement l’URL de hello de votre application Mobile. Par exemple, sur les clients .NET hello, hello `MobileServiceClient` constructeur est désormais :

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net" // URL of hello Mobile App
        );

Vous pouvez lire sur l’installation hello nouveaux kits de développement logiciel et à l’aide de la nouvelle structure de hello via les liens hello ci-dessous :

* [Android version 2.2 ou ultérieure](app-service-mobile-android-how-to-use-client-library.md)
* [iOS version 3.0.0 ou ultérieure](app-service-mobile-ios-how-to-use-client-library.md)
* [.NET (Windows/Xamarin) version 2.0.0 ou ultérieure](app-service-mobile-dotnet-how-to-use-client-library.md)
* [Apache Cordova version 2.0 ou ultérieure](app-service-mobile-cordova-how-to-use-client-library.md)

Si votre application effectue utiliser de notifications push, notez hello instructions d’inscription spécifique pour chaque plate-forme, comme des modifications ont été certains il également.

Lorsque vous avez hello nouvelle version du client prêt, essayez-le par rapport à votre projet de serveur mis à niveau. Après avoir vérifié qu’il fonctionne, vous pouvez libérer une nouvelle version de toocustomers de votre application. Par la suite, une fois que vos clients ont eu une chance tooreceive ces mises à jour, vous pouvez supprimer la version des Services mobiles hello de votre application. À ce stade, vous avez mis à niveau tooan application de Service d’applications mobiles à l’aide du serveur d’applications mobiles dernière hello Kit de développement logiciel.

<!-- URLs. -->

[Portail Azure]: https://portal.azure.com/
[Azure classic portal]: https://manage.windowsazure.com/
[quelles sont les applications mobiles ?]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[Mobile App Server SDK]: https://www.npmjs.com/package/azure-mobile-apps
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure Scheduler]: /en-us/documentation/services/scheduler/
[Web Job]: ../app-service-web/websites-webjobs-resources.md
[How toouse hello .NET server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[tarification du Service d’applications]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[.NET server SDK overview]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Concepts d’authentification]: ../app-service/app-service-authentication-overview.md
[démarrage rapide de l’authentification]: app-service-mobile-auth.md

[Azure Portal]: https://portal.azure.com/
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[basicapp sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[todo sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[samples directory on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js package]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
