---
title: "aaaHow effectue le travail de tooAzure de réplication de Hyper-V dans Azure Site Recovery ? | Microsoft Docs"
description: "Cet article fournit une vue d’ensemble des composants et architecture utilisée lors de la réplication locale tooAzure d’ordinateurs virtuels Hyper-V avec le service d’Azure Site Recovery hello."
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
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: 3b64156307f37764a8315dec68cf297acf279530
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-hyper-v-replication-tooazure-work-in-site-recovery"></a>Comment tooAzure de réplication Hyper-V fonctionne en mode de récupération de Site ?


Cet article décrit les composants hello et processus impliqués lors de la réplication locale virtuels Hyper-V, tooAzure à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service.

Site Recovery peut répliquer des machines virtuelles Hyper-V locales sur des clusters Hyper-V et hôtes autonomes qui sont gérés avec ou sans System Center Virtual Machine Manager (VMM).

Valider les commentaires en bas de hello de cet article ou Bonjour [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="architectural-components"></a>Composants architecturaux

Un certain nombre de composants sont impliqués lors de la réplication des ordinateurs virtuels Hyper-V tooAzure.

**Composant** | **Emplacement** | **Détails**
--- | --- | ---
**Microsoft Azure** | Dans Azure, vous avez besoin d’un compte Microsoft Azure, d’un compte de stockage Azure et d’un réseau Azure. | Les données répliquées sont stockées dans le compte de stockage hello et machines virtuelles Azure sont créés avec les données de salutation répliquée en cas de basculement à partir de votre site local.<br/><br/> Hello machines virtuelles Azure se connecter toohello réseau virtuel Azure lorsqu’elles sont créées.
**Serveur VMM** | Les hôtes Hyper-V sont situés dans des clouds VMM. | Si les ordinateurs hôtes Hyper-V sont gérées dans des clouds VMM, vous inscrivez serveur VMM de hello dans hello de coffre Recovery Services.<br/><br/> Sur le serveur VMM de hello vous installez hello fournisseur Site Recovery tooorchestrate la réplication avec Azure.<br/><br/> Vous avez besoin de logique et de réseaux d’ordinateurs virtuels tooconfigure le mappage réseau. Un réseau d’ordinateurs virtuels doit être lié tooa réseau logique qui est associé à nuage de hello.
**Hôte Hyper-V** | Les hôtes et clusters Hyper-V peuvent être déployés avec ou sans serveur VMM. | S’il n’existe aucun serveur VMM, hello fournisseur Site Recovery est installé sur la réplication de tooorchestrate hôte hello avec Site Recovery sur hello internet. S’il existe un serveur VMM, hello fournisseur est installé sur ce dernier et non sur l’hôte de hello.<br/><br/> Hello Recovery Services agent est installé sur la réplication des données toohandle hello hôte.<br/><br/> Les communications à partir de hello fournisseur et agent de hello sont sécurisé et chiffré. Les données répliquées dans le stockage Azure sont également chiffrées.
**Machines virtuelles Hyper-V** | Vous devez exécuter une ou plusieurs machines virtuelles sur le serveur hôte Hyper-V. | Aucune opération ne doit tooexplicitly installé sur des machines virtuelles.

En savoir plus sur les conditions préalables au déploiement de hello et la configuration requise pour chacun de ces composants Bonjour [matrice de prise en charge](site-recovery-support-matrix-to-azure.md).

**Figure 1 : Réplication de tooAzure de site Hyper-V**

![Composants](./media/site-recovery-components/arch-onprem-azure-hypervsite.png)

**Figure 2 : La réplication tooAzure des clouds Hyper-V dans VMM**

![Composants](./media/site-recovery-components/arch-onprem-onprem-azure-vmm.png)


## <a name="replication-process"></a>Processus de réplication

**Figure 3 : Les processus de réplication et la récupération de tooAzure de réplication Hyper-V**

![flux de travail](./media/site-recovery-components/arch-hyperv-azure-workflow.png)

### <a name="enable-protection"></a>Activer la protection

1. Une fois que vous activez la protection d’un ordinateur virtuel Hyper-V, Bonjour portail Azure ou localement, hello **activer la protection** démarre.
2. Hello tâche vérifie que l’ordinateur hello est conforme aux conditions préalables requises, avant d’appeler hello [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx), tooset la réplication avec des paramètres hello que vous avez configuré.
3. travail de Hello démarre la réplication initiale en appelant hello [StartReplication](https://msdn.microsoft.com/library/hh850303.aspx) méthode tooinitialize une réplication complète de la machine virtuelle et tooAzure de disques virtuels envoi hello VM.
4. Vous pouvez surveiller le travail hello Bonjour **travaux** onglet.      ![Liste des travaux](media/site-recovery-hyper-v-azure-architecture/image1.png)![Activer l’exploration de la protection](media/site-recovery-hyper-v-azure-architecture/image2.png)

### <a name="replicate-hello-initial-data"></a>Répliquer les données initiales de hello

1. Un [instantané des machines virtuelles Hyper-V](https://technet.microsoft.com/library/dd560637.aspx) a lieu au moment où la réplication initiale est déclenchée.
2. Disques durs virtuels sont répliquées un par un jusqu'à ce qu’ils sont tous les tooAzure copié. Il peut prendre un certain temps, en fonction de hello taille de machine virtuelle et la bande passante réseau. toooptimize l’utilisation du réseau, consultez [comment toomanage local tooAzure protection de bande passante](https://support.microsoft.com/kb/3056159).
3. Si les modifications du disque se produisent alors que la réplication initiale est en cours d’exécution, hello suivi de réplication réplica Hyper-V effectue le suivi de ces modifications en tant que les journaux de réplication Hyper-V (.hrl). Ces fichiers se trouvent dans hello même dossier que les disques hello. Chaque disque est un fichier .hrl associé qui sera envoyé toosecondary stockage.
4. Hello instantané et les fichiers journaux consomment des ressources de disque pendant la réplication initiale est en cours d’exécution.
5. Une fois la réplication initiale hello, instantané d’ordinateur virtuel hello est supprimé. Les modifications delta de disque dans le journal de hello sont disque parent de toohello synchronisé et fusionné.


### <a name="finalize-protection"></a>Finalisation de la protection

1. Après la réplication initiale hello, hello **finaliser la protection sur l’ordinateur virtuel de hello** tâche configure les paramètres réseau et autres après la réplication, afin que l’ordinateur virtuel de hello est protégé.
    ![Finaliser le travail de protection](media/site-recovery-hyper-v-azure-architecture/image3.png)
2. Si vous effectuez une réplication tooAzure, vous devrez peut-être les paramètres hello tootweak pour la machine virtuelle de hello afin qu’il soit prêt pour le basculement. À ce stade, vous pouvez exécuter un toocheck de basculement de test que tout fonctionne comme prévu.

### <a name="replicate-hello-delta"></a>Répliquer le delta de hello

1. Après la réplication initiale de hello, synchronisation delta commence, conformément aux paramètres de réplication.
2. Hello suivi de réplication Hyper-V réplica suit hello modifications tooa un disque dur virtuel en tant que fichiers de .hrl. Chaque disque configuré pour la réplication est associé à un fichier .hrl. Ce journal est envoyé toohello du compte de stockage après que la réplication initiale est terminée. Lorsqu’un journal est en transit tooAzure, les modifications apportées aux hello disque principal de hello sont suivies dans un autre fichier journal, Bonjour même répertoire.
3. Lors de la réplication initiale et delta, vous pouvez surveiller hello VM Bonjour vue de la machine virtuelle. [En savoir plus](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines).  

### <a name="synchronize-replication"></a>Synchroniser la réplication

1. Si la réplication différentielle échoue et si une réplication complète est exclue (car elle monopoliserait trop de bande passante ou prendrait trop de temps), une resynchronisation se produit au niveau d’une machine virtuelle. Par exemple, si les fichiers .hrl hello atteint 50 % de la taille du disque hello, puis hello machine virtuelle est marquée pour la resynchronisation.
2.  La resynchronisation de hello minimise de données envoyées par le calcul de sommes de contrôle de hello source et cible les ordinateurs virtuels et de renvoyer uniquement les données delta hello. La resynchronisation utilise un algorithme de segmentation de bloc fixe, dans lequel les fichiers source et cible sont divisés en segments fixes. Les sommes de contrôle pour chaque segment sont générés et toodetermine qui bloque hello source besoin toobe toohello appliqué cible doit être comparée.
3. Une fois la resynchronisation terminée, la réplication différentielle normale doit reprendre. Par défaut, la resynchronisation est planifiée toorun automatiquement en dehors des heures de bureau, mais vous pouvez resynchroniser manuellement un ordinateur virtuel. Par exemple, la resynchronisation peut reprendre en cas d’interruption du réseau ou autre panne. toodo cette option, sélectionnez hello machine virtuelle dans le portail de hello > **resynchroniser**.

    ![Resynchronisation manuelle](media/site-recovery-hyper-v-azure-architecture/image4.png)


### <a name="retry-logic"></a>Logique de nouvelle tentative

Si une erreur de réplication se produit, une nouvelle tentative intégrée est effectuée. Elle s’articule autour de deux catégories :

**Catégorie** | **Détails**
--- | ---
**Erreurs non récupérables** | Aucune nouvelle tentative n’est effectuée. L’état de la machine virtuelle est affiché comme **Critique** et l’intervention de l’administrateur est requise. Exemples de ces erreurs : rompu la chaîne du disque dur virtuel ; État non valide pour le réplica hello machine virtuelle ; Des erreurs d’authentification réseau : erreurs d’autorisation ; Machine virtuelle non trouvé des erreurs (pour les serveurs autonomes Hyper-V)
**Erreurs récupérables** | Nouvelles tentatives produisent à chaque intervalle de réplication, à l’aide une interruption exponentielle qui augmente l’intervalle avant nouvelle tentative de hello du début hello de la première tentative de hello par 1, 2, 4, 8 et 10 minutes. Si une erreur persiste, effectuez une nouvelle tentative toutes les 30 minutes. Voici quelques exemples : erreur réseau, erreur espace disque faible, conditions de mémoire insuffisante |



## <a name="failover-and-failback-process"></a>Processus de basculement et de restauration automatique

1. Vous pouvez exécuter planifié ou non planifié [basculement](site-recovery-failover.md) de tooAzure d’ordinateurs virtuels Hyper-V local. Si vous exécutez un basculement planifié, alors que les machines virtuelles source sont arrêtés tooensure aucune perte de données.
2. Vous pouvez basculer d’un seul ordinateur, ou créer [plans de récupération](site-recovery-create-recovery-plans.md) basculement tooorchestrate de plusieurs ordinateurs.
4. Après avoir exécuté hello basculement, vous devez être hello toosee en mesure de création de machines virtuelles de réplica dans Azure. Vous pouvez affecter un toohello d’adresse IP publique machine virtuelle si nécessaire.
5. Ensuite, vous validez toostart de basculement hello l’accès à la charge de travail hello du réplica de hello machine virtuelle Azure.
6. Lorsque votre site local principal est à nouveau disponible, vous pouvez lancer la [restauration automatique](site-recovery-failback-from-azure-to-hyper-v.md). Vous démarrez un basculement planifié à partir du site principal de toohello Azure. Pour un basculement planifié, que vous pouvez sélectionnez toofailback toohello même machine virtuelle ou tooan autre emplacement et de synchroniser change entre Azure et locaux, tooensure sans perte de données. Lorsque les ordinateurs virtuels sont créés localement, vous validez hello basculement.




## <a name="next-steps"></a>Étapes suivantes

Hello de révision [matrice de prise en charge](site-recovery-support-matrix-to-azure.md)
