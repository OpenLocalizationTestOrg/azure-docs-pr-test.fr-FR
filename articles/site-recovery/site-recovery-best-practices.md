---
title: "meilleures pratiques de récupération de Site aaaAzure | Documents Microsoft"
description: "Cet article décrit les meilleures pratiques pour le déploiement d’Azure Site Recovery"
services: site-recovery
documentationCenter: 
author: rayne-wiselman"
manager: cfreeman
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-support-matrix-to-azure
ms.openlocfilehash: 288df858a0e1c1f5ad96dbe8b9dd0dc69d8f56ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-ready-toodeploy-azure-site-recovery"></a>Obtenir toodeploy prêt Azure Site Recovery

Cet article décrit comment tooprepare pour le déploiement d’Azure Site Recovery.

## <a name="protecting-hyper-v-virtual-machines"></a>Protection des machines virtuelles Hyper-V

Pour protéger les machines virtuelles Hyper-V, vous avez le choix entre deux options de déploiement. Vous pouvez répliquer sur site Hyper-VMs tooAzure ou tooa de centre de données secondaire. Chaque déploiement a ses exigences propres.

**Prérequis** | **Répliquer tooAzure (avec VMM)** | **Répliquer des ordinateurs virtuels Hyper-V tooAzure (sans VMM)** | **Répliquer des ordinateurs virtuels Hyper-V toosecondary site (VMM)** | **Détails**
---|---|---|---|---
**VMM** | VMM exécuté sur System Center 2012 R2 <br/><br/>Au moins un cloud VMM contenant un ou plusieurs groupes d’hôtes VMM. | N/D | Serveurs VMM dans les sites principaux et secondaires hello s’exécutant sur au moins System Center 2012 SP1 avec les dernières mises à jour. <br/><br/> Au moins un cloud sur chaque serveur VMM. Profil de capacité hello Hyper-V des clouds doivent être défini.<br/><br/> cloud de Hello source doit avoir au moins un groupe d’hôtes VMM. | facultatif. Vous n’avez pas besoin toohave que System Center VMM déployé dans l’ordre tooreplicate Hyper-V virtual machines tooAzure, mais si vous le faites, vous devez toomake que le serveur VMM de hello est correctement configuré. Qui inclut de s’assurer que vous exécutez une version VMM hello correcte et que les clouds sont configurés.
**Hyper-V** | Au moins un serveur hôte de Hyper-V dans hello sur site local exécutant Windows Server 2012 R2 ou version ultérieure | Au moins un serveur Hyper-V dans les sites source et cible hello en cours d’exécution au moins Windows Server 2012 avec les dernières mises à jour de hello installé et connecté toohello internet.<br/><br/> serveurs Hyper-V de Hello doivent être dans un groupe hôte dans un cloud VMM. | Au moins un serveur Hyper-V dans les sites source et cible hello en cours d’exécution au moins Windows Server 2012 avec les dernières mises à jour de hello installé et connecté toohello internet.<br/><br/> serveurs Hyper-V de Hello doivent se trouver dans un groupe hôte dans un cloud VMM. |
**Machines virtuelles** | Au moins une machine virtuelle sur le serveur hôte de Hyper-V source hello | Au moins une machine virtuelle sur le serveur hôte de hello Hyper-V dans la source de hello cloud VMM | Au moins une machine virtuelle sur le serveur hôte de hello Hyper-V dans la source de hello cloud VMM. |  Machines virtuelles de réplication tooAzure doivent être conformes à la configuration requise de machine virtuelle Azure
**Compte Azure** | Vous aurez besoin d’un compte Azure et un service de récupération de Site de toohello abonnement. | Vous aurez besoin d’un compte Azure et un service de récupération de Site de toohello abonnement. | N/D | Si vous n’avez pas de compte, commencez avec un essai gratuit.
**Stockage Azure** | Vous aurez besoin d’un abonnement à un compte de stockage Azure pour lequel la géoréplication est activée. | Vous aurez besoin d’un abonnement à un compte de stockage Azure pour lequel la géoréplication est activée. | N/D | Hello compte doit se trouver dans hello même région que le coffre Azure Site Recovery hello et être associé à hello même abonnement.
**Mise en réseau** | Configuration réseau tooensure de mappage que toutes les machines qui basculent sur hello même réseau Azure peut se connecter tooeach autre, quel que soit le plan de récupération auquel elles sont dans. En outre si une passerelle de réseau est configuré sur la cible de hello réseau Azure, les ordinateurs virtuels peuvent se connecter tooother locaux virtuels. Si vous ne définissez pas de réseau mappage uniquement les machines qui basculent Bonjour même plan de récupération peut se connecter. | N/D |  <br/><br/>Configurer tooensure de mappage réseau que les ordinateurs virtuels sont connectés tooappropriate réseaux après le basculement et que les machines virtuelles de réplication sont placées de manière optimale sur les serveurs hôtes Hyper-V. Si vous ne configurez pas réseau mappage machines répliquées ne pourra plus être connecté tooany réseau d’ordinateurs virtuels après le basculement. |  tooset le mappage réseau avec VMM, vous devez toomake que que VMM logique et les réseaux d’ordinateurs virtuels sont configurés correctement.
**Fournisseurs et agents** | Au cours du déploiement, vous allez installer hello fournisseur Azure Site Recovery sur les serveurs VMM. Sur les serveurs Hyper-V dans les clouds VMM, vous allez installer l’agent Azure Recovery Services de hello. | Au cours du déploiement, vous allez installer hello fournisseur Azure Site Recovery et hello Azure Recovery Services agent sur le serveur hôte de Hyper-V hello ou un cluster| Au cours du déploiement, vous allez installer hello fournisseur Azure Site Recovery sur les serveurs VMM. Sur les serveurs Hyper-V dans les clouds VMM, vous allez installer l’agent Azure Recovery Services de hello. | Fournisseurs et agents de se connectent tooSite récupération sur hello internet à l’aide d’une connexion HTTPS chiffrée. Vous ne devez les exceptions de pare-feu tooadd ou créer un proxy spécifique pour la connexion du fournisseur hello.
**Connectivité Internet** | Seuls les serveurs VMM hello besoin d’une connexion internet | Uniquement les serveurs de hôte Hyper-V hello besoin d’une connexion internet | Seuls les serveurs VMM ont besoin d’une connexion Internet | Machines virtuelles n’avez pas besoin tous les composants installés sur ceux-ci et ne pas se connecter directement toohello internet.



## <a name="protect-vmware-virtual-machines-or-physical-servers"></a>Protéger des machines virtuelles VMware ou des serveurs physiques

Pour protéger des machines virtuelles VMware ou des serveurs physiques Windows/Linux, deux options de déploiement s’offrent à vous. Vous pouvez répliquer les tooAzure ou tooa de centre de données secondaire. Chaque déploiement a ses exigences propres.

**Prérequis** | **TooAzure de serveurs VMware répliquer les machines virtuelles/physiques)** | * **Répliquer le site de toosecondary de serveurs de machines virtuelles de VMware/physiques**  
---|---|---
**Site principal** | **Serveur de processus** : serveur Windows dédié (physique ou virtuel) | **Serveur de processus** : serveur Windows dédié (ordinateur physique ou machine virtuelle VMware)<br/><br/>  
**Site local secondaire** | N/D | **Serveur de configuration** : serveur Windows dédié (physique ou virtuel) <br/><br/> **Serveur cible maître** : serveur dédié (physique ou virtuel). Configurer avec des machines Windows tooprotect Windows ou Linux tooprotect Linux.
**Microsoft Azure** | **Abonnement**: vous devez avoir un abonnement pour hello service Site Recovery. <br/><br/> **Compte de stockage** : vous avez besoin d’un compte de stockage pour lequel la géoréplication est appliquée. Hello compte doit se trouver dans hello même région que le coffre Site Recovery hello et être associé à hello même abonnement. <br/><br/> **Serveur de configuration**: vous devez tooset serveur de configuration de hello en tant que d’une machine virtuelle Azure <br/><br/> **Serveur cible maître**: vous devez tooset serveur cible maître de hello comme une machine virtuelle Azure <br/><br/> Configurer avec des machines Windows tooprotect Windows ou Linux tooprotect Linux.<br/><br/> **Réseau virtuel Azure**: vous aurez besoin d’un réseau virtuel Azure sur le hello serveur de configuration et le serveur cible maître seront déployés. Elle doit être hello même abonnement et région que le coffre Azure Site Recovery hello | N/D  
**Machines virtuelles/serveurs physiques** | Au moins une machine virtuelle VMware ou un serveur Windows/Linux physique.<br/><br/>Au cours du déploiement hello service mobilité sera installé sur chaque ordinateur| Au moins une machine virtuelle VMware ou un serveur physique Linux/Windows.<br/><br/> Au cours du déploiement agent unifié de hello est installé sur chaque ordinateur.




## <a name="azure-virtual-machine-requirements"></a>Configuration requise des machines virtuelles Azure

Vous pouvez déployer des machines virtuelles de tooreplicate Site Recovery et des serveurs physiques exécutant n’importe quel système d’exploitation pris en charge par Azure. La plupart des versions de Windows et Linux sont concernées. Vous devez toomake sûr que locale des ordinateurs virtuels que vous souhaitez tooprotect est conforme aux exigences d’Azure.


## <a name="optimizing-your-deployment"></a>Optimisation de votre déploiement

Utilisez hello suivant les conseils toohelp optimiser et de mettre à l’échelle de votre déploiement.

- **Taille de volume de système d’exploitation**: lorsque vous répliquez un Bonjour tooAzure de machine virtuelle fonctionne le volume système doit être inférieure à 1 To. Si vous avez plusieurs volumes que vous pouvez les déplacer manuellement tooa autre disque avant de commencer le déploiement.
- **Taille du disque de données**: Si vous effectuez une réplication tooAzure, vous pouvez utiliser jusqu'à too32 des disques de données sur un ordinateur virtuel, chacun avec un maximum de 1 To. Vous pouvez répliquer et basculer efficacement une machine virtuelle présentant une taille d’environ 32 To.
- **Limites de plan de récupération**: récupération de Site peut évoluer toothousands d’ordinateurs virtuels. Plans de récupération sont conçus en tant que modèle pour les applications qui doivent basculer ensemble afin que nous limiter le nombre de hello d’ordinateurs dans un too50 de plan de récupération.
- **Limites des services Microsoft Azure** : chaque abonnement Microsoft Azure comporte un ensemble de limites par défaut liées aux services principaux, cloud, etc. Nous vous conseillons d’exécuter une test de basculement toovalidate hello la disponibilité des ressources dans votre abonnement. Vous pouvez modifier ces limites via le support Microsoft Azure.
- **Planification de la capacité** : planifiez l’évolutivité et les performances.
- **Bande passante de réplication**: si vous disposez d’une bande passante de réplication insuffisante, notez les points suivants :
    - **ExpressRoute**: Site Recovery s’associe à des optimiseurs Microsoft Azure ExpressRoute et WAN, tels que Riverbed.
    - **Le trafic de réplication**: récupération de Site effectue une réplication initiale active à l’aide des blocs de données et pas hello VHD entier. Seules les modifications sont répliquées au cours de la réplication en continu.
    - **Le trafic réseau**: vous pouvez contrôler le trafic de réseau utilisé pour la réplication en configurant la qualité de service Windows avec une stratégie basée sur le port et adresse IP de destination hello.  En outre, si vous effectuez une réplication tooAzure Site Recovery à l’aide de l’agent de sauvegarde Azure hello. Vous pouvez configurer la limitation de cet agent.
- **RTO**: Si vous souhaitez toomeasure hello temps de récupération (RTO) vous pouvez vous attendre avec Site Recovery nous suggérons vous exécutez un test de basculement et la vue tooanalyze de travaux de récupération de Site hello le temps que prend toocomplete les opérations hello. Si vous avez basculé tooAzure, pourquoi meilleur RTO, nous vous recommandons d’automatiser toutes les actions manuelles en intégrant à la récupération et Azure automation plans.
- **RPO**: récupération de Site prend en charge un objectif de point de récupération proche synchrone (RPO) lorsque vous répliquez tooAzure. Ceci est valable uniquement si vous disposez d’une bande passante suffisante entre votre centre de données et Azure.
