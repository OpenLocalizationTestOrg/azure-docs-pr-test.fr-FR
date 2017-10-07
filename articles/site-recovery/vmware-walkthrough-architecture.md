---
title: "architecture de hello aaaReview pour VMware réplication tooAzure | Documents Microsoft"
description: "Cet article fournit une vue d’ensemble des composants et architecture utilisée lors de la réplication tooAzure d’ordinateurs virtuels VMware locaux avec hello service Azure Site Recovery"
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
ms.topic: article
ms.date: 06/27.017
ms.author: raynew
ms.openlocfilehash: 7acb1d8e83a846dca79e175fd1af9324f2c31e65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-vmware-replication-tooazure"></a>Étape 1 : Passez en revue l’architecture hello pour VMware réplication tooAzure

Cet article décrit les composants hello et processus utilisés lors de la réplication locale tooAzure de machines virtuelles VMware à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service.

Valider les commentaires en bas de hello de cet article, ou poser des questions dans hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="architectural-components"></a>Composants architecturaux

Hello tableau composants hello.

**Composant** | **Prérequis** | **Détails**
--- | --- | ---
**Microsoft Azure** | Vous avez besoin d’un abonnement Azure, d’un compte de stockage Azure et d’un Réseau Azure. | Les données répliquées sont stockées dans le compte de stockage hello. Machines virtuelles Azure sont créés avec les données de salutation répliquée en cas de basculement à partir de votre site local. Hello machines virtuelles Azure se connecter toohello réseau virtuel Azure lorsqu’elles sont créées.
**Serveur de configuration** | Un seul local management server (VMware VM) qui s’exécute tous les hello localement des composants de Site Recovery pour le déploiement de hello. Ces derniers incluent un serveur de configuration, un serveur de processus et un serveur cible maître. | composant de serveur de configuration Hello coordonne les communications entre Azure et locaux et gère la réplication des données.
 **Serveur de traitement**:  | Installé par défaut sur le serveur de configuration hello. | Fait office de passerelle de réplication. Reçoit les données de réplication, il optimise avec la mise en cache, la compression et le chiffrement et l’envoie tooAzure stockage.<br/><br/> serveur de processus Hello gère l’installation push des machines de tooprotected de service de mobilité hello et effectue la détection automatique des ordinateurs virtuels VMware.<br/><br/> À mesure que votre déploiement augmente, vous pouvez ajouter toohandle de serveurs de processus dédié distinct supplémentaire augmentation des volumes de trafic de réplication.
 **Serveur cible maître** | Installé par défaut sur le serveur de configuration local hello. | Gère les données de réplication pendant la restauration automatique à partir d’Azure.<br/><br/> Si les volumes de trafic de restauration automatique sont importants, vous pouvez déployer un serveur cible maître distinct pour la restauration.
**Serveurs VMware** | Les ordinateurs virtuels VMware sont hébergés sur des serveurs vSphere ESXi, et nous recommandons un vCenter hôtes hello toomanage du serveur. | Vous ajoutez le coffre de Services de récupération de tooyour de serveurs VMware.
**Machines répliquées** | sera installé sur chaque VM VMware vous répliquez Hello service mobilité. Il peut être installé manuellement sur chaque ordinateur, ou avec une installation poussée du hello du serveur de processus.

**Figure 1 : VMware tooAzure composants**

![Composants](./media/vmware-walkthrough-architecture/arch-enhanced.png)

## <a name="replication-process"></a>Processus de réplication

1. Vous définissez le déploiement hello, y compris sur site et les composants Azure. Dans le coffre Recovery Services hello, vous spécifiez la source de réplication hello cible, configurez le serveur de configuration hello, créer une stratégie de réplication, déployer le service de mobilité hello, activer la réplication et exécuter un test de basculement.
2. Répliquer des machines conformément à la stratégie de réplication hello et une copie initiale des données de salutation est répliquée tooAzure stockage.
3. Une fois la réplication initiale terminée, la réplication delta modifications tooAzure commence. Le suivi des modifications d’une machine est conservé dans un fichier .hrl.
    - Réplication des ordinateurs communiquent avec le serveur de configuration hello sur le port HTTPS 443 entrants, pour la gestion de la réplication.
    - Réplication des machines envoient le serveur de processus de réplication données toohello sur le port HTTPS 9443 entrants (peut être modifié).
    - serveur de configuration Hello orchestre la gestion de la réplication avec Azure sur le port 443 HTTPS sortantes.
    - serveur de processus Hello reçoit des données à partir d’ordinateurs de la source, optimise crypte et transmet tooAzure stockage via le port 443 sortant.
    - Si vous activez la cohérence multimachine virtuelle, puis les ordinateurs dans le groupe de réplication hello communiquent entre eux sur le port 20004. Le mode multimachine virtuelle est utilisé si vous regroupez plusieurs machines dans des groupes de réplication qui partagent des points de récupération cohérents en cas d’incident et avec les applications lorsqu’ils basculent. Cela est utile si les ordinateurs hello la même charge de travail et devez toobe cohérent.
4. Le trafic est plus des points de terminaison publics répliquées tooAzure stockage, hello internet. L’autre solution consiste à utiliser l’[homologation publique](../expressroute/expressroute-circuit-peerings.md#public-peering) Azure ExpressRoute. Réplication du trafic via une connexion VPN de site à site à partir d’un tooAzure de site local n’est pas pris en charge.


**Figure 2 : VMware tooAzure réplication**

![Amélioré](./media/vmware-walkthrough-architecture/v2a-architecture-henry.png)

## <a name="failover-and-failback-process"></a>Processus de basculement et de restauration automatique

1. Après avoir vérifié que le test de basculement fonctionne comme prévu, vous pouvez exécuter des basculements non planifiés tooAzure en fonction des besoins. Le basculement planifié n’est pas pris en charge.
2. Vous pouvez basculer d’un seul ordinateur, ou créer [plans de récupération](site-recovery-create-recovery-plans.md), toofail sur plusieurs machines virtuelles.
3. Lorsque vous effectuez un basculement, les machines virtuelles répliquées sont créées dans Azure. Vous validez un basculement toostart accès hello la charge de travail à partir du réplica de hello machine virtuelle Azure.
4. Lorsque votre site local principal est à nouveau disponible, vous pouvez lancer la restauration automatique. Vous configurez une infrastructure de la restauration automatique, commence à répliquer l’ordinateur de hello de toohello de site secondaire hello principal et exécutez un basculement non planifié à partir du site secondaire de hello. Une fois que vous validez ce basculement, les données seront arrière localement, et vous devez tooenable réplication tooAzure à nouveau. [En savoir plus](site-recovery-failback-azure-to-vmware.md)

La restauration automatique doit répondre à plusieurs conditions requises :


- **Serveur de traitement temporaire Azure**: Si vous souhaitez toofail à partir de Azure après le basculement, vous devez tooset d’une machine virtuelle de Azure configuré comme un serveur de processus, la réplication toohandle depuis Azure. Vous pourrez supprimer cette machine virtuelle une fois la restauration terminée.
- **Connexion VPN**: pour la restauration automatique que vous aurez besoin d’une connexion VPN (ou le Azure ExpressRoute) configurer à partir du site local de hello réseau Azure toohello.
- **Serveur maître cible local distinct**: hello locale cible maître server gère la restauration automatique. serveur cible maître de Hello est installé par défaut sur le serveur d’administration hello, mais si vous êtes échouent précédent supérieure volumes de trafic vous devez configurer un serveur de la cible maître local distinct à cet effet.
- **Stratégie de restauration automatique**: tooyour de retour tooreplicate site local, vous avez besoin d’une stratégie de restauration automatique. Celle-ci est automatiquement créée lors de la création de votre stratégie de réplication.
- **VMware infrastructure**: vous devez restaurer tooan VMware VM sur site. Cela signifie que vous avez besoin d’une infrastructure VMware sur site, même si vous effectuez une réplication tooAzure des serveurs physiques sur site.

**Figure 3 : restauration automatique VMware/physique**

![Restauration automatique](./media/vmware-walkthrough-architecture/enhanced-failback.png)


## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 2 : vérifier les conditions préalables et restrictions](vmware-walkthrough-prerequisites.md)
