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
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a>Gérer l’expiration des contenus d’Azure Web Apps/Services cloud, d’ASP.NET ou d’IIS dans le réseau de distribution de contenu (CDN) Azure
> [!div class="op_single_selector"]
> * [Azure Web Apps/Cloud Services, ASP.NET ou IIS](cdn-manage-expiration-of-cloud-service-content.md)
> * [Service Azure Storage Blob](cdn-manage-expiration-of-blob-content.md)
> 
> 

Les fichiers d’un serveur web d’origine publiquement accessible peuvent être mis en cache dans le réseau de distribution de contenu (CDN) Azure jusqu’à l’expiration de leur durée de vie (TTL).  durée de vie Hello est déterminée par hello [ *Cache-Control* en-tête](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) en réponse hello HTTP à partir du serveur d’origine hello.  Cet article décrit comment tooset `Cache-Control` les en-têtes pour les applications Web Azure, Azure Cloud Services, les applications ASP.NET et les sites Internet Information Services, qui sont configurés de la même façon.

> [!TIP]
> Vous ne pouvez choisir tooset aucune durée de vie d’un fichier.  Dans ce cas, Azure CDN applique automatiquement une durée de vie de sept jours par défaut.
> 
> Pour plus d’informations sur le fonctionnement de Azure CDN toospeed toofiles d’accès et d’autres ressources, consultez hello [vue d’ensemble du CDN Azure](cdn-overview.md).
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a>Définition d’en-têtes Cache-Control dans la configuration
Pour le contenu statique, comme des images et des feuilles de style, vous pouvez contrôler la fréquence de mise à jour hello en modifiant hello **applicationHost.config** ou **web.config** les fichiers de votre application web.  Hello **system.webServer\staticContent\clientCache** élément dans le fichier de configuration hello définira hello `Cache-Control` en-tête pour votre contenu. Pour **web.config**, paramètres de configuration hello affectent tous les éléments dans le dossier de hello et tous ses sous-dossiers, sauf si la substitution au niveau du sous-dossier hello.  Par exemple, vous pouvez définir une valeur par défaut time-to-live à hello racine toohave statique tout le contenu mis en cache pendant 3 jours, mais ont un sous-dossier qui a le plus variable avec un paramètre de cache de 6 heures.  Pour **applicationHost.config**, toutes les applications sur site de hello seront affectées, mais peut être substituées dans **web.config** fichiers dans les applications de hello.

Hello code XML suivant montre un exemple de paramètre **clientCache** toospecify un âge maximal de 3 jours :  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

Spécification de **UseMaxAge** ajoute un `Cache-Control: max-age=<nnn>` toohello réponse de l’en-tête en fonction de la valeur hello spécifié dans hello **CacheControlMaxAge** attribut. format Hello hello TimeSpan concerne hello **cacheControlMaxAge** attribut est <days>.<hours>:<min>:<sec>. Pour plus d’informations sur hello **clientCache** nœud, consultez [cache du Client <clientCache> ](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).  

## <a name="setting-cache-control-headers-in-code"></a>Définition d’en-têtes Cache-Control dans le code
Pour les applications ASP.NET, vous pouvez définir comportement de mise en cache CDN hello par programme en définissant la hello **HttpResponse.Cache** propriété. Pour plus d’informations sur hello **HttpResponse.Cache** propriété, consultez [propriété HttpResponse.Cache](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) et [classe HttpCachePolicy](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).  

Si vous souhaitez que le contenu de l’application cache tooprogrammatically dans ASP.NET, assurez-vous que le contenu de hello est marqué comme pouvant être en définissant HttpCacheability trop*Public*. En outre, assurez-vous qu'un validateur de cache est défini. Validateur de cache Hello peut être une dernière modification timestamp définie en appelant SetLastModified, ou une valeur etag définie en appelant SetETag. Si vous le souhaitez, vous pouvez également spécifier un délai d’expiration de cache en appelant SetExpires, ou vous pouvez compter sur l’heuristique de cache par défaut hello décrit plus haut dans ce document.  

Par exemple, toocache le contenu d’une heure, ajoutez hello qui suit :  

```csharp
// Set hello caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a>Étapes suivantes
* [Lire les détails à propos de hello **clientCache** élément](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [Lire la documentation hello pour hello **HttpResponse.Cache** propriété](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* [Lire la documentation hello pour hello **classe HttpCachePolicy**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).  

