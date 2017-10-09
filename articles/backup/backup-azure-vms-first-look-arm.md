---
title: "Découverte : Protéger les machines virtuelles Azure avec un coffre Recovery Services | Microsoft Docs"
description: "Protégez les machines virtuelles Azure avec un coffre Recovery Services. Utilisez des sauvegardes de déployées par le Gestionnaire de ressources de machines virtuelles, déployé classique les machines virtuelles et Premium stockage machines virtuelles, les machines virtuelles chiffré, ordinateurs virtuels sur des disques gérés tooprotect vos données. Créez et enregistrez un coffre Recovery Services. Enregistrez des machines virtuelles, créez une stratégie et protégez des machines virtuelles dans Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keyword: backups; vm backup
ms.assetid: 45e773d6-c91f-4501-8876-ae57db517cd1
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/15/2017
ms.author: markgal;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70e4700abb76e16e32e1ead06ce1dbe277e1f0e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-toorecovery-services-vaults"></a>Sauvegarder les coffres des Services de machines virtuelles tooRecovery
> [!div class="op_single_selector"]
> * [Protéger les machines virtuelles avec un coffre Recovery Services](backup-azure-vms-first-look-arm.md)
> * [Protéger les machines virtuelles avec un coffre de sauvegarde](backup-azure-vms-first-look.md)
>
>

Ce didacticiel vous guide tout au long des étapes de hello pour créer un coffre de services de récupération et de sauvegarde d’une machine virtuelle Azure (VM). Les coffres Recovery Services protègent :

* Machines virtuelles déployées à l’aide de Resource Manager
* les machines virtuelles Classic,
* les machines virtuelles de stockage standard,
* les machines virtuelles Premium Storage.
* Machines virtuelles exécutées sur des disques gérés
* les machines virtuelles chiffrées à l’aide d’Azure Disk Encryption, avec des clés BEK et KEK
* Sauvegarde cohérente des applications des machines virtuelles Windows à l’aide de machines virtuelles VSS et Linux avec des scripts pré et post-instantané personnalisés

Pour plus d’informations sur la protection du stockage de Premium machines virtuelles, consultez l’article hello, [sauvegarder et restaurer des machines virtuelles de stockage Premium](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup). Pour plus d’informations sur la prise en charge des machines virtuelles sur disques gérés, consultez la section [Back up and restore VMs on managed disks](backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup) (Sauvegarder et restaurer des machines virtuelles sur des disques gérés). Pour plus d’informations sur l’infrastructure pré et post-script pour la sauvegarde de machine virtuelle Linux, consultez l’article [Sauvegarde de machine virtuelle Linux cohérente dans l’application à l’aide de pré/post-scripts] (https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).

toofind plus sur ce qui peut vous sauvegarde et que vous ne pouvez pas, consultez [ici](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)

> [!NOTE]
> Ce didacticiel suppose que vous avez déjà une machine virtuelle dans votre abonnement Azure et que vous avez pris les mesures tooallow hello service de sauvegarde tooaccess hello machine virtuelle.
>
>

[!INCLUDE [learn-about-Azure-Backup-deployment-models](../../includes/backup-deployment-models.md)]

En fonction du nombre de hello d’ordinateurs virtuels vous tooprotect, vous pouvez commencer à partir de points de départ. Si vous souhaitez tooback plusieurs machines virtuelles en une seule opération, accédez à Services de récupération toohello coffre et [tâche de sauvegarde hello lancer à partir du tableau de bord coffre hello](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-recovery-services-vault). Si vous souhaitez tooback une machine virtuelle unique, vous pouvez lancer le travail de sauvegarde hello à partir du Panneau de gestion de machine virtuelle.

## <a name="configure-hello-backup-job-from-hello-vm-management-blade"></a>Configurer la tâche de sauvegarde hello à partir du Panneau de gestion de machine virtuelle hello

Utilisez hello suivant les étapes tooconfigure hello de sauvegarde à partir du Panneau de gestion de machine virtuelle hello Bonjour portail Azure. Ces étapes ne s’appliquent pas virtuels toohello dans le portail classique de hello.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Dans le menu du Hub hello, cliquez sur **plus Services** et, dans la boîte de dialogue filtre hello, tapez **machines virtuelles**. Lorsque vous tapez, hello liste de filtres de ressources. Dès que vous voyez apparaître le service Machines virtuelles, sélectionnez-le.

  ![Sur le menu Hub, cliquez sur la boîte de dialogue Services plus tooopen texte et tapez des machines virtuelles](./media/backup-azure-vms-first-look-arm/open-vm-from-hub.png)

  liste Hello des machines virtuelles (VM) dans l’abonnement de hello, s’affiche.

  ![liste Hello de machines virtuelles dans l’abonnement de hello s’affiche.](./media/backup-azure-vms-first-look-arm/list-of-vms.png)

3. À partir de la liste de hello, sélectionnez un tooback de machine virtuelle.

  ![liste Hello de machines virtuelles dans l’abonnement de hello s’affiche.](./media/backup-azure-vms-first-look-arm/list-of-vms-selected.png)

  Lorsque vous sélectionnez hello VM, liste hello des machines virtuelles équipes toohello gauche et panneau de gestion de machine virtuelle hello et tableau de bord de machine virtuelle hello, ouvrir. </br>
 ![Panneau de gestion des machines virtuelles](./media/backup-azure-vms-first-look-arm/vm-management-blade.png)

4. Sur le panneau gestion des ordinateurs virtuels hello, Bonjour **paramètres** , cliquez sur **sauvegarde**. </br>

  ![Option Sauvegarde du panneau de gestion de la machine virtuelle](./media/backup-azure-vms-first-look-arm/backup-option-vm-management-blade.png)

  Panneau de sauvegarde Hello activer s’ouvre.

  ![Option Sauvegarde du panneau de gestion de la machine virtuelle](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

5. Pour le coffre Recovery Services hello, cliquez sur **sélectionnez existante** et choisissez hello coffre à partir de la liste déroulante de hello.

  ![Assistant Activer la sauvegarde](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

  Si aucun coffre Recovery Services, ou si vous voulez toouse un coffre, cliquez sur **nouvel** et fournir le nom hello pour le coffre hello. Un nouvel archivage est créé dans hello même groupe de ressources et le même emplacement que l’ordinateur virtuel de hello. Si vous voulez toocreate un coffre Recovery Services avec des valeurs différentes, consultez une section de hello sur la façon de trop[créer un coffre recovery services](backup-azure-vms-first-look-arm.md#create-a-recovery-services-vault-for-a-vm).

6. Détails de hello tooview Hello stratégie de sauvegarde, cliquez sur **stratégie de sauvegarde**.

  Hello **stratégie de sauvegarde** panneau s’ouvre et fournit des détails hello de stratégie de hello sélectionné. S’il existent d’autres stratégies, utilisez hello menu déroulant toochoose une autre stratégie de sauvegarde. Si vous souhaitez toocreate une stratégie, sélectionnez **créer un nouveau** à partir du menu déroulant de hello. Pour savoir comment définir une stratégie de sauvegarde, consultez la section [Définition d’une stratégie de sauvegarde](backup-azure-vms-first-look-arm.md#defining-a-backup-policy). stratégie de sauvegarde toosave hello modifications toohello et retour toohello activer Panneau de la sauvegarde, cliquez sur **OK**.

  ![Sélectionner la stratégie de sauvegarde](./media/backup-azure-vms-first-look-arm/setting-rs-backup-policy-new-2.png)

7. Dans le panneau de sauvegarde activer hello, cliquez sur **activez la sauvegarde** stratégie de hello toodeploy. Déploiement de la stratégie de hello associe le coffre hello et machines virtuelles de hello.

  ![Bouton Activer la sauvegarde](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-button.png)

8. Vous pouvez suivre la progression de la configuration via les notifications hello qui s’affichent dans le portail de hello hello. Hello, l’exemple suivant montre que le déploiement démarré.

  ![Notification Activer la sauvegarde](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-notification.png)

9. Une fois que la progression de la configuration hello terminée, dans le panneau gestion des ordinateurs virtuels hello, cliquez sur **sauvegarde** panneau d’élément de sauvegarde tooopen hello et vue hello détails.

  ![Affichage des éléments de sauvegarde de la machine virtuelle](./media/backup-azure-vms-first-look-arm/backup-item-view.png)

  Avant la fin de la sauvegarde initiale de hello, **état de la dernière sauvegarde** affiche sous la forme **avertissement (sauvegarde initiale en attente)**. toosee lorsque hello replanifié la tâche de sauvegarde se produit, sous **stratégie de sauvegarde** cliquez sur nom hello de stratégie de hello. Panneau de la stratégie de sauvegarde Hello s’ouvre et affiche les temps de hello de la sauvegarde planifiée de hello.

10. toorun une sauvegarde de la tâche et créer un point de récupération initial hello, sur hello sauvegarde coffre cliquez sur le panneau **sauvegarder maintenant**.

  ![Cliquez sur la sauvegarde initiale de sauvegarde maintenant toorun hello](./media/backup-azure-vms-first-look-arm/backup-now.png)

  panneau Hello sauvegarder maintenant s’ouvre.

  ![Affiche le panneau hello sauvegarder maintenant](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

11. Dans Panneau de sauvegarder maintenant du hello, cliquez l’icône de calendrier hello, utilisez Bonjour calendrier contrôle tooselect Bonjour dernier jour de ce point de récupération est conservé, puis cliquez sur **sauvegarde**.

  ![définir hello dernier jour hello sauvegarder maintenant point de récupération est conservé.](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  Notifications de déploiement vous permettent de connaître la tâche de sauvegarde hello a été déclenchée, et que vous pouvez surveiller la progression hello de hello de page de travaux de sauvegarde hello.

## <a name="configure-hello-backup-job-from-hello-recovery-services-vault"></a>Configurer la tâche de sauvegarde hello de hello de coffre Recovery Services
travail de sauvegarde tooconfigure hello, vous terminez hello comme suit.  

1. Vous créez un coffre Recovery Services pour une machine virtuelle.
2. Utilisez Bonjour tooselect portail Azure, un scénario de définir une stratégie de sauvegarde et identifier les éléments tooprotect.
3. Exécuter la sauvegarde initiale de hello.

## <a name="create-a-recovery-services-vault-for-a-vm"></a>Création d’un coffre Recovery Services pour une machine virtuelle
Un coffre Recovery Services est une entité qui stocke toutes les sauvegardes de hello et les points de récupération qui ont été créées au fil du temps. Hello coffre Recovery Services contient également des stratégie de sauvegarde hello appliqué toohello protégés des ordinateurs virtuels.

> [!NOTE]
> La sauvegarde de machines virtuelles est un processus local. Vous ne pouvez pas sauvegarder les machines virtuelles du coffre de Services de récupération tooa un emplacement dans un autre emplacement. Par conséquent, pour chaque emplacement Azure qui a toobe de machines virtuelles sauvegardé, au moins un coffre Recovery Services doit exister dans cet emplacement.
>
>

toocreate un coffre Recovery Services :

1. Si vous n’avez pas déjà fait, connectez-vous à toohello [portail Azure](https://portal.azure.com/) à l’aide de votre abonnement Azure.
2. Dans le menu du Hub hello, cliquez sur **davantage de services** et dans le type de boîte de dialogue filtre de hello **Recovery Services**. Lorsque vous tapez, hello liste de filtres de ressources. Lorsque vous voyez les coffres des Services de récupération dans la liste de hello, cliquez dessus.

    ![Créer un archivage de Recovery Services - Étape 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    S’il existe des coffres des Services de récupération dans l’abonnement de hello, coffres de hello sont répertoriés.

    ![Créer un coffre Recovery Services - Étape 2](./media/backup-azure-vms-first-look-arm/list-of-rs-vault.png)
3. Sur hello **les coffres de Services de récupération** menu, cliquez sur **ajouter**.

    ![Créer un coffre Recovery Services - Étape 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    Services de récupération Hello coffre s’ouvre le panneau, vous invitant à tooprovide un **nom**, **abonnement**, **groupe de ressources**, et **emplacement**.

    ![Créer un coffre Recovery Services - Étape 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. Pour **nom**, entrez un coffre de hello tooidentify nom convivial. nom de Hello doit toobe unique pour hello abonnement Azure. Tapez un nom contenant entre 2 et 50 caractères. Il doit commencer par une lettre, et ne peut contenir que des lettres, des chiffres et des traits d’union.

5. Bonjour **abonnement** section, utilisez hello toochoose de menu déroulant hello abonnement Azure. Si vous N'utilisez qu’un seul abonnement, cet abonnement s’affiche et vous pouvez ignorer toohello prochaine étape. Si vous ne savez pas quel toouse d’abonnement, utiliser la valeur par défaut hello (ou suggéré) abonnement. Vous ne disposez de plusieurs choix que si votre compte professionnel est associé à plusieurs abonnements Azure.

6. Bonjour **groupe de ressources** section :

    * Sélectionnez **nouvel** si vous voulez toocreate un groupe de ressources.
    Ou
    * Sélectionnez **utiliser l’existante** sur hello menu déroulant toosee hello disponible liste des groupes de ressources.

  Pour plus d’informations sur les groupes de ressources, consultez hello [vue d’ensemble du Gestionnaire de ressources Azure](../azure-resource-manager/resource-group-overview.md).

7. Cliquez sur **emplacement** tooselect hello région pour le coffre hello. Ce choix détermine la région géographique de hello où vos données de sauvegarde sont envoyées.

  > [!IMPORTANT]
  > Si vous n’êtes pas sûr de hello emplacement dans lequel votre machine virtuelle, fermer la boîte de dialogue Création de coffre hello et atteindre liste toohello des Machines virtuelles dans le portail de hello. Si vous possédez des machines virtuelles dans plusieurs régions, créez un coffre Recovery Services dans chacune d’entre elles. Créer hello coffre dans le premier emplacement de hello avant de passer l’emplacement suivant du toohello. Aucun compte de stockage nécessaire toospecify hello n’utilisé toostore hello sauvegarde des données--hello le coffre de Services de récupération et de hello Azure Backup service gérer automatiquement le stockage de hello.
  >

8. Au bas de hello du Panneau de coffre Recovery Services hello, cliquez sur **créer**.

    Il peut prendre plusieurs minutes pour hello que toobe créé de coffre de Services de récupération. Surveiller les notifications d’état hello dans la zone de droite supérieure hello du portail de hello. Une fois votre coffre est créé, il apparaît dans la liste hello des coffres des Services de récupération. Si vous ne voyez pas votre coffre après quelques minutes, cliquez sur **Actualiser**.

    ![Bouton Actualiser](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    Une fois que vous voyez votre coffre dans la liste hello des archivages de Recovery Services, vous êtes prêt tooset une redondance de stockage hello.

Maintenant que vous avez créé votre archivage, découvrez comment tooset hello la réplication du stockage.

### <a name="set-storage-replication"></a>Définir la réplication du stockage
option de réplication de stockage Hello permet toochoose entre le stockage géo-redondant et le stockage localement redondant. Par défaut, votre archivage utilise un stockage géo-redondant. Si hello de coffre Recovery Services est votre sauvegarde principale, laissez hello réplication option ensemble redondant toogeo stockage. Choisissez Stockage localement redondant si vous souhaitez une option plus économique, mais moins durable. En savoir plus sur [géo-redondant](../storage/common/storage-redundancy.md#geo-redundant-storage) et [localement redondant](../storage/common/storage-redundancy.md#locally-redundant-storage) des options de stockage Bonjour [vue d’ensemble de la réplication de stockage Azure](../storage/common/storage-redundancy.md).

paramètre de réplication de stockage tooedit hello :

1. À partir de hello **les coffres de Services de récupération** panneau, coffre hello select.

  ![Sélectionnez le coffre hello dans liste hello du coffre Recovery Services](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

  Lorsque vous sélectionnez le coffre de hello, hello panneau Paramètres (*qui a le nom du coffre hello haut hello*) et le panneau de détails du coffre hello ouvert.

  ![Afficher la configuration du stockage hello pour le nouveau coffre](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. Dans le panneau des paramètres du coffre hello nouvelle tooscroll de diapositive vertical hello toohello section gérer vers le bas, puis cliquez sur **Infrastructure de sauvegarde**.
    panneau d’Infrastructure de sauvegarde Hello s’ouvre.
3. Dans le panneau d’Infrastructure de sauvegarde hello, cliquez sur **Configuration de la sauvegarde** tooopen hello **Configuration de la sauvegarde** panneau.

    ![Définir la configuration de stockage hello pour le nouveau coffre](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. Choisissez l’option de réplication de stockage approprié de hello pour votre coffre.

    ![Options de configuration du stockage](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    Par défaut, votre archivage utilise un stockage géo-redondant. Si vous utilisez Azure comme un point de terminaison principal de stockage de sauvegarde, continuer toouse **géo-redondant**. Si vous n’utilisez pas Azure comme un point de terminaison principal de stockage de sauvegarde, puis choisissez **localement redondant**, ce qui réduit les coûts de stockage Azure hello. Pour en savoir plus sur les options de stockage [géo-redondant](../storage/common/storage-redundancy.md#geo-redundant-storage) et [localement redondant](../storage/common/storage-redundancy.md#locally-redundant-storage), consultez la [présentation de la redondance du stockage](../storage/common/storage-redundancy.md).


## <a name="select-a-backup-goal-set-policy-and-define-items-tooprotect"></a>Sélectionnez un objectif de sauvegarde, de définir la stratégie et de définir les éléments tooprotect
Avant d’inscrire un ordinateur virtuel dans un coffre, exécutez tooensure de processus de découverte hello que de nouvelles machines virtuelles qui ont été ajoutés toohello abonnement sont identifiés. Hello traiter les requêtes Azure pour la liste des ordinateurs virtuels dans l’abonnement hello, ainsi que les informations hello comme nom du service cloud hello et région de hello. Bonjour portail Azure, scénario fait référence toowhat vous allez tooput dans le coffre hello recovery services. La stratégie est planification hello pour la fréquence et à quel moment les points de récupération sont effectuées. Stratégie inclut également hello de rétention des points de récupération hello.

1. Si vous disposez déjà d’un coffre ouvrir les services de récupération, passez toostep 2. Sinon, cliquez sur hello Hub, **davantage de services** et, dans la liste hello des ressources, tapez **Services de récupération** et cliquez sur **les coffres de Services de récupération**.

    ![Créer un archivage de Recovery Services - Étape 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    liste de Hello des coffres des services de récupération s’affiche.

    ![Liste les coffres de vue de hello Recovery Services](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

    À partir de la liste de hello des archivages de recovery services, sélectionnez un coffre tooopen son tableau de bord.

     ![Ouvrir le panneau de l’archivage](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)

2. Dans le menu de tableau de bord du coffre hello, cliquez sur **sauvegarde** Panneau de sauvegarde tooopen hello.

    ![Ouvrir le panneau Sauvegarde](./media/backup-azure-arm-vms-prepare/backup-button.png)

    panneaux de sauvegarde et de sauvegarde objectif Hello ouvre.

    ![Ouvrir le panneau Scénario](./media/backup-azure-arm-vms-prepare/select-backup-goal-1.png)
3. Sur le panneau d’objectif de sauvegarde hello, à partir de hello **votre charge de travail exécutant** menu déroulant, choisissez Azure. À partir de hello **comment vous souhaitez toobackup** liste déroulante, choisissez l’ordinateur virtuel, puis cliquez sur **OK**.

    Ces actions inscrire l’extension de machine virtuelle hello avec le coffre de hello. Hello objectif sauvegarde panneau se ferme et hello **stratégie de sauvegarde** panneau s’ouvre.

    ![Ouvrir le panneau Scénario](./media/backup-azure-arm-vms-prepare/select-backup-goal-2.png)

4. Dans Panneau de stratégie de sauvegarde hello, sélectionnez hello sauvegarde stratégie tooapply toohello coffre.

    ![Sélectionner la stratégie de sauvegarde](./media/backup-azure-arm-vms-prepare/setting-rs-backup-policy-new.png)

    Détails de Hello de stratégie par défaut de hello sont répertoriées sous le menu déroulant de hello. Si vous souhaitez toocreate une stratégie, sélectionnez **créer un nouveau** à partir du menu déroulant de hello. Pour savoir comment définir une stratégie de sauvegarde, consultez la section [Définition d’une stratégie de sauvegarde](backup-azure-vms-first-look-arm.md#defining-a-backup-policy).
    Cliquez sur **OK** stratégie de sauvegarde hello tooassociate avec le coffre de hello.

    Hello se ferme Panneau de stratégie de sauvegarde et de hello **sélectionner des machines virtuelles** panneau s’ouvre.
5. Bonjour **sélectionner des machines virtuelles** panneau, choisissez tooassociate de machines virtuelles hello avec hello spécifié de stratégie et cliquez sur **OK**.

    ![Sélectionner la charge de travail](./media/backup-azure-arm-vms-prepare/select-vms-to-backup.png)

    machine virtuelle de Hello sélectionné est validé. Si vous ne voyez pas hello virtual machines que vous attendiez toosee, vérifiez qu’ils existent dans hello même emplacement que le coffre de Services de récupération hello. emplacement de Hello de hello que coffre des Services de récupération est indiqué dans le tableau de bord coffre hello.

6. Maintenant que vous avez défini tous les paramètres pour l’archivage de hello, dans le panneau de sauvegarde hello, cliquez sur **Enable Backup** toodeploy hello coffre toohello de stratégie et hello des machines virtuelles. Déploiement de stratégie de sauvegarde hello ne crée pas de point de récupération initial hello pour la machine virtuelle de hello.

    ![Activer la sauvegarde](./media/backup-azure-arm-vms-prepare/vm-validated-click-enable.png)

Après avoir activé avec succès la sauvegarde de hello, votre stratégie de sauvegarde s’exécute sur une planification. Toutefois, continuer tooinitiate hello première opération de sauvegarde.

## <a name="initial-backup"></a>Sauvegarde initiale
Une fois qu’une stratégie de sauvegarde a été déployée sur l’ordinateur virtuel hello, qui ne signifie pas que les données de salutation a été sauvegardées. Par défaut, hello première planifiées (comme défini dans la stratégie de sauvegarde hello) est hello initiale sauvegarde. Jusqu'à ce que la sauvegarde initiale de hello se produit, hello état de la dernière sauvegarde sur hello **les travaux de sauvegarde** panneau affiche sous la forme **avertissement (sauvegarde initiale en attente)**.

![Sauvegarde en attente](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

Sauf si votre sauvegarde initiale est due toobegin bientôt, il est recommandé d’exécuter **sauvegarder maintenant**.

toorun hello initiale travail de sauvegarde :

1. Tableau de bord du coffre hello, cliquez sur nombre hello sous **des éléments de sauvegarde**, ou cliquez sur hello **des éléments de sauvegarde** vignette. <br/>
  ![Icône Paramètres](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)

  Hello **des éléments de sauvegarde** panneau s’ouvre.

  ![Éléments de sauvegarde](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. Sur hello **des éléments de sauvegarde** les lames, les éléments select hello.

  ![Icône Paramètres](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  Hello **des éléments de sauvegarde** liste s’ouvre. <br/>

  ![Travail de sauvegarde déclenché](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. Sur hello **des éléments de sauvegarde** , cliquez sur le bouton de sélection hello **...**  menu de contexte tooopen hello.

  ![Menu contextuel](./media/backup-azure-vms-first-look-arm/context-menu.png)

  menu contextuel de Hello s’affiche.

  ![Menu contextuel](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. Dans le menu contextuel de hello, cliquez sur **sauvegarder maintenant**.

  ![Menu contextuel](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  panneau Hello sauvegarder maintenant s’ouvre.

  ![Affiche le panneau hello sauvegarder maintenant](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. Dans Panneau de sauvegarder maintenant du hello, cliquez l’icône de calendrier hello, utilisez Bonjour calendrier contrôle tooselect Bonjour dernier jour de ce point de récupération est conservé, puis cliquez sur **sauvegarde**.

  ![définir hello dernier jour hello sauvegarder maintenant point de récupération est conservé.](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  Notifications de déploiement vous permettent de connaître la tâche de sauvegarde hello a été déclenchée, et que vous pouvez surveiller la progression hello de hello de page de travaux de sauvegarde hello. Selon la taille de hello de votre machine virtuelle, la création de sauvegarde initiale de hello peut prendre un certain temps.

6. état de hello tooview ou le suivi de la sauvegarde initiale hello, tableau de bord du coffre hello, sur hello **les travaux de sauvegarde** cliquez sur la vignette **en cours d’exécution**.

  ![Vignette Travaux de sauvegarde](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  Panneau de travaux de sauvegarde Hello s’ouvre.

  ![Vignette Travaux de sauvegarde](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  Bonjour **travaux de sauvegarde** panneau, vous pouvez voir État hello de tous les travaux. Vérifiez si le travail de sauvegarde hello pour votre machine virtuelle est toujours en cours ou s’il s’est terminé. Une opération de sauvegarde est terminée, le statut de hello est *terminé*.

  > [!NOTE]
  > Dans le cadre de l’opération de sauvegarde hello, hello Azure Backup service émet une extension de sauvegarde commande toohello dans chaque tooflush de machine virtuelle, toutes les écritures et prendre un instantané cohérent.
  >
  >


[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Installer hello Agent de machine virtuelle sur l’ordinateur virtuel de hello
Ces informations sont fournies en cas de nécessité. Hello Agent de machine virtuelle Azure doit être installé sur la machine virtuelle Azure à hello sauvegarde extension toowork de hello. Toutefois, si votre machine virtuelle a été créé à partir de la galerie Azure de hello, puis hello Agent de machine virtuelle est déjà présent sur l’ordinateur virtuel de hello. Machines virtuelles qui sont migrés à partir de centres de données local ne serait pas hello Agent de machine virtuelle installé. Dans ce cas, hello Agent de machine virtuelle doit toobe installé. Si vous avez des problèmes de sauvegarde hello machine virtuelle Azure, vérifiez que l’Agent de machine virtuelle Azure de hello est correctement installé sur machine virtuelle de hello (voir hello tableau suivant). Si vous créez une machine virtuelle personnalisée, [Vérifiez hello **hello d’installer l’Agent de machine virtuelle** case à cocher](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) avant de la machine virtuelle de hello est configurée.

En savoir plus sur hello [Agent de machine virtuelle](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) et [comment tooinstall il](../virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Hello tableau suivant fournit des informations supplémentaires sur l’Agent de machine virtuelle hello pour Windows et les machines virtuelles Linux.

| **opération** | **Windows** | **Linux** |
| --- | --- | --- |
| Lors de l’installation hello Agent de machine virtuelle |<li>Téléchargez et installez hello [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Vous avez besoin d’installation de l’administrateur des privilèges toocomplete hello. <li>[Mettre à jour la propriété de machine virtuelle hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate qui hello agent est installé. |<li> Installer hello dernières [agent Linux](https://github.com/Azure/WALinuxAgent) à partir de GitHub. Vous avez besoin d’installation de l’administrateur des privilèges toocomplete hello. <li> [Mettre à jour la propriété de machine virtuelle hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate qui hello agent est installé. |
| Mise à jour hello Agent de machine virtuelle |Hello mise à jour l’Agent de machine virtuelle est aussi simple que la réinstallation hello [binaires de l’Agent de machine virtuelle](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br>Assurez-vous qu’aucune opération de sauvegarde n’est en cours d’exécution pendant que l’agent de machine virtuelle hello est en cours de mise à jour. |Suivez les instructions de hello [mise à jour hello Agent de machine virtuelle Linux](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). <br>Assurez-vous qu’aucune opération de sauvegarde n’est en cours d’exécution lors de l’Agent de machine virtuelle est en cours de mise à jour de hello. |
| Validation de l’installation de l’Agent de machine virtuelle hello |<li>Accédez toohello *C:\WindowsAzure\Packages* dossier Bonjour Azure VM. <li>Vous devez rechercher la présence du fichier WaAppAgent.exe hello.<li> Cliquez sur le fichier de hello, accédez trop**propriétés**, puis sélectionnez hello **détails** onglet hello Version du produit doit être 2.6.1198.718 ou une version ultérieure. |N/A |

### <a name="backup-extension"></a>Extension de sauvegarde
Une fois hello que l’Agent VM est installé sur l’ordinateur virtuel de hello, hello service sauvegarde Azure installe hello extension de sauvegarde toohello Agent de machine virtuelle. Hello service sauvegarde Azure met à niveau et correctifs d’extension de sauvegarde hello sans intervention de l’utilisateur supplémentaires en toute transparence.

service de sauvegarde Hello installe extension de sauvegarde hello, même si hello VM n’est pas en cours d’exécution. Une machine virtuelle en cours d’exécution fournit chance de plus grande hello d’obtention d’un point de récupération cohérents avec les applications. Toutefois, hello service Azure Backup continue tooback des hello VM même si elle est désactivée et l’extension de hello n’a pas pu être installée. Ce type de sauvegarde est appelé en mode hors connexion de machine virtuelle et de point de récupération hello est *cohérent d’incident*.

## <a name="troubleshooting-information"></a>Résolution de problèmes
Si vous avez des problèmes d’accomplir certaines tâches de hello dans cet article, consultez le [conseils de dépannage](backup-azure-vms-troubleshoot.md).

## <a name="pricing"></a>Tarification
coût de Hello de la sauvegarde des machines virtuelles Azure est basé sur nombre hello d’instances protégées. Pour obtenir une définition d’une instance protégée, voir [Qu’est-ce qu’une instance protégée](backup-introduction-to-azure-backup.md#what-is-a-protected-instance). Pour obtenir un exemple de calcul du coût hello de sauvegarde d’une machine virtuelle, consultez [instances protégées calcul](backup-azure-vms-introduction.md#calculating-the-cost-of-protected-instances). Consultez hello tarification d’Azure Backup page pour plus d’informations sur les [sauvegarde tarification](https://azure.microsoft.com/pricing/details/backup/).

## <a name="questions"></a>Des questions ?
Si vous avez des questions, ou s’il en existe toute fonctionnalité qui vous aimeriez toosee inclus, [envoyez-nous vos commentaires](http://aka.ms/azurebackup_feedback).
