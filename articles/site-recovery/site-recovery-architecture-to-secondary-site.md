---
title: "aaaHow fonctionne localement machine réplication tooa secondaire local site dans Azure Site Recovery ? | Microsoft Docs"
description: "Cet article fournit une vue d’ensemble des composants et architecture utilisée lors de la réplication locale machines virtuelles et des serveurs physiques tooa le site secondaire ayant hello service Azure Site Recovery."
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
ms.openlocfilehash: 097a3f43446fec69ed7f9e0b7f11e8d11f41cc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-on-premises-machine-replication-tooa-secondary-site-work-in-site-recovery"></a>Comment local machine travail de site secondaire tooa de réplication en cours de récupération de Site ?

Cet article décrit les composants hello et processus impliqués lors de la réplication locale des ordinateurs virtuels et tooAzure des serveurs physiques, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service.

Vous pouvez répliquer hello tooa secondaire local site suivant :
- Machines virtuelles Hyper-V locales, sur clusters Hyper-V et hôtes autonomes qui sont gérés dans des clouds System Center Virtual Machine Manager (VMM).
- Machines virtuelles VMware locales et serveurs physiques Windows/Linux. Dans ce scénario, la réplication est gérée par Scout.

Valider les commentaires en bas de hello de cet article ou Bonjour [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="replicate-hyper-v-vms-tooa-secondary-on-premises-site"></a>Répliquer des ordinateurs virtuels Hyper-V tooa secondaire sur-site local


### <a name="architectural-components"></a>Composants architecturaux

Voici ce que vous avez besoin pour la réplication de site secondaire de tooa des ordinateurs virtuels Hyper-V.

**Composant** | **Emplacement** | **Détails**
--- | --- | ---
**Microsoft Azure** | Vous avez besoin d’un compte Microsoft. |
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

**Figure 1 : Réplication de tooVMM VMM**

![Tooon-site local](./media/site-recovery-components/arch-onprem-onprem.png)

### <a name="failover-and-failback-process"></a>Processus de basculement et de restauration automatique

1. Vous pouvez effectuer un [basculement](site-recovery-failover.md) planifié ou non planifié entre des sites locaux. Si vous exécutez un basculement planifié, alors que les machines virtuelles source sont arrêtés tooensure aucune perte de données.
2. Vous pouvez basculer d’un seul ordinateur, ou créer [plans de récupération](site-recovery-create-recovery-plans.md) basculement tooorchestrate de plusieurs ordinateurs.
4. Si vous effectuez un basculement non planifié tooa site secondaire une fois que les machines de basculement hello dans l’emplacement secondaire de hello ne sont pas activés pour la réplication ou de protection. Si vous avez exécuté un basculement planifié, après le basculement de hello, dans l’emplacement secondaire de hello, les ordinateurs sont protégés.
5. Ensuite, vous validez hello basculement toostart accès hello la charge de travail à partir de l’ordinateur virtuel de réplication hello.
6. Lorsque votre site principal est à nouveau disponible, vous lancez tooreplicate la réplication inverse de hello toohello de site secondaire principal. La réplication inverse place les ordinateurs virtuels de hello dans un état protégé, mais hello de centre de données secondaire est toujours un emplacement Directory hello.
7. site principal de hello toomake dans un emplacement Directory hello là encore, vous initiez un basculement planifié à partir de tooprimary secondaire, suivie de la réplication inverse un autre.




## <a name="replicate-vmware-vmsphysical-servers-tooa-secondary-site"></a>Répliquer le site secondaire de machines virtuelles de VMware/physiques serveurs tooa

Vous pouvez répliquer des ordinateurs virtuels VMware ou serveurs physiques tooa secondaire à l’aide de InMage Scout, à l’aide de ces composants architecturaux :


### <a name="architectural-components"></a>Composants architecturaux

**Composant** | **Emplacement** | **Détails**
--- | --- | ---
**Microsoft Azure** | InMage Scout. | tooobtain InMage Scout, vous avez besoin d’un abonnement Azure.<br/><br/> Après avoir créé un coffre Recovery Services, vous téléchargez InMage Scout et installez hello dernières mises à jour tooset le déploiement de hello.
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

**Figure 2 : VMware tooVMware réplication**

![VMware tooVMware](./media/site-recovery-components/vmware-to-vmware.png)


## <a name="next-steps"></a>Étapes suivantes

Hello de révision [matrice de prise en charge](site-recovery-support-matrix-to-sec-site.md)
