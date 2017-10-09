---
title: "état aaaSession avec dans Azure App Service de cache Redis Azure"
description: "Découvrez comment toouse hello Azure Cache Service toosupport session état mise en cache ASP.NET."
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
manager: erikre
editor: none
ms.assetid: 4f98d289-2698-464d-85cd-99ec40fad1f2
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 06/27/2016
ms.author: riande
ms.openlocfilehash: f689b6754ea072aa195f822ab6482f4bf2748375
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a>État de session avec Cache Redis Azure dans Azure App Service
Cette rubrique explique comment toouse hello Service de Cache Redis Azure pour l’état de session.

Si votre application de web ASP.NET utilise l’état de session, vous devez tooconfigure un fournisseur d’état de session externe (Service de Cache Redis de hello ou un fournisseur d’état de session SQL Server). Si vous utilisez l’état de session et que vous n’utilisez pas un fournisseur externe, vous serez instance tooone limitée de votre application web. Hello Service de Cache Redis est tooenable plus rapide et plus simple de hello.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a id="createcache"></a>Créer hello du Cache
Suivez [ces instructions](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) cache de hello toocreate.

## <a id="configureproject"></a>Ajouter hello RedisSessionStateProvider NuGet package tooyour web app
Installer hello NuGet `RedisSessionStateProvider` package.  Suivant de hello utilisez commande tooinstall à partir de la console du Gestionnaire de package hello (**outils** > **Gestionnaire de Package NuGet** > **Package Manager Console**):

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

tooinstall de **outils** > **Gestionnaire de Package NuGet** > **gérer les Packages de Solution pépite**, recherchez `RedisSessionStateProvider`.

Pour plus d’informations, consultez hello [NuGet RedisSessionStateProvider page](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) et [client de cache configurer hello](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).

## <a id="configurewebconfig"></a>Modifier le fichier Web.Config de hello
En outre, toomaking assembly fait référence pour le Cache, package NuGet de hello ajoute des entrées de stub dans hello *web.config* fichier. 

1. Ouvrez hello *web.config* et recherche hello hello **sessionState** élément.
2. Entrez les valeurs hello pour `host`, `accessKey`, `port` (hello port SSL doit être 6380) et définissez `SSL` trop`true`. Ces valeurs peuvent être obtenues à partir de hello [portail Azure](http://go.microsoft.com/fwlink/?LinkId=529715) panneau pour votre instance de cache. Pour plus d’informations, consultez [connecter toohello cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache). Notez que le port de hello non-SSL est désactivé par défaut pour les nouveaux caches. Pour plus d’informations sur l’activation du port de hello non-SSL, consultez hello [Ports d’accès](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) section Bonjour [configurer un cache dans le Cache Redis Azure](https://msdn.microsoft.com/library/azure/dn793612.aspx) rubrique. Hello balise suivante montre hello modifications toohello *web.config* de fichiers, en particulier les modifications hello trop*port*, *hôte*, accessKey *, et *ssl*.
   
          <system.web>;
            <customErrors mode="Off" />;
            <authentication mode="None" />;
            <compilation debug="true" targetFramework="4.5" />;
            <httpRuntime targetFramework="4.5" />;
            <sessionState mode="Custom" customProvider="RedisSessionProvider">;
              <providers>;  
                  <!--<add name="RedisSessionProvider" 
                    host = "127.0.0.1" [String]
                    port = "" [number]
                    accessKey = "" [String]
                    ssl = "false" [true|false]
                    throwOnError = "true" [true|false]
                    retryTimeoutInMilliseconds = "0" [number]
                    databaseId = "0" [number]
                    applicationName = "" [String]
                  />;-->;
                 <add name="RedisSessionProvider" 
                      type="Microsoft.Web.Redis.RedisSessionStateProvider" 
                      port="6380"
                      host="movie2.redis.cache.windows.net" 
                      accessKey="m7PNV60CrvKpLqMUxosC3dSe6kx9nQ6jP5del8TmADk=" 
                      ssl="true" />;
              <!--<add name="MySessionStateStore" type="Microsoft.Web.Redis.RedisSessionStateProvider" host="127.0.0.1" accessKey="" ssl="false" />;-->;
              </providers>;
            </sessionState>;
          </system.web>;

## <a id="usesessionobject"></a>Utilisez hello objet de Session dans le Code
étape finale de Hello est toobegin à l’aide d’objet de Session hello dans votre code ASP.NET. Vous ajoutez l’état de toosession d’objets à l’aide de hello **méthode Session.Add** (méthode). Cette méthode utilise les éléments toostore de paires clé-valeur dans le cache d’état de session de hello.

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

Hello suivant code récupère cette valeur à partir de l’état de session.

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

Vous pouvez également utiliser les objets de toocache de Cache Redis hello dans votre application web. Pour plus d’informations, consultez [Application MVC dédiée aux films avec Cache Redis Azure en 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).
Pour plus d’informations sur l’état de session ASP.NET toouse, consultez [vue d’ensemble des état de Session ASP.NET][ASP.NET Session State Overview].

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

## <a name="whats-changed"></a>Changements apportés
* Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)
  
  *Par [Rick Anderson](https://twitter.com/RickAndMSFT)*

[installed hello latest]: http://www.windowsazure.com/downloads/?sdk=net  
[ASP.NET Session State Overview]: http://msdn.microsoft.com/library/ms178581.aspx

[NewIcon]: ./media/web-sites-dotnet-session-state-caching/CacheScreenshot_NewButton.png
[NewCacheDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CreateOptions.png
[CacheIcon]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheIcon.png
[NuGetDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_NuGet.png
[OutputConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_OC_WebConfig.png
[CacheConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheConfig.png
[EndpointURL]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_EndpointURL.png
[ManageKeys]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_ManageAccessKeys.png

