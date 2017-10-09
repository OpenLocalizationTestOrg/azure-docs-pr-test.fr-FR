---
title: "aaaAzure vue d’ensemble du CDN | Documents Microsoft"
description: "En savoir quelles hello est de réseau de distribution de contenu (CDN) Azure et comment toouse il toodeliver le contenu haut débit en mettant en cache des objets BLOB et le contenu statique."
services: cdn
documentationcenter: 
author: smcevoy
manager: akucer
editor: 
ms.assetid: 866e0c30-1f33-43a5-91f0-d22f033b16c6
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/08/2017
ms.author: v-semcev
ms.openlocfilehash: e0230a6e107969b845985f2f4d357bf93cd40d42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-azure-content-delivery-network-cdn"></a>Vue d’ensemble de hello réseau de distribution contenu (CDN) Azure
> [!NOTE]
> Ce document décrit le hello Azure réseau CDN (Content Delivery) est, de son fonctionnement et de fonctionnalités de hello de chaque produit Azure CDN.  Si vous souhaitez tooskip ces informations et que vous passez tooa droite didacticiel sur la façon de toocreate un point de terminaison CDN, consultez [à l’aide de Azure CDN](cdn-create-new-endpoint.md).  Si vous souhaitez toosee une liste des emplacements de nœud CDN actuels, consultez [Azure CDN POP emplacements](cdn-pop-locations.md).
> 
> 

Hello réseau de distribution de contenu (CDN) Azure met en cache le contenu web statique au débit maximal de tooprovide emplacements stratégiques pour la diffusion de contenu toousers.  Hello CDN offre aux développeurs une solution globale pour la diffusion de contenu haut débit en mettant en cache le contenu sur des nœuds physiques hello entre Bonjour. 

Hello les avantages de l’utilisation des ressources de site web toocache hello CDN :

* Meilleures performances et une expérience utilisateur pour les utilisateurs finaux, en particulier lorsque l’utilisation d’applications où se trouvent plusieurs allers-retours requis contenu de tooload.
* Grand mise à l’échelle toobetter handle instantanée des charges importantes, comme au début de hello d’un produit lancer l’événement.
* En répartissant les demandes utilisateur et fournit du contenu à partir de serveurs edge, moins de trafic est envoyé toohello origine.

## <a name="how-it-works"></a>Fonctionnement
![Présentation du CDN](./media/cdn-overview/cdn-overview.png)

1. Un utilisateur (Alice) demande un fichier (également appelé ressource) à l’aide d’une URL avec un nom de domaine spécial, par exemple `<endpointname>.azureedge.net`.  DNS achemine l’emplacement de Point de présence (POP) performante qui soit hello demande toohello.  Cela est généralement hello POP qui est le plus proche géographiquement toohello utilisateur.
2. Si les serveurs de bord de hello Bonjour POP n’ont pas de fichier de hello dans leur cache, hello fichier hello demandes du serveur de bord à partir de l’origine de hello.  origine de Hello peut être une application Web Azure, Azure Cloud Service, compte de stockage Azure ou n’importe quel serveur web accessible publiquement.
3. origine de Hello retourne hello toohello bord serveur de fichiers, y compris les en-têtes HTTP facultatifs décrivant Time-to-Live du fichier hello (TTL).
4. serveur de périphérie Hello met en cache les fichiers hello et retourne le demandeur d’origine hello fichier toohello (Alice).  fichier de Hello reste mis en cache sur le serveur de périphérie hello jusqu'à expiration de la durée de vie de hello.  Si l’origine de hello ne spécifiait pas une durée de vie, la valeur par défaut de hello durée de vie est de sept jours.
5. Des utilisateurs supplémentaires peuvent ensuite hello demande à l’aide de cette même URL de fichier et peut également être dirigé toothat même POP.
6. Si hello durée de vie pour le fichier de hello n’a pas expiré, serveur de périphérie hello retourne les fichier hello hello cache.  L’expérience utilisateur est en conséquence plus rapide et plus réactive.

## <a name="azure-cdn-features"></a>Fonctionnalités d’Azure CDN
Il existe trois produits Azure CDN :  **Azure CDN Standard fourni par Akamai**, **Azure CDN Standard fourni par Verizon** et **Azure CDN Premium fourni par Verizon**.  Hello tableau suivant répertorie les fonctionnalités de hello disponibles avec chaque produit.

|  | Standard Akamai | Standard Verizon | Premium Verizon |
| --- | --- | --- | --- |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  __Fonctionnalités de performance et optimisations__ |
| [Accélération de site dynamique](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration) | **&amp;#x2713;**  | **&amp;#x2713;** | **&amp;#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  [Accélération de Site dynamique - Compression d’Image adaptative](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#adaptive-image-compression-akamai-only) | **&amp;#x2713;**  |  |  |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  [Accélération de Site dynamique - Récupération de l’objet](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#object-prefetch-akamai-only) | **&amp;#x2713;**  |  |  |
| [Optimisation du streaming vidéo](https://docs.microsoft.com/azure/cdn/cdn-media-streaming-optimization) | **&amp;#x2713;**  | \* |  \* |
| [Optimisation des fichiers volumineux](https://docs.microsoft.com/azure/cdn/cdn-large-file-optimization) | **&amp;#x2713;**  | \* |  \* |
| [Équilibrage de charge du serveur global (GSLB)](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-load-balancing-azure) |**&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| [Purge rapide](cdn-purge-endpoint.md) |**&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| [Préchargement de ressources](cdn-preload-endpoint.md) | |**&amp;#x2713;** |**&amp;#x2713;** |
| [Mise en cache des chaînes de requête](cdn-query-string.md) |**&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| Double pile IPv4/IPv6 |**&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| [Assistance HTTP/2](cdn-http2.md) |**&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  __Sécurité__ |
| Prise en charge HTTPS avec un point de terminaison CDN |**&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| [HTTPS sur un domaine personnalisé](cdn-custom-ssl.md) | |**&amp;#x2713;** |**&amp;#x2713;** |
| [Prise en charge du nom de domaine personnalisé](cdn-map-content-to-custom-domain.md) |**&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| [Filtrage géographique](cdn-restrict-access-by-country.md) |**&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| [Jeton d’authentification](cdn-token-auth.md)|  |  |**&amp;#x2713;**| 
| [Protection DDOS](https://www.us-cert.gov/ncas/tips/ST04-015) |**&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  __Analyse et création de rapports__ |
| [Analyse principale](cdn-analyze-usage-patterns.md) | **&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| [Rapports HTTP avancés](cdn-advanced-http-reports.md) | | |**&amp;#x2713;** |
| [Statistiques en temps réel](cdn-real-time-stats.md) | | |**&amp;#x2713;** |
| [Alertes en temps réel](cdn-real-time-alerts.md) | | |**&amp;#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  __Simplicité d’utilisation__ |
| Intégration simple des services Azure tels que [Storage](cdn-create-a-storage-account-with-cdn.md), [Cloud Services](cdn-cloud-service-with-cdn.md), [Web Apps](../app-service-web/app-service-web-tutorial-content-delivery-network.md) et [Media Services](../media-services/media-services-portal-manage-streaming-endpoints.md) |**&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| Gestion via [REST API](https://msdn.microsoft.com/library/mt634456.aspx), [.NET](cdn-app-dev-net.md), [Node.js](cdn-app-dev-node.md) ou [PowerShell](cdn-manage-powershell.md). |**&amp;#x2713;** |**&amp;#x2713;** |**&amp;#x2713;** |
| [Moteur de distribution de contenu personnalisable et basé sur des règles](cdn-rules-engine.md) | | |**&amp;#x2713;** |
| Paramètres du cache/des en-têtes (à l’aide du [moteur de règles](cdn-rules-engine.md)) | | |**&amp;#x2713;** |
| Redirection/réécriture d’URL (à l’aide du [moteur de règles](cdn-rules-engine.md)) | | |**&amp;#x2713;** |
| Règles d’appareil mobile (à l’aide du [moteur de règles](cdn-rules-engine.md)) | | |**&amp;#x2713;** |

\* Verizon prend en charge l’envoi de fichiers et de médias volumineux directement via la livraison web générale.


> [!TIP]
> Existe-t-il une fonctionnalité que vous aimeriez toosee dans Azure CDN ?  [Envoyez-nous vos commentaires](https://feedback.azure.com/forums/169397-cdn)! 
> 
> 

## <a name="next-steps"></a>Étapes suivantes
tooget main CDN, consultez [à l’aide de Azure CDN](cdn-create-new-endpoint.md).

Si vous êtes un client CDN existant, vous pouvez désormais gérer vos points de terminaison CDN via hello [portail Microsoft Azure](https://portal.azure.com) ou [PowerShell](cdn-manage-powershell.md).

toosee hello CDN en action, consultez hello [vidéo de votre session de Build 2016](https://azure.microsoft.com/documentation/videos/build-2016-leveraging-the-new-azure-cdn-apis-to-build-wicked-fast-applications/).

Découvrez comment tooautomate CDN Azure avec [.NET](cdn-app-dev-net.md) ou [Node.js](cdn-app-dev-node.md).

Pour obtenir des informations sur la tarification, consultez la page [Prix appliqués au Réseau de distribution de contenu (CDN)](https://azure.microsoft.com/pricing/details/cdn/).

