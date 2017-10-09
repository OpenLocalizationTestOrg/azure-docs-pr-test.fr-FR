---
title: aaaCache fournisseur de Cache de sortie ASP.NET
description: "Découvrez comment faire à l’aide d’Azure Redis Cache de sortie de Page ASP.NET toocache"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 78469a66-0829-484f-8660-b2598ec60fbf
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/14/2017
ms.author: sdanie
ms.openlocfilehash: fc38cc657604b351f55ad8febac383783ac29700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a><span data-ttu-id="bd512-103">Fournisseur de caches de sortie ASP.NET pour le Cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="bd512-103">ASP.NET Output Cache Provider for Azure Redis Cache</span></span>
<span data-ttu-id="bd512-104">Hello fournisseur est un mécanisme de stockage d’out-of-process pour les données du cache de sortie.</span><span class="sxs-lookup"><span data-stu-id="bd512-104">hello Redis Output Cache Provider is an out-of-process storage mechanism for output cache data.</span></span> <span data-ttu-id="bd512-105">Ces données concernent spécialement les réponses HTTP complètes (mise en cache de la sortie de pages).</span><span class="sxs-lookup"><span data-stu-id="bd512-105">This data is specifically for full HTTP responses (page output caching).</span></span> <span data-ttu-id="bd512-106">fournisseur de Hello se connecte au hello nouvelle sortie cache fournisseur point d’extensibilité qui a été introduit dans ASP.NET 4.</span><span class="sxs-lookup"><span data-stu-id="bd512-106">hello provider plugs into hello new output cache provider extensibility point that was introduced in ASP.NET 4.</span></span>

<span data-ttu-id="bd512-107">toouse hello Redis d’un fournisseur de Cache de sortie, tout d’abord configurer votre cache, puis configurez votre application ASP.NET à l’aide du package NuGet du fournisseur du Cache de sortie Redis de hello.</span><span class="sxs-lookup"><span data-stu-id="bd512-107">toouse hello Redis Output Cache Provider, first configure your cache, and then configure your ASP.NET application using hello Redis Output Cache Provider NuGet package.</span></span> <span data-ttu-id="bd512-108">Cette rubrique fournit des conseils sur la configuration de votre hello de toouse application fournisseur.</span><span class="sxs-lookup"><span data-stu-id="bd512-108">This topic provides guidance on configuring your application toouse hello Redis Output Cache Provider.</span></span> <span data-ttu-id="bd512-109">Pour plus d’informations sur la création et la configuration d’une instance de Cache Redis Azure, consultez la section [Création d’un cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="bd512-109">For more information about creating and configuring an Azure Redis Cache instance, see [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

## <a name="store-aspnet-page-output-in-hello-cache"></a><span data-ttu-id="bd512-110">Stocker la sortie de la page ASP.NET dans le cache de hello</span><span class="sxs-lookup"><span data-stu-id="bd512-110">Store ASP.NET page output in hello cache</span></span>
<span data-ttu-id="bd512-111">tooconfigure une application cliente dans Visual Studio à l’aide du package NuGet d’état de Session du Cache Redis de hello, cliquez sur **Gestionnaire de Package NuGet**, **Package Manager Console** de hello **outils** menu.</span><span class="sxs-lookup"><span data-stu-id="bd512-111">tooconfigure a client application in Visual Studio using hello Redis Cache Session State NuGet package, click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>

<span data-ttu-id="bd512-112">Exécution hello après une commande à partir de hello `Package Manager Console` fenêtre.</span><span class="sxs-lookup"><span data-stu-id="bd512-112">Run hello following command from hello `Package Manager Console` window.</span></span>
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

<span data-ttu-id="bd512-113">package NuGet du fournisseur du Cache de sortie Redis de Hello a une dépendance sur le package StackExchange.Redis.StrongName de hello.</span><span class="sxs-lookup"><span data-stu-id="bd512-113">hello Redis Output Cache Provider NuGet package has a dependency on hello StackExchange.Redis.StrongName package.</span></span> <span data-ttu-id="bd512-114">Si le package StackExchange.Redis.StrongName de hello n’est pas présent dans votre projet, il est installé.</span><span class="sxs-lookup"><span data-stu-id="bd512-114">If hello StackExchange.Redis.StrongName package is not present in your project, it is installed.</span></span> <span data-ttu-id="bd512-115">Pour plus d’informations sur le package NuGet du fournisseur du Cache de sortie Redis de hello, consultez hello [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) page de NuGet.</span><span class="sxs-lookup"><span data-stu-id="bd512-115">For more information about hello Redis Output Cache Provider NuGet package, see hello [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet page.</span></span>

>[!NOTE]
><span data-ttu-id="bd512-116">Dans Ajout toohello fort package StackExchange.Redis.StrongName, également hello StackExchange.Redis sans nom fort version existe.</span><span class="sxs-lookup"><span data-stu-id="bd512-116">In addition toohello strong-named StackExchange.Redis.StrongName package, there is also hello StackExchange.Redis non-strong-named version.</span></span> <span data-ttu-id="bd512-117">Si votre projet utilise la version de StackExchange.Redis sans nom fort hello que vous devez le désinstaller, sinon vous des conflits de noms dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="bd512-117">If your project is using hello non-strong-named StackExchange.Redis version you must uninstall it, otherwise you get naming conflicts in your project.</span></span> <span data-ttu-id="bd512-118">Pour plus d’informations sur ces packages, consultez la section [Configuration des clients de cache .NET](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span><span class="sxs-lookup"><span data-stu-id="bd512-118">For more information about these packages, see [Configure .NET cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>
>
>

<span data-ttu-id="bd512-119">Hello NuGet package télécharge et ajoute hello requis assembly référence et ajoute des hello suivant la section dans votre fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="bd512-119">hello NuGet package downloads and adds hello required assembly references and adds hello following section into your web.config file.</span></span> <span data-ttu-id="bd512-120">Cette section contient la configuration requise de hello pour votre hello de toouse ASP.NET application fournisseur.</span><span class="sxs-lookup"><span data-stu-id="bd512-120">This section contains hello required configuration for your ASP.NET application toouse hello Redis Output Cache Provider.</span></span>

```xml
<caching>
  <outputCachedefault Provider="MyRedisOutputCache">
    <providers>
      <!--
      <add name="MyRedisOutputCache"
        host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
      />
      -->
      <add name="MyRedisOutputCache" type="Microsoft.Web.Redis.RedisOutputCacheProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
  </outputCache>
</caching>
```

<span data-ttu-id="bd512-121">Hello commenté section fournit un exemple des attributs de hello et des exemples de paramètres pour chaque attribut.</span><span class="sxs-lookup"><span data-stu-id="bd512-121">hello commented section provides an example of hello attributes and sample settings for each attribute.</span></span>

<span data-ttu-id="bd512-122">Configurer les attributs de hello avec des valeurs hello du Panneau de cache dans le portail de Microsoft Azure hello et configurer hello autres valeurs selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="bd512-122">Configure hello attributes with hello values from your cache blade in hello Microsoft Azure portal, and configure hello other values as desired.</span></span> <span data-ttu-id="bd512-123">Pour obtenir des instructions sur l’accès aux propriétés de votre cache, consultez la section [Configuration des paramètres de cache Redis](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="bd512-123">For instructions on accessing your cache properties, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

* <span data-ttu-id="bd512-124">**host** : spécifiez le point de terminaison de votre cache.</span><span class="sxs-lookup"><span data-stu-id="bd512-124">**host** – specify your cache endpoint.</span></span>
* <span data-ttu-id="bd512-125">**port** – utilisez votre port non-SSL ou votre port SSL, en fonction des paramètres ssl de hello.</span><span class="sxs-lookup"><span data-stu-id="bd512-125">**port** – use either your non-SSL port or your SSL port, depending on hello ssl settings.</span></span>
* <span data-ttu-id="bd512-126">**accessKey** – utilisez clé hello principal ou secondaire de votre cache.</span><span class="sxs-lookup"><span data-stu-id="bd512-126">**accessKey** – use either hello primary or secondary key for your cache.</span></span>
* <span data-ttu-id="bd512-127">**SSL** : true si vous voulez toosecure les communications de cache/client avec ssl ; sinon, false.</span><span class="sxs-lookup"><span data-stu-id="bd512-127">**ssl** – true if you want toosecure cache/client communications with ssl; otherwise false.</span></span> <span data-ttu-id="bd512-128">Être vraiment toospecify hello correct.</span><span class="sxs-lookup"><span data-stu-id="bd512-128">Be sure toospecify hello correct port.</span></span>
  * <span data-ttu-id="bd512-129">port non-SSL de Hello est désactivé par défaut pour les nouveaux caches.</span><span class="sxs-lookup"><span data-stu-id="bd512-129">hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="bd512-130">Spécifiez true pour cette hello toouse de paramètre port SSL.</span><span class="sxs-lookup"><span data-stu-id="bd512-130">Specify true for this setting toouse hello SSL port.</span></span> <span data-ttu-id="bd512-131">Pour plus d’informations sur l’activation du port de hello non-SSL, consultez hello [Ports d’accès](cache-configure.md#access-ports) section Bonjour [configurer un cache](cache-configure.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="bd512-131">For more information about enabling hello non-SSL port, see hello [Access Ports](cache-configure.md#access-ports) section in hello [Configure a cache](cache-configure.md) topic.</span></span>
* <span data-ttu-id="bd512-132">**databaseId** – spécifié le toouse de la base de données pour le cache des données de sortie.</span><span class="sxs-lookup"><span data-stu-id="bd512-132">**databaseId** – Specified which database toouse for cache output data.</span></span> <span data-ttu-id="bd512-133">Si non spécifié, la valeur par défaut 0 hello est utilisé.</span><span class="sxs-lookup"><span data-stu-id="bd512-133">If not specified, hello default value of 0 is used.</span></span>
* <span data-ttu-id="bd512-134">**applicationName** : les clés sont stockées dans redis sous `<AppName>_<SessionId>_Data`.</span><span class="sxs-lookup"><span data-stu-id="bd512-134">**applicationName** – Keys are stored in redis as `<AppName>_<SessionId>_Data`.</span></span> <span data-ttu-id="bd512-135">Ce schéma d’affectation de noms permet hello de tooshare plusieurs applications même clé.</span><span class="sxs-lookup"><span data-stu-id="bd512-135">This naming scheme enables multiple applications tooshare hello same key.</span></span> <span data-ttu-id="bd512-136">Ce paramètre est facultatif. Si vous n’indiquez aucune valeur, une valeur par défaut sera utilisée.</span><span class="sxs-lookup"><span data-stu-id="bd512-136">This parameter is optional and if you do not provide it a default value is used.</span></span>
* <span data-ttu-id="bd512-137">**connectionTimeoutInMilliseconds** : ce paramètre vous permet de connectTimeout de hello toooverride définition dans le client StackExchange.Redis de hello.</span><span class="sxs-lookup"><span data-stu-id="bd512-137">**connectionTimeoutInMilliseconds** – This setting allows you toooverride hello connectTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="bd512-138">Si non spécifié, le paramètre connectTimeout 5000 hello par défaut est utilisé.</span><span class="sxs-lookup"><span data-stu-id="bd512-138">If not specified, hello default connectTimeout setting of 5000 is used.</span></span> <span data-ttu-id="bd512-139">Pour plus d’informations, consultez le [modèle de configuration StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="bd512-139">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>
* <span data-ttu-id="bd512-140">**operationTimeoutInMilliseconds** : ce paramètre vous permet de syncTimeout de hello toooverride définition dans le client StackExchange.Redis de hello.</span><span class="sxs-lookup"><span data-stu-id="bd512-140">**operationTimeoutInMilliseconds** – This setting allows you toooverride hello syncTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="bd512-141">Si non spécifié, la valeur syncTimeout 1000 hello par défaut est utilisée.</span><span class="sxs-lookup"><span data-stu-id="bd512-141">If not specified, hello default syncTimeout setting of 1000 is used.</span></span> <span data-ttu-id="bd512-142">Pour plus d’informations, consultez le [modèle de configuration StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="bd512-142">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>

<span data-ttu-id="bd512-143">Ajouter une page de tooeach directive OutputCache pour laquelle vous souhaitez la sortie de hello toocache.</span><span class="sxs-lookup"><span data-stu-id="bd512-143">Add an OutputCache directive tooeach page for which you wish toocache hello output.</span></span>

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

<span data-ttu-id="bd512-144">Dans l’exemple précédent de hello, hello mises en cache les données de page reste dans le cache de hello pendant 60 secondes, et une version différente de la page de hello est mis en cache pour chaque combinaison de paramètres.</span><span class="sxs-lookup"><span data-stu-id="bd512-144">In hello previous example, hello cached page data remains in hello cache for 60 seconds, and a different version of hello page is cached for each parameter combination.</span></span> <span data-ttu-id="bd512-145">Pour plus d’informations sur la directive OutputCache de hello, consultez [ @OutputCache ](http://go.microsoft.com/fwlink/?linkid=320837).</span><span class="sxs-lookup"><span data-stu-id="bd512-145">For more information about hello OutputCache directive, see [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837).</span></span>

<span data-ttu-id="bd512-146">Une fois ces étapes effectuées, votre application est configurée toouse hello fournisseur.</span><span class="sxs-lookup"><span data-stu-id="bd512-146">Once these steps are performed, your application is configured toouse hello Redis Output Cache Provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd512-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bd512-147">Next steps</span></span>
<span data-ttu-id="bd512-148">Extraire hello [fournisseur d’état de Session ASP.NET pour le Cache Redis Azure](cache-aspnet-session-state-provider.md).</span><span class="sxs-lookup"><span data-stu-id="bd512-148">Check out hello [ASP.NET Session State Provider for Azure Redis Cache](cache-aspnet-session-state-provider.md).</span></span>

