---
title: tooResource de passerelle classique aaaVPN Gestionnaire de Migration | Documents Microsoft
description: "Cette page fournit une vue d’ensemble de tooResource classique de passerelle VPN de hello migration du gestionnaire."
documentationcenter: na
services: vpn-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: caa8eb19-825a-4031-8b49-18fbf3ebc04e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: amsriva
ms.openlocfilehash: c1d84bf5315224c5c8faac53d7957b496ed205ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="vpn-gateway-classic-tooresource-manager-migration"></a>TooResource classique de passerelle VPN Manager migration
Passerelles VPN peuvent désormais être migrés à partir du modèle de déploiement du gestionnaire tooResource classique. Vous pouvez découvrir plus en détail les [fonctionnalités et les avantages](../azure-resource-manager/resource-group-overview.md) d’Azure Resource Manager. Dans cet article, nous avons décrit en détail comment le modèle basé sur toomigrate à partir des déploiements classique toonewer Gestionnaire de ressources. 

Passerelles VPN sont migrés en tant que partie de la migration de réseau virtuel à partir de tooResource classique Manager. Cette migration porte sur un réseau virtuel à la fois. Il n’existe aucune exigence supplémentaire en termes d’outils ou des conditions préalables toomigration. Étapes de migration sont la migration du réseau virtuel tooexisting identiques et sont documentés dans [page de migration de ressources IaaS](../virtual-machines/windows/migration-classic-resource-manager-ps.md). Il n’existe aucun temps d’arrêt du chemin d’accès de données pendant la migration, et par conséquent, les charges de travail existants continue toofunction sans perte de connectivité locale pendant la migration. adresse IP publique Hello associé hello VPN passerelle ne change pas pendant le processus de migration hello. Cela implique que pas lorsque vous devez tooreconfigure votre routeur local hello migration est terminée.  

modèle de Hello dans le Gestionnaire de ressources est différent du modèle classique et est composé de passerelles de réseau virtuel, les passerelles de réseau local et les ressources de connexion. Ceux-ci représentent la passerelle VPN de hello lui-même, hello représentant respectivement sur l’espace d’adressage local et la connectivité entre hello deux-site local. À l’issue de la migration, les passerelles ne sont pas disponibles dans le modèle Classic et toutes les opérations de gestion au niveau des passerelles de réseau virtuel, des passerelles de réseau local et des objets de connexion doivent être effectuées selon le modèle Resource Manager.

## <a name="supported-scenarios"></a>Scénarios pris en charge
Scénarios de connectivité VPN les plus courants sont couverts par classique tooResource migration du gestionnaire. scénarios de Hello pris en charge sont les suivants :

* Connectivité de point toosite
* Site toosite dotée de la passerelle VPN connecté emplacement local de tooon
* Connectivité de tooVNet de réseau virtuel entre deux réseaux virtuels à l’aide de passerelles VPN
* Plusieurs réseaux virtuels connectés toosame sur un emplacement local
* Connectivité multisite
* Réseaux virtuels compatibles avec le tunneling forcé

Les scénarios non pris en charge sont les suivants :  

* Réseau virtuel doté d’une passerelle ExpressRoute et d’une passerelle VPN.
* Scénarios de transit où les extensions de machine virtuelle sont connectés tooon des serveurs locaux. Les limitations de connectivité VPN de transit sont détaillées ci-après.

> [!NOTE]
> Validation du CIDR dans le modèle de gestionnaire de ressources est plus stricte que hello un dans le modèle classique. Avant de migrer, vérifiez que les plages d’adresses classique donnés sont conformes toovalid le format CIDR avant de commencer la migration de hello. Le routage CIDR peut être validé à l’aide de l’un des validateurs CIDR courants. La migration de réseaux virtuels ou de sites locaux avec des plages CIDR non valides se traduirait par un état d’échec.
> 
> 

## <a name="vnet-toovnet-connectivity-migration"></a>Migration de connectivité de réseau virtuel tooVNet
Connectivité de tooVNet de réseau virtuel dans classic a été obtenue en créant un site local, la représentation sous forme de hello connecté réseau virtuel. Les clients ont été toocreate requis deux sites locaux représentés hello deux réseaux virtuels requis toobe connectés entre eux. Il s’agit alors connecté toohello correspondant à l’aide de la connectivité de tooestablish de tunnel IPsec entre des réseaux virtuels hello deux réseaux virtuels. Ce modèle présente des inconvénients de la facilité de gestion dans la mesure où toutes les modifications de plage d’adresse dans un réseau virtuel doivent également être maintenues en représentation sous forme de site local correspondant hello. Dans le modèle Resource Manager, cette solution de contournement n’est plus nécessaire. Bonjour connexion entre deux réseaux virtuels peuvent être obtenus directement à l’aide du type de connexion 'Vnet2Vnet' dans la ressource de connexion de hello. 

![Capture d’écran de réseau virtuel tooVNet migration.](./media/vpn-gateway-migration/migration1.png)

Lors de la migration de réseau virtuel, nous détectons qui hello entité connectée passerelle VPN de réseau virtuel toocurrent est un autre réseau virtuel et vérifiez si une fois la migration de ces deux réseaux virtuels est terminée, vous serez n’est plus voyez deux sites locaux représentant hello autre réseau virtuel. modèle classique Hello deux passerelles VPN, les deux sites locaux et les deux connexions entre eux est transformé tooResource modèle du gestionnaire avec deux passerelles VPN et deux connexions de type Vnet2Vnet.

## <a name="transit-vpn-connectivity"></a>Connectivité VPN de transit
Vous pouvez configurer des passerelles VPN dans une topologie de telles que la connectivité locale pour un réseau virtuel est obtenue en vous connectant tooanother réseau virtuel qui est directement connecté tooon local. Il s’agit transit connectivité VPN où les instances dans le premier réseau virtuel sont les ressources tooon locaux connectés via une passerelle VPN toohello de transit dans le réseau virtuel connecté qui est directement connecté tooon local. tooachieve cette configuration dans le modèle de déploiement classique, vous devez toocreate un site local a ensuite regroupées préfixes représentant les deux espace d’adressage de réseau virtuel et sur site hello connecté. Cet représentation site local est connecté toohello tooachieve de réseau virtuel de transit connectivité. Ce modèle classique a également les défis de gestion similaires, car toute modification dans la plage d’adresses locales doit également être maintenue sur site local de hello représentant agrégat hello de réseau virtuel et sur site. Présentation de prise en charge BGP dans le Gestionnaire de ressources pris en charge les passerelles simplifie la facilité de gestion depuis hello passerelles connectés peuvent apprennent les itinéraires de localement sans modification manuelle tooprefixes.

![Capture d’écran du scénario de routage de transit.](./media/vpn-gateway-migration/migration2.png)

Étant donné que nous devons transformer connectivité tooVNet de réseau virtuel sans nécessiter de sites locaux, scénario de transit hello perd connectivité locale pour le réseau virtuel qui est connecté indirectement tooon local. Hello perte de connectivité peut être atténuée Bonjour suivant deux méthodes, une fois la migration est terminée. 

* Activer le protocole BGP sur tooon locaux et de passerelles VPN sont connectés entre eux. L’activation du protocole BGP a pour effet de restaurer la connectivité sans aucune autre modification de la configuration, car les itinéraires sont déterminés et annoncés entre les passerelles de réseau virtuel. Notez que l’option BGP est uniquement disponible sur les références (SKU) Standard et supérieures.
* Établir une connexion explicite de la passerelle réseau local toohello affecté réseau virtuel représentant l’emplacement local. Cela serait exigent le changement de configuration sur toocreate de routeur local hello et de configurer également tunnel d’IPsec hello.

## <a name="next-steps"></a>Étapes suivantes
Après avoir de formation sur la prise en charge de la migration de passerelle VPN, passez trop[plateforme prise en charge la migration des ressources IaaS de classique tooResource Manager](../virtual-machines/windows/migration-classic-resource-manager-ps.md) tooget a démarré.

