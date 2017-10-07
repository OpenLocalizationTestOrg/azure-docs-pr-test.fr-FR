---
title: "Répliquer les machines virtuelles Azure entre les régions Azure pour la récupération d’urgence doit : tooAzure Azure | Documents Microsoft"
description: "Résume les étapes hello vous avez besoin de machines virtuelles Azure de tooreplicate entre les régions Azure (Azure pour Azure) avec le service d’Azure Site Recovery hello pour les besoins de récupération d’urgence."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: raynew
ms.openlocfilehash: c4c425af260a9bcc3dd4dcc13da26109e20f03bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a>Répliquer des machines virtuelles Azure entre des régions avec Azure Site Recovery

>[!NOTE]
>
> La réplication Azure Site Recovery pour les machines virtuelles Azure est actuellement en préversion.

Cet article décrit comment tooreplicate machines virtuelles Azure entre des régions Azure à l’aide de hello [Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.

Ajouter des commentaires et questions bas hello de cet article ou sur hello [forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="disaster-recovery-in-azure"></a>Récupération d’urgence dans Azure

Fonctionnalités et fonctions d’infrastructure Azure intégrée contribuent tooa stratégie de disponibilité solide et fiable pour les charges de travail qui s’exécutent sur des machines virtuelles Azure. Toutefois, il existe de nombreuses raisons pour lesquelles vous devez tooplan pour la récupération d’urgence entre les régions Azure vous-même :

- Vous avez besoin en matière de conformité toomeet pour des applications spécifiques et les charges de travail qui nécessitent une continuité des activités et la stratégie de récupération d’urgence.
- Hello capacité tooprotect et de récupérer les machines virtuelles de Azure en fonction de vos décisions professionnelles et pas uniquement basée sur la fonctionnalité Azure intégrée.
- Vous devez tootest basculement et récupération conformément à vos besoins commerciaux et de conformité, sans aucun impact sur la production.
- Vous devez toofail de région de récupération toohello dans les cas de hello d’urgence et que vous échouer de région de la source d’origine toohello arrière en toute transparence.

Utilisez la récupération de Site pour la machine virtuelle Azure à Azure réplication toohelp vous effectuer toutes ces tâches.


## <a name="why-use-site-recovery"></a>Pourquoi utiliser Azure Site Recovery ?      

Récupération de site fournit un moyen simple de tooreplicate machines virtuelles Azure entre les régions :

- **Déploiement automatique**. Contrairement à un modèle de réplication d’actif-actif, il est inutile d’une infrastructure coûteuse et complexe dans la région secondaire hello. Lorsque vous activez la réplication, Site Recovery crée automatiquement les ressources de hello requis dans la région cible hello, selon les paramètres de région de code source.
- **Contrôle des régions**. Site Recovery, vous pouvez répliquer à partir de n’importe quelle région tooany de région sur un continent. Comparez ceci au stockage géoredondant avec accès en lecture, qui réplique uniquement de façon asynchrone entre des [régions jumelées](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) standard. Un stockage géo-redondant avec accès en lecture fournit des données de toohello d’accès en lecture seule dans la région cible hello.
- **Réplication automatisée**. Site Recovery fournit une réplication continue automatisée. Le basculement et la restauration automatique peuvent être déclenchés en un seul clic.
- **RTO et RPO**. Récupération de site tire parti de l’infrastructure réseau Azure hello se connecte régions tookeep RTO et le RPO très faible.
- **Test**. Vous pouvez exécuter des exercices de récupération d’urgence avec des tests de basculement à la demande en fonction de vos besoins, sans affecter vos charges de travail de production ou la réplication continue.
- **Plans de récupération**. Vous pouvez utiliser le basculement de tooorchestrate de plans de récupération et de restauration de hello ensemble de l’application en cours d’exécution sur plusieurs machines virtuelles. fonctionnalité de plan de récupération Hello a riche integration de première classe aux runbooks Azure automation.


## <a name="deployment-summary"></a>Résumé du déploiement

Voici un résumé de ce que vous devez tooset toodo la réplication des machines virtuelles entre les régions Azure :

1. Créez un coffre Recovery Services. coffre de Hello contient les paramètres de configuration et orchestre la réplication.
2. Activer la réplication pour hello machines virtuelles Azure.
3. Exécutez toomake d’un basculement test assurer que tout fonctionne comme prévu.

>[!IMPORTANT]
>
> Vous pouvez vérifier hello [matrice de prise en charge pour la réplication de la machine virtuelle Azure](./site-recovery-support-matrix-azure-to-azure.md).

>[!IMPORTANT]
>
> Pour plus d’informations sur comment tooconfigure hello requis connectivité sortante du réseau de machines virtuelles Azure pour la réplication de Site Recovery, consultez hello [document du Guide de mise en réseau](./site-recovery-azure-to-azure-networking-guidance.md).

### <a name="before-you-start"></a>Avant de commencer

* Votre compte d’utilisateur Azure doit toohave certaines [autorisations](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la réplication d’une machine virtuelle Azure.
* Votre abonnement Azure doit être VMs toocreate activée dans l’emplacement cible de hello que vous souhaitez toouse comme région de récupération d’urgence hello. Contactez le support technique tooenable hello quota requis.

## <a name="create-a-recovery-services-vault"></a>Créer un coffre Recovery Services

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> Nous vous recommandons de créer le coffre Recovery Services hello dans hello emplacement où votre tooreplicate de machines virtuelles. Par exemple, si votre emplacement cible est hello central US, créer dans le coffre hello **du centre des États-Unis**.

## <a name="enable-replication"></a>Activer la réplication

Dans **les coffres de Services de récupération**, cliquez sur le nom du coffre hello. Dans le coffre de hello, cliquez sur hello **+ répliquer** bouton.

### <a name="step-1-configure-hello-source"></a>Étape 1. Configurer la source de hello
1. Dans **Source**, sélectionnez **Azure - PREVIEW**.
2. Dans **emplacement Source**, sélectionnez la source de hello région Azure où vos machines virtuelles en cours d’exécution.
3. Modèle de déploiement sélectionnez hello de vos machines virtuelles : **le Gestionnaire de ressources** ou **classique**.
4. Sélectionnez hello **groupe de ressources Source** pour les machines virtuelles du Gestionnaire de ressources ou **service de cloud computing** pour les machines virtuelles classiques.

    ![Configurer la source de hello](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a>Étape 2. Sélectionner les machines virtuelles

* Sélectionnez les machines virtuelles de hello vous souhaitez tooreplicate, puis cliquez sur **OK**.

    ![Sélectionner les machines virtuelles](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a>Étape 3. Configurer les paramètres

1. par défaut de toooverride hello cibler des paramètres et spécifiez les paramètres de hello de votre choix, cliquez sur **personnaliser**. Pour plus d’informations, consultez [Personnaliser les ressources cibles](site-recovery-replicate-azure-to-azure.md##customize-target-resources).

    ![Configurer les paramètres](./media/site-recovery-azure-to-azure/settings.png)


2. Par défaut, Site Recovery crée une stratégie de réplication qui effectue des captures instantanées de cohérence des applications toutes les quatre heures et conserve les points de récupération pendant 24 heures. toocreate une stratégie avec des paramètres différents, cliquez sur **personnaliser** suivant trop**stratégie de réplication**.

    ![Personnaliser la stratégie](./media/site-recovery-azure-to-azure/customize-policy.png)

3. toostart configurer hello cible les ressources, cliquez sur **créer des ressources de la cible**. L’approvisionnement prend environ une minute. Ne fermez pas les lames hello lors de la configuration, ou vous devez toostart sur.

4. réplication tootrigger Hello sélectionné la machine virtuelle, cliquez sur **activer la réplication**.

5. Vous pouvez suivre la progression de hello **activer la protection** de la tâche dans **paramètres** > **travaux** > **tâches de récupération de Site**.

6. Dans **paramètres** > **répliquées des éléments**, vous pouvez afficher l’état de hello de machines virtuelles et hello la progression de la réplication initiale. Cliquez sur hello VM toodrill vers le bas dans ses paramètres.

## <a name="run-a-test-failover"></a>Exécution d’un test de basculement

Une fois que vous avez tout configuré, exécutez un toomake de basculement de test que tout fonctionne comme prévu :

1. toofail sur un seul ordinateur, dans **paramètres** > **répliquées des éléments**, cliquez sur la machine virtuelle de hello **+ Test de basculement** icône.

2. toofail sur la récupération d’un plan, en **paramètres** > **les Plans de récupération**, plan de hello avec le bouton **Test de basculement**. toocreate un plan de récupération, [suivez ces instructions](site-recovery-create-recovery-plans.md). 

3. Dans **Test de basculement**, sélectionnez toowhich de réseau virtuel Azure cible hello machines virtuelles Azure sont connectés après basculement hello.

4. toostart hello de basculement, cliquez sur **OK**. tootrack de progression, cliquez sur hello VM tooopen ses propriétés. Vous pouvez également cliquer sur hello **Test de basculement** travail dans le nom du coffre hello > **paramètres** > **travaux** > **les tâches de récupération de Site**.

5. Après avoir hello basculement se termine, le réplica de hello machine Azure s’affiche dans hello portail Azure > **virtuels**. Assurez-vous que cette machine virtuelle hello est la taille appropriée de hello, que sa connexion réseau approprié de toohello, et qu’il s’exécute.

6. toodelete hello machines virtuelles qui ont été créés pendant le basculement de test hello, cliquez sur **basculement de test de nettoyage** sur hello répliquées élément hello ou un plan de récupération. Dans **Notes**, enregistrer et enregistrer toutes les observations associées au basculement de test hello. 

Pour plus d’informations sur les tests de basculement, cliquez [ici](site-recovery-test-failover-to-azure.md).


## <a name="next-steps"></a>Étapes suivantes

Après avoir tester le déploiement de hello :

- [En savoir plus](site-recovery-failover.md) sur différents types de basculement et la manière dont toorun les.
- En savoir plus sur [à l’aide de plans de récupération](site-recovery-create-recovery-plans.md) tooreduce RTO.
