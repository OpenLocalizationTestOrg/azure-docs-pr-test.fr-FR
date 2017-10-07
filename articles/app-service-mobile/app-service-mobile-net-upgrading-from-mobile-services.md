---
title: "aaaUpgrade à partir des Services mobiles tooAzure du Service d’applications"
description: "Découvrez comment tooeasily mettre à niveau votre tooan d’application Mobile Services application de Service d’applications mobiles"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 9c0ac353-afb6-462b-ab94-d91b8247322f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2b75a1b824e8ef0d36c9053f2f19af051479f928
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-net-azure-mobile-service-tooapp-service"></a>Mettre à niveau votre tooApp .NET Azure Mobile Service existant Service
Service d’application Mobile est une nouvelle façon toobuild applications mobiles à l’aide de Microsoft Azure. toolearn, voir [quelles sont les applications mobiles ?].

Cette rubrique décrit comment tooupgrade une application de serveur principal .NET existante à partir d’Azure Mobile Services tooa nouvelle App Service Mobile Apps. Lorsque vous exécutez cette mise à niveau, votre application Mobile Services existante peut continuer toooperate.   Si vous devez tooupgrade une application principale de Node.js, consultez trop[la mise à niveau vos Services mobiles de Node.js](app-service-mobile-node-backend-upgrading-from-mobile-services.md).

Une fois un service principal mobile tooAzure mis à niveau du Service d’applications, il a tooall d’accès aux fonctionnalités du Service de l’application et sont facturés en fonction de trop[tarification du Service d’applications], pas les Services mobiles de tarification.

## <a name="migrate-vs-upgrade"></a>Migration et mise à niveau
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> Il est recommandé d’ [effectuer une migration](app-service-mobile-migrating-from-mobile-services.md) avant une mise à niveau. De cette manière, vous pouvez placer les deux versions de votre application hello même un Plan App Service et entraîner une baisse sans coût supplémentaire.
>
>

### <a name="improvements-in-mobile-apps-net-server-sdk"></a>Améliorations du Kit de développement logiciel (SDK) serveur .NET Mobile Apps
La mise à niveau toohello nouvelle [SDK des applications mobiles](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) fournit hello avantages suivants :

* Plus de flexibilité sur les dépendances NuGet. Hello environnement d’hébergement n’est plus fournit sa propre version des packages NuGet, vous pouvez utiliser les autres versions compatibles. Toutefois, s’il existe de nouvelles bugfixes critique ou toohello de mises à jour de sécurité Mobile serveur SDK ou dépendances, vous devez mettre à jour manuellement votre service.
* Plus de souplesse dans hello mobile SDK. Vous pouvez contrôler explicitement les fonctionnalités et les itinéraires sont configurés, telles que l’authentification, API, de table et hello du point de terminaison par émission de données d’inscription. toolearn, voir [comment toouse hello .NET server SDK pour les applications mobiles Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).
* Prise en charge d'autres itinéraires et types de projets ASP.NET. Vous pouvez maintenant héberger contrôleurs MVC et les API Web Bonjour même projet comme projet de service principal mobile.
* Prise en charge des nouvelles fonctionnalités de l’authentification du Service d’applications, ce qui vous toouse une configuration de l’authentification commune entre vos applications web et mobiles.

## <a name="overview"></a>Présentation de la mise à niveau de base
Dans de nombreux cas, la mise à niveau sera aussi simple que le basculement de serveur d’applications mobiles nouvelle toohello Kit de développement logiciel et si vous republiez votre code vers une nouvelle instance de l’application Mobile. Il existe toutefois des scénarios qui nécessitent une configuration supplémentaire, tels que les scénarios d'authentification avancée et l'utilisation de tâches planifiées. Chacun de ces est couvert en hello sections ultérieurement.

> [!TIP]
> Il est recommandé de lire et comprendre reste hello de cette rubrique complètement avant de démarrer une mise à niveau. Prenez note de toutes les fonctionnalités répertoriées ci-dessous que vous utilisez.
>
>

sont des kits de développement logiciel client des Services mobiles Hello **pas** compatibles avec les serveurs d’applications mobiles nouvelle hello Kit de développement logiciel. Dans la continuité des activités tooprovide de commande de service pour votre application, vous ne devez pas publier site tooa de modifications actuellement le clients publiées. Vous devez plutôt créer une application mobile qui sert de doublon. Vous pouvez placer cette application sur hello du Service d’applications plan tooavoid encourir le coût financier supplémentaire.

Vous aurez alors deux versions de l’application hello : un qui reste identique hello et sert des applications publiées dans hello générique et hello autres dont vous pouvez ensuite mettre à niveau et la cible avec une nouvelle version du client. Vous pouvez déplacer et tester votre code à votre rythme, mais vous devez vous assurer que tous les correctifs de bogue que vous apportez obtenir tooboth appliqué. Une fois que vous estimez que nombre désiré de Bonjour générique, les applications clientes ont mis à jour la version la plus récente toohello, vous pouvez supprimer l’application hello de migrées d’origine si vous le souhaitez.

structure complète de Hello pour le processus de mise à niveau hello est la suivante :

1. Créer une application Mobile App
2. Mise à jour hello projet toouse hello nouveaux kits de développement logiciel serveur
3. Publier une nouvelle version de votre application cliente
4. (Facultatif) Supprimer l’instance originale qui a migré

## <a name="mobile-app-version"></a>Création d’une seconde instance d’application
Bonjour première étape de la mise à niveau est la ressource de l’application Mobile toocreate hello qui hébergera hello nouvelle version de votre application. Si vous avez déjà migré un service mobile existant, vous pouvez toocreate cette version sur hello même plan d’hébergement. Ouvrez hello [portail Azure] et accédez tooyour migrer l’application. Prenez note de hello du Plan App Service il s’exécute sur.

Ensuite, créez seconde instance d’application hello en hello suivant [instructions de création de serveur principal .NET](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app). Lorsque tooselect invité à choisir de vous Plan App Service ou « plan d’hébergement » hello plan de votre application migrée.

Vous pouvez toouse hello la même base de données et le concentrateur de Notification que vous l’avez fait dans les Services mobiles. Vous pouvez copier ces valeurs en ouvrant [portail Azure] , navigation dans les applications d’origine toohello, puis **paramètres** > **paramètres de l’Application**. Sous **Chaînes de connexion**, copiez `MS_NotificationHubConnectionString` et `MS_TableConnectionString`. Accédez tooyour un nouveau site de mise à niveau et les coller en remplaçant toutes les valeurs existantes. Répétez ce processus pour tous les autres paramètres d’application dont votre application a besoin. Si vous N'utilisez pas un service migré, vous pouvez lire des chaînes de connexion et les paramètres de l’application hello **configurer** onglet Hello section de Services mobiles de hello [portail Azure classic].

Effectuer une copie du projet ASP.NET de hello pour votre application et le publier tooyour nouveau site. À l’aide d’une copie de votre application client mis à jour avec la nouvelle URL de hello, valider que tout fonctionne comme prévu.

## <a name="updating-hello-server-project"></a>Mise à jour de projet de serveur hello
Applications mobiles fournit une nouvelle [serveur SDK de l’application Mobile] qui fournit la majeure partie de hello même fonctionnalité que l’exécution des Services mobiles hello. Tout d’abord, vous devez supprimer tous les packages de Services mobiles toohello références. Dans le Gestionnaire de package NuGet hello, recherchez `WindowsAzure.MobileServices.Backend`. La plupart des applications affichent plusieurs packages, notamment `WindowsAzure.MobileServices.Backend.Tables` et `WindowsAzure.MobileServices.Backend.Entity`. Dans ce cas, démarrez avec le package de hello plus bas dans l’arborescence des dépendances hello, tel que `Entity`et le supprimer. Quand vous y êtes invité, ne supprimez pas tous les packages dépendants. Répétez ce processus jusqu’à ce que vous ayez supprimé `WindowsAzure.MobileServices.Backend` .

À ce stade, vous avez un projet qui ne fait plus référence aux SDK Mobile Services.

Vous allez ensuite ajouter des références hello SDK des applications mobiles. Cette mise à niveau, la plupart des développeurs seront toodownload et installer hello `Microsoft.Azure.Mobile.Server.Quickstart` du package, comme cela extraira dans ensemble hello requis.

Il y a quelques erreurs du compilateur résultant des différences entre les kits de développement logiciel hello, mais ceux-ci sont tooaddress facile et sont traités dans le reste de hello de cette section.

### <a name="base-configuration"></a>Configuration de base
Ensuite, dans WebApiConfig.cs, vous pouvez remplacer :

        // Use this class tooset configuration options for your mobile service
        ConfigOptions options = new ConfigOptions();

        // Use this class tooset WebAPI configuration options
        HttpConfiguration config = ServiceConfig.Initialize(new ConfigBuilder(options));

par

        HttpConfiguration config = new HttpConfiguration();
        new MobileAppConfiguration()
            .UseDefaultConfiguration()
        .ApplyTo(config);

> [!NOTE]
> Si vous le souhaitez toolearn plus sur hello nouveau .NET serveur SDK et comment tooadd ou supprimer des fonctionnalités à partir de votre application, consultez hello [comment toouse hello .NET server SDK] rubrique.
>
>

Si votre application effectue des fonctionnalités d’authentification hello, vous devez également tooregister un intergiciel (middleware) OWIN. Dans ce cas, vous devez déplacer hello au-dessus de code de configuration dans une nouvelle classe de démarrage OWIN.

1. Ajoutez le package NuGet de hello `Microsoft.Owin.Host.SystemWeb` s’il n’est pas déjà inclus dans votre projet.
2. Dans Visual Studio, cliquez avec le bouton droit sur votre projet, puis sélectionnez **Ajouter** -> **Nouvel élément**. Sélectionnez **Web** -> **Général** -> **Classe de démarrage OWIN**.
3. Déplacer hello au-dessus de code pour MobileAppConfiguration de `WebApiConfig.Register()` toohello `Configuration()` méthode de votre nouvelle classe de démarrage.

Vérifiez que hello `Configuration()` méthode se termine par :

        app.UseWebApi(config)
        app.UseAppServiceAuthentication(config);

Il existe des modifications supplémentaires des tooauthentication connexes qui sont traitées dans la section de l’authentification complète hello ci-dessous.

### <a name="working-with-data"></a>Utilisation des données
Dans les Services mobiles, nom de l’application mobile hello pris en charge en tant que nom de schéma par défaut hello dans le programme d’installation de hello Entity Framework.

tooensure que vous avez hello même schéma référencé comme avant, hello utilisation suivant le schéma de hello tooset Bonjour DbContext pour votre application :

        string schema = System.Configuration.ConfigurationManager.AppSettings.Get("MS_MobileServiceName");

Vérifiez que vous avez MS_MobileServiceName définie si vous hello ci-dessus. Vous pouvez également fournir un autre nom de schéma si votre application l’a personnalisé précédemment.

### <a name="system-properties"></a>Propriétés système
#### <a name="naming"></a>Dénomination
Dans le serveur de Services mobiles Azure hello SDK, les propriétés système contiennent toujours un trait de soulignement double (`__`) préfixe pour les propriétés de hello :

* __createdAt
* __updatedAt
* __deleted
* __version

client des Services mobiles Hello kits de développement logiciel ont une logique spéciale pour l’analyse des propriétés système dans ce format.

Dans les applications mobiles Azure, propriétés système ont n’est plus une spéciale en forme et avez hello nom :

* createdAt
* updatedAt
* deleted
* version

Hello Mobile Apps client kits de développement logiciel utilisez hello nouveau système propriétés noms, donc aucune modification n’est nécessaires tooclient code. Toutefois, si vous êtes directement reste appels tooyour service, puis vous devez modifier vos requêtes en conséquence.

#### <a name="local-store"></a>Magasin local
Hello modifications toohello noms de propriétés système signifient qu’une base de données locale de synchronisation hors connexion pour les Services mobiles n’est pas compatible avec les applications mobiles. Si possible, vous devez éviter de mettre à niveau les applications clientes tooMobile Mobile Services Qu'applications jusqu'à ce qu’après les modifications en attente ont été envoyées toohello server. Ensuite, application mis à niveau hello doit utiliser un nouveau nom de fichier de base de données.

Si une application cliente est mis à niveau à partir des Services mobiles tooMobile applications bien qu’il existe des modifications en mode hors connexion en attente dans la file d’attente de fonctionnement de hello, base de données système hello doit être mis à jour toouse hello nouveaux noms de colonnes. Sur iOS, il est possible à l’aide des noms de colonnes de migrations léger toochange hello. Sur Android et hello .NET client géré, vous devez écrire les colonnes hello personnalisé SQL toorename pour vos tables d’objet de données.

Sur iOS, vous devez modifier votre schéma de données de base pour vos données entités toomatch hello suit. Notez que les propriétés de hello `createdAt`, `updatedAt` et `version` n’ont plus un `ms_` préfixe :

| Attribut | Type | Remarque |
| --- | --- | --- |
| id |Chaîne, marquée requise |clé primaire dans le magasin distant |
| createdAt |Date |propriété de système de toocreatedAt maps (facultatif) |
| updatedAt |Date |propriété de système de tooupdatedAt maps (facultatif) |
| version |String |conflits toodetect utilisé (facultatif), tooversion de mappages |

#### <a name="querying-system-properties"></a>Interrogation des propriétés système
Dans les Services mobiles Azure, les propriétés système ne sont pas envoyées par défaut, mais uniquement lorsqu’elles sont demandées à l’aide de la chaîne de requête hello `__systemProperties`. En revanche, les propriétés sont dans le système d’applications mobiles Azure **toujours sélectionné** , car ils font partie du modèle d’objet hello serveur SDK.

Cette modification affecte principalement les implémentations personnalisées des gestionnaires de domaine, comme les extensions de `MappedEntityDomainManager`. Dans les Services mobiles, si un client demande jamais les propriétés du système, il est possible de toouse un `MappedEntityDomainManager` qui ne correspondent pas réellement de toutes les propriétés. Toutefois, dans Azure Mobile Apps, ces propriétés non mappées provoquent une erreur dans les requêtes GET.

Hello plus simple problème de hello tooresolve moyen est toomodify vos données afin qu’ils héritent de `ITableData` au lieu de `EntityData`. Ensuite, ajoutez hello `[NotMapped]` toohello les champs qui doivent être omis d’attribut.

Par exemple, suivant de hello définit `TodoItem` sans propriétés système :

    using System.ComponentModel.DataAnnotations.Schema;

    public class TodoItem : ITableData
    {
        public string Text { get; set; }

        public bool Complete { get; set; }

        public string Id { get; set; }

        [NotMapped]
        public DateTimeOffset? CreatedAt { get; set; }

        [NotMapped]
        public DateTimeOffset? UpdatedAt { get; set; }

        [NotMapped]
        public bool Deleted { get; set; }

        [NotMapped]
        public byte[] Version { get; set; }
    }

Remarque : Si vous obtenez des erreurs `NotMapped`, ajouter un assembly de toohello référence `System.ComponentModel.DataAnnotations`.

### <a name="cors"></a>CORS
Services mobiles inclus une prise en charge pour le service CORS en insérant hello solution d’ASP.NET CORS. Cette couche d’habillage n’a été supprimé toogive développeur de hello plus de contrôle, et vous pouvez exploiter directement [prise en charge ASP.NET CORS](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).

zones principales posant problème si vous utilisez CORS Hello sont que hello `eTag` et `Location` en-têtes doivent être autorisés par ordre de hello client SDK toowork correctement.

### <a name="push-notifications"></a>Notifications Push
Pour envoyer des données, élément principal hello qui peuvent s’avérer manquant dans hello Kit de développement logiciel serveur est la classe de PushRegistrationHandler de hello. Les inscriptions sont traitées légèrement différemment dans Mobile Apps et les inscriptions sans balise sont activées par défaut. La gestion des balises peut être accomplie à l'aide d'API personnalisées. Consultez hello [l’inscription pour les balises](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags) instructions pour plus d’informations.

### <a name="scheduled-jobs"></a>Tâches planifiées
Les tâches planifiées ne sont pas générés dans des applications mobiles, les travaux existants que vous avez dans votre service principal .NET devez toobe mis à jour individuellement. Une option est planifiée de toocreate [de tâche Web] sur le site de code de l’application Mobile hello. Vous pouvez également configurer un contrôleur qui contient votre code de projet et configurer hello [Azure Scheduler] toohit ce point de terminaison sur la planification de hello attendu.

### <a name="miscellaneous-changes"></a>Modifications diverses
Tous les ApiControllers qui seront utilisés par un client mobile doit maintenant avoir hello `[MobileAppController]` attribut. Cela n’est plus inclus par défaut afin que les autres toogo ApiControllers pas affecté par hello formateurs mobiles.

Hello `ApiServices` objet ne fait plus partie du Kit de développement logiciel de hello. tooaccess les paramètres de l’application Mobile, vous pouvez utiliser suivant de hello :

    MobileAppSettingsDictionary settings = this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

De même, la journalisation est désormais possible à l’aide d’écriture de trace ASP.NET standard hello :

    ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
    traceWriter.Info("Hello, World");  

## <a name="authentication"></a>Considérations relatives à l’authentification
composants d’authentification Hello de Services mobiles ont désormais été déplacés en fonction de l’authentification/autorisation du Service application hello. Vous pouvez en savoir plus sur l’activation de celle-ci pour votre site par la lecture de hello [application mobile d’Ajouter authentication tooyour](app-service-mobile-ios-get-started-users.md) rubrique.

Pour certains fournisseurs, tels que Google, Facebook et AAD, vous devez être en mesure de tooleverage une inscription existante hello à partir de votre application de copie. Simplement, vous avez besoin de portail du fournisseur d’identité toohello toonavigate et que vous ajoutez une nouvelle inscription de toohello URL de redirection. Puis configurez l’authentification/autorisation du Service application avec l’ID de client hello et secret.

### <a name="controller-action-authorization"></a>Autorisation des actions de contrôleur
Toutes les instances de hello `[AuthorizeLevel(AuthorizationLevel.User)]` l’attribut doit être présent toouse modifiée hello ASP.NET standard `[Authorize]` attribut. En outre, les contrôleurs sont désormais anonymes par défaut, comme dans d’autres applications ASP.NET.
Si vous utilisez une des hello autres options AuthorizeLevel, telles que l’administrateur ou d’une Application, notez que ceux-ci ont disparu. Vous pouvez à la place configurer AuthorizationFilters des clés secrètes partagées ou configurer un Principal du Service AAD tooenable les appels de service en toute sécurité.

### <a name="getting-additional-user-information"></a>Obtention d’informations utilisateur supplémentaires
Vous pouvez obtenir des informations utilisateur supplémentaires, y compris les jetons d’accès via hello `GetAppServiceIdentityAsync()` méthode :

        FacebookCredentials creds = await this.User.GetAppServiceIdentityAsync<FacebookCredentials>();

En outre, si votre application prend des dépendances sur les ID utilisateur, telles que de les stocker dans une base de données, il est important de toonote qui hello ID utilisateur entre les Services mobiles et les applications Mobile App Service sont différents. Vous pouvez toujours obtenir hello ID d’utilisateur Mobile Services, cependant. Toutes les sous-classes de ProviderCredentials hello ont une propriété de nom d’utilisateur. Par conséquent, reprenons l’exemple hello avant :

        string mobileServicesUserId = creds.Provider + ":" + creds.UserId;

Si votre application ne prend pas de dépendances sur l’ID d’utilisateur, il est important d’exploiter hello le même type d’enregistrement avec un fournisseur d’identité si possible. ID utilisateur sont généralement incluses dans l’étendue toohello inscription d’application qui a été utilisée, afin d’introduire une nouvelle inscription peut créer des problèmes avec les utilisateurs tootheir données correspondantes.

### <a name="custom-authentication"></a>Authentification personnalisée
Si votre application utilise une solution d’authentification personnalisée, vous pouvez toomake que ce site mis à niveau hello accès toohello système. Suivez les instructions de nouveau hello pour l’authentification personnalisée dans hello [vue d’ensemble du Kit de développement logiciel .NET server] toointegrate votre solution. Notez que les composants d’authentification personnalisée hello sont toujours en version préliminaire.

## <a name="updating-clients"></a>Mise à jour des clients
Une fois que vous avez un serveur principal Mobile App opérationnel, vous pouvez travailler sur une nouvelle version de votre application cliente qui la consomme. Applications mobiles inclut également une nouvelle version du client de hello kits de développement logiciel et similaire toohello mise à niveau server ci-dessus, vous devez tooremove toutes les références toohello Mobile Services SDK avant l’installation des versions des applications mobiles hello.

Une des principales modifications de hello entre les versions de hello est que les constructeurs hello ne nécessitent plus une clé d’application. Vous maintenant transmettez simplement l’URL de hello de votre application Mobile. Par exemple, sur les clients .NET hello, hello `MobileServiceClient` constructeur est désormais :

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net", // URL of hello Mobile App
        );

Vous pouvez lire sur l’installation hello nouveaux kits de développement logiciel et à l’aide de la nouvelle structure de hello via les liens hello ci-dessous :

* [iOS version 3.0.0 ou ultérieure](app-service-mobile-ios-how-to-use-client-library.md)
* [.NET (Windows/Xamarin) version 2.0.0 ou ultérieure](app-service-mobile-dotnet-how-to-use-client-library.md)

Si votre application effectue utiliser de notifications push, notez hello instructions d’inscription spécifique pour chaque plate-forme, comme des modifications ont été certains il également.

Lorsque vous avez hello nouvelle version du client prêt, essayez-le par rapport à votre projet de serveur mis à niveau. Après avoir vérifié qu’il fonctionne, vous pouvez libérer une nouvelle version de toocustomers de votre application. Par la suite, une fois que vos clients ont eu une chance tooreceive ces mises à jour, vous pouvez supprimer la version des Services mobiles hello de votre application. À ce stade, vous avez mis à niveau tooan application de Service d’applications mobiles à l’aide du serveur d’applications mobiles dernière hello Kit de développement logiciel.

<!-- URLs. -->

[portail Azure]: https://portal.azure.com/
[portail Azure classic]: https://manage.windowsazure.com/
[quelles sont les applications mobiles ?]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[serveur SDK de l’application Mobile]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Azure Scheduler]: /en-us/documentation/services/scheduler/
[de tâche Web]: ../app-service-web/websites-webjobs-resources.md
[comment toouse hello .NET server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[tarification du Service d’applications]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[vue d’ensemble du Kit de développement logiciel .NET server]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
