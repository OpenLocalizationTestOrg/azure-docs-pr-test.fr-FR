---
title: "Fonctionnement de la réplication VMware sur Azure dans Azure Site Recovery | Microsoft Docs"
description: "Cet article fournit une vue d’ensemble des composants et de l’architecture utilisés lors de la réplication de serveurs physiques et de machines virtuelles VMware locaux vers Azure avec le service Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: vmware-walkthrough-architecture
ms.openlocfilehash: 81f02c1277ae8a2c377ca0d6db67ec4211e9aa5e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-does-vmware-replication-to-azure-work-in-site-recovery"></a>Fonctionnement de la réplication VMware sur Azure dans Site Recovery

Cet article décrit les composants et les processus impliqués dans la réplication des serveurs physiques Windows/Linux et des machines virtuelles VMware locaux sur Azure à l’aide du service [Azure Site Recovery](site-recovery-overview.md).

Lorsque vous répliquez des serveurs physiques locaux vers Azure, la réplication utilise également les mêmes composants et processus que pour la réplication de machine virtuelle VMware, mais les différences suivantes sont à noter :

- Vous pouvez utiliser un serveur physique pour le serveur de configuration, au lieu d’une machine virtuelle VMware.
- Il vous faudra une infrastructure VMware locale pour la restauration. Il est impossible d’effectuer une restauration sur un serveur physique.

Publiez des commentaires au bas de cet article ou posez des questions sur le [Forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="architectural-components"></a>Composants architecturaux

Un certain nombre de composants sont impliqués dans la réplication des serveurs physiques et des machines virtuelles VMware Azure.

**Composant** | **Emplacement** | **Détails**
--- | --- | ---
**Microsoft Azure** | Dans Azure, vous avez besoin d’un Compte Azure, d’un compte de stockage Azure et d’un Réseau Azure. | Les données répliquées sont stockées dans le compte de stockage, et les machines virtuelles Azure sont créées avec les données répliquées lors du basculement à partir de votre site local. Les machines virtuelles Azure se connectent au réseau virtuel Azure lors de leur création.
**Serveur de configuration** | Un seul serveur d’administration local (machine virtuelle VMWare) qui exécute tous les composants nécessaires au déploiement, y compris le serveur de configuration, le serveur de traitement, le serveur cible maître | Le composant de serveur de configuration coordonne la communication entre les ordinateurs locaux et Azure, et gère la réplication des données.
 **Serveur de traitement**:  | Installé par défaut sur le serveur de configuration. | Fait office de passerelle de réplication. Reçoit les données de réplication, les optimise grâce à la mise en cache, la compression et le chiffrement et les envoie vers le stockage Azure.<br/><br/> Le serveur de traitement gère également l’installation Push du service Mobilité sur des machines protégées et assure la détection automatique des machines virtuelles VMware.<br/><br/> À mesure que s’étend votre déploiement, vous pouvez ajouter des serveurs de traitement dédiés supplémentaires afin de gérer de plus grands volumes de trafic de réplication.
 **Serveur cible maître** | Installé par défaut sur le serveur de configuration local. | Gère les données de réplication pendant la restauration automatique à partir d’Azure.<br/><br/> Si les volumes de trafic de restauration automatique sont importants, vous pouvez déployer un serveur cible maître distinct pour la restauration.
**Serveurs VMware** | Les machines virtuelles VMware sont hébergées sur des serveurs vSphere ESXi et nous vous recommandons d’utiliser un serveur vCenter pour gérer les ordinateurs hôtes. | Vous ajoutez des serveurs VMware à votre coffre Recovery Services.
**Machines répliquées** | Le service Mobilité sera installé sur chaque machine virtuelle VMware que vous souhaitez répliquer. Il peut être installé manuellement sur chaque ordinateur ou avec une installation push à partir du serveur de traitement.

En savoir plus sur les conditions préalables au déploiement et la configuration requise pour chacun de ces composants dans la [matrice de prise en charge](site-recovery-support-matrix-to-azure.md).

**Figure 1 : composants VMware vers Azure**

![Composants](./media/site-recovery-components/arch-enhanced.png)

## <a name="replication-process"></a>Processus de réplication

1. Vous configurez le déploiement, y compris les composants Azure et un coffre Recovery Services. Dans le coffre, vous spécifiez la source et la cible de réplication, configurez le serveur de configuration, ajoutez des serveurs VMware, créez une stratégie de réplication, déployez le service Mobility, autorisez la réplication et effectuez un test de basculement.
2.  Les machines débutent la réplication conformément à la stratégie définie, et une copie initiale des données est répliquée sur le stockage Azure.
4. La réplication des modifications delta dans Azure commence une fois la réplication initiale terminée. Le suivi des modifications d’une machine est conservé dans un fichier .hrl.
    - Les machines qui assurent la réplication communiquent avec le serveur de configuration sur le port HTTPS 443 entrants, pour la gestion de la réplication.
    - Les machines qui assurent la réplication envoient des données de réplication au serveur de traitement sur le port HTTPS 9443 entrant (configuration possible).
    - Le serveur de configuration orchestre la gestion de la réplication avec Azure sur le port HTTPS 443 sortant.
    - Le serveur de traitement reçoit les données à partir des machines source, puis les chiffre et les envoie au stockage Azure via le port 443 sortant.
    - Si vous activez la cohérence multimachine virtuelle, les machines du groupe de réplication communiquent entre elles sur le port 20004. Le mode multimachine virtuelle est utilisé si vous regroupez plusieurs machines dans des groupes de réplication qui partagent des points de récupération cohérents en cas d’incident et avec les applications lorsqu’ils basculent. Cela est utile si les machines exécutent la même charge de travail et doivent être cohérentes.
5. Le trafic est répliqué sur des points de terminaison publics de stockage Azure via Internet. L’autre solution consiste à utiliser l’[homologation publique](../expressroute/expressroute-circuit-peerings.md#public-peering) Azure ExpressRoute. La réplication du trafic à partir d’un site local vers Azure via un réseau VPN de site à site n’est pas prise en charge.

**Figure 2 : réplication de VMware vers Azure**

![Amélioré](./media/site-recovery-components/v2a-architecture-henry.png)

## <a name="failover-and-failback-process"></a>Processus de basculement et de restauration automatique

1. Après avoir vérifié que le test de basculement fonctionne comme prévu, vous pouvez exécuter des basculements non planifiés sur Azure en fonction des besoins. Le basculement planifié n’est pas pris en charge.
2. Vous pouvez basculer une seule machine ou créer des [plans de récupération](site-recovery-create-recovery-plans.md) pour basculer plusieurs machines virtuelles.
3. Lorsque vous effectuez un basculement, les machines virtuelles répliquées sont créées dans Azure. Vous validez un basculement pour accéder à la charge de travail à partir de la machine virtuelle Azure répliquée.
4. Lorsque votre site local principal est à nouveau disponible, vous pouvez lancer la restauration automatique. Vous configurez une infrastructure de restauration automatique, lancez la réplication de la machine à partir du site secondaire vers le site principal et effectuez un basculement non planifié à partir du site secondaire. Une fois ce basculement validé, les données sont à nouveau disponibles en local et vous devez relancer la réplication sur Azure. [En savoir plus](site-recovery-failback-azure-to-vmware.md)

La restauration automatique doit répondre à plusieurs conditions requises :


- **Serveur de traitement temporaire dans Azure**: si vous souhaitez effectuer une restauration automatique à partir d’Azure après le basculement, vous devez définir une machine virtuelle Azure configurée comme serveur de traitement pour gérer la réplication à partir d’Azure. Vous pourrez supprimer cette machine virtuelle une fois la restauration terminée.
- **Connexion VPN**: pour une restauration automatique, vous devrez disposer d’une connexion VPN (ou d’Azure ExpressRoute) configurée à partir du réseau Azure sur le site local.
- **Serveur cible maître local distinct** : le serveur cible maître local gère la restauration automatique. Le serveur cible maître est installé par défaut sur le serveur d’administration. Toutefois, si vous restaurez automatiquement de plus grands volumes de trafic vous devez définir un serveur cible maître local à cet effet.
- **Stratégie de restauration automatique** : pour répliquer vers votre site local, vous avez besoin d’une stratégie de restauration automatique. Celle-ci est automatiquement créée lors de la création de votre stratégie de réplication.
- **Infrastructure VMware** : vous devez basculer vers une machine virtuelle VMware locale. Cela signifie que vous avez besoin d’une infrastructure VMware locale, même si vous répliquez des serveurs physiques locaux vers Azure.

**Figure 3 : restauration automatique VMware/physique**

![Restauration automatique](./media/site-recovery-components/enhanced-failback.png)


## <a name="next-steps"></a>Étapes suivantes

Examen de la [matrice de prise en charge](site-recovery-support-matrix-to-azure.md)
