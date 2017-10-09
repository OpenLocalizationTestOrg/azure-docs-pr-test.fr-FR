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
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a><span data-ttu-id="caa14-103">État de session avec Cache Redis Azure dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="caa14-103">Session state with Azure Redis cache in Azure App Service</span></span>
<span data-ttu-id="caa14-104">Cette rubrique explique comment toouse hello Service de Cache Redis Azure pour l’état de session.</span><span class="sxs-lookup"><span data-stu-id="caa14-104">This topic explains how toouse hello Azure Redis Cache Service for session state.</span></span>

<span data-ttu-id="caa14-105">Si votre application de web ASP.NET utilise l’état de session, vous devez tooconfigure un fournisseur d’état de session externe (Service de Cache Redis de hello ou un fournisseur d’état de session SQL Server).</span><span class="sxs-lookup"><span data-stu-id="caa14-105">If your ASP.NET web app uses session state, you will need tooconfigure an external session state provider (either hello Redis Cache Service or a SQL Server session state provider).</span></span> <span data-ttu-id="caa14-106">Si vous utilisez l’état de session et que vous n’utilisez pas un fournisseur externe, vous serez instance tooone limitée de votre application web.</span><span class="sxs-lookup"><span data-stu-id="caa14-106">If you use session state, and don't use an external provider, you will be limited tooone instance of your web app.</span></span> <span data-ttu-id="caa14-107">Hello Service de Cache Redis est tooenable plus rapide et plus simple de hello.</span><span class="sxs-lookup"><span data-stu-id="caa14-107">hello Redis Cache Service is hello fastest and simplest tooenable.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="caa14-108"><a id="createcache"></a>Créer hello du Cache</span><span class="sxs-lookup"><span data-stu-id="caa14-108"><a id="createcache"></a>Create hello Cache</span></span>
<span data-ttu-id="caa14-109">Suivez [ces instructions](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) cache de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="caa14-109">Follow [these directions](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) toocreate hello cache.</span></span>

## <span data-ttu-id="caa14-110"><a id="configureproject"></a>Ajouter hello RedisSessionStateProvider NuGet package tooyour web app</span><span class="sxs-lookup"><span data-stu-id="caa14-110"><a id="configureproject"></a>Add hello RedisSessionStateProvider NuGet package tooyour web app</span></span>
<span data-ttu-id="caa14-111">Installer hello NuGet `RedisSessionStateProvider` package.</span><span class="sxs-lookup"><span data-stu-id="caa14-111">Install hello NuGet `RedisSessionStateProvider` package.</span></span>  <span data-ttu-id="caa14-112">Suivant de hello utilisez commande tooinstall à partir de la console du Gestionnaire de package hello (**outils** > **Gestionnaire de Package NuGet** > **Package Manager Console**):</span><span class="sxs-lookup"><span data-stu-id="caa14-112">Use hello following command tooinstall from hello package manager console (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span></span>

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

<span data-ttu-id="caa14-113">tooinstall de **outils** > **Gestionnaire de Package NuGet** > **gérer les Packages de Solution pépite**, recherchez `RedisSessionStateProvider`.</span><span class="sxs-lookup"><span data-stu-id="caa14-113">tooinstall from **Tools** > **NuGet Package Manager** > **Manage NugGet Packages for Solution**, search for `RedisSessionStateProvider`.</span></span>

<span data-ttu-id="caa14-114">Pour plus d’informations, consultez hello [NuGet RedisSessionStateProvider page](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) et [client de cache configurer hello](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span><span class="sxs-lookup"><span data-stu-id="caa14-114">For more information see hello [NuGet RedisSessionStateProvider page](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) and [Configure hello cache client](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span></span>

## <span data-ttu-id="caa14-115"><a id="configurewebconfig"></a>Modifier le fichier Web.Config de hello</span><span class="sxs-lookup"><span data-stu-id="caa14-115"><a id="configurewebconfig"></a>Modify hello Web.Config File</span></span>
<span data-ttu-id="caa14-116">En outre, toomaking assembly fait référence pour le Cache, package NuGet de hello ajoute des entrées de stub dans hello *web.config* fichier.</span><span class="sxs-lookup"><span data-stu-id="caa14-116">In addition toomaking assembly references for Cache, hello NuGet package adds stub entries in hello *web.config* file.</span></span> 

1. <span data-ttu-id="caa14-117">Ouvrez hello *web.config* et recherche hello hello **sessionState** élément.</span><span class="sxs-lookup"><span data-stu-id="caa14-117">Open hello *web.config* and find hello hello **sessionState** element.</span></span>
2. <span data-ttu-id="caa14-118">Entrez les valeurs hello pour `host`, `accessKey`, `port` (hello port SSL doit être 6380) et définissez `SSL` trop`true`.</span><span class="sxs-lookup"><span data-stu-id="caa14-118">Enter hello values for `host`, `accessKey`, `port` (hello SSL port should be 6380), and set `SSL` too`true`.</span></span> <span data-ttu-id="caa14-119">Ces valeurs peuvent être obtenues à partir de hello [portail Azure](http://go.microsoft.com/fwlink/?LinkId=529715) panneau pour votre instance de cache.</span><span class="sxs-lookup"><span data-stu-id="caa14-119">These values can be obtained from hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) blade for your cache instance.</span></span> <span data-ttu-id="caa14-120">Pour plus d’informations, consultez [connecter toohello cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span><span class="sxs-lookup"><span data-stu-id="caa14-120">For more information, see [Connect toohello cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span></span> <span data-ttu-id="caa14-121">Notez que le port de hello non-SSL est désactivé par défaut pour les nouveaux caches.</span><span class="sxs-lookup"><span data-stu-id="caa14-121">Note that hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="caa14-122">Pour plus d’informations sur l’activation du port de hello non-SSL, consultez hello [Ports d’accès](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) section Bonjour [configurer un cache dans le Cache Redis Azure](https://msdn.microsoft.com/library/azure/dn793612.aspx) rubrique.</span><span class="sxs-lookup"><span data-stu-id="caa14-122">For more information about enabling hello non-SSL port, see hello [Access Ports](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) section in hello [Configure a cache in Azure Redis Cache](https://msdn.microsoft.com/library/azure/dn793612.aspx) topic.</span></span> <span data-ttu-id="caa14-123">Hello balise suivante montre hello modifications toohello *web.config* de fichiers, en particulier les modifications hello trop*port*, *hôte*, accessKey *, et *ssl*.</span><span class="sxs-lookup"><span data-stu-id="caa14-123">hello following markup shows hello changes toohello *web.config* file, specifically hello changes too*port*, *host*, accessKey*, and *ssl*.</span></span>
   
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

## <span data-ttu-id="caa14-124"><a id="usesessionobject"></a>Utilisez hello objet de Session dans le Code</span><span class="sxs-lookup"><span data-stu-id="caa14-124"><a id="usesessionobject"></a> Use hello Session Object in Code</span></span>
<span data-ttu-id="caa14-125">étape finale de Hello est toobegin à l’aide d’objet de Session hello dans votre code ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="caa14-125">hello final step is toobegin using hello Session object in your ASP.NET code.</span></span> <span data-ttu-id="caa14-126">Vous ajoutez l’état de toosession d’objets à l’aide de hello **méthode Session.Add** (méthode).</span><span class="sxs-lookup"><span data-stu-id="caa14-126">You add objects toosession state by using hello **Session.Add** method.</span></span> <span data-ttu-id="caa14-127">Cette méthode utilise les éléments toostore de paires clé-valeur dans le cache d’état de session de hello.</span><span class="sxs-lookup"><span data-stu-id="caa14-127">This method uses key-value pairs toostore items in hello session state cache.</span></span>

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

<span data-ttu-id="caa14-128">Hello suivant code récupère cette valeur à partir de l’état de session.</span><span class="sxs-lookup"><span data-stu-id="caa14-128">hello following code retrieves this value from session state.</span></span>

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

<span data-ttu-id="caa14-129">Vous pouvez également utiliser les objets de toocache de Cache Redis hello dans votre application web.</span><span class="sxs-lookup"><span data-stu-id="caa14-129">You can also use hello Redis Cache toocache objects in your web app.</span></span> <span data-ttu-id="caa14-130">Pour plus d’informations, consultez [Application MVC dédiée aux films avec Cache Redis Azure en 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span><span class="sxs-lookup"><span data-stu-id="caa14-130">For more info, see [MVC movie app with Azure Redis Cache in 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span></span>
<span data-ttu-id="caa14-131">Pour plus d’informations sur l’état de session ASP.NET toouse, consultez [vue d’ensemble des état de Session ASP.NET][ASP.NET Session State Overview].</span><span class="sxs-lookup"><span data-stu-id="caa14-131">For more details about how toouse ASP.NET session state, see [ASP.NET Session State Overview][ASP.NET Session State Overview].</span></span>

> [!NOTE]
> <span data-ttu-id="caa14-132">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="caa14-132">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="caa14-133">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="caa14-133">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="caa14-134">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="caa14-134">What's changed</span></span>
* <span data-ttu-id="caa14-135">Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="caa14-135">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
  
  <span data-ttu-id="caa14-136">*Par [Rick Anderson](https://twitter.com/RickAndMSFT)*</span><span class="sxs-lookup"><span data-stu-id="caa14-136">*By [Rick Anderson](https://twitter.com/RickAndMSFT)*</span></span>

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

