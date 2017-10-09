---
title: les connexions sortantes aaaUnderstanding dans Azure | Documents Microsoft
description: Cet article explique comment Azure permet de toocommunicate de machines virtuelles avec les services Internet publics.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
ms.assetid: 5f666f2a-3a63-405a-abcd-b2e34d40e001
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 5/31/2017
ms.author: kumud
ms.openlocfilehash: ffe59971b934a16c9f6f78e3b15869a0072320d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-outbound-connections-in-azure"></a>Comprendre les connexions sortantes dans Azure

Une machine virtuelle (VM) dans Azure peut communiquer avec des points de terminaison en dehors d’Azure dans l’espace d’adressage IP public. Lorsqu’une machine virtuelle lance une destination de tooa flux sortant dans l’espace d’adressage IP public, Azure mappe privé tooa publique adresse IP la machine virtuelle hello et permet de hello tooreach de trafic de retour machine virtuelle.

Azure fournit trois méthodes différentes connectivité sortante de tooachieve. Chaque méthode possède ses propres fonctionnalités et contraintes. Chaque méthode de consulter attentivement toochoose celui qui répond à vos besoins.

| Scénario | Méthode | Remarque |
| --- | --- | --- |
| Machine virtuelle autonome (aucun équilibrage de charge, aucune adresse IP publique de niveau d’instance) |SNAT par défaut |Azure associe une adresse IP publique pour SNAT |
| Machine virtuelle à charge équilibrée (aucune adresse IP publique de niveau d’instance sur la machine virtuelle) |SNAT à l’aide d’équilibrage de charge hello |Azure utilise une adresse IP publique de l’équilibrage de charge de hello pour SNAT |
| Machine virtuelle avec l’adresse IP publique de niveau d’instance (avec ou sans équilibrage de charge) |SNAT n’est pas utilisé |Azure utilise l’adresse IP publique hello affecté toohello machine virtuelle |

Si vous ne souhaitez pas un toocommunicate de machine virtuelle avec les points de terminaison en dehors d’Azure dans l’espace d’adressage IP public, vous pouvez utiliser l’accès tooblock de groupes de sécurité réseau (NSG). L’utilisation de groupes de sécurité réseau est abordée plus en détail dans [Empêchement de la connectivité publique](#preventing-public-connectivity).

## <a name="standalone-vm-with-no-instance-level-public-ip-address"></a>Machine virtuelle autonome sans adresse IP publique de niveau d’instance

Dans ce scénario, hello machine virtuelle ne fait pas partie d’un pool d’équilibrage de charge Azure et n’a pas une adresse Instance niveau IP Public (ILPIP) tooit. Lorsque hello VM crée un flux sortant, Azure traduit adresse hello source privée de l’adresse IP de hello flux sortant tooa source publique. adresse IP publique Hello utilisé pour ce flux sortant n’est pas configurable et ne compte pas par rapport à la limite de ressource IP publique de l’abonnement hello. Azure utilise tooperform de traduction d’adresse de Source réseau (SNAT) de cette fonction. Les ports éphémères d’adresse IP publique de hello sont des flux d’individuels toodistinguish utilisé par hello machine virtuelle. SNAT alloue dynamiquement des ports éphémères lors de la création de flux. Dans ce contexte, les ports éphémères hello utilisés pour SNAT sont visées tooas SNAT ports.

Les ports SNAT sont une ressource limitée qui peut être épuisée. Il est important toounderstand comment ils sont utilisés. Un seul port SNAT est consommé par l’adresse IP de destination de tooa flux. Pour plusieurs flux toohello adresse IP de destination même, chaque flux consomme un seul port SNAT. Cela garantit que les flux hello sont unique lorsque provenance même hello toohello d’adresse IP publique même adresse IP de destination. Plusieurs flux, chaque adresse IP de destination différent tooa consommer un seul port SNAT par la destination. adresse IP de destination Hello rend hello flux unique.

Vous pouvez utiliser [Analytique de journal pour l’équilibrage de charge](load-balancer-monitor-log.md) et [toomonitor d’alerte de journaux des événements pour les messages d’épuisement du port SNAT](load-balancer-monitor-log.md#alert-event-log). En cas d’épuisement des ressources de port SNAT, les flux sortants échouent jusqu'à ce que des ports SNAT soient libérés par flux existants. L’équilibrage de charge utilise un délai d’inactivité de 4 minutes pour la récupération des ports SNAT.

## <a name="load-balanced-vm-with-no-instance-level-public-ip-address"></a>Machine virtuelle à charge équilibrée sans adresse IP publique de niveau d’instance

Dans ce scénario, hello machine virtuelle fait partie d’un pool d’équilibrage de charge Azure.  Hello machine virtuelle n’a pas une adresse IP publique affectée tooit. Hello ressource d’équilibrage de charge doit être configuré avec une règle toolink hello IP frontale publique avec le pool principal d’hello.  Si vous n’effectuez pas cette configuration, le comportement de hello est comme décrit dans la section hello ci-dessus pour [VM Standalone avec l’adresse IP publique aucun niveau Instance](load-balancer-outbound-connections.md#standalone-vm-with-no-instance-level-public-ip-address).

Lorsque hello équilibrés en charge la machine virtuelle crée un flux sortant, Azure traduit adresse hello source privée de hello flux sortant toohello adresse IP publique d’un serveur frontal de hello publique équilibrage de charge. Azure utilise tooperform de traduction d’adresse de Source réseau (SNAT) de cette fonction. Les ports éphémères d’adresse IP publique de l’équilibreur de charge hello sont des flux d’individuels toodistinguish utilisé par hello machine virtuelle. SNAT alloue dynamiquement des ports éphémères lors de la création de flux sortants. Dans ce contexte, les ports éphémères hello utilisés pour SNAT sont visées tooas SNAT ports.

Les ports SNAT sont une ressource limitée qui peut être épuisée. Il est important toounderstand comment ils sont utilisés. Un seul port SNAT est consommé par l’adresse IP de destination de tooa flux. Pour plusieurs flux toohello adresse IP de destination même, chaque flux consomme un seul port SNAT. Cela garantit que les flux hello sont unique lorsque provenance même hello toohello d’adresse IP publique même adresse IP de destination. Plusieurs flux, chaque adresse IP de destination différent tooa consommer un seul port SNAT par la destination. adresse IP de destination Hello rend hello flux unique.

Vous pouvez utiliser [Analytique de journal pour l’équilibrage de charge](load-balancer-monitor-log.md) et [toomonitor d’alerte de journaux des événements pour les messages d’épuisement du port SNAT](load-balancer-monitor-log.md#alert-event-log). En cas d’épuisement des ressources de port SNAT, les flux sortants échouent jusqu'à ce que des ports SNAT soient libérés par flux existants. L’équilibrage de charge utilise un délai d’inactivité de 4 minutes pour la récupération des ports SNAT.

## <a name="vm-with-an-instance-level-public-ip-address-with-or-without-load-balancer"></a>Machine virtuelle avec une adresse IP publique de niveau d’instance (avec ou sans équilibrage de charge)

Dans ce scénario, hello machine virtuelle a une Instance de niveau publique IP (ILPIP) attribué tooit. Peu importe si hello VM équilibrée de charge est ou non. Lorsqu’une adresse ILPIP est utilisée, SNAT (Source Network Address Translation) n’est pas utilisé. Hello machine virtuelle utilise hello ILPIP pour tous les flux sortants. Si votre application lance plusieurs flux sortants et vous rencontrez l’épuisement de SNAT, vous devez envisager d’affectation d’un tooavoid ILPIP les contraintes SNAT.

## <a name="discovering-hello-public-ip-used-by-a-given-vm"></a>Découverte hello adresse IP publique utilisée par une machine virtuelle donnée

Il existe plusieurs façons d’adresse d’IP toodetermine hello source publique d’une connexion sortante. OpenDNS fournit un service qui vous permet d’afficher hello adresse IP publique de votre machine virtuelle. À l’aide de la commande nslookup de hello, vous pouvez envoyer une requête DNS pour le programme de résolution hello nom myip.opendns.com toohello OpenDNS. service de Hello retourne les adresse IP hello source qui a été de requête de hello toosend utilisé. Lorsque vous exécutez hello suivant la requête à partir de votre machine virtuelle, réponse de hello est hello qu'adresse IP publique utilisée pour cette machine virtuelle.

    nslookup myip.opendns.com resolver1.opendns.com

## <a name="preventing-public-connectivity"></a>Empêchement de la connectivité publique

Parfois, il n’est pas souhaitable pour un ordinateur virtuel toobe autorisé toocreate un flux sortant ou il peut y avoir un toomanage exigence les destinations peuvent être atteint avec flux sortants. Dans ce cas, vous utilisez [groupes de sécurité réseau (NSG)](../virtual-network/virtual-networks-nsg.md) toomanage hello destinations que hello machine virtuelle peut atteindre. Lorsque vous appliquez un groupe de sécurité réseau tooa équilibrée machine virtuelle, vous devez toopay attention toohello [par défaut de balises](../virtual-network/virtual-networks-nsg.md#default-tags) et [règles par défaut](../virtual-network/virtual-networks-nsg.md#default-rules).

Vous devez vous assurer que hello machine virtuelle peut recevoir des demandes de sonde d’intégrité à partir de l’équilibrage de charge Azure. Si un groupe de sécurité réseau blocs intégrité demandes de sonde de hello balise par défaut AZURE_LOADBALANCER, votre sondage de l’intégrité des ordinateurs virtuels échoue et hello machine virtuelle est marquée vers le bas. Équilibrage de charge cesse d’envoyer des toothat flux nouvelle machine virtuelle.

## <a name="limitations"></a>Limites

Si [plusieurs adresses IP (publiques) sont associées à un équilibreur de charge](load-balancer-multivip-overview.md), toutes ces adresses IP publiques sont candidates pour des flux sortants.

Azure utilise un nombre algorithme toodetermine hello de ports SNAT disponibles pour selon la taille hello du pool de hello.  Ce n’est pas configurable pour l’instant.

Il est important de toorememember qui hello du nombre de ports SNAT disponibles ne traduit pas directement toonumber de connexions. Consultez ci-dessus pour plus de détails sur quand et comment les ports SNAT sont allouées et toomanage cette ressource épuisable.
