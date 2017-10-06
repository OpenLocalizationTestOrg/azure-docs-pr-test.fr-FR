---
title: "aaaIntroduction tooAzure passerelle d’Application | Documents Microsoft"
description: "Cette page fournit une vue d’ensemble du service de passerelle d’Application hello couche 7 l’équilibrage de charge, y compris les tailles de passerelle, l’affinité de session basé sur cookie, l’équilibrage de charge HTTP et le déchargement SSL."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: b37a2473-4f0e-496b-95e7-c0594e96f83e
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: c40c9dba64ab03d9f6f81b3cb8f26c6562ac26c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-application-gateway"></a>Vue d’ensemble de la passerelle Application Gateway

Microsoft Azure Application Gateway est une appliance virtuelle dédiée qui propose un contrôleur de livraison d’applications (ADC) en tant que service. Elle offre diverses fonctionnalités d’équilibrage de charge de couche 7 pour votre application. Il permet de productivité de batterie de serveurs web toooptimize clients en déchargeant la passerelle d’application UC intensif SSL arrêt toohello. Il fournit également des autres fonctionnalités de routage de couche 7, y compris la distribution Round robin de trafic entrant d’affinité de session basée sur un cookie, le routage basé sur le chemin d’accès URL et hello capacité toohost plusieurs sites Web derrière une passerelle d’Application unique. Un pare-feu d’applications web (WAF) est également fourni dans le cadre de la passerelle d’application hello WAF référence (SKU). Il offre une protection tooweb les applications courantes des vulnérabilités de web et des exploits. La passerelle Application Gateway peut être configurée en tant que passerelle internet, passerelle interne uniquement ou une combinaison des deux. 

![scénario](./media/application-gateway-introduction/scenario.png)

## <a name="features"></a>Caractéristiques

Passerelle d’application fournit actuellement hello suivant de fonctionnalités :


* **[Pare-feu d’applications Web](application-gateway-webapplicationfirewall-overview.md)**  -hello web application (WAF) dans la passerelle d’Application Azure protège les applications web à partir des attaques courantes basée sur le web telles que l’injection SQL, les attaques de script entre sites et des détournements de session.
* **Équilibrage de charge HTTP** - La passerelle Application Gateway fournit un équilibrage de charge de type tourniquet (round robin). L’équilibrage de charge s’effectue à la couche 7 et est utilisé pour le trafic HTTP(S) uniquement.
* **Affinité de session basée sur le cookie** -fonctionnalité d’affinité de session basée sur le cookie hello est utile lorsque vous souhaitez tookeep une session utilisateur sur hello même principal. À l’aide de cookies de géré par passerelle hello passerelle d’Application est toodirect en mesure de trafic suivants à partir d’un toohello de session utilisateur même principal pour traitement. Cette fonctionnalité est importante dans les cas où l’état de session est enregistré localement sur le serveur principal de hello pour une session utilisateur.
* **[Déchargement de Secure Sockets Layer (SSL) sécurisé](application-gateway-ssl-arm.md)**  -cette fonctionnalité prend la tâche coûteux hello de décrypter le trafic HTTPS vos serveurs web. En fin hello connexion SSL sur hello passerelle d’Application et hello demande toohello serveur non chiffré de transfert, le serveur web de hello est unburdened par le déchiffrement.  Passerelle d’application rechiffre les réponse hello avant de l’envoyer toohello précédent client. Cette fonctionnalité est utile dans les scénarios où se trouve le principal hello hello même sécurisée réseau virtuel comme hello passerelle d’Application dans Azure.
* **[Fin tooEnd SSL](application-gateway-backend-ssl.md)**  -tooend le chiffrement du trafic de fin de prise en charge de la passerelle d’Application. Pour cela, passerelle d’application termine la connexion SSL de hello au niveau de la passerelle d’application hello. passerelle de Hello applique ensuite des règles de routage hello toohello trafic, rechiffre les paquets hello et transfère hello principal paquet toohello approprié en fonction des règles de routage hello définis. Une réponse de serveur web de hello traverse hello même processus utilisateur toohello précédent.
* **[Basée sur l’URL de routage contenu](application-gateway-url-route-overview.md)**  -cette fonctionnalité offre une capacité de hello toouse des serveurs principaux différents de trafic différents. Le trafic d’un dossier sur le serveur web de hello ou pour un CDN peut être routé tooa autre principal. Cette fonctionnalité réduit la charge inutile sur les serveurs principaux qui ne traitent pas de contenu spécifique.
* **[Routage de plusieurs sites](application-gateway-multi-site-overview.md)**  -passerelle d’Application permet de vous tooconsolidate des sites Web de too20 sur une passerelle d’application unique.
* **[Prise en charge de WebSocket](application-gateway-websocket.md)**  -une autre fonctionnalité intéressante de passerelle d’Application est prise en charge native de hello pour Websocket.
* **[Contrôle d’intégrité](application-gateway-probe-overview.md)**  -passerelle d’Application fournit le contrôle d’intégrité par défaut analyse des ressources de serveur principal et personnalisée sondes toomonitor pour des scénarios plus spécifiques.
* **[Stratégie SSL et les chiffrements](application-gateway-ssl-policy-overview.md)**  : cette fonctionnalité permet hello versions du protocole SSL toolimit hello et hello chiffrements de suites de tests qui sont prises en charge et hello l’ordre dans lequel ils sont traités.
* **[Demande de redirection](application-gateway-redirect-overview.md)**  -cette fonctionnalité fournit hello capacité tooredirect HTTP demandes tooan port d’écoute HTTPS.
* **[Prise en charge de serveurs principaux multilocataires](application-gateway-web-app-overview.md)** : Application Gateway prend en charge la configuration de services de serveurs principaux multilocataires comme Azure Web Apps et la passerelle d’API en tant que membres de pool principal. 
* **[Diagnostics avancés](application-gateway-diagnostics.md)** - Application Gateway fournit des journaux de diagnostic et d’accès complets. Les journaux de pare-feu sont disponibles pour les ressources de passerelle d’application avec WAF activé.

## <a name="benefits"></a>Avantages

Application Gateway est utile pour :

* Les applications qui nécessitent des demandes à partir de hello même tooreach de session client/utilisateur hello même d’ordinateur virtuel principal. Exemples d’applications : panier d’achat et serveurs de messagerie.
* Suppression de surcharge de terminaison SSL pour les batteries de serveurs web.
* Les applications, tel qu’un réseau de diffusion de contenu, qui requiert plusieurs demandes HTTP sur hello même toobe de connexion TCP longue routés ou charger toodifferent à charge équilibrée sur les serveurs principaux.
* Applications prenant en charge le trafic websocket
* Protection des applications web des attaques basées sur le web courantes comme l’injection de code SQL, les attaques de script de site à site et les piratages de session.
* Distribution logique du trafic selon différents critères de routage, comme le chemin d’accès de l’URL ou les en-têtes de domaine.

La passerelle Application Gateway est une solution Azure entièrement gérée, hautement évolutive et hautement disponible. Elle fournit un ensemble complet de fonctionnalités de diagnostics et de journalisation, pour une meilleure gérabilité. Quand vous créez une passerelle Application Gateway, un point de terminaison (VIP public ou IP ILB interne) est associé et utilisé pour le trafic réseau en entrée. Cette adresse IP virtuelle ou le ILB IP est fournie par l’équilibrage de charge Azure fonctionne au niveau du transport hello (TCP/UDP) et avoir du trafic réseau entrant tout en cours de passerelle d’application à charge équilibrée toohello charge les instances de processus de travail. Hello passerelle d’application, puis les itinéraires hello trafic HTTP/HTTPS en fonction de sa configuration, qu’il s’agisse d’un ordinateur virtuel, service cloud, interne ou une adresse IP externe.

Passerelle d’application l’équilibrage de charge comme un service géré de Azure permet l’approvisionnement d’un équilibrage de charge de couche 7 derrière l’équilibrage de charge logicielle Azure hello hello. Gestionnaire de trafic peut être scénario de hello toocomplete utilisés comme Bonjour suivant image, où Traffic Manager fournit la redirection et disponibilité du trafic toomultiple des ressources de passerelle d’application dans différentes régions, tandis que la passerelle d’application fournit entre l’équilibrage de charge couche 7 région. Vous trouverez un exemple de ce scénario à : [Using équilibrage des services Bonjour Azure cloud](../traffic-manager/traffic-manager-load-balancing-azure.md)

![scénario avec traffic manager et application gateway](./media/application-gateway-introduction/tm-lb-ag-scenario.png)

[!INCLUDE [load-balancer-compare-tm-ag-lb-include.md](../../includes/load-balancer-compare-tm-ag-lb-include.md)]

## <a name="gateway-sizes-and-instances"></a>Instances et tailles de passerelle

Application Gateway est actuellement disponible en 3 tailles : **Petit**, **Moyen** et **Grand**. Les instances de petite taille sont conçues pour les scénarios de développement et de test.

Vous pouvez créer des passerelles d’application too50 par abonnement, et chaque passerelle d’application peut avoir des instances too10 chaque. Chaque passerelle Application Gateway peut contenir 20 écouteurs HTTP. Pour obtenir la liste complète des limites de la passerelle Application Gateway, consultez la page [Application Gateway limits](../azure-subscription-service-limits.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#application-gateway-limits) (Limites de la passerelle Application Gateway).

Hello tableau suivant montre un débit moyen de performances pour chaque instance de passerelle d’application avec déchargement SSL activé :

| Réponse de la page principale | Petite | Moyenne | Grande |
| --- | --- | --- | --- |
| 6K |7,5 Mbits/s |13 Mbits/s |50 Mbits/s |
| 100K |35 Mbits/s |100 Mbits/s |200 Mbits/s |

> [!NOTE]
> Ces valeurs sont des valeurs approximatives pour un débit de passerelle d’application. le débit réel Hello dépend de divers détails de l’environnement, telles que la taille moyenne de pages, emplacement des instances de serveur principal et le traitement des temps tooserve une page. Pour des calculs de performance exacts, vous devez exécuter vos propres tests. Ces valeurs sont fournies uniquement pour vous donner des conseils de planification de la capacité.

## <a name="health-monitoring"></a>Surveillance de l’intégrité

Passerelle d’Application Azure analyse automatiquement hello l’intégrité des instances de serveur principal hello via les sondes d’intégrité de base ou personnalisée. À l’aide de sondes d’intégrité, elle garantit que les hôtes uniquement intègres répondent tootraffic. Pour plus d’informations, consultez [Vue d’ensemble de l’analyse d’intégrité Application Gateway](application-gateway-probe-overview.md).

## <a name="configuring-and-managing"></a>Configuration et gestion

Le point de terminaison de la passerelle Application Gateway peut être une adresse IP publique, une adresse IP privée ou les deux. La passerelle Application Gateway est configurée à l’intérieur d’un réseau virtuel dans son propre sous-réseau. sous-réseau Hello créés ou utilisés pour la passerelle d’application ne peut pas contenir d’autres types de ressources, hello seules les ressources qui sont autorisés dans un sous-réseau de hello sont d’autres passerelles d’application. toosecure vos ressources de serveur principal, serveurs principaux de hello peuvent être contenus dans un autre sous-réseau Bonjour même réseau virtuel en tant que passerelle d’application hello. Ce sous-réseau que pas requise pour les applications principales de hello. Tant que passerelle d’application hello peut atteindre l’adresse ip de hello, la passerelle d’application est tooprovide en mesure des capacités de connecteur Active Directory pour les serveurs principaux de hello. 

Vous pouvez créer et gérer une passerelle Application Gateway à l’aide des API REST, des applets de commande PowerShell, de la ligne de commande Azure ou du [portail Azure](https://portal.azure.com/). Pour d’autres questions sur la passerelle d’Application visitez [FAQ de passerelle d’Application](application-gateway-faq.md) tooview une liste de commun des questions fréquemment posées.

## <a name="pricing"></a>Tarification

La tarification est basée sur les frais d’instance de passerelle par heure et les frais de traitement des données. Par heure passerelle tarification pour hello WAF référence (SKU) est différente de frais de référence (SKU) Standard. Vous trouverez ces informations de tarification dans [Tarification de Application Gateway](https://azure.microsoft.com/pricing/details/application-gateway/). Le traitement des données des frais restent hello identiques.

## <a name="faq"></a>Forum Aux Questions

Pour les questions fréquemment posées sur Application Gateway, consultez [Forum aux questions pour Azure Application Gateway](application-gateway-faq.md).

## <a name="next-steps"></a>Étapes suivantes

Après l’apprentissage sur la passerelle d’Application, vous pouvez [créer une passerelle d’application](application-gateway-create-gateway-portal.md) ou vous pouvez [créer une passerelle d’application de déchargement SSL](application-gateway-ssl-arm.md) tooload-équilibrer les connexions HTTPS.

toolearn comment toocreate une passerelle d’application à l’aide d’URL de routage en fonction du contenu, consultez trop[créer une passerelle d’application à l’aide de routage basé sur l’URL](application-gateway-create-url-route-arm-ps.md) pour plus d’informations.

toolearn sur certaines des hello autre clé mise en réseau des capacités de Azure, consultez [réseau Azure](../networking/networking-overview.md).
