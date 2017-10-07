---
title: "la réplication de machines virtuelles Azure tooanother région Azure avec Azure Site Recovery aaaEnable | Documents Microsoft"
description: "Résume les étapes hello vous devez tooenable réplication tooanother région Azure pour les machines virtuelles Azure, à l’aide du service d’Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a309644f-d36b-4188-bba7-ad45a2d9bede
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 8/01/2017
ms.author: raynew
ms.openlocfilehash: 2fa03db45a18ccb8b9f31ed05589be0dd6d5f031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-enable-replication-for-azure-vms"></a>Étape 5 : Activer la réplication des machines virtuelles Azure


Après avoir configuré un [de coffre Recovery Services](azure-to-azure-walkthrough-vault.md), utilisez cette réplication tooenable de l’article de machines virtuelles (VM), tooanother région Azure, avec [Azure Site Recovery](site-recovery-overview.md). tooenable la réplication, vous avez configuré les paramètres source et cible, vérifiez la stratégie de réplication hello et sélectionnez les machines virtuelles que vous souhaitez tooreplicate.

- Lorsque vous avez terminé l’article hello, vos machines virtuelles Azure doit être réplication toohello de région Azure secondaire.
- Valider les commentaires en bas de hello de cet article, ou poser des questions dans hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

>[!NOTE]
>
> La réplication de machines virtuelles Azure est actuellement disponible en préversion.


## <a name="select-hello-source"></a>Sélectionnez la source de hello 

1. Dans les coffres des Services de récupération, cliquez sur le nom du coffre hello > **+ répliquer**.
2. Dans **Source**, sélectionnez **Azure - PREVIEW**.
2. Dans **emplacement Source**, sélectionnez la source de hello région Azure où vos machines virtuelles en cours d’exécution.
3. Sélectionnez hello **modèle de déploiement de machine virtuelle Azure** pour les ordinateurs virtuels : **le Gestionnaire de ressources** ou **classique**.
4. Sélectionnez hello **groupe de ressources Source** pour les machines virtuelles du Gestionnaire de ressources, ou **service de cloud computing** pour les machines virtuelles classiques.
5. Cliquez sur **OK** toosave les paramètres hello.

    ![Configurer la source de hello](./media/azure-to-azure-walkthrough-enable-replication/source.png)

## <a name="select-hello-vms"></a>Sélectionnez les ordinateurs virtuels de hello

Site Recovery récupère une liste de hello que machines virtuelles associées à l’abonnement de hello et ressource groupe/service cloud.

1. Dans **virtuels**, sélectionnez hello machines virtuelles tooreplicate.
2. Cliquez sur **OK**.

    ![Sélectionner les machines virtuelles](./media/azure-to-azure-walkthrough-enable-replication/vms.png)


## <a name="configure-settings"></a>Configurer les paramètres

Récupération de site configure les paramètres par défaut pour la région cible hello (selon les paramètres de région de code source hello) et la stratégie de réplication hello :

   - **Emplacement cible**: hello cible la région toouse pour la récupération d’urgence. Nous recommandons qu’emplacement cible de hello correspond à emplacement hello de coffre de récupération de Site hello.
   - **Groupe de ressources cible**: groupe de ressources toowhich machines virtuelles Azure dans la région cible hello appartiendra après le basculement. Par défaut, Site Recovery crée un nouveau groupe de ressources dans la région cible hello avec un suffixe « asr ». 
   - **Réseau virtuel cible**: réseau hello dans les machines virtuelles Azure hello région cible se trouve après le basculement. Par défaut, la récupération de Site crée un nouveau réseau virtuel (et des sous-réseaux) dans la région cible hello avec un suffixe « asr ». Ce réseau est mappé tooyour source réseau. Notez que vous pouvez affecter une adresse IP spécifique après le basculement d’un ordinateur virtuel, si vous avez besoin de tooretain hello même adresse IP dans les emplacements source et cible hello. 
   - **Comptes de stockage de cache**: récupération de Site utilise un compte de stockage dans la région de la source hello. Modifications sur des machines virtuelles source sont envoyées toothis compte, avant que l’emplacement de la réplication toohello cible. 
   - **Cibler des comptes de stockage**: par défaut, Site Recovery crée un nouveau compte de stockage dans la région cible hello, source de hello toomirror compte de stockage de machine virtuelle.
   -  **Cibler des groupes à haute disponibilité**: par défaut, Site Recovery crée un nouveau groupe à haute disponibilité région cible hello, avec le suffixe « asr » de hello. 
   - **Nom de la stratégie de réplication** : nom de la stratégie.
   - **Rétention des points de récupération** : par défaut, Site Recovery conserve les points de récupération pendant 24 heures. Vous pouvez configurer une valeur comprise entre 1 et 72 heures.
   - **Fréquence des instantanés de cohérence des applications** : par défaut, Site Recovery prend un instantané de cohérence des applications toutes les 4 heures. Vous pouvez configurer une valeur comprise entre 1 et 12 heures. Les données sont répliquées en continu :
    - Des points de récupération cohérents d’incident conservent un ordre d’écriture cohérent des données lors de leur création. Ce type de point de récupération est généralement suffisant si votre application est conçue toorecover à partir d’un incident sans des incohérences de données
    - Des points de récupération cohérents d’incident sont générés toutes les quelques minutes. À l’aide de ces toofail de points de récupération sur et récupérer vos machines virtuelles fournit un objectif de Point de récupération (RPO) dans l’ordre de hello de minutes.
    - Des points de récupération cohérents au niveau de l’application (dans la cohérence de l’ordre toowrite ajout) assurent que des applications en cours d’exécution terminer toutes les opérations et vider les mémoires tampons toodisk (suspension de l’application). Nous vous recommandons d’utiliser ces points de récupération pour les applications de base de données comme SQL Server, Oracle et Exchange.
        
    ![Configurer les paramètres](./media/azure-to-azure-walkthrough-enable-replication/settings.png)


### <a name="modify-settings"></a>Modifier les paramètres

Si vous souhaitez que les paramètres de stratégie de toomodify cible et la réplication, procédez comme hello suivant :

1. tooview ou modifier les paramètres de la cible, cliquez sur **paramètres**.
2. Cliquez sur les paramètres de cible par défaut toooverride hello, **personnaliser**. Vous pouvez spécifier un groupe de ressources cible, un réseau virtuel, un groupe à haute disponibilité et un compte de stockage cible. Vous pouvez uniquement ajouter des groupes à haute disponibilité si les machines virtuelles font partie d’un jeu dans la région de la source hello.

    ![Configurer les paramètres](./media/azure-to-azure-walkthrough-enable-replication/customize-target.png)

3. toooverride les paramètres de réplication pour les points de récupération et des instantanés cohérents au niveau de l’application, cliquez sur **personnaliser** suivant trop**stratégie de réplication**.
 
    ![Configurer les paramètres](./media/azure-to-azure-walkthrough-enable-replication/customize-policy.png)

4. toostart configurer hello cible les ressources, cliquez sur **créer des ressources de la cible**. L’approvisionnement prend environ une minute. Ne fermez pas les lames hello lors de la configuration, ou vous avez toostart sur.




## <a name="enable-replication"></a>Activer la réplication

1. Dans **Paramètres**, cliquez sur **Activer la réplication**. Ainsi, la réplication initiale de hello machines virtuelles que vous avez sélectionné. État de réplication initiale peut prendre quelques toorefresh de temps. Cliquez sur **Actualiser** état le plus récent tooget hello.

2. Vous pouvez suivre la progression de hello **activer la protection** de la tâche dans **paramètres** > **travaux** > **tâches de récupération de Site**.

3. Dans **paramètres** > **répliquées des éléments**, vous pouvez afficher l’état de hello de machines virtuelles et hello la progression de la réplication initiale. Cliquez sur hello VM toodrill vers le bas dans ses paramètres.



## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 6 : exécuter un test de basculement](azure-to-azure-walkthrough-test-failover.md)
