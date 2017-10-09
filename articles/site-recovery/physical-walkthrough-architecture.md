---
title: "architecture de hello aaaReview pour tooAzure de réplication de serveur physique à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "Cet article fournit une vue d’ensemble des composants et architecture utilisée lors de la réplication tooAzure de serveurs physiques locaux avec hello service Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 09c9b136-35f5-465e-8d0f-f4c5d5d9f880
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 4f334c181fa6f0821adf978ebe9dbd7d36a3c753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-physical-server-replication-tooazure"></a>Étape 1 : Passez en revue l’architecture hello pour tooAzure de réplication de serveur physique

Cet article décrit les composants hello et processus utilisés lors de la réplication locale tooAzure de serveurs physiques Windows/Linux, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service.

Valider les commentaires en bas de hello de cet article, ou poser des questions dans hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="architectural-components"></a>Composants architecturaux

Hello tableau composants hello.

**Composant** | **Prérequis** | **Détails**
--- | --- | ---
**Microsoft Azure** | Vous avez besoin d’un compte Azure, d’un compte de stockage Azure et d’un réseau Azure. | Les données répliquées sont stockées dans le compte de stockage hello et machines virtuelles Azure sont créés avec les données répliquée de hello lorsque le basculement se produit. Machines virtuelles Azure connectent toohello réseau virtuel Azure lorsqu’elles sont créées.
**Serveur de configuration** | Un seul local server de gestion (serveur physique ou VMware VM) qui s’exécute localement toutes les hello de composants de Site Recovery. Ces derniers incluent un serveur de configuration, un serveur de processus et un serveur cible maître. | composant de serveur de configuration Hello coordonne les communications entre Azure et locaux et gère la réplication des données.
 **Serveur de traitement**  | Installé par défaut sur le serveur de configuration hello. | Fait office de passerelle de réplication. Reçoit les données de réplication, il optimise avec la mise en cache, la compression et le chiffrement et l’envoie tooAzure stockage.<br/><br/> serveur de processus Hello gère également la poussée des machines de tooprotected de service de mobilité hello.<br/><br/> Vous pouvez ajouter des serveurs de processus dédié distinct, toohandle augmentation des volumes de trafic de réplication.
 **Serveur cible maître** | Installé par défaut sur le serveur de configuration local hello. | Gère les données de réplication pendant la restauration automatique à partir d’Azure.<br/><br/> Si les volumes de trafic de restauration automatique sont importants, vous pouvez déployer un serveur cible maître distinct pour la restauration.
**Serveurs répliqués** | Hello composant du service mobilité est installé sur chaque serveur Windows/Linux, vous souhaitez tooreplicate. Il peut être installé manuellement sur chaque ordinateur, ou avec une installation poussée du hello du serveur de processus.
**Restauration automatique** | Une infrastructure VMware est requise pour la restauration automatique. Vous ne peuvent pas basculer le serveur physique de tooa précédent.


**Figure 1 : Les composants physiques tooAzure**

![Composants](./media/physical-walkthrough-architecture/arch-enhanced.png)

## <a name="replication-process"></a>Processus de réplication

1. Vous définissez le déploiement hello, y compris sur site et les composants Azure. Dans le coffre Recovery Services hello, vous spécifiez la source de réplication hello cible, configurez le serveur de configuration hello, créer une stratégie de réplication, déployer le service de mobilité hello, activer la réplication et exécuter un test de basculement.
2.  Répliquer des machines conformément à la stratégie de réplication hello et une copie initiale des données de salutation est répliquée tooAzure stockage.
4. Une fois la réplication initiale terminée, la réplication delta modifications tooAzure commence. Le suivi des modifications d’une machine est conservé dans un fichier .hrl.
    - Réplication des ordinateurs communiquent avec le serveur de configuration hello sur le port HTTPS 443 entrants, pour la gestion de la réplication.
    - Réplication des machines envoient le serveur de processus de réplication données toohello sur le port HTTPS 9443 entrants (peut être modifié).
    - serveur de configuration Hello orchestre la gestion de la réplication avec Azure sur le port 443 HTTPS sortantes.
    - serveur de processus Hello reçoit des données à partir d’ordinateurs de la source, optimise crypte et transmet tooAzure stockage via le port 443 sortant.
    - Si vous activez la cohérence multimachine virtuelle, puis les ordinateurs dans le groupe de réplication hello communiquent entre eux sur le port 20004. Le mode multimachine virtuelle est utilisé si vous regroupez plusieurs machines dans des groupes de réplication qui partagent des points de récupération cohérents en cas d’incident et avec les applications lorsqu’ils basculent. Cela est utile si les ordinateurs hello la même charge de travail et devez toobe cohérent.
5. Le trafic est plus des points de terminaison publics répliquées tooAzure stockage, hello internet. L’autre solution consiste à utiliser l’[homologation publique](../expressroute/expressroute-circuit-peerings.md#public-peering) Azure ExpressRoute. Réplication du trafic via une connexion VPN de site à site à partir d’un tooAzure de site local n’est pas pris en charge.

**Figure 2 : La réplication tooAzure physique**

![Amélioré](./media/physical-walkthrough-architecture/v2a-architecture-henry.png)

## <a name="failover-and-failback-process"></a>Processus de basculement et de restauration automatique

Après avoir vérifié que le test de basculement fonctionne comme prévu, vous pouvez exécuter des basculements non planifiés tooAzure en fonction des besoins. Lorsque vous exécutez un basculement, les machines virtuelles Azure sont créées à partir des données répliquées. Lorsque votre site local principal est à nouveau disponible, vous pouvez lancer la restauration automatique. Notez les points suivants :

- Le basculement planifié n’est pas pris en charge.
- Vous pouvez basculer d’un seul ordinateur, ou créer [plans de récupération](site-recovery-create-recovery-plans.md), toofail sur plusieurs ordinateurs simultanément.
- Vous validez un basculement toostart accès hello la charge de travail à partir du réplica de hello machine virtuelle Azure.
- Lorsque le site principal de hello est à nouveau disponible, vous répliquez machine de hello à partir du site principal de hello toohello secondaire. Ensuite, exécutez un basculement non planifié à partir du site secondaire de hello. Une fois que vous validez ce basculement, les données seront arrière localement, et vous devez tooenable réplication tooAzure à nouveau.

Composants de la restauration automatique :

- **Serveur de traitement temporaire Azure**: vous devez tooset une réplication toohandle depuis Azure tooact de machine virtuelle Azure en tant qu’un serveur de processus, entre autres. Vous pourrez supprimer cette machine virtuelle une fois la restauration terminée.
- **Connexion VPN**: vous avez besoin d’une connexion VPN (ou Azure ExpressRoute) à partir du site local de hello réseau Azure toohello.
- **Serveur maître cible local distinct**: serveur du serveur cible maître local hello (installé par défaut sur le serveur de configuration hello) gère la restauration automatique. Si vous restaurez automatiquement de grands volumes de trafic, vous devez configurer un serveur cible maître local distinct à cet effet.
- **Stratégie de restauration automatique** : vous devez définir une stratégie de restauration automatique. Celle-ci est automatiquement créée lors de la création de votre stratégie de réplication.
- **VMware infrastructure**: vous devez restaurer tooan VMware VM sur site. Cela signifie que vous avez besoin d’une infrastructure VMware sur site, même si vous effectuez une réplication tooAzure des serveurs physiques sur site.

**Figure 3 : restauration automatique de serveur physique**

![Restauration automatique](./media/physical-walkthrough-architecture/enhanced-failback.png)


## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 2 : vérifier les conditions préalables et restrictions](physical-walkthrough-prerequisites.md)
