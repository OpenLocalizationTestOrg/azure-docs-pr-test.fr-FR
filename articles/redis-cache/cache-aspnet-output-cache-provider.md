---
title: Mise en cache du fournisseur de caches de sortie ASP.NET
description: "Découvrez comment mettre en cache les sortie de pages ASP.NET à l’aide du Cache Redis Azure"
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
ms.openlocfilehash: 845f25637a0e48460fc76c1ee36060274b3cec38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a><span data-ttu-id="77cd6-103">Fournisseur de caches de sortie ASP.NET pour le Cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="77cd6-103">ASP.NET Output Cache Provider for Azure Redis Cache</span></span>
<span data-ttu-id="77cd6-104">Le fournisseur de caches de sortie Redis est un mécanisme de stockage hors processus pour les données de cache de sortie.</span><span class="sxs-lookup"><span data-stu-id="77cd6-104">The Redis Output Cache Provider is an out-of-process storage mechanism for output cache data.</span></span> <span data-ttu-id="77cd6-105">Ces données concernent spécialement les réponses HTTP complètes (mise en cache de la sortie de pages).</span><span class="sxs-lookup"><span data-stu-id="77cd6-105">This data is specifically for full HTTP responses (page output caching).</span></span> <span data-ttu-id="77cd6-106">Le fournisseur se connecte au nouveau point d'extension du fournisseur de caches de sortie introduit dans ASP.NET 4.</span><span class="sxs-lookup"><span data-stu-id="77cd6-106">The provider plugs into the new output cache provider extensibility point that was introduced in ASP.NET 4.</span></span>

<span data-ttu-id="77cd6-107">Pour utiliser le fournisseur de caches de sortie Redis, configurez d’abord votre cache, puis configurez votre application ASP.NET en utilisant le package NuGet du fournisseur de caches de sortie Redis.</span><span class="sxs-lookup"><span data-stu-id="77cd6-107">To use the Redis Output Cache Provider, first configure your cache, and then configure your ASP.NET application using the Redis Output Cache Provider NuGet package.</span></span> <span data-ttu-id="77cd6-108">Cette rubrique fournit des conseils sur la configuration de votre application pour utiliser le fournisseur de caches de sortie Redis.</span><span class="sxs-lookup"><span data-stu-id="77cd6-108">This topic provides guidance on configuring your application to use the Redis Output Cache Provider.</span></span> <span data-ttu-id="77cd6-109">Pour plus d’informations sur la création et la configuration d’une instance de Cache Redis Azure, consultez la section [Création d’un cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="77cd6-109">For more information about creating and configuring an Azure Redis Cache instance, see [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

## <a name="store-aspnet-page-output-in-the-cache"></a><span data-ttu-id="77cd6-110">Stockage de la sortie de pages ASP.NET dans le cache</span><span class="sxs-lookup"><span data-stu-id="77cd6-110">Store ASP.NET page output in the cache</span></span>
<span data-ttu-id="77cd6-111">Pour configurer une application cliente dans Visual Studio avec le package NuGet de l’état de session Cache Redis, cliquez sur **Gestionnaire de package NuGet**, **Console du Gestionnaire de package** dans le menu **Outils**.</span><span class="sxs-lookup"><span data-stu-id="77cd6-111">To configure a client application in Visual Studio using the Redis Cache Session State NuGet package, click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>

<span data-ttu-id="77cd6-112">Exécutez la commande suivante depuis la fenêtre `Package Manager Console`.</span><span class="sxs-lookup"><span data-stu-id="77cd6-112">Run the following command from the `Package Manager Console` window.</span></span>
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

<span data-ttu-id="77cd6-113">Le package NuGet du fournisseur de caches de sortie Redis a une dépendance sur le package StackExchange.Redis.StrongName.</span><span class="sxs-lookup"><span data-stu-id="77cd6-113">The Redis Output Cache Provider NuGet package has a dependency on the StackExchange.Redis.StrongName package.</span></span> <span data-ttu-id="77cd6-114">Le package StackExchange.Redis.StrongName est automatiquement installé s’il ne figure pas déjà dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="77cd6-114">If the StackExchange.Redis.StrongName package is not present in your project, it is installed.</span></span> <span data-ttu-id="77cd6-115">Pour plus d’informations sur le package NuGet du fournisseur de caches de sortie Redis, consultez la page NuGet [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/).</span><span class="sxs-lookup"><span data-stu-id="77cd6-115">For more information about the Redis Output Cache Provider NuGet package, see the [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet page.</span></span>

>[!NOTE]
><span data-ttu-id="77cd6-116">Il existe, en plus du package StackExchange.Redis.StrongName avec nom fort, une version de StackExchange.Redis sans nom fort.</span><span class="sxs-lookup"><span data-stu-id="77cd6-116">In addition to the strong-named StackExchange.Redis.StrongName package, there is also the StackExchange.Redis non-strong-named version.</span></span> <span data-ttu-id="77cd6-117">Si votre projet utilise la version StackExchange.Redis sans nom fort, vous devez la désinstaller, sans quoi vous aurez des conflits de noms dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="77cd6-117">If your project is using the non-strong-named StackExchange.Redis version you must uninstall it, otherwise you get naming conflicts in your project.</span></span> <span data-ttu-id="77cd6-118">Pour plus d’informations sur ces packages, consultez la section [Configuration des clients de cache .NET](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span><span class="sxs-lookup"><span data-stu-id="77cd6-118">For more information about these packages, see [Configure .NET cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>
>
>

<span data-ttu-id="77cd6-119">Le package NuGet télécharge et ajoute les références d’assembly nécessaires et ajoute la section suivante dans votre fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="77cd6-119">The NuGet package downloads and adds the required assembly references and adds the following section into your web.config file.</span></span> <span data-ttu-id="77cd6-120">Cette section contient la configuration requise pour que votre application ASP.NET utilise le fournisseur de cache de sortie Redis.</span><span class="sxs-lookup"><span data-stu-id="77cd6-120">This section contains the required configuration for your ASP.NET application to use the Redis Output Cache Provider.</span></span>

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

<span data-ttu-id="77cd6-121">La section commentée fournit un exemple d’attributs et de paramétrage pour chacun de ces attributs.</span><span class="sxs-lookup"><span data-stu-id="77cd6-121">The commented section provides an example of the attributes and sample settings for each attribute.</span></span>

<span data-ttu-id="77cd6-122">Configurez les attributs avec les valeurs du panneau de votre cache sur le portail Microsoft Azure et configurez les autres valeurs selon votre choix.</span><span class="sxs-lookup"><span data-stu-id="77cd6-122">Configure the attributes with the values from your cache blade in the Microsoft Azure portal, and configure the other values as desired.</span></span> <span data-ttu-id="77cd6-123">Pour obtenir des instructions sur l’accès aux propriétés de votre cache, consultez la section [Configuration des paramètres de cache Redis](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="77cd6-123">For instructions on accessing your cache properties, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

* <span data-ttu-id="77cd6-124">**host** : spécifiez le point de terminaison de votre cache.</span><span class="sxs-lookup"><span data-stu-id="77cd6-124">**host** – specify your cache endpoint.</span></span>
* <span data-ttu-id="77cd6-125">**port** : utilisez votre port non SSL ou votre port SSL, selon les paramètres ssl.</span><span class="sxs-lookup"><span data-stu-id="77cd6-125">**port** – use either your non-SSL port or your SSL port, depending on the ssl settings.</span></span>
* <span data-ttu-id="77cd6-126">**accessKey** : utilisez la clé primaire ou secondaire pour votre cache.</span><span class="sxs-lookup"><span data-stu-id="77cd6-126">**accessKey** – use either the primary or secondary key for your cache.</span></span>
* <span data-ttu-id="77cd6-127">**ssl** : choisissez « true » si vous souhaitez sécuriser les communications cache/client avec ssl ; sinon, choisissez « false ».</span><span class="sxs-lookup"><span data-stu-id="77cd6-127">**ssl** – true if you want to secure cache/client communications with ssl; otherwise false.</span></span> <span data-ttu-id="77cd6-128">Veillez à spécifier le port approprié.</span><span class="sxs-lookup"><span data-stu-id="77cd6-128">Be sure to specify the correct port.</span></span>
  * <span data-ttu-id="77cd6-129">Le port non SSL est désactivé par défaut pour les nouveaux caches.</span><span class="sxs-lookup"><span data-stu-id="77cd6-129">The non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="77cd6-130">Spécifiez true pour utiliser le port SSL pour ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="77cd6-130">Specify true for this setting to use the SSL port.</span></span> <span data-ttu-id="77cd6-131">Pour plus d’informations sur l’activation du port non SSL, consultez la section relative aux [ports d’accès](cache-configure.md#access-ports) dans la rubrique [Configuration d’un cache](cache-configure.md).</span><span class="sxs-lookup"><span data-stu-id="77cd6-131">For more information about enabling the non-SSL port, see the [Access Ports](cache-configure.md#access-ports) section in the [Configure a cache](cache-configure.md) topic.</span></span>
* <span data-ttu-id="77cd6-132">**databaseId** : spécifiez la base de données à utiliser pour les données de sortie du cache.</span><span class="sxs-lookup"><span data-stu-id="77cd6-132">**databaseId** – Specified which database to use for cache output data.</span></span> <span data-ttu-id="77cd6-133">Si ce champ n’est pas spécifié, la valeur 0 sera utilisée par défaut.</span><span class="sxs-lookup"><span data-stu-id="77cd6-133">If not specified, the default value of 0 is used.</span></span>
* <span data-ttu-id="77cd6-134">**applicationName** : les clés sont stockées dans redis sous `<AppName>_<SessionId>_Data`.</span><span class="sxs-lookup"><span data-stu-id="77cd6-134">**applicationName** – Keys are stored in redis as `<AppName>_<SessionId>_Data`.</span></span> <span data-ttu-id="77cd6-135">Ce schéma d’affectation permet à plusieurs applications de partager la même clé.</span><span class="sxs-lookup"><span data-stu-id="77cd6-135">This naming scheme enables multiple applications to share the same key.</span></span> <span data-ttu-id="77cd6-136">Ce paramètre est facultatif. Si vous n’indiquez aucune valeur, une valeur par défaut sera utilisée.</span><span class="sxs-lookup"><span data-stu-id="77cd6-136">This parameter is optional and if you do not provide it a default value is used.</span></span>
* <span data-ttu-id="77cd6-137">**connectionTimeoutInMilliseconds** : ce paramètre vous permet de remplacer le paramètre connectTimeout dans le client StackExchange.Redis.</span><span class="sxs-lookup"><span data-stu-id="77cd6-137">**connectionTimeoutInMilliseconds** – This setting allows you to override the connectTimeout setting in the StackExchange.Redis client.</span></span> <span data-ttu-id="77cd6-138">S’il n’est pas spécifié, le paramètre par défaut connectTimeout 5000 est utilisé.</span><span class="sxs-lookup"><span data-stu-id="77cd6-138">If not specified, the default connectTimeout setting of 5000 is used.</span></span> <span data-ttu-id="77cd6-139">Pour plus d’informations, consultez le [modèle de configuration StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="77cd6-139">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>
* <span data-ttu-id="77cd6-140">**operationTimeoutInMilliseconds** : ce paramètre vous permet de remplacer le paramètre syncTimeout dans le client StackExchange.Redis.</span><span class="sxs-lookup"><span data-stu-id="77cd6-140">**operationTimeoutInMilliseconds** – This setting allows you to override the syncTimeout setting in the StackExchange.Redis client.</span></span> <span data-ttu-id="77cd6-141">S’il n’est pas spécifié, le paramètre par défaut syncTimeout 1000 est utilisé.</span><span class="sxs-lookup"><span data-stu-id="77cd6-141">If not specified, the default syncTimeout setting of 1000 is used.</span></span> <span data-ttu-id="77cd6-142">Pour plus d’informations, consultez le [modèle de configuration StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="77cd6-142">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>

<span data-ttu-id="77cd6-143">Ajoutez une directive OutputCache à chaque page pour laquelle vous voulez mettre en cache la sortie.</span><span class="sxs-lookup"><span data-stu-id="77cd6-143">Add an OutputCache directive to each page for which you wish to cache the output.</span></span>

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

<span data-ttu-id="77cd6-144">Dans l’exemple précédent, les données de page mises en cache resteront dans le cache pendant 60 secondes et une version différente de la page est mise en cache pour chaque combinaison de paramètres.</span><span class="sxs-lookup"><span data-stu-id="77cd6-144">In the previous example, the cached page data remains in the cache for 60 seconds, and a different version of the page is cached for each parameter combination.</span></span> <span data-ttu-id="77cd6-145">Pour plus d’informations sur la directive OutputCache, consultez [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837).</span><span class="sxs-lookup"><span data-stu-id="77cd6-145">For more information about the OutputCache directive, see [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837).</span></span>

<span data-ttu-id="77cd6-146">Une fois ces étapes effectuées, votre application est configurée pour utiliser le fournisseur de caches de sortie Redis.</span><span class="sxs-lookup"><span data-stu-id="77cd6-146">Once these steps are performed, your application is configured to use the Redis Output Cache Provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77cd6-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="77cd6-147">Next steps</span></span>
<span data-ttu-id="77cd6-148">Consultez la page [ASP.NET Session State Provider for Azure Redis Cache](cache-aspnet-session-state-provider.md)(en anglais).</span><span class="sxs-lookup"><span data-stu-id="77cd6-148">Check out the [ASP.NET Session State Provider for Azure Redis Cache](cache-aspnet-session-state-provider.md).</span></span>

