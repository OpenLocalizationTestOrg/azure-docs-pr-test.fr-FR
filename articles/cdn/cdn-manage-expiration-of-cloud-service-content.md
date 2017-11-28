---
title: expiration aaaManage du contenu web dans Azure CDN | Documents Microsoft
description: "Découvrez comment expiration toomanage de contenu Azure Web Apps/Cloud Services, ASP.NET ou IIS dans Azure CDN."
services: cdn
documentationcenter: .NET
author: zhangmanling
manager: erikre
editor: 
ms.assetid: bef53fcc-bb13-4002-9324-9edee9da8288
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a0154236c3893b627f4480e0688f555964862556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a><span data-ttu-id="7f68a-103">Gérer l’expiration des contenus d’Azure Web Apps/Services cloud, d’ASP.NET ou d’IIS dans le réseau de distribution de contenu (CDN) Azure</span><span class="sxs-lookup"><span data-stu-id="7f68a-103">Manage expiration of Azure Web Apps/Cloud Services, ASP.NET, or IIS content in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7f68a-104">Azure Web Apps/Cloud Services, ASP.NET ou IIS</span><span class="sxs-lookup"><span data-stu-id="7f68a-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="7f68a-105">Service Azure Storage Blob</span><span class="sxs-lookup"><span data-stu-id="7f68a-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="7f68a-106">Les fichiers d’un serveur web d’origine publiquement accessible peuvent être mis en cache dans le réseau de distribution de contenu (CDN) Azure jusqu’à l’expiration de leur durée de vie (TTL).</span><span class="sxs-lookup"><span data-stu-id="7f68a-106">Files from any publicly accessible origin web server can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="7f68a-107">durée de vie Hello est déterminée par hello [ *Cache-Control* en-tête](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) en réponse hello HTTP à partir du serveur d’origine hello.</span><span class="sxs-lookup"><span data-stu-id="7f68a-107">hello TTL is determined by hello [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in hello HTTP response from hello origin server.</span></span>  <span data-ttu-id="7f68a-108">Cet article décrit comment tooset `Cache-Control` les en-têtes pour les applications Web Azure, Azure Cloud Services, les applications ASP.NET et les sites Internet Information Services, qui sont configurés de la même façon.</span><span class="sxs-lookup"><span data-stu-id="7f68a-108">This article describes how tooset `Cache-Control` headers for Azure Web Apps, Azure Cloud Services, ASP.NET applications, and Internet Information Services sites, all of which are configured similarly.</span></span>

> [!TIP]
> <span data-ttu-id="7f68a-109">Vous ne pouvez choisir tooset aucune durée de vie d’un fichier.</span><span class="sxs-lookup"><span data-stu-id="7f68a-109">You may choose tooset no TTL on a file.</span></span>  <span data-ttu-id="7f68a-110">Dans ce cas, Azure CDN applique automatiquement une durée de vie de sept jours par défaut.</span><span class="sxs-lookup"><span data-stu-id="7f68a-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="7f68a-111">Pour plus d’informations sur le fonctionnement de Azure CDN toospeed toofiles d’accès et d’autres ressources, consultez hello [vue d’ensemble du CDN Azure](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7f68a-111">For more information about how Azure CDN works toospeed up access toofiles and other resources, see hello [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a><span data-ttu-id="7f68a-112">Définition d’en-têtes Cache-Control dans la configuration</span><span class="sxs-lookup"><span data-stu-id="7f68a-112">Setting Cache-Control Headers in configuration</span></span>
<span data-ttu-id="7f68a-113">Pour le contenu statique, comme des images et des feuilles de style, vous pouvez contrôler la fréquence de mise à jour hello en modifiant hello **applicationHost.config** ou **web.config** les fichiers de votre application web.</span><span class="sxs-lookup"><span data-stu-id="7f68a-113">For static content, such as images and style sheets, you can control hello update frequency by modifying hello **applicationHost.config** or **web.config** files for your web application.</span></span>  <span data-ttu-id="7f68a-114">Hello **system.webServer\staticContent\clientCache** élément dans le fichier de configuration hello définira hello `Cache-Control` en-tête pour votre contenu.</span><span class="sxs-lookup"><span data-stu-id="7f68a-114">hello **system.webServer\staticContent\clientCache** element in hello configuration file will set hello `Cache-Control` header for your content.</span></span> <span data-ttu-id="7f68a-115">Pour **web.config**, paramètres de configuration hello affectent tous les éléments dans le dossier de hello et tous ses sous-dossiers, sauf si la substitution au niveau du sous-dossier hello.</span><span class="sxs-lookup"><span data-stu-id="7f68a-115">For **web.config**, hello configuration settings will affect everything in hello folder and all subfolders, unless overridden at hello subfolder level.</span></span>  <span data-ttu-id="7f68a-116">Par exemple, vous pouvez définir une valeur par défaut time-to-live à hello racine toohave statique tout le contenu mis en cache pendant 3 jours, mais ont un sous-dossier qui a le plus variable avec un paramètre de cache de 6 heures.</span><span class="sxs-lookup"><span data-stu-id="7f68a-116">For example, you can set a default time-to-live at hello root toohave all static content cached for 3 days, but have a subfolder that has more variable content with a cache setting of 6 hours.</span></span>  <span data-ttu-id="7f68a-117">Pour **applicationHost.config**, toutes les applications sur site de hello seront affectées, mais peut être substituées dans **web.config** fichiers dans les applications de hello.</span><span class="sxs-lookup"><span data-stu-id="7f68a-117">For **applicationHost.config**, all applications on hello site will be affected, but can be overridden in **web.config** files in hello applications.</span></span>

<span data-ttu-id="7f68a-118">Hello code XML suivant montre un exemple de paramètre **clientCache** toospecify un âge maximal de 3 jours :</span><span class="sxs-lookup"><span data-stu-id="7f68a-118">hello following XML shows an example of setting **clientCache** toospecify a maximum age of 3 days:</span></span>  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

<span data-ttu-id="7f68a-119">Spécification de **UseMaxAge** ajoute un `Cache-Control: max-age=<nnn>` toohello réponse de l’en-tête en fonction de la valeur hello spécifié dans hello **CacheControlMaxAge** attribut.</span><span class="sxs-lookup"><span data-stu-id="7f68a-119">Specifying **UseMaxAge** adds a `Cache-Control: max-age=<nnn>` header toohello response based on hello value specified in hello **CacheControlMaxAge** attribute.</span></span> <span data-ttu-id="7f68a-120">format Hello hello TimeSpan concerne hello **cacheControlMaxAge** attribut est <days>.<hours>:<min>:<sec>.</span><span class="sxs-lookup"><span data-stu-id="7f68a-120">hello format of hello timespan is for hello **cacheControlMaxAge** attribute is <days>.<hours>:<min>:<sec>.</span></span> <span data-ttu-id="7f68a-121">Pour plus d’informations sur hello **clientCache** nœud, consultez [cache du Client <clientCache> ](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span><span class="sxs-lookup"><span data-stu-id="7f68a-121">For more information on hello **clientCache** node, see [Client Cache <clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span></span>  

## <a name="setting-cache-control-headers-in-code"></a><span data-ttu-id="7f68a-122">Définition d’en-têtes Cache-Control dans le code</span><span class="sxs-lookup"><span data-stu-id="7f68a-122">Setting Cache-Control Headers in Code</span></span>
<span data-ttu-id="7f68a-123">Pour les applications ASP.NET, vous pouvez définir comportement de mise en cache CDN hello par programme en définissant la hello **HttpResponse.Cache** propriété.</span><span class="sxs-lookup"><span data-stu-id="7f68a-123">For ASP.NET applications, you can set hello CDN caching behavior programmatically by setting hello **HttpResponse.Cache** property.</span></span> <span data-ttu-id="7f68a-124">Pour plus d’informations sur hello **HttpResponse.Cache** propriété, consultez [propriété HttpResponse.Cache](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) et [classe HttpCachePolicy](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f68a-124">For more information on hello **HttpResponse.Cache** property, see [HttpResponse.Cache Property](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) and [HttpCachePolicy Class](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

<span data-ttu-id="7f68a-125">Si vous souhaitez que le contenu de l’application cache tooprogrammatically dans ASP.NET, assurez-vous que le contenu de hello est marqué comme pouvant être en définissant HttpCacheability trop*Public*.</span><span class="sxs-lookup"><span data-stu-id="7f68a-125">If you want tooprogrammatically cache application content in ASP.NET, make sure that hello content is marked as cacheable by setting HttpCacheability too*Public*.</span></span> <span data-ttu-id="7f68a-126">En outre, assurez-vous qu'un validateur de cache est défini.</span><span class="sxs-lookup"><span data-stu-id="7f68a-126">Also, ensure that a cache validator is set.</span></span> <span data-ttu-id="7f68a-127">Validateur de cache Hello peut être une dernière modification timestamp définie en appelant SetLastModified, ou une valeur etag définie en appelant SetETag.</span><span class="sxs-lookup"><span data-stu-id="7f68a-127">hello cache validator can be a Last Modified timestamp set by calling SetLastModified, or an etag value set by calling SetETag.</span></span> <span data-ttu-id="7f68a-128">Si vous le souhaitez, vous pouvez également spécifier un délai d’expiration de cache en appelant SetExpires, ou vous pouvez compter sur l’heuristique de cache par défaut hello décrit plus haut dans ce document.</span><span class="sxs-lookup"><span data-stu-id="7f68a-128">Optionally, you can also specify a cache expiration time by calling SetExpires, or you can rely on hello default cache heuristics described earlier in this document.</span></span>  

<span data-ttu-id="7f68a-129">Par exemple, toocache le contenu d’une heure, ajoutez hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="7f68a-129">For example, toocache content for one hour, add hello following:</span></span>  

```csharp
// Set hello caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a><span data-ttu-id="7f68a-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7f68a-130">Next Steps</span></span>
* [<span data-ttu-id="7f68a-131">Lire les détails à propos de hello **clientCache** élément</span><span class="sxs-lookup"><span data-stu-id="7f68a-131">Read details about hello **clientCache** element</span></span>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [<span data-ttu-id="7f68a-132">Lire la documentation hello pour hello **HttpResponse.Cache** propriété</span><span class="sxs-lookup"><span data-stu-id="7f68a-132">Read hello documentation for hello **HttpResponse.Cache** Property</span></span>](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* <span data-ttu-id="7f68a-133">[Lire la documentation hello pour hello **classe HttpCachePolicy**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f68a-133">[Read hello documentation for hello **HttpCachePolicy Class**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

