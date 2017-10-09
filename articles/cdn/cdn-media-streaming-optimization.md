---
title: aaaMedia optimisation via hello Azure Content Delivery Network de diffusion en continu
description: "Optimisation de la diffusion en continu de fichiers multimédias pour une distribution lisse"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: v-semcev
ms.openlocfilehash: a05a86204708c7ea7ef1f9be04323cdda6a2d403
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="media-streaming-optimization-via-hello-azure-content-delivery-network"></a>Optimisation via hello Azure Content Delivery Network de diffusion multimédia en continu 
 
Utilisation de la vidéo haute définition augmente sur hello Internet, ce qui pose des difficultés pour la remise efficace des fichiers volumineux. Les clients attendent une lecture fluide de vidéo à la demande ou live ressources vidéo sur des réseaux et les clients monde hello. Un mécanisme de livraison rapide et efficace pour les fichiers de diffusion multimédia en continu est critique tooensure une expérience de consommateur lisse et plus agréable.  

Support de diffusion en continu en direct est toodeliver particulièrement difficile en raison de grande taille de hello et le nombre d’utilisateurs simultanés. Un retard provoque tooleave d’utilisateurs. Étant donné que les flux live ne peut pas être mis en cache avance et latences élevées ne sont pas acceptables tooviewers, fragments vidéo doivent être remis en temps voulu. 

modèles de demande Hello de diffusion en continu fournissent également certains défis. Quand un flux en direct populaires ou une nouvelle série est publiée pour la vidéo à la demande, des milliers toomillions des visionneuses peut demander le flux hello en hello même temps. Dans ce cas, demande active consolidation est vital toonot surcharger les serveurs d’origine hello lorsque les ressources hello ne sont pas encore mis en cache.
 
Bonjour Azure Content Delivery Network à partir d’Akamai propose désormais une fonctionnalité qui fournit les éléments multimédias en flux continu efficacement toousers monde hello à grande échelle. fonctionnalité de Hello réduit les latences, car il réduit la charge de hello sur les serveurs d’origine hello. Cette fonctionnalité est disponible avec le niveau de tarification Standard Akamai hello. 

Bonjour Azure Content Delivery Network de Verizon remet la diffusion multimédia en continu directement dans le type d’optimisation remise hello web général.
 
## <a name="configure-an-endpoint-toooptimize-media-streaming-in-hello-azure-content-delivery-network-from-akamai"></a>Configurer un point de terminaison toooptimize diffusion multimédia en continu Bonjour Azure Content Delivery Network à partir d’Akamai
 
Vous pouvez configurer la remise toooptimize point de terminaison de votre diffusion de contenu (CDN) de réseau pour les fichiers volumineux via hello portail Azure. Vous pouvez également utiliser nos API REST ou des hello client SDK toodo cela. Hello étapes suivantes montrent les processus hello via hello portail Azure :

1. tooadd un nouveau point de terminaison, sur hello **profil CDN** page, sélectionnez **point de terminaison**.
  
    ![Nouveau point de terminaison](./media/cdn-media-streaming-optimization/01_Adding.png)

2. Bonjour **optimisé pour** la liste déroulante, sélectionnez **vidéo sur la diffusion de contenu multimédia à la demande** pour les ressources de vidéo à la demande. Si vous offrez une combinaison de diffusion en continu en direct et de vidéo à la demande, sélectionnez **Streaming de contenu général**.

    ![Diffusion en continu sélectionné](./media/cdn-media-streaming-optimization/02_Creating.png) 
 
Après avoir créé le point de terminaison hello, elle s’applique à l’optimisation de hello pour tous les fichiers qui correspondent à certains critères. Hello après section décrit ce processus. 
 
## <a name="media-streaming-optimizations-for-hello-azure-content-delivery-network-from-akamai"></a>Optimisations pour hello Azure Content Delivery Network à partir d’Akamai de diffusion multimédia en continu
 
L’optimisation de la diffusion multimédia en continu d’Akamai est efficace pour la diffusion multimédia en continu en direct ou en vidéo à la demande, qui utilise des fragments multimédias individuels pour la remise. Ce processus diffère du transfert d’une seule ressource volumineuse via un téléchargement progressif ou en utilisant des demandes de plage d’octets. Pour plus d’informations sur ce style de livraison de données multimédia, voir [Optimisation des fichiers volumineux](cdn-large-file-optimization.md).


Hello media général de remise ou de vidéo à la demande media remise optimisation types utilisent un CDN multimédias toodeliver de back-end optimisations plus rapidement. Elle utilisent également des configurations pour les ressources multimédias, basées sur les meilleures pratiques apprises au fil du temps.

### <a name="caching"></a>Mise en cache

Si hello Azure Content Delivery Network à partir d’Akamai détecte que cet élément multimédia hello est un manifeste de diffusion en continu ou un fragment, il utilise différents délais d’expiration mise en cache à partir de la diffusion sur le web général. (Consultez la liste complète de hello Bonjour tableau suivant). Comme toujours, le cache-control ou Expires les en-têtes envoyés à partir de l’origine de hello sont respectées. Si l’élément multimédia de hello n’est pas une ressource multimédia, il met en cache à l’aide des délais d’expiration hello pour la remise de web général.

temps de mise en cache négatif court Hello est utile pour origine déchargement lorsque de nombreux utilisateurs demandent un fragment qui n’existe pas encore. Un exemple est un flux en continu où les paquets hello ne sont pas disponibles à partir de l’origine de hello cette seconde. intervalle de mise en cache plus Hello permet également de décharger des demandes à partir de l’origine de hello, car il est en général, le contenu vidéo n’est pas modifié.
 

|    | Généralités<br> web<br>livraison continue | Généralités<br> Médias<br> diffusion en continu | Vidéo à la demande <br>Médias<br> diffusion en continu  
--- | --- | --- | ---
Mise en cache : positive <br> HTTP 200, 203, 300, <br> 301, 302 et 410 | 7 jours |365 jours | 365 jours   
Mise en cache : négative <br> HTTP 204, 305, 404, <br> et 405 | Aucune | 1 seconde | 1 seconde
 
### <a name="deal-with-origin-failure"></a>Traitement des défaillances de l’origine  

Les livraisons de données multimédias générale et en vidéo à la demande ont aussi un délai d’expiration d’origine et un journal des tentatives basé sur les meilleures pratiques pour les modèles de demande standard. Par exemple, car la remise de support général est dynamiquement pour et livraison du support de vidéo à la demande, il utilise un délai plus court de la connexion en raison de la nature de temps toohello de diffusion en continu.

Lorsqu’une connexion arrive à expiration, hello CDN tente de renvoyer un nombre de fois avant l’envoi d’un client de toohello d’erreur « délai de la passerelle 504 - ». 

Lorsqu’un fichier correspond à la liste conditions hello fichier type et la taille, hello CDN utilise un comportement de hello pour la diffusion multimédia en continu. Autrement, il utilise une livraison web générale.
   
### <a name="conditions-for-media-streaming-optimization"></a>Conditions d’optimisation de la diffusion multimédia en direct 

Hello tableau suivant répertorie hello de toobe des critères pour l’optimisation de diffusion multimédia en continu : 
 
Types de diffusions en continu pris en charge | Extensions de fichier  
--- | ---  
Apple HLS | m3u8, m3u, m3ub, key, ts, aac
Adobe HDS | f4m, f4x, drmmeta, bootstrap, f4f,<br>Structure de l’URL seg-frag <br> (expression régulière correspondante : ^(/.*)Seq(\d+)-Frag(\d+)
DASH | mpd, dash, divx, ismv, m4s, m4v, mp4, mp4v, <br> sidx, webm, mp4a, m4a, isma
Diffusion en continu lisse | /manifest/,/QualityLevels/Fragments/
  

 
## <a name="media-streaming-optimizations-for-hello-azure-content-delivery-network-from-verizon"></a>Optimisations pour hello Azure Content Delivery Network de Verizon de diffusion multimédia en continu

Bonjour Azure Content Delivery Network de Verizon remet multimédias diffusion en continu directement à l’aide du type d’optimisation remise hello web général. Quelques fonctionnalités hello CDN aider directement à la livraison de ressources par défaut.

### <a name="partial-cache-sharing"></a>Partage de cache partiel

Partage du cache partiel permet de demandes de contenu toonew hello CDN tooserve partiellement mises en cache. Par exemple, si hello première demande toohello CDN entraîne une absence dans le cache, demande de hello est envoyé toohello origine. Bien que ce contenu incomplète est chargé dans hello cache du CDN, autres toohello demandes CDN peut démarrer l’obtention de ces données. 

### <a name="cache-fill-wait-time"></a>Temps d’attente de remplissage du cache

 fonction d’heure Hello cache remplissage attente force hello edge server toohold toutes les demandes ultérieures pour hello même ressource jusqu'à ce que la réponse HTTP en-têtes arrivent à partir du serveur d’origine hello. Si les en-têtes de réponse HTTP à partir de l’origine de hello arrivent avant expiration de hello, toutes les demandes qui ont été mis en attente sont pris en charge hors hello agrandissement du cache. À hello même moment, hello cache est rempli par les données d’origine de hello. Par défaut, le temps d’attente de hello cache remplissage a la valeur too3, 000 millisecondes. 

