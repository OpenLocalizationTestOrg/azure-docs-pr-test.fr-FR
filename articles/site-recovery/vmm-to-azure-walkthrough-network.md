---
title: "Planification de la mise en réseau pour la réplication de Hyper-V (avec System Center VMM) vers Azure avec Azure Site Recovery | Microsoft Docs"
description: "Cet article décrit la planification réseau requise pour la réplication de machines virtuelles Hyper-V (avec VMM) vers Azure"
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
ms.openlocfilehash: ef87cd82b021e40f0da05142878daff245cd9c62
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="step-4-plan-networking-for-hyper-v-with-vmm-to-azure-replication"></a>Étape 4 : Planifier la mise en réseau pour la réplication de Hyper-V (avec VMM) vers Azure

Après avoir effectué la [planification de la capacité](vmm-to-azure-walkthrough-capacity.md) (si vous effectuez un déploiement complet), lisez cet article pour en savoir plus sur les considérations en matière de planification réseau lors de la réplication de machines virtuelles Hyper-V locales dans les clouds System Center Virtual Machine Manager (VMM) vers Azure, à l’aide du service [Azure Site Recovery](site-recovery-overview.md).

Publiez des commentaires au bas de cet article ou posez des questions sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="network-mapping-for-replication-to-azure"></a>Mappage réseau pour réplication sur Azure

Un mappage réseau est utilisé lors de la réplication de machines virtuelles Hyper-V (gérées dans VMM) sur Azure. Le mappage réseau opère entre des réseaux de machines virtuelles sur un serveur VMM source et des réseaux Azure cibles. Il effectue les opérations suivantes :

- **Connexion réseau** : après le basculement, toutes les machines virtuelles Azure répliquées sont connectées au réseau Azure mappé. Toutes les machines qui basculent sur le même réseau peuvent se connecter entre elles, même si elles ont basculé dans des plans de récupération différents.
- **Passerelle réseau** : si une passerelle réseau est configurée sur le réseau Azure cible, les machines virtuelles peuvent se connecter à d’autres machines virtuelles locales sur le réseau local mappé.

### <a name="prepare-vmm-for-network-mapping"></a>Préparer VMM pour le mappage réseau

Préparez VMM pour le mappage réseau comme suit :

1. Si vous n’en avez pas, préparez un [réseau logique VMM](https://docs.microsoft.com/system-center/vmm/network-logical) qui est associé au cloud dans lequel se trouvent les hôtes Hyper-V.
2. Si vous n’en avez pas, créez un [réseau de machines virtuelles](https://docs.microsoft.com/system-center/vmm/network-virtual) lié au réseau logique que vous avez préparé ci-dessus.
3. Connectez les machines virtuelles sur le cluster/serveur hôte Hyper-V dans le cloud VMM au réseau de machines virtuelles.

 
Notez les points suivants : 
- Les nouvelles machines virtuelles connectées au réseau de machines virtuelles source sont connectées au réseau Azure mappé lors de la réplication.
- Si le réseau cible est associé à plusieurs sous-réseaux et que l’un d’eux présente le même nom que le sous-réseau dans lequel se trouve la machine virtuelle source, la machine virtuelle de réplication se connecte à ce sous-réseau cible après le basculement.
- S’il n’existe aucun sous-réseau cible avec un nom correspondant, la machine virtuelle se connecte au premier sous-réseau du réseau.
- Vous préparez un réseau Azure et configurez les mappages de réseau, en même temps que vous déployez le scénario.

## <a name="connecting-to-azure-vms-after-failover"></a>Connexion aux machines virtuelles Azure après le basculement

Lorsque vous planifiez votre stratégie de basculement et de réplication, l’une des questions clés est de savoir comment se connecter à la machine virtuelle Azure après le basculement. Il existe plusieurs options lors de la conception de votre stratégie réseau pour les machines virtuelles réplica Azure :

- **Utiliser une adresse IP différente** : vous pouvez choisir d’utiliser une autre plage d’adresses IP pour le réseau de la machine virtuelle Azure répliquée. Dans ce scénario, la machine virtuelle reçoit une nouvelle adresse IP après le basculement, et une mise à jour DNS est nécessaire.
- **Conserver la même adresse IP** : vous souhaiterez peut-être utiliser la même plage d’adresses IP que celle du réseau principal local pour le réseau Azure après le basculement.  La conservation des mêmes adresses IP simplifie la récupération en réduisant les problèmes liés au réseau après le basculement. Toutefois, lorsque vous effectuez une réplication vers Azure, vous devez mettre à jour des itinéraires avec le nouvel emplacement des adresses IP après le basculement.


## <a name="retain-ip-addresses"></a>Conserver les adresses IP

Site Recovery offre la possibilité de conserver des adresses IP fixes lors du basculement vers Azure, grâce à un basculement de sous-réseau.

Avec le basculement de sous-réseau, un sous-réseau spécifique est présent sur le Site 1 ou sur le Site 2, mais jamais sur les deux sites simultanément. Pour conserver l’espace d’adressage IP en cas de basculement, vous pouvez mettre en place un programme pour que l’infrastructure du routeur déplace les sous-réseaux d’un site à un autre. Pendant le basculement, les sous-réseaux se déplacent avec les machines virtuelles protégées associées. Le principal inconvénient est qu’en cas de défaillance, vous devez déplacer le sous-réseau tout entier.



### <a name="failover-example"></a>Exemple de basculement

Examinons un exemple de basculement vers Azure.

- La banque Woodgrove, une société fictive, possède une infrastructure locale pour l’hébergement de ses applications métier. Ses applications mobiles sont hébergées sur Azure.
- La connectivité entre les machines virtuelles de la banque Woodgrove sur Azure et les serveurs locaux est fournie par une connexion de site à site (VPN) entre le réseau de périmètre et le réseau virtuel Azure.
- Ce type de VPN signifie que le réseau virtuel de la société dans Azure s’affiche comme une extension de son réseau local.
- Woodgrove souhaite utiliser Site Recovery pour répliquer les charges de travail locales vers Azure.
 - Woodgrove doit traiter des applications et des configurations qui dépendent d’adresses IP codées en dur. De ce fait, la société doit conserver les adresses IP de ses applications après le basculement vers Azure.
 - Woodgrove a assigné des adresses IP de la plage 172.16.1.0/24, 172.16.2.0/24 à ses ressources exécutées dans Azure.


Pour pouvoir répliquer ses machines virtuelles vers Azure en conservant les adresses IP, voici ce que Woodgrove doit faire :

1. Créez un réseau virtuel Azure. Il doit s’agir d’une extension du réseau local afin que les applications puissent basculer en toute transparence.
2. Azure vous permet d’ajouter une connectivité VPN de site à site en plus de la connectivité de point à site avec les réseaux virtuels créés dans Azure.
3. Lorsque vous configurez la connexion de site à site, dans le réseau Azure, vous pouvez acheminer le trafic vers l’emplacement local (réseau local) uniquement si la plage d’adresses IP est différente de la plage d’adresses IP locales.
    - Cela est dû au fait qu’Azure ne prend pas en charge les sous-réseaux étirés. Si vous avez un sous-réseau local 192.168.1.0/24, vous ne pouvez donc pas ajouter un réseau local 192.168.1.0/24 dans le réseau Azure.
    - Ceci est dû au fait que Azure ne sait pas qu’aucune machine virtuelle n’est active dans le sous-réseau et que le sous-réseau est créé uniquement à des fins de récupération d’urgence.
    - Pour pouvoir acheminer correctement le trafic réseau à partir d’un réseau Azure, les sous-réseaux du réseau et le réseau local ne doivent pas entrer en conflit.

![Avant le basculement de sous-réseau](./media/vmm-to-azure-walkthrough-network/network-design7.png)

### <a name="before-failover"></a>Avant le basculement

1. Créez un réseau supplémentaire (par exemple, un réseau de récupération). Il s’agit du réseau dans lequel les machines virtuelles basculées sont créées.
2. Pour vous assurer que l’adresse IP d’une machine virtuelle est conservée après un basculement, dans Propriétés de la machine virtuelle > **Configurer**, spécifiez la même adresse IP que celle utilisée par la machine virtuelle en local, puis cliquez sur **Enregistrer**.
3. Au basculement de la machine virtuelle, Azure Site Recovery affecte l’adresse IP fournie à cette machine virtuelle.

    ![Propriétés du réseau](./media/vmm-to-azure-walkthrough-network/network-design8.png)

4. Une fois que le basculement a été déclenché et que les machines virtuelles ont été créées dans Azure avec l’adresse IP requise, vous pouvez vous connecter au réseau à l’aide d’une [connexion de réseau virtuel à réseau virtuel](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md). Cette action peut être scriptée.
5. Les itinéraires doivent être modifiés de façon appropriée afin de refléter le déplacement de l’adresse IP 192.168.1.0/24 vers Azure.

    ![Après le basculement de sous-réseau](./media/vmm-to-azure-walkthrough-network/network-design9.png)

### <a name="after-failover"></a>Après le basculement

Si vous ne possédez pas de réseau Azure comme illustré ci-dessus, vous pouvez créer une connexion VPN de site à site entre votre site principal et Azure après le basculement.

## <a name="change-ip-addresses"></a>Modifier les adresses IP

Cet [article de blog](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explique comment configurer le service d’infrastructure réseau Azure lorsqu’il n’est pas nécessaire de conserver les adresses IP après le basculement. Il commence par une description de l’application, aborde la procédure de configuration des services de mise en réseau locaux et se conclut par des informations sur l’exécution des basculements.  

## <a name="next-steps"></a>Étapes suivantes

Aller à [Étape 5 : Préparer Azure](vmm-to-azure-walkthrough-prepare-azure.md)
