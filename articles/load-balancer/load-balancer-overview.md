---
title: "vue d’ensemble du programme d’équilibrage de charge aaaAzure | Documents Microsoft"
description: "Présentation des fonctionnalités, de l'architecture et de l'implémentation de l'équilibrage de charge Azure. Découvrez le fonctionne de l’équilibrage de charge hello et l’exploiter dans le cloud de hello."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
ms.assetid: 0f313dc0-f007-4cee-b2b9-f542357925a3
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 2376a02f7cbbbed6a90f216419c0c3d30f594272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-load-balancer-overview"></a>Vue d’ensemble de l’équilibreur de charge Azure

Équilibrage de charge Azure offre une haute disponibilité et les performances réseau tooyour applications. Il s’agit d’un équilibreur de charge Layer-4 (TCP, UDP) qui distribue le trafic entrant parmi des instances saines de services définis dans un jeu à charge équilibrée.

Azure Load Balancer peut être configuré pour :

* La charge des machines de solde entrants Internet trafic toovirtual. Cette configuration est appelée [équilibrage de charge avec accès par Internet](load-balancer-internet-overview.md).
* équilibrer le trafic entre des machines virtuelles dans un réseau virtuel, entre des machines virtuelles dans les services cloud ou entre des ordinateurs locaux et des machines virtuelles dans un réseau virtuel entre différents locaux. Cette configuration est appelée [équilibrage de charge interne](load-balancer-internal-overview.md).
* Transférer le trafic externe tooa ordinateur virtuel spécifique.

Toutes les ressources de cloud de hello peut-être un toobe d’adresse IP publique accessible à partir de hello Internet. infrastructure en nuage Hello dans Azure utilise des adresses IP non routable pour ses ressources. Azure utilise la traduction d’adresses réseau (NAT) avec publique toohello de toocommunicate d’adresses IP Internet.

## <a name="azure-deployment-models"></a>Modèles de déploiement Azure

Il est important de toounderstand hello différences hello Azure classic et Gestionnaire de ressources [modèles de déploiement](../azure-resource-manager/resource-manager-deployment-model.md). Azure Load Balancer est configuré différemment selon les modèles.

### <a name="azure-classic-deployment-model"></a>Modèle de déploiement classique Azure

Ordinateurs virtuels déployés dans une limite de service cloud peuvent être groupée toouse un équilibreur de charge. Dans ce modèle à une adresse IP publique et un nom de domaine complet, le (FQDN) sont affectés tooa le service cloud. équilibrage de charge Hello le port traduction et équilibre la charge du trafic réseau hello à l’aide de l’adresse IP hello pour le service cloud hello.

Le trafic à charge équilibrée est défini par points de terminaison. Points de terminaison de port traduction ont une relation un à un entre hello attribué par le public ports de l’adresse IP publique de hello et hello local affecté service toohello sur un ordinateur virtuel spécifique. Les points de terminaison de l’équilibrage de charge ont une relation un-à-plusieurs entre les adresse IP publique hello et hello local ports attribués toohello services sur des ordinateurs virtuels de hello dans le service cloud hello.

![Équilibrage de charge Azure dans le modèle de déploiement classique de hello](./media/load-balancer-overview/asm-lb.png)

Figure 1 : équilibrage de charge Azure dans le modèle de déploiement classique de hello

nom de domaine Hello pour hello adresse IP publique qui utilise d’équilibrage de charge pour ce modèle de déploiement de hello est \<nom du service cloud\>. cloudapp.net. Hello graphique suivant illustre hello équilibrage de charge Azure dans ce modèle.

### <a name="azure-resource-manager-deployment-model"></a>Modèle de déploiement Azure Resource Manager

Dans le modèle de déploiement du Gestionnaire de ressources hello n’existe aucun besoin toocreate un service Cloud. équilibrage de charge Hello est créé tooexplicitly acheminer le trafic entre plusieurs machines virtuelles.

Une adresse IP publique est une ressource individuelle qui a une étiquette de domaine (nom DNS). adresse IP publique de Hello est associé à des ressources d’équilibrage de charge hello. Règles d’équilibrage de charge et les règles NAT entrantes utilisent une adresse IP publique de hello comme point de terminaison Internet pour les ressources hello qui reçoivent le trafic réseau à charge équilibrée de hello.

Une adresse IP privée ou publique est affectée toohello network interface ressource attachée tooa virtuels. Une fois qu’une interface réseau est ajoutée à un pool d’adresses IP l’équilibreur de charge tooa terminale, équilibrage de charge hello est en mesure de toosend équilibrage de la charge de trafic réseau en fonction des règles d’équilibrage de la charge hello qui sont créés.

Hello graphique suivant illustre hello équilibrage de charge Azure dans ce modèle :

![L’équilibrage de charge Azure dans Resource Manager](./media/load-balancer-overview/arm-lb.png)

Illustration 2 - L’équilibrage de charge Azure dans Resource Manager

équilibrage de charge Hello peut être géré par le biais de modèles basés sur le Gestionnaire de ressources, les API et les outils. toolearn plus sur la gestion de ressources, consultez hello [vue d’ensemble du Gestionnaire de ressources](../azure-resource-manager/resource-group-overview.md).

## <a name="load-balancer-features"></a>Fonctionnalités d’équilibrage de charge

* Distribution basée sur le hachage

    L'Équilibrage de charge Azure utilise un algorithme de distribution basé sur le hachage. Par défaut, il utilise un hachage de 5-tuple composé de l’adresse IP source, port source, adresse IP de destination, le port de destination et serveurs de protocole type toomap trafic tooavailable. Il fournit l’adhérence uniquement *dans* une session de transport. Les paquets hello même session TCP ou UDP sera dirigé toohello même instance derrière le point de terminaison avec équilibrage de charge hello. Lorsque le client de hello se ferme et rouvre la connexion de hello ou démarre une nouvelle session de hello la même adresse IP source, modifications de port source hello. Cela peut entraîner hello trafic toogo tooa autre point de terminaison dans un autre centre de données.

    Pour en savoir plus, consultez [Mode de distribution de l’équilibrage de charge](load-balancer-distribution-mode.md). Hello graphique suivant illustre distribution basée sur le hachage de hello :

    ![Distribution basée sur le hachage](./media/load-balancer-overview/load-balancer-distribution.png)

    Figure 3 : distribution basée sur le hachage

* Réacheminement de port

    L'équilibrage de charge Azure vous permet de contrôler la gestion des communications entrantes. Ces communications comprennent le trafic initié par des hôtes Internet, des machines virtuelles dans d'autres services cloud ou des réseaux virtuels. Ce contrôle est représenté par un point de terminaison (également appelé point de terminaison d'entrée).

    Un point de terminaison écoute sur un port public et transfère le trafic de port interne de tooan. Vous pouvez mapper hello même ports pour un point de terminaison interne ou externe ou utiliser un port différent pour eux. Par exemple, vous pouvez avoir un tooport toolisten du serveur configuré web 81 alors que le mappage de point de terminaison public hello est le port 80. la création d’un point de terminaison public Hello déclenche la création d’une instance d’équilibrage de charge hello.

    Lorsque créé à l’aide de hello le portail Azure, portal de hello crée automatiquement une machine virtuelle points de terminaison toohello hello protocole RDP (Remote Desktop) et le trafic de session Windows PowerShell à distance. Vous pouvez utiliser ces points de terminaison tooremotely administrer hello virtual machine via hello Internet.

* Reconfiguration automatique

    L'équilibrage de charge Azure se reconfigure instantanément lors de la mise à l'échelle d'instances vers le haut ou vers le bas. Par exemple, cette reconfiguration se produit lorsque vous augmentez hello du nombre d’instances pour les rôles web/de travail dans un service cloud ou lorsque vous ajoutez des ordinateurs virtuels supplémentaires en hello même équilibrée définie.

* Surveillance des services

    Équilibrage de charge Azure peut détecter intégrité hello hello différentes instances de serveur. Lorsqu’une sonde échoue toorespond, équilibrage de charge hello cesse d’envoyer des toohello des instances non intègre de nouvelles connexions. Les connexions existantes ne sont pas concernées.

    Trois types de sondes sont pris en charge :

    + **Sonde de l’agent invité (sur la plateforme en tant qu’un Service les ordinateurs virtuels uniquement) :** équilibrage de charge hello utilise l’agent invité de hello à l’intérieur de machine virtuelle de hello. Hello agent invité d’écoute et répond avec une réponse HTTP 200 OK uniquement lorsque hello instance est prête hello (c'est-à-dire hello instance n’est pas dans un état comme occupé, le recyclage ou l’arrêt). Si l’agent de hello échoue toorespond avec un OK de 200 HTTP, les marques de programme d’équilibrage de charge hello hello instance ne répond pas et cesse d’envoyer l’instance toothat de trafic. équilibrage de charge Hello continue d’instance de hello tooping. Si l’agent invité de hello répond avec un HTTP 200, équilibrage de charge hello envoie à nouveau instance toothat de trafic. Lorsque vous utilisez un rôle web, votre code de site Web s’exécute généralement dans w3wp.exe, ce qui n’est pas analysé par hello tissu Azure ou l’agent invité. Cela signifie que les échecs dans w3wp.exe (par exemple, les réponses HTTP 500) ne sera pas l’agent invité de toohello signalé et équilibrage de charge hello ne saura pas tootake cette instance hors rotation.
    + **Sonde personnalisée HTTP :** sonde de hello par défaut (l’agent invité) substitue à cette sonde. Vous pouvez l’utiliser toocreate votre propre logique personnalisée toodetermine hello la santé de l’instance de rôle hello. équilibrage de charge Hello chercheront régulièrement votre point de terminaison (toutes les 15 secondes, par défaut). instance de Hello est considéré comme toobe en rotation s’il répond avec HTTP 200 de TCP ACK au sein de la période de délai d’attente hello (31 secondes par défaut). Cela est utile pour implémenter vos propres instances de tooremove logique de la rotation de l’équilibreur de charge hello. Par exemple, vous pouvez configurer hello instance tooreturn un état autre que 200 si l’instance de hello est supérieure à 90 % de l’UC. Pour les rôles web qui utilisent w3wp.exe, vous obtenez également automatique d’analyse de votre site Web, puisque les défaillances dans votre code de site Web retournent une sonde toohello d’état de non-200.
    + **Sonde personnalisée TCP :** cette sonde s’appuie sur la réussite session établissement tooa défini sonde le port TCP.

    Pour plus d’informations, consultez hello [schéma LoadBalancerProbe](https://msdn.microsoft.com/library/azure/jj151530.aspx).

* Source NAT

    Tout le trafic sortant toohello Internet qui proviennent de votre service subit source NAT (SNAT) à l’aide de hello la même adresse IP virtuelle comme hello le trafic entrant. SNAT offre des avantages importants :

    + Il permet une simple mise à niveau et récupération d’urgence de services, puisque hello qu'adresse IP virtuelle peut être dynamiquement mappée instance tooanother du service de hello.
    + Il facilite la gestion des listes de contrôle d’accès (ACL). Les ACL exprimées sous forme d’adresses IP virtuelles ne changent pas lorsque les services montent en puissance, descendent en puissance ou sont redéployés.

    configuration d’équilibrage de charge de Hello prend en charge complète cône NAT pour le protocole UDP. Cône plein NAT est un type de NAT où port de hello autorise les connexions entrantes à partir de n’importe quel hôte externe (dans la demande sortante tooan de réponse).

    Pour chaque nouvelle connexion sortante qui lance d’un ordinateur virtuel, un port de sortie est également alloué par l’équilibrage de charge hello. l’hôte externe Hello voit le trafic avec un port virtuel alloué par l’adresse IP virtuelle de l’IP. Pour les scénarios qui requièrent un grand nombre de connexions sortantes, il est recommandé de toouse [adresse IP publique au niveau de l’instance](../virtual-network/virtual-networks-instance-level-public-ip.md) adresses afin que les ordinateurs virtuels de hello disposent d’une adresse IP sortante dédiée pour SNAT. Cela réduit le risque de hello d’épuisement du port.

    Consultez l’article [connexions sortantes](load-balancer-outbound-connections.md) pour plus d’informations sur ce sujet.

### <a name="support-for-multiple-load-balanced-ip-addresses-for-virtual-machines"></a>Prise en charge de plusieurs adresses IP à équilibrage de charge pour les machines virtuelles
Vous pouvez affecter plusieurs équilibrée publics tooa ensemble d’adresses IP des ordinateurs virtuels. Avec cette possibilité, vous pouvez héberger plusieurs sites Web SSL et/ou plusieurs écouteurs de groupe de disponibilité AlwaysOn de SQL Server sur le même ensemble d’ordinateurs virtuels de hello. Pour en savoir plus, consultez [Plusieurs adresses IP virtuelles par service cloud](load-balancer-multivip.md).

[!INCLUDE [load-balancer-compare-tm-ag-lb-include.md](../../includes/load-balancer-compare-tm-ag-lb-include.md)]

## <a name="limitations"></a>Limites

Les pools back-end d’équilibreur de charge peuvent héberger toutes les références SKU de machines virtuelles, sauf le niveau De base.

## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur l’[équilibrage de charge accessible sur Internet](load-balancer-internet-overview.md)

- En savoir plus sur l’[équilibrage de charge interne](load-balancer-internal-overview.md)

- Créer un [équilibrage de charge accessible sur Internet](load-balancer-get-started-internet-portal.md)

- En savoir plus sur certaines des hello autre clé [fonctionnalités de réseau](../networking/networking-overview.md) de Azure

