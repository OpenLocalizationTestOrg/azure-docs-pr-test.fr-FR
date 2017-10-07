---
title: "aaaHow effectue le travail de tooAzure de réplication de Hyper-V dans la récupération de Site ? | Microsoft Docs"
description: "Cet article fournit une vue d’ensemble du fonctionnement de la réplication Hyper-V dans Azure Site Recovery."
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
redirect_url: site-recovery-architecture-hyper-v-to-azure
ms.openlocfilehash: e982806b4d6cdec2f71f82d8c73c17cc50ad3c33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-hyper-v-replication-tooazure-work"></a>Comment fonctionne le tooAzure de réplication Hyper-V ?

Lire cette architecture de l’article toounderstand hello et le flux de travail pour tooAzure de réplication Hyper-V à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service.

Valider les commentaires en bas de hello de cet article ou Bonjour [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Vous pouvez répliquer hello suivant tooAzure :
- **Hyper-V avec VMM** : machines virtuelles situées sur les hôtes Hyper-V locaux gérés dans des clouds System Center Virtual Machine Manager (VMM). Les hôtes peuvent exécuter tout type de [système d’exploitation pris en charge](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers). Vous pouvez répliquer des machines virtuelles Hyper-V exécutant un système d’exploitation invité [pris en charge par Hyper-V et Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).
- **Hyper-V sans VMM** : machines virtuelles locales situées sur des hôtes Hyper-V qui ne sont pas gérés dans des clouds VMM. Les hôtes peuvent exécuter des hello [les systèmes d’exploitation pris en charge](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions). Vous pouvez répliquer des machines virtuelles Hyper-V exécutant un système d’exploitation invité [pris en charge par Hyper-V et Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).


## <a name="architectural-components"></a>Composants architecturaux

**Zone** | **Composant** | **Détails**
--- | --- | ---
**Microsoft Azure** | Dans Azure, vous avez besoin d’un compte Microsoft Azure, d’un compte de stockage Azure et d’un réseau Azure. | Le stockage et le réseau peuvent être des comptes Resource Manager ou Classic.<br/><br/> Les données répliquées sont stockées dans le compte de stockage hello et machines virtuelles Azure sont créés avec les données de salutation répliquée en cas de basculement à partir de votre site local.<br/><br/> Hello machines virtuelles Azure se connecter toohello réseau virtuel Azure lorsqu’elles sont créées.
**Serveur VMM** | Hôtes Hyper-V situés dans des clouds VMM | Si les ordinateurs hôtes Hyper-V sont gérées dans des clouds VMM, vous inscrivez serveur VMM de hello dans hello de coffre Recovery Services.<br/><br/> Sur le serveur VMM de hello vous installez hello fournisseur Site Recovery tooorchestrate la réplication avec Azure.<br/><br/> Vous avez besoin de logique et de réseaux d’ordinateurs virtuels tooconfigure le mappage réseau. Un réseau d’ordinateurs virtuels doit être lié tooa réseau logique qui est associé à nuage de hello.
**Hôte Hyper-V** | Les serveurs Hyper-V peuvent être déployés avec ou sans serveur VMM. | S’il n’existe aucun serveur VMM, hello fournisseur Site Recovery est installé sur la réplication de tooorchestrate hôte hello avec Site Recovery sur hello internet. S’il existe un serveur VMM, hello fournisseur est installé sur ce dernier et non sur l’hôte de hello.<br/><br/> Hello Recovery Services agent est installé sur la réplication des données toohandle hello hôte.<br/><br/> Les communications à partir de hello fournisseur et agent de hello sont sécurisé et chiffré. Les données répliquées dans le stockage Azure sont également chiffrées.
**Machines virtuelles Hyper-V** | Vous avez besoin d’un ou plusieurs des ordinateurs virtuels sur le serveur hôte de Hyper-V hello. | Aucune opération ne doit tooexplicitly installé sur des machines virtuelles

## <a name="deployment-steps"></a>Étapes du déploiement

1. **Azure**: configurer hello composants Azure. Nous vous recommandons de configurer les comptes de stockage et de réseau avant de lancer le déploiement de Site Recovery.
2. **Coffre** : vous créez un coffre Recovery Services pour Site Recovery et vous configurez les paramètres du coffre, y compris les paramètres sources et cibles, la définition d’une stratégie de réplication et l’activation de la réplication.
3. **Source et cible** :
    - **Les hôtes Hyper-V dans les clouds VMM**: dans le cadre de la spécification des paramètres de la source, vous télécharger et installer hello fournisseur Azure Site Recovery sur le serveur VMM de hello et l’agent Azure Recovery Services de hello sur chaque ordinateur hôte Hyper-V. source de Hello sera le serveur VMM de hello. cible de Hello est Azure.
    - Les hôtes Hyper-V sans VMM : lorsque vous spécifiez des paramètres de la source, vous téléchargez et installez hello fournisseur et l’agent sur chaque ordinateur hôte Hyper-V. Durant le déploiement vous regroupez les hôtes de hello dans un site Hyper-V et spécifiez ce site en tant que source de hello. cible de Hello est Azure.

    ![La réplication Hyper-V/VMM tooAzure](./media/site-recovery-components/arch-onprem-onprem-azure-vmm.png) ![tooAzure de réplication de site Hyper-V](./media/site-recovery-components/arch-onprem-azure-hypervsite.png)


4. **Stratégie de réplication**: vous créez une stratégie de réplication pour le site de hello Hyper-V ou un cloud VMM. stratégie de Hello est machines virtuelles de tooall appliquée situées sur des ordinateurs hôtes dans le cloud ou le site de hello.
5. **Activer la réplication** : vous activez la réplication pour les machines virtuelles Hyper-V. La réplication initiale se produit conformément aux paramètres de stratégie de réplication hello. Suivi des modifications de données et la réplication de delta modifications tooAzure commence une fois la réplication initiale hello terminée. Les modifications qui font l’objet d’un suivi sont conservées dans un fichier .hrl.
6. **Test de basculement**: vous exécutez un toomake de basculement de test que tout fonctionne comme prévu.

Pour en savoir plus sur le déploiement :
- [Prise en main tooAzure de réplication de machine virtuelle Hyper-V - avec VMM](site-recovery-vmm-to-azure.md)
- [Prise en main tooAzure de réplication de machine virtuelle Hyper-V - sans VMM](site-recovery-hyper-v-site-to-azure.md)

## <a name="hyper-v-replication-workflow"></a>Flux de travail de réplication Hyper-V

### <a name="enable-protection"></a>Activer la protection

1. Une fois que vous activez la protection d’un ordinateur virtuel Hyper-V, Bonjour portail Azure ou localement, hello **activer la protection** démarre.
2. Hello tâche vérifie que l’ordinateur hello est conforme aux conditions préalables requises, avant d’appeler hello [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx), tooset la réplication avec des paramètres hello que vous avez configuré.
3. travail de Hello démarre la réplication initiale en appelant hello [StartReplication](https://msdn.microsoft.com/library/hh850303.aspx) méthode tooinitialize une réplication complète de la machine virtuelle et tooAzure de disques virtuels envoi hello VM.
4. Vous pouvez surveiller le travail hello Bonjour **travaux** onglet.      ![Liste des travaux](media/site-recovery-hyper-v-azure-architecture/image1.png)![Activer l’exploration de la protection](media/site-recovery-hyper-v-azure-architecture/image2.png)

### <a name="initial-replication"></a>Réplication initiale

1. Un [instantané des machines virtuelles Hyper-V](https://technet.microsoft.com/library/dd560637.aspx) a lieu au moment où la réplication initiale est déclenchée.
2. Disques durs virtuels sont répliquées un par un jusqu'à ce qu’ils sont tous les tooAzure copié. Il peut prendre un certain temps, en fonction de hello taille de machine virtuelle et la bande passante réseau. toooptimize l’utilisation du réseau, consultez [comment toomanage local tooAzure protection de bande passante](https://support.microsoft.com/kb/3056159).
3. Si les modifications du disque se produisent alors que la réplication initiale est en cours d’exécution, hello suivi de réplication réplica Hyper-V effectue le suivi de ces modifications en tant que les journaux de réplication Hyper-V (.hrl). Ces fichiers se trouvent dans hello même dossier que les disques hello. Chaque disque est un fichier .hrl associé qui sera envoyé toosecondary stockage.
4. Hello instantané et les fichiers journaux consomment des ressources de disque pendant la réplication initiale est en cours d’exécution.
5. Une fois la réplication initiale hello, instantané d’ordinateur virtuel hello est supprimé. Les modifications delta de disque dans le journal de hello sont disque parent de toohello synchronisé et fusionné.


### <a name="finalize-protection"></a>Finalisation de la protection

1. Après la réplication initiale hello, hello **finaliser la protection sur l’ordinateur virtuel de hello** tâche configure les paramètres réseau et autres après la réplication, afin que l’ordinateur virtuel de hello est protégé.
    ![Finaliser le travail de protection](media/site-recovery-hyper-v-azure-architecture/image3.png)
2. Si vous effectuez une réplication tooAzure, vous devrez peut-être les paramètres hello tootweak pour la machine virtuelle de hello afin qu’il soit prêt pour le basculement. À ce stade, vous pouvez exécuter un toocheck de basculement de test que tout fonctionne comme prévu.

### <a name="delta-replication"></a>Réplication différentielle

1. Après la réplication initiale de hello, synchronisation delta commence, conformément aux paramètres de réplication.
2. Hello suivi de réplication Hyper-V réplica suit hello modifications tooa un disque dur virtuel en tant que fichiers de .hrl. Chaque disque configuré pour la réplication est associé à un fichier .hrl. Ce journal est envoyé toohello du compte de stockage après que la réplication initiale est terminée. Lorsqu’un journal est en transit tooAzure, les modifications apportées aux hello disque principal de hello sont suivies dans un autre fichier journal, Bonjour même répertoire.
3. Lors de la réplication initiale et delta, vous pouvez surveiller hello VM Bonjour vue de la machine virtuelle. [En savoir plus](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines).  

### <a name="replication-synchronization"></a>Synchronisation de réplication

1. Si la réplication différentielle échoue et si une réplication complète est exclue (car elle monopoliserait trop de bande passante ou prendrait trop de temps), une resynchronisation se produit au niveau d’une machine virtuelle. Par exemple, si les fichiers .hrl hello atteint 50 % de la taille du disque hello, puis hello machine virtuelle est marquée pour la resynchronisation.
2.  La resynchronisation de hello minimise de données envoyées par le calcul de sommes de contrôle de hello source et cible les ordinateurs virtuels et de renvoyer uniquement les données delta hello. La resynchronisation utilise un algorithme de segmentation de bloc fixe, dans lequel les fichiers source et cible sont divisés en segments fixes. Les sommes de contrôle pour chaque segment sont générés et toodetermine qui bloque hello source besoin toobe toohello appliqué cible doit être comparée.
3. Une fois la resynchronisation terminée, la réplication différentielle normale doit reprendre. Par défaut, la resynchronisation est planifiée toorun automatiquement en dehors des heures de bureau, mais vous pouvez resynchroniser manuellement un ordinateur virtuel. Par exemple, la resynchronisation peut reprendre en cas d’interruption du réseau ou autre panne. toodo cette option, sélectionnez hello machine virtuelle dans le portail de hello > **resynchroniser**.

    ![Resynchronisation manuelle](media/site-recovery-hyper-v-azure-architecture/image4.png)


### <a name="retries"></a>Nouvelle tentatives

Si une erreur de réplication se produit, une nouvelle tentative intégrée est effectuée. Elle s’articule autour de deux catégories :

**Catégorie** | **Détails**
--- | ---
**Erreurs non récupérables** | Aucune nouvelle tentative n’est effectuée. L’état de la machine virtuelle est affiché comme **Critique** et l’intervention de l’administrateur est requise. Exemples de ces erreurs : rompu la chaîne du disque dur virtuel ; État non valide pour le réplica hello machine virtuelle ; Des erreurs d’authentification réseau : erreurs d’autorisation ; Machine virtuelle non trouvé des erreurs (pour les serveurs autonomes Hyper-V)
**Erreurs récupérables** | Nouvelles tentatives produisent à chaque intervalle de réplication, à l’aide une interruption exponentielle qui augmente l’intervalle avant nouvelle tentative de hello du début hello de la première tentative de hello par 1, 2, 4, 8 et 10 minutes. Si une erreur persiste, effectuez une nouvelle tentative toutes les 30 minutes. Voici quelques exemples : erreur réseau, erreur espace disque faible, conditions de mémoire insuffisante |

## <a name="protection-and-recovery-lifecycle"></a>Cycle de vie de protection et de récupération

![flux de travail](./media/site-recovery-components/arch-hyperv-azure-workflow.png)

## <a name="next-steps"></a>Étapes suivantes

- [Vérification des conditions préalables au déploiement](site-recovery-prereq.md)
- Résolution des problèmes avec :
    - [Surveiller et dépanner la protection](site-recovery-monitoring-and-troubleshooting.md)
    - [Aide du support Microsoft](site-recovery-monitoring-and-troubleshooting.md#reach-out-for-microsoft-support)
    - [Problèmes courants et leur résolution](site-recovery-monitoring-and-troubleshooting.md#common-azure-site-recovery-errors-and-their-resolutions)
