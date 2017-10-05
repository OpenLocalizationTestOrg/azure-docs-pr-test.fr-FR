---
title: "Gérer l’expiration du contenu web dans Azure CDN | Microsoft Docs"
description: "Découvrez comment gérer l’expiration des contenus d’Azure Web Apps/Services cloud, d’ASP.NET ou d’IIS dans le réseau de distribution de contenu (CDN) Azure."
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
ms.openlocfilehash: c207d780857a61d4b1fc0f39e6185cae67abc955
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a><span data-ttu-id="aa6a9-103">Gérer l’expiration des contenus d’Azure Web Apps/Services cloud, d’ASP.NET ou d’IIS dans le réseau de distribution de contenu (CDN) Azure</span><span class="sxs-lookup"><span data-stu-id="aa6a9-103">Manage expiration of Azure Web Apps/Cloud Services, ASP.NET, or IIS content in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aa6a9-104">Azure Web Apps/Cloud Services, ASP.NET ou IIS</span><span class="sxs-lookup"><span data-stu-id="aa6a9-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="aa6a9-105">Service Azure Storage Blob</span><span class="sxs-lookup"><span data-stu-id="aa6a9-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="aa6a9-106">Les fichiers d’un serveur web d’origine publiquement accessible peuvent être mis en cache dans le réseau de distribution de contenu (CDN) Azure jusqu’à l’expiration de leur durée de vie (TTL).</span><span class="sxs-lookup"><span data-stu-id="aa6a9-106">Files from any publicly accessible origin web server can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="aa6a9-107">La durée de vie est déterminée par [l’en-tête *Cache-Control*](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) dans la réponse HTTP du serveur d’origine.</span><span class="sxs-lookup"><span data-stu-id="aa6a9-107">The TTL is determined by the [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in the HTTP response from the origin server.</span></span>  <span data-ttu-id="aa6a9-108">Cet article décrit comment définir des en-têtes `Cache-Control` pour Azure Web Apps, Services cloud Azure, les applications ASP.NET et les sites Internet Information Services, qui sont tous configurés de façon similaire.</span><span class="sxs-lookup"><span data-stu-id="aa6a9-108">This article describes how to set `Cache-Control` headers for Azure Web Apps, Azure Cloud Services, ASP.NET applications, and Internet Information Services sites, all of which are configured similarly.</span></span>

> [!TIP]
> <span data-ttu-id="aa6a9-109">Vous pouvez choisir de ne pas définir de durée de vie sur un fichier.</span><span class="sxs-lookup"><span data-stu-id="aa6a9-109">You may choose to set no TTL on a file.</span></span>  <span data-ttu-id="aa6a9-110">Dans ce cas, Azure CDN applique automatiquement une durée de vie de sept jours par défaut.</span><span class="sxs-lookup"><span data-stu-id="aa6a9-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="aa6a9-111">Pour plus d’informations sur la façon dont le CDN Azure accélère l’accès aux fichiers et à d’autres ressources, consultez [Vue d’ensemble du réseau de distribution de contenu (CDN) Azure](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aa6a9-111">For more information about how Azure CDN works to speed up access to files and other resources, see the [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a><span data-ttu-id="aa6a9-112">Définition d’en-têtes Cache-Control dans la configuration</span><span class="sxs-lookup"><span data-stu-id="aa6a9-112">Setting Cache-Control Headers in configuration</span></span>
<span data-ttu-id="aa6a9-113">Pour le contenu statique, tel que les images et les feuilles de style, vous pouvez contrôler la fréquence de mise à jour en modifiant les fichiers **applicationHost.config** ou **web.config** de votre application web.</span><span class="sxs-lookup"><span data-stu-id="aa6a9-113">For static content, such as images and style sheets, you can control the update frequency by modifying the **applicationHost.config** or **web.config** files for your web application.</span></span>  <span data-ttu-id="aa6a9-114">L’élément **system.webServer\staticContent\clientCache** du fichier de configuration définit l’en-tête `Cache-Control` pour votre contenu.</span><span class="sxs-lookup"><span data-stu-id="aa6a9-114">The **system.webServer\staticContent\clientCache** element in the configuration file will set the `Cache-Control` header for your content.</span></span> <span data-ttu-id="aa6a9-115">Pour **web.config**, les paramètres de configuration affectent tous les éléments du dossier et de tous les sous-dossiers, sauf s’ils sont remplacés au niveau sous-dossier.</span><span class="sxs-lookup"><span data-stu-id="aa6a9-115">For **web.config**, the configuration settings will affect everything in the folder and all subfolders, unless overridden at the subfolder level.</span></span>  <span data-ttu-id="aa6a9-116">Par exemple, vous pouvez définir une durée de vie par défaut à la racine pour que tout le contenu statique soit mis en cache pendant 3 jours, tout en définissant une durée de mise en cache de 6 heures pour un sous-dossier dont le contenu varie davantage.</span><span class="sxs-lookup"><span data-stu-id="aa6a9-116">For example, you can set a default time-to-live at the root to have all static content cached for 3 days, but have a subfolder that has more variable content with a cache setting of 6 hours.</span></span>  <span data-ttu-id="aa6a9-117">Pour **applicationHost.config**, toutes les applications du site sont affectées, mais peuvent être remplacées dans les fichiers **web.config** des applications.</span><span class="sxs-lookup"><span data-stu-id="aa6a9-117">For **applicationHost.config**, all applications on the site will be affected, but can be overridden in **web.config** files in the applications.</span></span>

<span data-ttu-id="aa6a9-118">Le code XML suivant montre comment configurer **clientCache** pour spécifier un âge maximal de 3 jours :</span><span class="sxs-lookup"><span data-stu-id="aa6a9-118">The following XML shows an example of setting **clientCache** to specify a maximum age of 3 days:</span></span>  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

<span data-ttu-id="aa6a9-119">Le fait de spécifier **UseMaxAge** ajoute un en-tête `Cache-Control: max-age=<nnn>` à la réponse en fonction de la valeur spécifiée dans l’attribut **CacheControlMaxAge**.</span><span class="sxs-lookup"><span data-stu-id="aa6a9-119">Specifying **UseMaxAge** adds a `Cache-Control: max-age=<nnn>` header to the response based on the value specified in the **CacheControlMaxAge** attribute.</span></span> <span data-ttu-id="aa6a9-120">Le format de la période pour l’attribut **cacheControlMaxAge** est <days>.<hours>:<min>:<sec>.</span><span class="sxs-lookup"><span data-stu-id="aa6a9-120">The format of the timespan is for the **cacheControlMaxAge** attribute is <days>.<hours>:<min>:<sec>.</span></span> <span data-ttu-id="aa6a9-121">Pour plus d’informations sur le nœud **clientCache**, consultez [Cache client <clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span><span class="sxs-lookup"><span data-stu-id="aa6a9-121">For more information on the **clientCache** node, see [Client Cache <clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span></span>  

## <a name="setting-cache-control-headers-in-code"></a><span data-ttu-id="aa6a9-122">Définition d’en-têtes Cache-Control dans le code</span><span class="sxs-lookup"><span data-stu-id="aa6a9-122">Setting Cache-Control Headers in Code</span></span>
<span data-ttu-id="aa6a9-123">Pour les applications ASP.NET, vous pouvez définir le comportement de mise en cache dans le CDN par programme en définissant la propriété **HttpResponse.Cache** .</span><span class="sxs-lookup"><span data-stu-id="aa6a9-123">For ASP.NET applications, you can set the CDN caching behavior programmatically by setting the **HttpResponse.Cache** property.</span></span> <span data-ttu-id="aa6a9-124">Pour plus d’informations sur la propriété **HttpResponse.Cache**, consultez les pages [HttpResponse.Cache, propriété](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) et [HttpCachePolicy, classe](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="aa6a9-124">For more information on the **HttpResponse.Cache** property, see [HttpResponse.Cache Property](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) and [HttpCachePolicy Class](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

<span data-ttu-id="aa6a9-125">Si vous souhaitez mettre en cache du contenu d’application par programme dans ASP.NET, assurez-vous que le contenu est marqué comme pouvant être mis en cache en définissant HttpCacheability sur *Public*.</span><span class="sxs-lookup"><span data-stu-id="aa6a9-125">If you want to programmatically cache application content in ASP.NET, make sure that the content is marked as cacheable by setting HttpCacheability to *Public*.</span></span> <span data-ttu-id="aa6a9-126">En outre, assurez-vous qu'un validateur de cache est défini.</span><span class="sxs-lookup"><span data-stu-id="aa6a9-126">Also, ensure that a cache validator is set.</span></span> <span data-ttu-id="aa6a9-127">Le validateur de cache peut être un horodatage de dernière modification défini en appelant SetLastModified, ou une valeur etag définie en appelant SetETag.</span><span class="sxs-lookup"><span data-stu-id="aa6a9-127">The cache validator can be a Last Modified timestamp set by calling SetLastModified, or an etag value set by calling SetETag.</span></span> <span data-ttu-id="aa6a9-128">Si vous le souhaitez, vous pouvez également spécifier un délai d'expiration du cache en appelant SetExpires, ou vous pouvez vous en remettre à la méthode heuristique de mise en cache par défaut décrite précédemment dans ce document.</span><span class="sxs-lookup"><span data-stu-id="aa6a9-128">Optionally, you can also specify a cache expiration time by calling SetExpires, or you can rely on the default cache heuristics described earlier in this document.</span></span>  

<span data-ttu-id="aa6a9-129">Par exemple, pour mettre en cache du contenu pendant une heure, ajoutez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="aa6a9-129">For example, to cache content for one hour, add the following:</span></span>  

```csharp
// Set the caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a><span data-ttu-id="aa6a9-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aa6a9-130">Next Steps</span></span>
* [<span data-ttu-id="aa6a9-131">Découvrir les détails de l’élément **clientCache**</span><span class="sxs-lookup"><span data-stu-id="aa6a9-131">Read details about the **clientCache** element</span></span>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [<span data-ttu-id="aa6a9-132">Consulter la documentation de la propriété **HttpResponse.Cache**</span><span class="sxs-lookup"><span data-stu-id="aa6a9-132">Read the documentation for the **HttpResponse.Cache** Property</span></span>](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* <span data-ttu-id="aa6a9-133">[Lire la documentation concernant la **classe HttpCachePolicy**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="aa6a9-133">[Read the documentation for the **HttpCachePolicy Class**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

