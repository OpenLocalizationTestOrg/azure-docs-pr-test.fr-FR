---
title: "Considérations relatives à l’aaaPerformance de Azure Traffic Manager | Documents Microsoft"
description: "Comprendre les performances de Traffic Manager et comment tootest les performances de votre site Web lors de l’utilisation de Traffic Manager"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 3ba5dfa1-2922-43f1-9a23-d06969c4a516
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: fd4e6cb221a2ceee63ec57237ee90fd714e91db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-considerations-for-traffic-manager"></a>Considérations sur les performances de Traffic Manager

Cette page explique les considérations relatives aux performances de Traffic Manager. Tenez compte des hello scénario :

Vous avez des instances de votre site Web Bonjour WestUS et régions de l’Asie de l’est. Une des instances de hello est en cours d’intégrité hello pour la sonde de hello traffic manager. Trafic de l’application est la région d’intègre de toohello dirigée. Ce basculement est attendu mais performances peuvent être un problème en fonction de latence hello du trafic hello maintenant en déplacement tooa la région géographiquement distincts.

## <a name="performance-considerations-for-traffic-manager"></a>Considérations sur les performances de Traffic Manager

Hello uniquement impact sur les performances que Traffic Manager peut avoir sur votre site Web est la recherche DNS hello initiale. Une requête DNS pour le nom hello de votre profil Traffic Manager est gérée par le serveur de racine DNS Microsoft hello qui héberge la zone trafficmanager.net hello. Traffic Manager remplit et régulièrement mises à jour, hello DNS racine serveurs Microsoft basés sur une stratégie Traffic Manager hello et les résultats de la sonde hello. Par conséquent, même pendant la recherche DNS initiale hello, aucune requête DNS n’est envoyés tooTraffic Manager.

Traffic Manager est constitué de plusieurs composants : serveurs, un service API, couche de stockage hello et un point de terminaison de service d’analyse de nom DNS. Si un composant de service de Traffic Manager échoue, il n’a aucun effet sur le nom DNS de hello associé à votre profil Traffic Manager. enregistrements Hello dans les serveurs DNS Microsoft hello restent inchangés. Toutefois, la surveillance des points de terminaison et la mise à jour DNS n’ont pas lieu. Par conséquent, Traffic Manager n’est pas le site de basculement en mesure de tooupdate DNS toopoint tooyour lorsque votre site principal tombe en panne.

La résolution de noms DNS est rapide et les résultats sont mis en cache. la vitesse de recherche DNS initiale hello Hello dépend hello client hello de serveurs DNS utilise pour la résolution de nom. En règle générale, un client peut effectuer une recherche DNS en environ 50 ms. Hello de recherche de hello sont mis en cache pour la durée hello Hello DNS Time-to-live (TTL). la valeur par défaut de Hello durée de vie de Traffic Manager est de 300 secondes.

Le trafic N’est PAS transmis via Traffic Manager. Une fois la recherche DNS hello terminée, client de hello a une adresse IP d’une instance de votre site web. Hello client connecte directement toothat adresse et ne passe pas par le biais de Traffic Manager. Hello stratégie Traffic Manager que vous choisissez a aucune influence sur les performances de DNS hello. Toutefois, une méthode routage performances peut nuire aux expérience d’application hello. Par exemple, si votre stratégie redirige le trafic à partir de l’instance de tooan Amérique du Nord hébergé en Asie, latence du réseau hello pour les sessions peut être un problème de performances.

## <a name="measuring-traffic-manager-performance"></a>Mesure des performances de Traffic Manager

Il existe plusieurs sites Web, vous pouvez utiliser toounderstand hello et les performances d’un profil Traffic Manager. La plupart de ces sites sont gratuits mais peuvent comporter des limites. Certains sites proposent des fonctionnalités payantes de surveillance et de génération de rapports améliorées.

outils Hello sur ces sites mesurent des latences de DNS et affichage hello résolu des adresses IP pour les emplacements des clients monde hello. La plupart de ces outils ne mettent pas en cache des résultats DNS hello. Par conséquent, les outils de hello montrent la recherche DNS complet hello chaque fois qu'un test est exécuté. Lorsque vous testez votre propre client, vous rencontrez uniquement performances de recherche DNS complet hello qu’une seule fois pendant la durée de vie hello.

## <a name="sample-tools-toomeasure-dns-performance"></a>Exemple outils toomeasure DNS performances

* [SolveDNS](http://www.solvedns.com/dns-comparison/)

    SolveDNS offre de nombreux outils de performances. outil de comparaison de DNS Hello vous indique la durée tooresolve votre nom DNS et comment qui compare les fournisseurs de services DNS tooother.

* [WebSitePulse](http://www.websitepulse.com/help/tools.php)

    Un des outils de la plus simple de hello est WebSitePulse. Entrez les temps de résolution DNS hello URL toosee, le premier octet, dernier octet et autres statistiques sur les performances. Vous pouvez choisir entre trois emplacements de test différents. Dans cet exemple, vous voyez que l’exécution du premier hello indique que la recherche DNS accepte 0.204 s.

    ![pulse1](./media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse.png)

    Étant donné que hello sont mis en cache, le deuxième test un hello pour hello recherche DNS de hello du point de terminaison Traffic Manager même prend 0,002 s.

    ![pulse2](./media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse2.png)

* [CA App Synthetic Monitor](https://asm.ca.com/en/checkit.php)

    Anciennement appelé outil du site Web de vérification Watchmouse hello, ce site vous montrent hello résolution DNS de temps à partir de plusieurs zones géographiques simultanément. Entrez les temps de résolution DNS hello URL toosee, heure de la connexion et la vitesse de plusieurs emplacements géographiques. Utilisez cette toosee test le service hébergé qui est retourné pour différents emplacements monde hello.

    ![pulse1](./media/traffic-manager-performance-considerations/traffic-manager-web-site-watchmouse.png)

* [Pingdom](http://tools.pingdom.com/)

    Cet outil fournit des statistiques de performances pour chaque élément d’une page web. Hello onglet analyse de la Page affiche le pourcentage hello temps consacré à la recherche DNS.

* [Qu’est-ce que Mon DNS ?](http://www.whatsmydns.net/)

    Ce site effectue une recherche DNS à partir de 20 différents emplacements et affiche les résultats hello sur une carte.

* [Dig Web Interface](http://www.digwebinterface.com)

    Ce site affiche plus d’informations DNS détaillées, notamment les enregistrements CNAME et A. Vérifiez que vous vérifiez hello 'Coloriser output' et 'Statistiques' sous options, sélectionnez « All » sous serveurs de noms.

## <a name="next-steps"></a>Étapes suivantes

[À propos des méthodes de routage du trafic de Traffic Manager](traffic-manager-routing-methods.md)

[Tester vos paramètres de Traffic Manager](traffic-manager-testing-settings.md)

[Opérations sur Traffic Manager (Référence sur l’API REST)](http://go.microsoft.com/fwlink/?LinkId=313584)

[Applets de commande Azure Traffic Manager](http://go.microsoft.com/fwlink/p/?LinkId=400769)

