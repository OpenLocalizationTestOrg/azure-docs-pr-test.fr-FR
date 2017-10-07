---
title: "aaaAzure mise en réseau des instructions de l’infrastructure - Windows | Documents Microsoft"
description: "Découvrez hello clé conception et implémentation des recommandations pour le déploiement d’un réseau virtuel dans les services d’infrastructure Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e2d45973-5eba-4904-8ba0-1821f64feed7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 64c288957e7c7b89578d871a74ff45ce470ed922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-infrastructure-guidelines-for-windows-vms"></a>Instructions pour les infrastructures réseau Azure pour machines virtuelles Windows 

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Cet article se concentre sur hello compréhension requises de planification pour un réseau virtuel dans Azure et la connectivité entre les environnements local existant.

## <a name="implementation-guidelines-for-virtual-networks"></a>Instructions d’implémentation pour les réseaux virtuels
Décisions :

* Le type de réseau virtuel devez-vous toohost votre charge de travail informatique ou d’infrastructure (cloud uniquement ou intersite) ?
* Pour les réseaux virtuels intersite, quel espace d’adressage devez-vous sous-réseaux de hello toohost et les machines virtuelles maintenant et pour l’expansion raisonnable Bonjour futures ?
* Sont allez-vous toocreate centralisée des réseaux virtuels ou créer des réseaux virtuels individuels pour chaque groupe de ressources ?

Tâches :

* Définir un espace d’adressage hello hello toobe de réseaux virtuels créé.
* Définir l’hello des sous-réseaux et de l’espace d’adressage hello pour chacun.
* Pour les réseaux virtuels intersite, définir hello des espaces d’adressage de réseau local pour les sites locaux hello hello des machines virtuelles dans hello réseau virtuel nécessaire tooreach.
* Travail avec mise en réseau équipe tooensure hello appropriée le routage est configuré lors de la création en local entre sites réseaux virtuels.
* Créez hello de réseau virtuel à l’aide de votre convention d’affectation de noms.

## <a name="virtual-networks"></a>Réseaux virtuels
Les réseaux virtuels sont nécessaires toosupport les communications entre les machines virtuelles (VM). Vous pouvez définir des sous-réseaux, des adresses IP personnalisées, des paramètres DNS, des filtrages de sécurité et l’équilibrage de charge, tout comme avec les réseaux physiques. En utilisant un [passerelle VPN](../../vpn-gateway/vpn-gateway-about-vpngateways.md) ou [circuit Express Route](../../expressroute/expressroute-introduction.md), vous pouvez vous connecter à des réseaux virtuels Azure tooyour sur des réseaux locaux. Vous pouvez en savoir plus sur [les réseaux virtuels et leurs composants](../../virtual-network/virtual-networks-overview.md).

Avec les groupes de ressources, vous disposez de plus de flexibilité dans la façon dont vous concevez vos composants de réseau virtuel. Machines virtuelles peuvent se connecter à des réseaux de toovirtual en dehors de leur propre groupe de ressources. Une approche de conception courante serait de groupes de ressources toocreate centralisée qui contiennent votre infrastructure réseau de base qui peut être géré par une équipe commune, et ensuite les ordinateurs virtuels et leurs applications déploiement tooseparate les groupes de ressources. Cette approche permet aux propriétaires d’applications accès groupe de ressources toohello qui contient leurs ordinateurs virtuels sans ouverture de la configuration de l’accès toohello de hello plus large réseau ressources virtuelles.

## <a name="site-connectivity"></a>Connectivité de site
### <a name="cloud-only-virtual-networks"></a>Réseaux virtuels cloud uniquement
Si les ordinateurs et les utilisateurs locaux ne requièrent pas tooVMs de connectivité en cours dans un réseau virtuel Azure, votre conception de réseau virtuel n’est simple :

![Diagramme d’un réseau virtuel de base uniquement dans le cloud](./media/infrastructure-networking-guidelines/vnet01.png)

Cette approche s’applique généralement à des charges de travail Internet, telles qu’un serveur web Internet. Vous pouvez gérer ces machines virtuelles par RDP ou connexion VPN point à site.

Car ils ne connectent pas de réseau local de tooyour, les Azure uniquement des réseaux virtuels peuvent Utilisez toute partie d’un espace d’adressage IP privé hello, même si hello même espace privé utilise local.

### <a name="cross-premises-virtual-networks"></a>Réseaux virtuels intersite
Si les ordinateurs et les utilisateurs locaux requièrent tooVMs de connectivité en cours dans un réseau virtuel Azure, créez un réseau virtuel intersite.  Connexion de réseau local de tooyour avec un ExpressRoute ou d’une connexion VPN de site à site.

![Diagramme de réseau virtuel entre sites locaux](./media/infrastructure-networking-guidelines/vnet02.png)

Dans cette configuration, hello réseau virtuel Azure est essentiellement une extension en cloud de votre réseau local.

Puisqu’ils se connectent tooyour réseau local, des réseaux virtuels doivent utiliser une partie de l’espace d’adressage hello utilisé par votre organisation qui est unique entre différents locaux. Hello même façon que différents endroits de l’entreprise assignés un sous-réseau IP spécifique, Azure devient un autre emplacement que vous étendez votre réseau.

tooallow tootravel de paquets de votre réseau de local de tooyour de réseau virtuel intersite, vous devez configurer ensemble hello de préfixes d’adresse pertinentes sur site dans le cadre de la définition de réseau local hello pour le réseau virtuel de hello. En fonction de l’adresse de hello espace hello virtuel réseau et hello ensemble de pertinentes local emplacements, il peut y avoir plusieurs préfixes d’adresse de réseau local de hello.

Vous pouvez convertir un réseau virtuel de réseau virtuel cloud uniquement tooa entre différents locaux, mais il s’agit probablement nécessite toore IP votre espace d’adressage de réseau virtuel et les ressources Azure. Par conséquent, étudiez attentivement si un réseau virtuel doit toobe tooyour connectés sur réseau local lorsque vous affectez un sous-réseau IP.

## <a name="subnets"></a>Sous-réseaux
Autoriser les sous-réseaux vous tooorganize les ressources qui sont liées, soit logiquement (par exemple, un sous-réseau pour les machines virtuelles associées toohello même application), ou physiquement (par exemple, il s’agit d’un sous-réseau par groupe de ressources). Vous pouvez également employer des techniques d’isolation de sous-réseaux pour renforcer la sécurité.

Pour les réseaux virtuels intersite, vous devez concevoir des sous-réseaux avec hello mêmes conventions que vous utilisez pour les ressources locales. **Azure toujours utilise hello trois premières adresses IP de l’espace d’adressage hello pour chaque sous-réseau**. nombre de hello toodetermine d’adresses requises pour le sous-réseau de hello, démarrez en comptant le nombre de hello d’ordinateurs virtuels dont vous avez besoin maintenant. Estimation de la croissance future et utilisez hello suivant la taille du sous-réseau de hello hello de toodetermine la table.

| Nombre de machines virtuelles nécessaires | Nombre de bits hôte nécessaires | Taille du sous-réseau de hello |
| --- | --- | --- |
| 1 à 3 |3 |/29 |
| 4 à 11 |4 |/28 |
| 12 à 27 |5 |/27 |
| 28 à 59 |6 |/26 |
| 60 à 123 |7 |/25 |

> [!NOTE]
> Pour les sous-réseaux locaux normal, nombre maximal de hello d’adresses d’hôte pour un sous-réseau avec bits hôte n est 2<sup> n </sup> : 2. Pour un sous-réseau Azure, le nombre maximal de hello d’adresses d’hôte pour un sous-réseau avec bits hôte n est 2<sup> n </sup> – 5 (2 et 3 pour les adresses de hello Azure utilise sur chaque sous-réseau).
> 
> 

Si vous choisissez une taille de sous-réseau est trop petite, vous disposez de toore-IP et redéployez les machines virtuelles de hello dans le sous-réseau de hello.

## <a name="network-security-groups"></a>Network Security Group
Vous pouvez appliquer le filtrage trafic toohello règles qui circulent via vos réseaux virtuels à l’aide de groupes de sécurité réseau. Vous pouvez générer toosecure de règles de filtrage granulaire votre environnement de réseau virtuel, entrants et sortants du trafic, source et destination plages IP, autorisé de ports, etc. de contrôle. Groupes de sécurité réseau peut être appliqué toosubnets au sein d’un réseau virtuel ou directement tooa donné d’interface réseau virtuelle. Il est recommandé de toohave un niveau de filtrage du trafic sur vos réseaux virtuels de groupe de sécurité réseau. Vous pouvez en savoir plus sur [Groupes de sécurité réseau](../../virtual-network/virtual-networks-nsg.md).

## <a name="additional-network-components"></a>Composants réseau supplémentaires
Comme avec une infrastructure de réseau local physique, un réseau virtuel Azure peut contenir plus que des sous-réseaux et des adresses IP. Lorsque vous concevez votre infrastructure d’application, vous souhaiterez peut-être tooincorporate certains de ces composants supplémentaires :

* [Passerelles VPN](../../vpn-gateway/vpn-gateway-about-vpngateways.md) -se connecter à des réseaux virtuels Azure tooother Azure virtual networks ou connectez-vous tooon des réseaux locaux via une connexion VPN de Site à Site. Implémentez des connexions Express Route dédiées et sécurisées. Vous pouvez également fournir aux utilisateurs un accès direct grâce à des connexions VPN de point à site.
* [Un équilibreur de charge](../../load-balancer/load-balancer-overview.md) - fournit l’équilibrage de la charge du trafic pour le trafic externe et interne de la façon dont vous le souhaitez.
* [Passerelle d’application](../../application-gateway/application-gateway-introduction.md) - HTTP, l’équilibrage de charge au niveau de la couche d’application hello, qui fournit des avantages supplémentaires pour les applications web plutôt que de déployer l’équilibrage de charge Azure hello.
* [Traffic Manager](../../traffic-manager/traffic-manager-overview.md) - basée sur DNS distribution toodirect les utilisateurs finaux toohello le plus proche disponible application point de terminaison, toohost vous permettant de trafic de votre application en dehors des centres de données Azure dans des régions différentes.

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

