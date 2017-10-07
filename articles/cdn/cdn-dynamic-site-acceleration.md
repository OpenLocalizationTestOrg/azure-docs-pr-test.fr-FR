---
title: "aaaDynamic accélération de Site via le CDN Azure"
description: "Présentation approfondie de l’accélération de site dynamique"
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
ms.date: 08/02/2017
ms.author: v-semcev
ms.openlocfilehash: 37e6312ae5e83448f2d87c95ef48c387355748bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-site-acceleration-via-azure-cdn"></a>Accélération de site dynamique via Azure CDN

Avec éclatement de hello de médias sociaux, du commerce électronique et hello hyper personnalisés web, un pourcentage croissant de hello contenu tooend utilisateurs pris en charge est généré en temps réel. Les utilisateurs attendent des expériences web rapides, fiables et personnalisées, indépendamment de leur navigateur, de leur emplacement géographique, de leur appareil ou du réseau. Toutefois, les innovations très hello qui rendent ces expériences donc recourant également ralentir les téléchargements de la page et risque de compromettre la qualité de l’expérience du consommateur hello hello. 

Capacité de normes de CDN inclut hello capacité toocache fichiers proche tooend utilisateurs toospeed paramétrer la livraison des fichiers statiques. Toutefois, avec des applications web dynamiques, que le contenu dans les emplacements de bords de la mise en cache n’est pas possible, car le serveur de hello génère du contenu de hello dans toouser comportement de la réponse. Accélération de remise hello de ce contenu est plus complexe que traditionnelles de mise en cache et nécessite une solution de bout en bout qui règle finement chaque élément le long du chemin d’accès de la totalité des données hello à partir du début d’un toodelivery. Avec Azure CDN dynamique Site accélération (DSA), hello performances des pages web avec un contenu dynamique est sensiblement améliorées.

Azure CDN Akamai et Verizon optimise DSA via hello **optimisé pour** menu lors de la création du point de terminaison.

## <a name="configuring-cdn-endpoint-tooaccelerate-delivery-of-dynamic-files"></a>Configuration de la remise de tooaccelerate de point de terminaison CDN des fichiers dynamiques

Vous pouvez configurer la remise de votre toooptimize de point de terminaison CDN de fichiers dynamiques via le portail Azure en sélectionnant hello **accélération de site dynamique** option sous hello **optimisé pour** sélection de propriété lors de création du point de terminaison Hello. Vous pouvez également utiliser nos API REST ou des toodo de kits de développement logiciel client hello hello même chose par programme. 

### <a name="probe-path"></a>Chemin d’analyse
Chemin d’accès de la sonde est un tooDynamic spécifique de fonctionnalité accélération de Site, et valide est requis pour la création. DSA utilise un petit *chemin d’accès de la sonde* fichier placé sur hello origine toooptimize réseau configurations de routage pour hello CDN. Vous pouvez télécharger et télécharger notre exemple de site tooyour fichier ou utiliser un élément multimédia existant sur votre origine est à peu près 10 Ko pour le chemin d’accès de hello sonde à la place si hello actif existe.

> [!Note]
> L’accélération de site dynamique entraîne des frais supplémentaires. Pour plus d’informations, consultez hello [page de tarification](https://azure.microsoft.com/pricing/details/cdn/) pour plus d’informations.

Hello suivant des captures d’écran illustre les processus de hello via le portail Azure.
 
![Ajout d’un point de terminaison CDN](./media/cdn-dynamic-site-acceleration/01_Endpoint_Profile.png) 

*Figure 1 : Ajout d’un nouveau point de terminaison CDN de hello profil CDN*
 
![Création d’un point de terminaison CDN avec accélération de site dynamique](./media/cdn-dynamic-site-acceleration/02_Optimized_DSA.png)  

*Figure 2 : création d’un point de terminaison CDN avec l’option Optimisation de l’accélération de site dynamique sélectionnée*

Une fois que le point de terminaison CDN hello est créée, elle s’applique optimisations de DSA hello pour tous les fichiers qui correspondent à certains critères. Hello après section décrit l’optimisation de DSA en détail.

## <a name="dsa-optimization-using-azure-cdn"></a>Optimisation d’accélération de site dynamique à l’aide de la fonctionnalité Azure CDN

Accélération de Site dynamique sur Azure CDN accélère la remise de ressources dynamiques à l’aide de hello suivant techniques :

-   Optimisation du routage
-   Optimisations de protocole TCP
-   Prérécupération d’objet (Akamai uniquement)
-   Compression d’image mobile (Akamai uniquement)

### <a name="route-optimization"></a>Optimisation du routage

Optimisation de l’itinéraire est importante car hello Internet est dynamique, où le trafic et temporairement pannes constamment la topologie de réseau hello. Hello protocole BGP (Border Gateway) est le protocole de routage hello Hello Internet, mais il peut y avoir des itinéraires plus rapides via les serveurs de Point de présence (PoP) intermédiaires. 

Optimisation de l’itinéraire choisit d’origine toohello chemin d’accès optimal de hello afin qu’un site soit en continu le contenu accessible et dynamique est remis aux utilisateurs de tooend via hello plus rapide et plus fiable itinéraire possible. 

réseau de Akamai Hello utilise des données en temps réel de techniques toocollect et comparer des chemins d’accès différents via différents nœuds dans le serveur de Akamai hello, ainsi que l’itinéraire par défaut BGP hello sur hello ouvrir Internet toodetermine hello chemin le plus rapide entre l’origine de hello et hello Bord CDN. Ces techniques évitent les points de surcharge d’Internet et les itinéraires longs. 

De même, hello Verizon réseau utilise une combinaison de haute capacité Anycast DNS prend en charge POP et contrôles d’intégrité, toodetermine hello meilleures passerelles toobest données d’itinéraire à partir de hello origine toohello de client.
 
Par conséquent, de remettre le contenu entièrement dynamique et transactionnels plus rapidement et plus fiable tooend utilisateurs, même lorsqu’elle est uncacheable. 

### <a name="tcp-optimizations"></a>Optimisations de protocole TCP

Protocole TCP (Transmission Control) est la norme hello de suite de protocoles Internet hello utilisé toodeliver d’informations entre applications sur un réseau IP.  Par défaut, il existe plusieurs précédent et les deux sens demandes requis tooset d’une connexion TCP, ainsi que les limites tooavoid réseau des congestions, ce qui entraîne des inefficacités à grande échelle. Le CDN Azure d’Akamai traite ce problème en optimisant de trois façons : 

 - élimination des démarrages lents ;
 - exploitation des connexions persistantes ;
 - réglage des paramètres de paquet TCP (Akamai uniquement).

#### <a name="eliminating-slow-start"></a>Élimination des démarrages lents

*Démarrage lent* fait partie du protocole TCP hello qui empêche la congestion du réseau en limitant la quantité de hello des données envoyées via le réseau de hello. Il commence avec des tailles de fenêtre de congestion petite entre expéditeur et récepteur jusqu'à ce que hello maximale est atteinte ou une perte de paquets est détectée.

Azure CDN d’Akamai et de Verizon élimine les démarrages lents en trois étapes :

1.  Akamai et du Verizon réseau utilisent l’intégrité et la bande passante de l’analyse de la bande passante de hello toomeasure des connexions entre les serveurs de PoP edge.
2. métriques de Hello sont partagés entre les serveurs edge PoP afin que chaque serveur tient compte des conditions de réseau hello et l’intégrité du serveur de hello autres POP autour d’elles.  
3. Hello CDN bord les serveurs sont désormais en mesure de toomake hypothèses certains paramètres de transmission, telles que la taille de fenêtre optimale que hello doit être lors de la communication avec d’autres serveurs de périmètre CDN dans sa proximité. Cette étape signifie que la taille de fenêtre de congestion initiale hello peut être augmentée si la santé de connexion hello entre les serveurs de périmètre CDN hello hello est capable de transferts de données de paquet plus élevées.  

#### <a name="leveraging-persistent-connections"></a>Exploitation des connexions persistantes

Nombre d’ordinateurs uniques à l’aide d’un réseau CDN, connecteront tooyour directement par rapport aux utilisateurs qui se connectent directement tooyour origine du serveur d’origine. Azure CDN Akamai et Verizon regroupe également moins de connexions à l’origine de hello tooestablish ensemble de requêtes utilisateur.

Comme indiqué précédemment, les connexions TCP prennent plusieurs requêtes dans les deux sens dans une négociation de tooestablish une nouvelle connexion. Connexions persistantes, également appelé « HTTP Keep-Alive, » réutiliser les connexions TCP existantes pour plusieurs fois aller-retour HTTP demandes toosave et accélérer la remise. 

réseau de Verizon Hello envoie également des paquets persistants périodiques sur tooprevent de connexion TCP hello une connexion ouverte à partir de la fermeture.

#### <a name="tuning-tcp-packet-parameters"></a>Réglage des paramètres de paquet TCP

CDN Azure à partir d’Akamai également ajuste les paramètres hello qui régissent les connexions serveur à serveur et réduit hello trajet long round tooretrieve allers-retours requis contenu incorporé dans le site de hello à l’aide de hello suivant techniques :

1.  Augmentation de fenêtre de congestion initiale hello afin que plusieurs paquets peuvent être envoyés sans attendre d’accusé de réception.
2.  Réduit le délai d’attente de retransmission initiale hello afin qu’une perte est détectée, et retransmission se produit plus rapidement.
3.  Baisse hello et retransmettre le temps d’attente du délai d’attente tooreduce hello avant de considérer que les paquets ont été perdus durant la transmission.

### <a name="object-prefetch-akamai-only"></a>Prérécupération d’objet (Akamai uniquement)

La plupart des sites web sont constitués d’une page HTML, qui fait référence à diverses autres ressources telles que des images et des scripts. En général, lorsqu’un client demande une page Web, navigateur de hello télécharge tout d’abord analyse hello HTML objet et fait ensuite les demandes supplémentaires toolinked actifs qui sont requis toofully chargement la page de hello. 

*La prérécupération* est une technique tooretrieve images et des scripts intégrés dans hello page HTML tandis que hello HTML est pris en charge toohello navigateur avant hello navigateur permet même de ces demandes de l’objet. 

Avec hello **Prérécupérer** option est activée au moment de hello lorsque hello CDN sert le navigateur du client toohello hello HTML page de base, hello CDN analyse hello HTML fichier et effectuer des demandes supplémentaires pour toutes les ressources liées et stockez-le dans son cache. Lorsque hello client effectue des demandes de hello hello liée aux ressources de, serveur de périphérie hello CDN déjà a hello objets demandés et peut traiter les immédiatement sans une origine de toohello aller-retour. Cette optimisation est bénéfique pour le contenu tant mis en cache que non mis en cache.

### <a name="adaptive-image-compression-akamai-only"></a>Compression d’image adaptative (Akamai uniquement)

Certains appareils, en particulier les plus mobiles, expérience plus lents vitesses du réseau à partir de tootime de temps. Dans ces scénarios, il est plus avantageux pour les images plus petites tooreceive utilisateur hello dans leur page Web plus rapidement, au lieu d’en attente beaucoup de temps pour les images de résolution.

Cette fonctionnalité est automatiquement surveille la qualité du réseau et utilise les méthodes de compression JPEG standard lorsque les vitesses de réseau ont une durée de remise tooimprove plus lente.

Compression d’image adaptative | Extensions de fichier  
--- | ---  
Compression JPEG | .jpg, .jpeg, .jpe, .jig, .jgig, .jgi

## <a name="caching"></a>Mise en cache

Avec DSA, la mise en cache est désactivée par défaut sur hello CDN, même lorsque l’origine de hello inclut les en-têtes de cache-contrôle/arrive à expiration dans la réponse de hello. Cette valeur par défaut est désactivée, car DSA est généralement utilisée pour les ressources dynamiques de ne doivent pas être mis en cache, car elles sont tooeach unique client, et la mise en cache par défaut sous tension provoquer ce comportement.

Si vous avez un site Web avec un mélange de ressources statiques et dynamiques, il est meilleure tootake un hybride approche tooget hello des performances optimales. 

Si vous utilisez ADN avec Verizon Premium, vous pouvez activer la mise en cache dans des cas spécifiques à l’aide de hello du moteur de règles.  

Une autre solution consiste à toouse deux CDN points de terminaison. Un avec les composants DSA toodeliver dynamiques et un autre point de terminaison avec une optimisation statique type, par exemple général diffusion sur le web, les ressources pouvant être toodelivery. Dans tooaccomplish d’ordre ce remplacement, vous allez modifier votre toolink d’URL de page Web directement asset toohello sur hello de point de terminaison CDN vous envisagez de toouse. 

Par exemple : `mydynamic.azureedge.net/index.html` est une page dynamique et est chargé à partir du point de terminaison hello DSA.  Hello page html fait référence à plusieurs ressources statiques telles que des bibliothèques JavaScript ou les images qui sont chargés à partir de hello point de terminaison CDN statique, tel que `mystatic.azureedge.net/banner.jpg` et `mystatic.azureedge.net/scripts.js`. 

Vous trouverez un exemple [ici](https://docs.microsoft.com/azure/cdn/cdn-cloud-service-with-cdn#controller) sur comment contrôleurs toouse dans ASP.NET web tooserve contenu de l’application via une URL du CDN spécifique.




