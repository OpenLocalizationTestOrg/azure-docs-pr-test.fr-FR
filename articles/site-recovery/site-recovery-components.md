---
title: "aaaHow fonctionne de la récupération de Site ? | Microsoft Docs"
description: "Cet article propose une vue d’ensemble de l’architecture de Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-azure-to-azure-architecture
ms.openlocfilehash: ff1580d0fe294148dc0c621728491e6119c3048a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-site-recovery-work-for-on-premises-infrastructure"></a>Comment Azure Site Recovery fonctionne-t-il pour l’infrastructure locale ?

> [!div class="op_single_selector"]
> * [Répliquer des machines virtuelles Azure](site-recovery-azure-to-azure-architecture.md)
> * [Répliquer des machines locales](site-recovery-components.md)

Cet article décrit l’architecture sous-jacente de hello [Azure Site Recovery](site-recovery-overview.md) service et les composants hello qui la rendent fonctionnent pour répliquer les charges de travail local tooAzure.

Valider les commentaires en bas de hello de cet article ou Bonjour [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="replicate-tooazure"></a>Répliquer tooAzure

Vous pouvez répliquer et protéger suivant hello sur site infrastructure tooAzure :

- **VMware**: Machines virtuelles VMware locales s’exécutant sur un [hôte pris en charge](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers). Vous pouvez répliquer des machines virtuelles VMware exécutant les [systèmes d’exploitation pris en charge](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)
- **Hyper-V**: machines virtuelles Hyper-V locales s’exécutant sur des [hôtes pris en charge](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).
- **Machines physiques**: serveurs physiques locaux exécutant Windows ou Linux sur les [systèmes d’exploitation pris en charge](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions). Vous pouvez répliquer des machines virtuelles Hyper-V exécutant un système d’exploitation invité [pris en charge par Hyper-V et Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).

## <a name="vmware-tooazure"></a>VMware tooAzure

Voici ce que vous avez besoin pour répliquer des ordinateurs virtuels VMware tooAzure.

Domaine | Composant | Détails
--- | --- | ---
**Serveur de configuration** | Un seul serveur d’administration (Machine virtuelle VMware) exécute tous les composants locaux - serveur de configuration, serveur de traitement, serveur cible maître | serveur de configuration Hello coordonne les communications entre les locaux et Azure et gère la réplication des données.
 **Serveur de traitement**:  | Installé par défaut sur le serveur de configuration hello. | Fait office de passerelle de réplication. Reçoit les données de réplication, il optimise avec la mise en cache, la compression et le chiffrement et l’envoie tooAzure stockage.<br/><br/> serveur de processus Hello gère l’installation push des machines de tooprotected de service de mobilité hello et effectue la détection automatique des ordinateurs virtuels VMware.<br/><br/> À mesure que votre déploiement augmente, vous pouvez ajouter toohandle de serveurs de processus dédié distinct supplémentaire augmentation des volumes de trafic de réplication.
 **Serveur cible maître** | Installé par défaut sur le serveur de configuration local hello. | Gère les données de réplication pendant la restauration automatique à partir d’Azure.<br/><br/> Si les volumes de trafic de restauration automatique sont importants, vous pouvez déployer un serveur cible maître distinct pour la restauration.
**Serveurs VMware** | Les ordinateurs virtuels VMware sont hébergés sur des serveurs vSphere ESXi, et nous recommandons un vCenter hôtes hello toomanage du serveur. | Vous ajoutez le coffre de Services de récupération de tooyour de serveurs VMware.<br/><br/>
**Machines répliquées** | Hello service mobilité sera installé sur chaque machine virtuelle que vous souhaitez tooreplicate VMware. Il peut être installé manuellement sur chaque ordinateur, ou avec une installation poussée du hello du serveur de processus.| -

**Figure 1 : VMware tooAzure composants**

![Composants](./media/site-recovery-components/arch-enhanced.png)

### <a name="replication-process"></a>Processus de réplication

1. Vous définissez le déploiement hello, y compris les composants Azure et un coffre Recovery Services. Dans le coffre de hello, vous spécifiez la source de réplication hello cible, configurez le serveur de configuration hello, ajouter des serveurs VMware, créer une stratégie de réplication, déployer le service de mobilité hello, activer la réplication et exécuter un test de basculement.
2.  Ordinateurs commence à répliquer conformément à la stratégie de réplication hello et une copie initiale des données de salutation est répliquée tooAzure stockage.
4. La réplication de delta modifications tooAzure commence une fois la réplication initiale hello terminée. Le suivi des modifications d’une machine est conservé dans un fichier .hrl.
    - Réplication des ordinateurs communiquent avec le serveur de configuration hello sur le port HTTPS 443 entrants, pour la gestion de la réplication.
    - Réplication des machines envoient le serveur de processus de réplication données toohello sur le port HTTPS 9443 entrants (peut être configuré).
    - serveur de configuration Hello orchestre la gestion de la réplication avec Azure sur le port 443 HTTPS sortantes.
    - serveur de processus Hello reçoit des données à partir d’ordinateurs de la source, optimise crypte et transmet tooAzure stockage via le port 443 sortant.
    - Si vous activez la cohérence multimachine virtuelle, puis les ordinateurs dans le groupe de réplication hello communiquent entre eux sur le port 20004. Le mode multimachine virtuelle est utilisé si vous regroupez plusieurs machines dans des groupes de réplication qui partagent des points de récupération cohérents en cas d’incident et avec les applications lorsqu’ils basculent. Cela est utile si les ordinateurs hello la même charge de travail et devez toobe cohérent.
5. Le trafic est plus des points de terminaison publics répliquées tooAzure stockage, hello internet. L’autre solution consiste à utiliser l’[homologation publique](https://docs.microsoft.com/en-us/azure/expressroute/expressroute-circuit-peerings#public-peering) Azure ExpressRoute. Réplication du trafic via une connexion VPN de site à site à partir d’un tooAzure de site local n’est pas pris en charge.

**Figure 2 : VMware tooAzure réplication**

![Amélioré](./media/site-recovery-components/v2a-architecture-henry.png)

### <a name="failover-and-failback"></a>Basculement et restauration automatique

1. Après avoir vérifié que le test de basculement fonctionne comme prévu, vous pouvez exécuter des basculements non planifiés tooAzure en fonction des besoins. Le basculement planifié n’est pas pris en charge.
2. Vous pouvez basculer d’un seul ordinateur, ou créer [plans de récupération](site-recovery-create-recovery-plans.md), toofail sur plusieurs machines virtuelles.
3. Lorsque vous effectuez un basculement, les machines virtuelles répliquées sont créées dans Azure. Vous validez un basculement toostart accès hello la charge de travail à partir du réplica de hello machine virtuelle Azure.
4. Lorsque votre site local principal est à nouveau disponible, vous pouvez lancer la restauration automatique. Vous configurez une infrastructure de la restauration automatique, commence à répliquer l’ordinateur de hello de toohello de site secondaire hello principal et exécutez un basculement non planifié à partir du site secondaire de hello. Une fois que vous validez ce basculement, les données seront arrière localement, et vous devez tooenable réplication tooAzure à nouveau. [En savoir plus](site-recovery-failback-azure-to-vmware.md)

**Figure 3 : restauration automatique VMware/physique**

![Restauration automatique](./media/site-recovery-components/enhanced-failback.png)

## <a name="physical-tooazure"></a>TooAzure physique

Lorsque vous répliquez tooAzure des serveurs physiques locaux, la réplication utilise hello également même des composants et des processus en tant que [VMware tooAzure](#vmware-replication-to-azure), mais notez ces différences :

- Vous pouvez utiliser un serveur physique pour le serveur de configuration hello, au lieu d’un VM VMware
- Il vous faudra une infrastructure VMware locale pour la restauration. Vous ne peuvent pas basculer l’ordinateur physique tooa précédent.

## <a name="hyper-v-tooazure"></a>Hyper-V tooAzure

### <a name="replication-process"></a>Processus de réplication

1. Permet de paramétrer hello composants Azure. Nous vous recommandons de configurer les comptes de stockage et de réseau avant de lancer le déploiement de Site Recovery.
2. Vous créez un coffre Replication Services pour Site Recovery et configurez les paramètres du coffre, notamment :
    - Paramètres source et cible. Si vous ne gérez pas des hôtes Hyper-V dans un cloud VMM, pour la cible de hello vous créez un conteneur de site Hyper-V et ajoutez tooit des ordinateurs hôtes Hyper-V. Si les ordinateurs hôtes Hyper-V sont gérées dans VMM, source de hello est cloud VMM de hello. cible de Hello est Azure.
    - Installation de type hello fournisseur Azure Site Recovery et l’agent de Microsoft Azure Recovery Services hello. Si vous avez hello VMM fournisseur sera installé sur celui-ci et hello agent sur chaque ordinateur hôte Hyper-V. Si vous n’avez pas VMM, hello fournisseur et l’agent sont installés sur chaque ordinateur hôte.
    - Vous créez une stratégie de réplication pour le site de Hyper-V hello ou un cloud VMM. stratégie de Hello est machines virtuelles de tooall appliquée situées sur des ordinateurs hôtes dans le cloud ou le site de hello.
    - Vous activez la réplication pour les machines virtuelles Hyper-V. La réplication initiale se produit conformément aux paramètres de stratégie de réplication hello.
4. Suivi des modifications de données et la réplication de delta modifications tooAzure commence une fois la réplication initiale hello terminée. Les modifications qui font l’objet d’un suivi sont conservées dans un fichier .hrl.
5. Vous exécutez un toomake de basculement de test que tout fonctionne.

### <a name="failover-and-failback-process"></a>Processus de basculement et de restauration automatique

1. Vous pouvez exécuter planifié ou non planifié [basculement](site-recovery-failover.md) de tooAzure d’ordinateurs virtuels Hyper-V local. Si vous exécutez un basculement planifié, alors que les machines virtuelles source sont arrêtés tooensure aucune perte de données.
2. Vous pouvez basculer d’un seul ordinateur, ou créer [plans de récupération](site-recovery-create-recovery-plans.md) basculement tooorchestrate de plusieurs ordinateurs.
4. Après avoir exécuté hello basculement, vous devez être hello toosee en mesure de création de machines virtuelles de réplica dans Azure. Vous pouvez affecter un toohello d’adresse IP publique machine virtuelle si nécessaire.
5. Ensuite, vous validez toostart de basculement hello l’accès à la charge de travail hello du réplica de hello machine virtuelle Azure.
6. Lorsque votre site local principal est à nouveau disponible, vous pouvez lancer la [restauration automatique](site-recovery-failback-from-azure-to-hyper-v.md). Vous démarrez un basculement planifié à partir du site principal de toohello Azure. Pour un basculement planifié, que vous pouvez sélectionnez toofailback toohello même machine virtuelle ou tooan autre emplacement et de synchroniser change entre Azure et locaux, tooensure sans perte de données. Lorsque les ordinateurs virtuels sont créés localement, vous validez hello basculement.

**Figure 4 : Réplication de tooAzure de site Hyper-V**

![Composants](./media/site-recovery-components/arch-onprem-azure-hypervsite.png)

**Figure 5 : La réplication tooAzure des clouds Hyper-V dans VMM**

![Composants](./media/site-recovery-components/arch-onprem-onprem-azure-vmm.png)


## <a name="replicate-tooa-secondary-site"></a>Répliquer le site secondaire de tooa

Vous pouvez répliquer hello site secondaire de tooyour suivant :

- **VMware**: Machines virtuelles VMware locales s’exécutant sur un [hôte pris en charge](site-recovery-support-matrix-to-sec-site.md#on-premises-servers). Vous pouvez répliquer des machines virtuelles VMware exécutant les [systèmes d’exploitation pris en charge](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions)
- **Machines physiques**: serveurs physiques locaux exécutant Windows ou Linux sur les [systèmes d’exploitation pris en charge](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions).
- **Hyper-V**: machines virtuelles Hyper-V locales s’exécutant sur des [hôtes Hyper-V pris en charge](site-recovery-support-matrix-to-sec-site.md#on-premises-servers) gérés dans des clouds VMM. [Systèmes d’exploitation pris en charge](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers). Vous pouvez répliquer des machines virtuelles Hyper-V exécutant un système d’exploitation invité [pris en charge par Hyper-V et Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).


## <a name="vmwarephysical-tooa-secondary-site"></a>Site secondaire de VMware/physiques tooa

Pour répliquer des ordinateurs virtuels VMware ou serveurs physiques tooa secondaire à l’aide de InMage Scout.

### <a name="components"></a>Composants

**Zone** | **Composant** | **Détails**
--- | --- | ---
**Serveur de traitement** | Situé dans le site principal | Vous déployez hello processus serveur toohandle la mise en cache, la compression et l’optimisation des données.<br/><br/> Il gère également installation push du hello toomachines unifiée de l’Agent vous souhaitez tooprotect.
**Serveur de configuration** | Situé sur le site secondaire | serveur de configuration Hello gère, configurer et surveiller votre déploiement, soit à l’aide du site Web de gestion hello ou console v-continuum de hello.
**Serveur vContinuum** | facultatif. Installation Bonjour même emplacement que le serveur de configuration hello. | Il intègre une console qui vous permet de gérer et surveiller votre environnement protégé.
**Serveur cible maître** | Situé dans le site secondaire de hello | serveur cible maître de Hello conserve les données répliquées. Reçoit les données de serveur de processus hello, crée une machine de réplication dans le site secondaire de hello et contient des points de rétention de données hello.<br/><br/> nombre de Hello de serveurs cible maître que nécessaires dépend de nombre de hello d’ordinateurs que vous protégez.<br/><br/> Si vous souhaitez que le site principal de toofail toohello précédent, vous devez un serveur cible maître il trop. Hello unifiée de l’Agent est installé sur ce serveur.
**Serveur VMware ESX/ESXi et vCenter** |  Les machines virtuelles sont hébergées sur des hôtes ESX/ESXi. Les hôtes sont gérés avec un serveur vCenter | Vous avez besoin d’un tooreplicate d’infrastructure VMware les ordinateurs virtuels VMware.
**Machines virtuelles/serveurs physiques** |  Unifiée Agent installé sur les ordinateurs virtuels VMware et des serveurs physiques que vous souhaitez tooreplicate. | l’agent de Hello agit comme un fournisseur de la communication entre tous les composants de hello.


### <a name="replication-process"></a>Processus de réplication

1. Configurer des serveurs de composant hello dans chaque site (configuration, process, serveur cible maître) et les installer hello unifié Agent sur les ordinateurs que vous souhaitez tooreplicate.
2. Après la réplication initiale, l’agent de hello sur chaque ordinateur envoie delta de réplication modifications toohello processus serveur.
3. serveur de processus Hello optimise les données de salutation et les transfère de serveur cible maître de toohello sur le site secondaire de hello. serveur de configuration Hello gère le processus de réplication hello.

**Figure 6 : VMware tooVMware réplication**

![VMware tooVMware](./media/site-recovery-components/vmware-to-vmware.png)



## <a name="hyper-v-tooa-secondary-site"></a>Site secondaire de Hyper-V tooa

Voici ce que vous avez besoin pour la réplication de site secondaire de tooa des ordinateurs virtuels Hyper-V.


**Zone** | **Composant** | **Détails**
--- | --- | ---
**Serveur VMM** | Nous vous recommandons d’un serveur VMM dans le site principal de hello et un site secondaire de hello | Chaque serveur VMM doit être connecté toohello internet.<br/><br/> Chaque serveur doit avoir au moins un cloud privé VMM avec l’ensemble de profils de capacité hello Hyper-V.<br/><br/> Vous installez hello fournisseur Azure Site Recovery sur le serveur VMM de hello. Hello fournisseur coordonne et orchestre la réplication avec hello service Site Recovery sur hello internet. Les communications entre hello fournisseur et Azure sont sécurisé et chiffré.
**Serveur Hyper-V** |  Serveurs d’hôte Hyper-V un ou plusieurs dans des clouds VMM principaux et secondaires hello.<br/><br/> Les serveurs doivent être connecté toohello internet.<br/><br/> Données sont répliquées entre hello serveurs principaux et secondaires Hyper-V hôte via hello LAN ou VPN, à l’aide de l’authentification Kerberos ou le certificat.  
**Machines virtuelles Hyper-V** | Situé sur le serveur hôte de hello source Hyper-V. | serveur hôte de Hello source doit avoir au moins une machine virtuelle que vous souhaitez tooreplicate.

### <a name="replication-process"></a>Processus de réplication

1. Permet de paramétrer hello compte Azure.
2. Vous créez un coffre Replication Services pour Site Recovery et configurez les paramètres du coffre, notamment :

    - Hello réplication sites source et cible (principales et secondaires).
    - Installation de type hello fournisseur Azure Site Recovery et l’agent de Microsoft Azure Recovery Services hello. Hello fournisseur est installé sur les serveurs VMM et agent hello sur chaque ordinateur hôte Hyper-V.
    - Vous créez une stratégie de réplication pour le cloud VMM source. stratégie de Hello est appliqué tooall machines virtuelles situées sur des ordinateurs hôtes dans le cloud de hello.
    - Vous activez la réplication pour les machines virtuelles Hyper-V. La réplication initiale se produit conformément aux paramètres de stratégie de réplication hello.
4. Suivi des modifications de données et la réplication delta change toobegins après la réplication initiale hello. Les modifications qui font l’objet d’un suivi sont conservées dans un fichier .hrl.
5. Vous exécutez un toomake de basculement de test que tout fonctionne.

**Figure 7 : Réplication de tooVMM VMM**

![Tooon-site local](./media/site-recovery-components/arch-onprem-onprem.png)

### <a name="failover-and-failback"></a>Basculement et restauration automatique

1. Vous pouvez effectuer un [basculement](site-recovery-failover.md) planifié ou non planifié entre des sites locaux. Si vous exécutez un basculement planifié, alors que les machines virtuelles source sont arrêtés tooensure aucune perte de données.
2. Vous pouvez basculer d’un seul ordinateur, ou créer [plans de récupération](site-recovery-create-recovery-plans.md) basculement tooorchestrate de plusieurs ordinateurs.
4. Si vous effectuez un basculement non planifié tooa site secondaire une fois que les machines de basculement hello dans l’emplacement secondaire de hello ne sont pas activés pour la réplication ou de protection. Si vous avez exécuté un basculement planifié, après le basculement de hello, dans l’emplacement secondaire de hello, les ordinateurs sont protégés.
5. Ensuite, vous validez hello basculement toostart accès hello la charge de travail à partir de l’ordinateur virtuel de réplication hello.
6. Lorsque votre site principal est à nouveau disponible, vous lancez tooreplicate la réplication inverse de hello toohello de site secondaire principal. La réplication inverse place les ordinateurs virtuels de hello dans un état protégé, mais hello de centre de données secondaire est toujours un emplacement Directory hello.
7. site principal de hello toomake dans un emplacement Directory hello là encore, vous initiez un basculement planifié à partir de tooprimary secondaire, suivie de la réplication inverse un autre.


## <a name="next-steps"></a>Étapes suivantes

- [En savoir plus](site-recovery-hyper-v-azure-architecture.md) sur les flux de travail de réplication hello Hyper-V.
- [Vérifiez les composants requis](site-recovery-prereq.md)
