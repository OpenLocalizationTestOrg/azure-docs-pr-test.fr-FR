---
title: "aaaCache fournisseur d’état de Session ASP.NET | Documents Microsoft"
description: "Découvrez comment l’état de Session ASP.NET toostore en utilisant le Cache Redis Azure"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 192f384c-836a-479a-bb65-8c3e6d6522bb
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 05/01/2017
ms.author: sdanie
ms.openlocfilehash: 9ea84cf67b9314b15dce696f596d399921194510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-session-state-provider-for-azure-redis-cache"></a>Fournisseur d’état de session ASP.NET pour Cache Redis Azure
Cache Redis Azure fournit un fournisseur d’état de session que vous pouvez utiliser toostore votre état de session dans un cache plutôt qu’en mémoire ou dans un serveur SQL Server de la base de données. toouse hello fournisseur d’état de session mise en cache, tout d’abord configurer votre cache, puis configurer votre application ASP.NET pour le cache à l’aide du package NuGet d’état de Session du Cache Redis de hello.

Il est souvent pas pratique dans un tooavoid d’application cloud réelle le stockage d’une forme d’état de session utilisateur, mais certaines approches un impact sur les performances et évolutivité plus que d’autres. Si vous avez toostore état, mieux hello est tookeep hello état petit et stockez-le dans des cookies. Si ce n’est pas possible, meilleure solution suivante hello est toouse l’état de session ASP.NET avec un fournisseur de cache distribué en mémoire. solution de pire Hello à partir d’un point de vue de performances et l’évolutivité est toouse un fournisseur d’état de session de sauvegarde de base de données. Cette rubrique fournit des conseils sur l’utilisation de hello fournisseur d’état de Session ASP.NET pour le Cache Redis Azure. Pour plus d’informations sur les autres options d’état de session, consultez [Options d’état de session ASP.NET](#aspnet-session-state-options).

## <a name="store-aspnet-session-state-in-hello-cache"></a>Stocker l’état de session ASP.NET dans le cache de hello
tooconfigure une application cliente dans Visual Studio à l’aide du package NuGet d’état de Session du Cache Redis de hello, cliquez sur **Gestionnaire de Package NuGet**, **Package Manager Console** de hello **outils** menu.

Exécution hello après une commande à partir de hello `Package Manager Console` fenêtre.
    
```
Install-Package Microsoft.Web.RedisSessionStateProvider
```

> [!IMPORTANT]
> Si vous utilisez hello fonctionnalité de clustering de niveau premium de hello, vous devez utiliser [RedisSessionStateProvider](https://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider) 2.0.1 ou plus élevé ou une exception est levée. Déplacement de too2.0.1 ou supérieure est une modification avec rupture ; Pour plus d’informations, consultez [v2.0.0 Détails de la modification avec rupture](https://github.com/Azure/aspnet-redis-providers/wiki/v2.0.0-Breaking-Change-Details). Au moment de cette mise à jour de l’article de hello, hello version actuelle de ce package est 2.2.3.
> 
> 

package NuGet du fournisseur des état de Session Redis de Hello a une dépendance sur le package StackExchange.Redis.StrongName de hello. Si le package StackExchange.Redis.StrongName de hello n’est pas présent dans votre projet, il est installé.

>[!NOTE]
>Dans Ajout toohello fort package StackExchange.Redis.StrongName, également hello StackExchange.Redis sans nom fort version existe. Si votre projet utilise la version de StackExchange.Redis sans nom fort hello que vous devez le désinstaller, sinon vous des conflits de noms dans votre projet. Pour plus d’informations sur ces packages, consultez la section [Configuration des clients de cache .NET](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).
>
>

Hello NuGet package télécharge et ajoute hello requis assembly référence et ajoute des hello suivant la section dans votre fichier web.config. Cette section contient la configuration requise de hello pour votre hello de toouse de l’application ASP.NET fournisseur d’état de Session du Cache Redis.

```xml
<sessionState mode="Custom" customProvider="MySessionStateStore">
    <providers>
    <!--
    <add name="MySessionStateStore"
           host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        throwOnError = "true" [true|false]
        retryTimeoutInMilliseconds = "0" [number]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
    />
    -->
    <add name="MySessionStateStore" type="Microsoft.Web.Redis.RedisSessionStateProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
</sessionState>
```

Hello commenté section fournit un exemple des attributs de hello et des exemples de paramètres pour chaque attribut.

Configurer les attributs de hello avec des valeurs hello du Panneau de cache dans le portail de Microsoft Azure hello et configurer hello autres valeurs selon vos besoins. Pour obtenir des instructions sur l’accès aux propriétés de votre cache, consultez la section [Configuration des paramètres de cache Redis](cache-configure.md#configure-redis-cache-settings).

* **host** : spécifiez le point de terminaison de votre cache.
* **port** – utilisez votre port non-SSL ou votre port SSL, en fonction des paramètres ssl de hello.
* **accessKey** – utilisez clé hello principal ou secondaire de votre cache.
* **SSL** : true si vous voulez toosecure les communications de cache/client avec ssl ; sinon, false. Être vraiment toospecify hello correct.
  * port non-SSL de Hello est désactivé par défaut pour les nouveaux caches. Spécifiez true pour cette hello toouse de paramètre port SSL. Pour plus d’informations sur l’activation du port de hello non-SSL, consultez hello [Ports d’accès](cache-configure.md#access-ports) section Bonjour [configurer un cache](cache-configure.md) rubrique.
* **throwOnError** : vrai si vous souhaitez un toobe exception levée s’il existe un échec, ou false si vous souhaitez hello opération toofail en mode silencieux. Pour rechercher un échec en vérifiant la propriété Microsoft.Web.Redis.RedisSessionStateProvider.LastException statique de hello. valeur par défaut de Hello est true.
* **retryTimeoutInMilliseconds** : intervalle, en millisecondes, au cours duquel interviennent les nouvelles tentatives d’exécution des opérations ayant échoué. Hello première tentative se produit après 20 millisecondes et nouvelles tentatives sont effectués chaque seconde jusqu'à ce que l’intervalle de retryTimeoutInMilliseconds hello arrive à expiration. Immédiatement après cet intervalle, hello opération est tentée à nouveau une dernière fois. Si l’opération de hello échoue toujours, exception de hello est levée appelant toohello, en fonction du paramètre de throwOnError hello. valeur par défaut de Hello est 0, ce qui signifie aucune tentative.
* **databaseId** – Spécifie le toouse de la base de données pour le cache des données de sortie. Si non spécifié, la valeur par défaut 0 hello est utilisé.
* **applicationName`{<Application Name>_<Session ID>}_Data` : les clés sont stockées dans redis sous** . Ce schéma d’affectation de noms permet à plusieurs applications tooshare hello même instance Redis. Ce paramètre est facultatif. Si vous n’indiquez aucune valeur, une valeur par défaut sera utilisée.
* **connectionTimeoutInMilliseconds** : ce paramètre vous permet de connectTimeout de hello toooverride définition dans le client StackExchange.Redis de hello. Si non spécifié, le paramètre connectTimeout 5000 hello par défaut est utilisé. Pour plus d’informations, consultez le [modèle de configuration StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).
* **operationTimeoutInMilliseconds** : ce paramètre vous permet de syncTimeout de hello toooverride définition dans le client StackExchange.Redis de hello. Si non spécifié, la valeur syncTimeout 1000 hello par défaut est utilisée. Pour plus d’informations, consultez le [modèle de configuration StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).

Pour plus d’informations sur ces propriétés, consultez hello d’origine annonce billet de blog [annonce du fournisseur état de Session ASP.NET pour Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx).

N’oubliez pas toocomment hello standard InProc session état fournisseur section dans votre fichier web.config.

```xml
<!-- <sessionState mode="InProc"
     customProvider="DefaultSessionProvider">
     <providers>
        <add name="DefaultSessionProvider"
              type="System.Web.Providers.DefaultSessionStateProvider,
                    System.Web.Providers, Version=1.0.0.0, Culture=neutral,
                    PublicKeyToken=31bf3856ad364e35"
              connectionStringName="DefaultConnection" />
      </providers>
</sessionState> -->
```

Une fois ces étapes effectuées, votre application est configurée toouse hello fournisseur d’état de Session du Cache Redis. Lorsque vous utilisez l’état de session dans votre application, il est stocké dans une instance de Cache Redis Azure.

> [!IMPORTANT]
> Les données stockées dans le cache de hello doit être sérialisable, contrairement aux données hello qui peuvent être stockées dans hello par défaut le fournisseur d’état de Session ASP.NET en mémoire. Lorsque hello fournisseur d’état de Session pour Redis est utilisé, assurez-vous que les types de données hello qui sont stockés dans l’état de session sont sérialisables.
> 
> 

## <a name="aspnet-session-state-options"></a>Options d’état de session ASP.NET
* Dans le fournisseur d’état de Session mémoire - ce fournisseur stocke l’état de Session hello en mémoire. avantage Hello de ce fournisseur est simple et rapide. Vous ne pourrez cependant pas faire évoluer vos applications Web si vous utilisez le fournisseur en mémoire dans la mesure où il n’est pas distribué.
* Fournisseur d’état de Session SQL Server - ce fournisseur stocke l’état de Session hello dans Sql Server. Utilisez ce fournisseur si vous souhaitez que l’état de Session toostore hello dans un stockage persistant. Vous pouvez faire évoluer votre application Web, mais l’utilisation du serveur SQL pour la session a un impact sur les performances de votre application Web.
* Distribué dans Session fournisseur d’état interne comme Cache de Session de fournisseur d’état Redis - ainsi fournisseur hello de meilleur des deux mondes. Votre application Web peut bénéficier d’un fournisseur d’état de session à la fois simple, rapide et évolutif. Étant donné que cette hello de magasins d’état de Session dans un Cache, votre application fournisseur a tootake en considération tous hello caractéristiques associées lorsqu’ils s’adressent tooa distribués dans le Cache mémoire, telles que des défaillances temporaires du réseau. Pour obtenir des recommandations sur l’utilisation du Cache, consultez la page [Caching Guidance](../best-practices-caching.md) dans le [Guide de conception et d’implémentation des applications Azure Cloud](https://github.com/mspnp/azure-guidance) de Microsoft Patterns & Practices.

Pour plus d'informations sur l’état de session et obtenir d’autres meilleures pratiques, consultez la page [Web Development Best Practices (Building Real-World Cloud Apps with Azure)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices).

## <a name="next-steps"></a>Étapes suivantes
Extraire hello [fournisseur de Cache de sortie ASP.NET pour le Cache Redis Azure](cache-aspnet-output-cache-provider.md).

