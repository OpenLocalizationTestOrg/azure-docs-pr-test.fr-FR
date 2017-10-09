---
title: "aaaManage stratégie de mise en cache Azure CDN dans Azure Media Services | Documents Microsoft"
description: "Découvrez comment toomanage stratégie de mise en cache Azure CDN dans Azure Media Services."
services: media-services,cdn
documentationcenter: .NET
author: juliako
manager: erikre
editor: 
ms.assetid: be33aecc-6dbe-43d7-a056-10ba911e0e94
ms.service: media-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/04/2017
ms.author: juliako
ms.openlocfilehash: 4c7ee2922fcbb5727e10fbe44fc6e61b79f6917c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-cdn-caching-policy-in-azure-media-services"></a>Gérer la stratégie de mise en cache CDN dans Azure Media Services
Azure Media Services fournit la diffusion en continu adaptative HTTP et le téléchargement progressif. La diffusion en continu HTTP est hautement évolutive de par les avantages de mise en cache dans le proxy et les couches CDN, et la mise en cache côté client. Les points de terminaison de la diffusion en continu fournissent des fonctionnalités générales de diffusion en continu et de configuration pour les en-têtes HTTP du cache. Les points de terminaison de diffusion en continu définissent le contrôle de cache HTTP : les en-têtes max-age et Expires. Pour plus d'informations sur les en-têtes de cache HTTP, rendez-vous sur le site [W3.org](http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html).

## <a name="default-caching-headers"></a>En-têtes de mise en cache par défaut
Les points de terminaison de diffusion en continu appliquent par défaut des en-têtes de cache de 3 jours pour les données de diffusion en continu à la demande (fragments/segments de médias réels) et les fichiers manifestes (ou sélections). Pour la diffusion en continu en direct, les points de terminaison de diffusion en continu appliquent des en-têtes de cache de 3 jours pour les données (fragments/segments de médias réels) et une en-tête de cache de 2 secondes pour les requêtes de fichier manifeste (ou sélections). En-têtes du cache de la diffusion en continu à la demande s’appliquent lorsque le programme en direct active à la demande tooon (archive en direct).

## <a name="azure-cdn-integration"></a>Intégration d’Azure CDN
Azure Media Services propose un [CDN intégré](https://azure.microsoft.com/updates/azure-media-services-now-fully-integrated-with-azure-cdn/) pour les points de terminaison de diffusion en continu. En-têtes du cache-control applique Bonjour même façon que la diffusion en continu tooCDN de points de terminaison activé des points de terminaison de diffusion en continu. Azure CDN utilise en interne de diffusion en continu configuré un point de terminaison du cache valeurs toodefine hello durée de vie hello objets mis en cache et utilise également ce en-têtes du cache de valeur tooset hello remise. Lors de l’utilisation du CDN activé des points de terminaison de diffusion en continu, il est déconseillé tooset les valeurs de cache de petite taille. Petites valeurs de paramètre pour réduire les performances de hello et réduire l’avantage hello du CDN. En-têtes de cache tooset inférieures à 600 secondes pour le CDN activé des points de terminaison de diffusion en continu n’est pas autorisée.

> [!IMPORTANT]
>Azure Media Services est complètement intégré à Azure CDN. Avec un seul clic, vous pouvez intégrer tous les hello disponible Azure CDN fournisseurs (Akamai et Verizon) tooyour point de terminaison, y compris les produits CDN Standard et Premium de diffusion en continu. Pour plus d’informations, consultez cette [annonce](https://azure.microsoft.com/blog/standardstreamingendpoint/).
> 
> Frais de données à partir de la diffusion en continu de point de terminaison tooCDN obtient désactivé uniquement si hello CDN est activé sur le point de terminaison API de diffusion en continu ou à l’aide de la section de point de terminaison de diffusion en continu du portail de gestion Azure. Intégration manuelle ou créer directement un point de terminaison CDN à l’aide des API de CDN ou de la section portail ne désactive pas les frais de données hello.

## <a name="configuring-cache-headers-with-azure-media-services"></a>Configuration des en-têtes de cache avec Azure Media Services
Vous pouvez utiliser le portail de gestion Azure ou les valeurs d’en-tête cache tooconfigure API Azure Media Services.

1. les en-têtes de cache tooconfigure à l’aide de la gestion de portail, consultez trop[comment les points de terminaison de diffusion en continu de tooManage](../media-services/media-services-portal-manage-streaming-endpoints.md) hello de configuration section point de terminaison de diffusion en continu.
2. API REST d'Azure Media Services, [StreamingEndpoint](https://msdn.microsoft.com/library/azure/dn783468.aspx#StreamingEndpointCacheControl).
3. Kit de développement logiciel (SDK) .NET Azure Media Services, [Propriétés StreamingEndpointCacheControl](http://go.microsoft.com/fwlink/?LinkId=615302).

## <a name="cache-configuration-precedence-order"></a>Ordre de priorité de la configuration du cache
1. La valeur configurée du cache Azure Media Services remplace la valeur par défaut.
2. S'il n'existe aucune configuration manuelle, les valeurs par défaut s'appliquent.
3. Par défaut, 2 secondes en-têtes du cache s’applique toolive manifest(playlist), quelle que soit la configuration d’Azure Media ou le stockage Azure de diffusion en continu et de la substitution de cette valeur n’est pas disponible.

