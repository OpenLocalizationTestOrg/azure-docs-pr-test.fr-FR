---
title: "État de session avec Cache Redis Azure dans Azure App Service"
description: "Découvrez comment utiliser Azure Cache Service pour prendre en charge la mise en cache de l’état de session ASP.NET."
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
ms.openlocfilehash: 64fa909daf92b2b1f0cf4c7b334edba807fe7228
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a><span data-ttu-id="db0dc-103">État de session avec Cache Redis Azure dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="db0dc-103">Session state with Azure Redis cache in Azure App Service</span></span>
<span data-ttu-id="db0dc-104">Cette rubrique explique comment utiliser le service Cache Redis Azure pour l’état de session.</span><span class="sxs-lookup"><span data-stu-id="db0dc-104">This topic explains how to use the Azure Redis Cache Service for session state.</span></span>

<span data-ttu-id="db0dc-105">Si votre application web ASP.NET utilise l'état de session, vous devez configurer un fournisseur d'état de session externe (le service Redis Cache ou un fournisseur d'état de session SQL).</span><span class="sxs-lookup"><span data-stu-id="db0dc-105">If your ASP.NET web app uses session state, you will need to configure an external session state provider (either the Redis Cache Service or a SQL Server session state provider).</span></span> <span data-ttu-id="db0dc-106">Si vous utilisez l'état de session mais aucun fournisseur externe, vous êtes limité à une seule instance de votre application web.</span><span class="sxs-lookup"><span data-stu-id="db0dc-106">If you use session state, and don't use an external provider, you will be limited to one instance of your web app.</span></span> <span data-ttu-id="db0dc-107">Le service Redis Cache est la solution la plus rapide et la plus simple.</span><span class="sxs-lookup"><span data-stu-id="db0dc-107">The Redis Cache Service is the fastest and simplest to enable.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="db0dc-108"><a id="createcache"></a>Créer le cache</span><span class="sxs-lookup"><span data-stu-id="db0dc-108"><a id="createcache"></a>Create the Cache</span></span>
<span data-ttu-id="db0dc-109">Suivez les [instructions indiquées](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) pour créer le cache.</span><span class="sxs-lookup"><span data-stu-id="db0dc-109">Follow [these directions](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) to create the cache.</span></span>

## <span data-ttu-id="db0dc-110"><a id="configureproject"></a>Ajouter le package NuGet RedisSessionStateProvider à votre application web</span><span class="sxs-lookup"><span data-stu-id="db0dc-110"><a id="configureproject"></a>Add the RedisSessionStateProvider NuGet package to your web app</span></span>
<span data-ttu-id="db0dc-111">Installez le package NuGet `RedisSessionStateProvider` .</span><span class="sxs-lookup"><span data-stu-id="db0dc-111">Install the NuGet `RedisSessionStateProvider` package.</span></span>  <span data-ttu-id="db0dc-112">Utilisez la commande suivante pour effectuer l’installation à partir de la console du gestionnaire de package : (**Outils** > **Gestionnaire de package NuGet** > **Console du gestionnaire de package**) :</span><span class="sxs-lookup"><span data-stu-id="db0dc-112">Use the following command to install from the package manager console (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span></span>

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

<span data-ttu-id="db0dc-113">Pour effectuer l’installation à partir d’**Outils** > **Gestionnaire de package NuGet** > **Gérer les packages NuGet pour la solution**, recherchez `RedisSessionStateProvider`.</span><span class="sxs-lookup"><span data-stu-id="db0dc-113">To install from **Tools** > **NuGet Package Manager** > **Manage NugGet Packages for Solution**, search for `RedisSessionStateProvider`.</span></span>

<span data-ttu-id="db0dc-114">Pour plus d’informations, consultez la [page NuGet RedisSessionStateProvider](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) et [Configuration des clients du cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span><span class="sxs-lookup"><span data-stu-id="db0dc-114">For more information see the [NuGet RedisSessionStateProvider page](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) and [Configure the cache client](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span></span>

## <span data-ttu-id="db0dc-115"><a id="configurewebconfig"></a>Modifier le fichier web.config</span><span class="sxs-lookup"><span data-stu-id="db0dc-115"><a id="configurewebconfig"></a>Modify the Web.Config File</span></span>
<span data-ttu-id="db0dc-116">Outre la création de références d'assembly pour le cache, le package NuGet ajoute des entrées de stub dans le fichier *web.config* .</span><span class="sxs-lookup"><span data-stu-id="db0dc-116">In addition to making assembly references for Cache, the NuGet package adds stub entries in the *web.config* file.</span></span> 

1. <span data-ttu-id="db0dc-117">Ouvrez le fichier *web.config* , puis recherchez l'élément **sessionState** .</span><span class="sxs-lookup"><span data-stu-id="db0dc-117">Open the *web.config* and find the the **sessionState** element.</span></span>
2. <span data-ttu-id="db0dc-118">Entrez les valeurs appropriées pour `host`, `accessKey`, `port` (le port SSL doit être 6380), puis affectez à `SSL` la valeur `true`.</span><span class="sxs-lookup"><span data-stu-id="db0dc-118">Enter the values for `host`, `accessKey`, `port` (the SSL port should be 6380), and set `SSL` to `true`.</span></span> <span data-ttu-id="db0dc-119">Ces valeurs peuvent être obtenues à partir du panneau du [portail Azure](http://go.microsoft.com/fwlink/?LinkId=529715) pour votre instance de cache.</span><span class="sxs-lookup"><span data-stu-id="db0dc-119">These values can be obtained from the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) blade for your cache instance.</span></span> <span data-ttu-id="db0dc-120">Pour plus d’informations, consultez [Connexion au cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span><span class="sxs-lookup"><span data-stu-id="db0dc-120">For more information, see [Connect to the cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span></span> <span data-ttu-id="db0dc-121">Notez que le port non-SSL est désactivé par défaut pour les nouveaux caches.</span><span class="sxs-lookup"><span data-stu-id="db0dc-121">Note that the non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="db0dc-122">Pour plus d’informations sur l’activation du port non SSL, consultez la section relative aux [ports d’accès](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) dans la rubrique [Configuration d’un cache Redis Azure](https://msdn.microsoft.com/library/azure/dn793612.aspx).</span><span class="sxs-lookup"><span data-stu-id="db0dc-122">For more information about enabling the non-SSL port, see the [Access Ports](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) section in the [Configure a cache in Azure Redis Cache](https://msdn.microsoft.com/library/azure/dn793612.aspx) topic.</span></span> <span data-ttu-id="db0dc-123">Le balisage suivant montre les modifications apportées à la *web.config* de fichiers, en particulier les modifications apportées à *port*, *hôte*, accessKey *, et *ssl* .</span><span class="sxs-lookup"><span data-stu-id="db0dc-123">The following markup shows the changes to the *web.config* file, specifically the changes to *port*, *host*, accessKey*, and *ssl*.</span></span>
   
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

## <span data-ttu-id="db0dc-124"><a id="usesessionobject"></a> Utiliser l’objet Session dans le code</span><span class="sxs-lookup"><span data-stu-id="db0dc-124"><a id="usesessionobject"></a> Use the Session Object in Code</span></span>
<span data-ttu-id="db0dc-125">La dernière étape consiste à utiliser l'objet Session dans votre code ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="db0dc-125">The final step is to begin using the Session object in your ASP.NET code.</span></span> <span data-ttu-id="db0dc-126">Pour ajouter des objets à l'état de session, utilisez la méthode **Session.Add** .</span><span class="sxs-lookup"><span data-stu-id="db0dc-126">You add objects to session state by using the **Session.Add** method.</span></span> <span data-ttu-id="db0dc-127">Cette méthode utilise des paires clé-valeur pour stocker des éléments dans le cache d'état de session.</span><span class="sxs-lookup"><span data-stu-id="db0dc-127">This method uses key-value pairs to store items in the session state cache.</span></span>

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

<span data-ttu-id="db0dc-128">Le code suivant récupère cette valeur dans l'état de session.</span><span class="sxs-lookup"><span data-stu-id="db0dc-128">The following code retrieves this value from session state.</span></span>

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

<span data-ttu-id="db0dc-129">Vous pouvez également utiliser le Cache Redis pour mettre en cache des objets dans votre application web.</span><span class="sxs-lookup"><span data-stu-id="db0dc-129">You can also use the Redis Cache to cache objects in your web app.</span></span> <span data-ttu-id="db0dc-130">Pour plus d’informations, consultez [Application MVC dédiée aux films avec Cache Redis Azure en 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span><span class="sxs-lookup"><span data-stu-id="db0dc-130">For more info, see [MVC movie app with Azure Redis Cache in 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span></span>
<span data-ttu-id="db0dc-131">Pour plus d’informations sur l’utilisation de l’état de session ASP.NET, consultez la page [Vue d’ensemble de l’état de session ASP.NET][ASP.NET Session State Overview].</span><span class="sxs-lookup"><span data-stu-id="db0dc-131">For more details about how to use ASP.NET session state, see [ASP.NET Session State Overview][ASP.NET Session State Overview].</span></span>

> [!NOTE]
> <span data-ttu-id="db0dc-132">Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application web temporaire dans App Service.</span><span class="sxs-lookup"><span data-stu-id="db0dc-132">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="db0dc-133">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="db0dc-133">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="db0dc-134">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="db0dc-134">What's changed</span></span>
* <span data-ttu-id="db0dc-135">Pour obtenir un guide présentant les modifications apportées dans le cadre de la transition entre Sites Web et App Service, consultez la page [Azure App Service et les services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="db0dc-135">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
  
  <span data-ttu-id="db0dc-136">*Par [Rick Anderson](https://twitter.com/RickAndMSFT)*</span><span class="sxs-lookup"><span data-stu-id="db0dc-136">*By [Rick Anderson](https://twitter.com/RickAndMSFT)*</span></span>

[installed the latest]: http://www.windowsazure.com/downloads/?sdk=net  
[ASP.NET Session State Overview]: http://msdn.microsoft.com/library/ms178581.aspx

[NewIcon]: ./media/web-sites-dotnet-session-state-caching/CacheScreenshot_NewButton.png
[NewCacheDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CreateOptions.png
[CacheIcon]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheIcon.png
[NuGetDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_NuGet.png
[OutputConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_OC_WebConfig.png
[CacheConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheConfig.png
[EndpointURL]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_EndpointURL.png
[ManageKeys]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_ManageAccessKeys.png

