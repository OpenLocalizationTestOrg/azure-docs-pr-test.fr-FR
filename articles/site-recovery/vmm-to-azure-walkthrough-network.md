---
title: "aaaPlan mise en réseau pour la réplication Hyper-V (withSystem Center VMM) tooAzure avec Azure Site Recovery | Documents Microsoft"
description: "Cet article décrit la planification d’un réseau requis lors de la réplication des ordinateurs virtuels Hyper-V (avec VMM) tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 41c3c83e-6b1a-496a-8179-498c552ef0c7
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 51ca8b939b6f96880f83599ea8009eb0bfa5b957
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-plan-networking-for-hyper-v-with-vmm-tooazure-replication"></a>Étape 4 : Planifier la mise en réseau pour la réplication Hyper-V (avec VMM) tooAzure

Après avoir effectué [planification de la capacité](vmm-to-azure-walkthrough-capacity.md) (si vous effectuez un déploiement complet), lire cette toolearn l’article sur les considérations de planification lors de la réplication locale des ordinateurs virtuels Hyper-V dans System Center Virtual Machine Manager (VMM) de réseau clouds tooAzure, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service.

Valider les commentaires en bas de hello de cet article, ou poser des questions dans hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="network-mapping-for-replication-tooazure"></a>Mappage réseau pour la réplication tooAzure

Le mappage réseau est utilisé pour répliquer des machines virtuelles de Hyper-V (géré dans VMM) tooAzure. Le mappage réseau opère entre des réseaux de machines virtuelles sur un serveur VMM source et des réseaux Azure cibles. Mappage hello suivant :

- **Connexion réseau**— après basculement, toutes les machines virtuelles de Azure répliquées sont connectés toohello de réseau Azure mappé. Toutes les machines qui basculent sur hello même réseau peut se connecter tooeach autre, même si elles ont échoué sur les plans de récupération différent.
- **Passerelle de réseau**: si une passerelle de réseau est configurée sur le réseau Azure cible de hello, les machines virtuelles peuvent se connecter réseau de machines virtuelles dans hello mappé sur site local tooother.

### <a name="prepare-vmm-for-network-mapping"></a>Préparer VMM pour le mappage réseau

Préparez VMM pour le mappage réseau comme suit :

1. Si vous n’en avez, préparez un [réseau logique VMM](https://docs.microsoft.com/system-center/vmm/network-logical) associé cloud hello dans le hello Hyper-V se trouvent les hôtes.
2. Si vous n’en avez, créé un [réseau d’ordinateurs virtuels](https://docs.microsoft.com/system-center/vmm/network-virtual) toohello lié de réseau logique que vous préparé ci-dessus.
3. Connecter les machines virtuelles sur hello Hyper-V server/cluster hôte Bonjour cloud VMM, toohello réseau d’ordinateurs virtuels.

 
Notez les points suivants : 
- Nouvelles machines virtuelles sont ajoutés au réseau d’ordinateurs virtuels toohello source sont connectés toohello mappé réseau Azure lors de la réplication a lieu.
- Si le réseau cible de hello possède plusieurs sous-réseaux, et un de ces sous-réseaux a hello le même nom que le sous-réseau sur lequel virtual machine de hello source se trouve, puis hello ordinateur virtuel se connecte le sous-réseau de toothat cible après le basculement.
- S’il n’existe aucun sous-réseau cible avec un nom correspondant, ordinateur virtuel de hello se connecte toohello premier sous-réseau de réseau de hello.
- Vous préparez un réseau Azure et définissez des mappages de réseau, que vous déployez un scénario de hello.

## <a name="connecting-tooazure-vms-after-failover"></a>Connecter des machines virtuelles de tooAzure après le basculement

Lorsque vous planifiez votre stratégie de basculement et de réplication, une des questions clés de hello est comment tooconnect toohello machine virtuelle Azure après le basculement. Il existe plusieurs options lors de la conception de votre stratégie réseau pour les machines virtuelles réplica Azure :

- **Utiliser une autre adresse IP**: vous pouvez sélectionner toouse une plage d’adresses IP différentes pour hello répliquées réseau d’ordinateurs virtuels de Azure. Dans cette hello scénario VM Obtient une nouvelle adresse IP après un basculement, et une mise à jour DNS est requis.
- **Conserver hello la même adresse IP**: vous souhaiterez peut-être toouse hello même plage d’adresses IP comme qui dans votre site local principal de réseau, pour hello réseau Azure après le basculement.  Hello conserver des adresses IP mêmes simplifie la récupération hello en réduisant les problèmes de réseau après le basculement. Toutefois, lorsque vous effectuez une réplication tooAzure, vous devez les itinéraires tooupdate avec hello nouvel emplacement des adresses IP de hello après le basculement.


## <a name="retain-ip-addresses"></a>Conserver les adresses IP

Récupération de site fournit la fonctionnalité hello tooretain fixée des adresses IP lors du basculement tooAzure, avec un basculement de sous-réseau.

Avec le basculement de sous-réseau, un sous-réseau spécifique est présent sur le Site 1 ou sur le Site 2, mais jamais sur les deux sites simultanément. Dans l’ordre toomaintain hello espace d’adressage IP dans les événements hello d’un basculement, vous organiser par programme des sous-réseaux de hello hello routeur infrastructure toomove à partir d’un site tooanother. Pendant le basculement, déplacement de sous-réseaux hello avec hello associés à des ordinateurs virtuels protégés. Hello principal inconvénient est que dans l’événement hello d’une défaillance, vous disposez de sous-réseau entier de toomove hello.



### <a name="failover-example"></a>Exemple de basculement

Examinons un exemple de tooAzure de basculement.

- La banque Woodgrove, une société fictive, possède une infrastructure locale pour l’hébergement de ses applications métier. Ses applications mobiles sont hébergées sur Azure.
- Connectivité entre machines virtuelles Woodgrove Bank serveurs locaux et Azure est fournie par une connexion (VPN) de site à site entre le réseau de périmètre local hello et hello réseau virtuel Azure.
- Cela signifie que VPN qui hello réseau virtuel de la société dans Azure s’affiche comme une extension de leur réseau local.
- Woodgrove veut toouse Site Recovery tooreplicate localement les charges de travail tooAzure.
 - Woodgrove a toodeal avec des applications et des configurations dépendent codé en dur des adresses IP et doivent tooretain des adresses IP pour leurs applications après basculement tooAzure.
 - Woodgrove a des adresses IP à partir de la plage 172.16.1.0/24, 172.16.2.0/24 tooits les ressources affectées s’exécutant dans Azure.


Pour Woodgrove toobe en mesure de tooreplicate son tooAzure de machines virtuelles pendant en conservant hello IP adresses, ce qui est société hello doit toodo :

1. Créez un réseau virtuel Azure. Il doit être une extension de hello local réseau, afin que les applications peuvent basculer en toute transparence.
2. Azure permet vous tooadd site-à-site connectivité VPN, en outre, les réseaux virtuels toohello toopoint-à-site connectivité créés dans Azure.
3. Lorsque vous configurez la connexion de site à site hello, Bonjour Azure réseau, vous pouvez acheminer un emplacement de site du trafic toohello (réseau local) uniquement si la plage d’adresses IP hello est différent de la plage d’adresses IP hello localement.
    - Cela est dû au fait qu’Azure ne prend pas en charge les sous-réseaux étirés. Par conséquent, si vous avez sous-réseau 192.168.1.0/24 locale, Impossible d’ajouter un 192.168.1.0/24 réseau local Bonjour réseau Azure.
    - Ceci est dû au fait que Azure ne sait pas qu’il en existe aucune machine virtuelle active dans le sous-réseau de hello, et ce sous-réseau hello est en cours de création pour la récupération d’urgence uniquement.
    - toobe toocorrectly en mesure de router le trafic réseau en dehors d’un Azure hello des sous-réseaux dans le réseau de hello et réseau local hello ne doit pas entrer en conflit.

![Avant le basculement de sous-réseau](./media/vmm-to-azure-walkthrough-network/network-design7.png)

### <a name="before-failover"></a>Avant le basculement

1. Créez un réseau supplémentaire (par exemple, un réseau de récupération). Il s’agit hello réseau qui a échoué sur les ordinateurs virtuels sont créés.
2. tooensure qui hello d’adresse IP pour une machine virtuelle est conservée après un basculement, dans les propriétés de machine virtuelle hello > **configurer**, spécifiez hello même adresse IP que hello machine virtuelle a local, puis cliquez sur **enregistrer**.
3. Lorsque hello machine virtuelle est basculé, Azure Site Recovery attribuera hello fourni tooit d’adresse IP.

    ![Propriétés du réseau](./media/vmm-to-azure-walkthrough-network/network-design8.png)

4. Une fois le basculement déclencheur est déclenché et machines virtuelles de hello sont créés dans Azure avec l’adresse IP de hello requis, vous pouvez vous connecter à l’aide du réseau toohello un [Vnet tooVnet vonnection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md). Cette action peut être scriptée.
5. Itinéraires doivent toobe modifiée en conséquence, tooreflect que 192.168.1.0/24 est passée tooAzure.

    ![Après le basculement de sous-réseau](./media/vmm-to-azure-walkthrough-network/network-design9.png)

### <a name="after-failover"></a>Après le basculement

Si vous ne possédez pas de réseau Azure comme illustré ci-dessus, vous pouvez créer une connexion VPN de site à site entre votre site principal et Azure après le basculement.

## <a name="change-ip-addresses"></a>Modifier les adresses IP

Cela [billet de blog](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explique comment tooset des hello Azure infrastructure réseau lorsque vous n’avez pas besoin de tooretain IP répond après le basculement. Il commence par une description de l’application, ressemble à la tooset un réseau local et dans Azure et se termine avec des informations sur l’exécution des basculements.  

## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 5 : préparer le Azure](vmm-to-azure-walkthrough-prepare-azure.md)
