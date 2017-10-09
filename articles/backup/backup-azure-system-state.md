---
title: "aaaBack des tooAzure d’état Windows système | Documents Microsoft"
description: "En savoir plus tooback état du système de Windows Server et/ou tooAzure des ordinateurs Windows hello."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: carmonm
editor: 
keywords: "Comment toobackup ; Comment tooback ; sauvegarde des fichiers et dossiers"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: saurse;markgal
ms.openlocfilehash: be5d4be81af981c10de82add9fe962a730753cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a>Sauvegarder l’état du système Windows dans un déploiement Resource Manager
Cet article explique comment l’état tooAzure tooback de votre système Windows Server. Il s’agit d’un didacticiel toowalk prévue vous guident dans les principes de base hello.

Si vous souhaitez tooknow plus d’informations sur Azure Backup, lire ce [vue d’ensemble](backup-introduction-to-azure-backup.md).

Si vous ne disposez pas d’un abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/) pour accéder à n’importe quel service Azure.

## <a name="create-a-recovery-services-vault"></a>Créer un coffre Recovery Services
tooback des fichiers et des dossiers, vous devez toocreate un coffre de Services de récupération dans la région de hello où vous souhaitez toostore hello données. Vous devez également toodetermine comment vous souhaitez que votre stockage répliqué.

### <a name="toocreate-a-recovery-services-vault"></a>toocreate un coffre Recovery Services
1. Si vous n’avez pas déjà fait, connectez-vous à toohello [portail Azure](https://portal.azure.com/) à l’aide de votre abonnement Azure.
2. Dans le menu du Hub hello, cliquez sur **davantage de services** et, dans la liste hello des ressources, tapez **Services de récupération** et cliquez sur **les coffres de Services de récupération**.

    ![Créer un archivage de Recovery Services - Étape 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    S’il existe des coffres des services de récupération dans l’abonnement de hello, coffres de hello sont répertoriés.
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

8. Au bas de hello du Panneau de coffre Recovery Services hello, cliquez sur **créer**.

    Il peut prendre plusieurs minutes pour hello que toobe créé de coffre de Services de récupération. Surveiller les notifications d’état hello dans la zone de droite supérieure hello du portail de hello. Une fois votre coffre est créé, il apparaît dans la liste hello des coffres des Services de récupération. Si vous ne voyez pas votre coffre après quelques minutes, cliquez sur **Actualiser**.

    ![Bouton Actualiser](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    Une fois que vous voyez votre coffre dans la liste hello des archivages de Recovery Services, vous êtes prêt tooset une redondance de stockage hello.

### <a name="set-storage-redundancy-for-hello-vault"></a>Définir une redondance de stockage pour l’archivage de hello
Lorsque vous créez un coffre Recovery Services, assurez-vous de redondance du stockage est configuré hello librement.

1. À partir de hello **les coffres de Services de récupération** panneau, cliquez sur le coffre hello.

    ![Sélectionnez le coffre hello dans liste hello du coffre Recovery Services](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    Lorsque vous sélectionnez le coffre de hello, hello **de coffre Recovery Services** panneau restreint et panneau de paramètres hello (*qui a le nom hello du coffre de hello de haut hello*) et le panneau de détails du coffre hello ouvert.

    ![Afficher la configuration du stockage hello pour le nouveau coffre](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. Dans le panneau des paramètres du coffre hello nouvelle tooscroll de diapositive vertical hello toohello section gérer vers le bas, puis cliquez sur **Infrastructure de sauvegarde**.
    panneau d’Infrastructure de sauvegarde Hello s’ouvre.
3. Dans le panneau d’Infrastructure de sauvegarde hello, cliquez sur **Configuration de la sauvegarde** tooopen hello **Configuration de la sauvegarde** panneau.

    ![Définir la configuration de stockage hello pour le nouveau coffre](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. Choisissez l’option de réplication de stockage approprié de hello pour votre coffre.

    ![Options de configuration du stockage](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    Par défaut, votre archivage utilise un stockage géo-redondant. Si vous utilisez Azure comme un point de terminaison principal de stockage de sauvegarde, continuer toouse **géo-redondant**. Si vous n’utilisez pas Azure comme un point de terminaison principal de stockage de sauvegarde, puis choisissez **localement redondant**, ce qui réduit les coûts de stockage Azure hello. Pour en savoir plus sur les options de stockage [géo-redondant](../storage/common/storage-redundancy.md#geo-redundant-storage) et [localement redondant](../storage/common/storage-redundancy.md#locally-redundant-storage), consultez la [présentation de la redondance du stockage](../storage/common/storage-redundancy.md).

Une fois votre coffre créé, vous devez le configurer pour la sauvegarde de l’état du système Windows.

## <a name="configure-hello-vault"></a>Configurer le coffre de hello
1. On hello panneau du coffre Recovery Services (pour hello coffre vous venez de créer), dans la section prise en main de hello, cliquez sur **sauvegarde**, puis sur hello **mise en route de la sauvegarde** panneau, sélectionnez  **Objectif de sauvegarde**.

    ![Ouvrir le panneau Objectif de sauvegarde](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    Hello **sauvegarde objectif** panneau s’ouvre.

    ![Ouvrir le panneau Objectif de sauvegarde](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. À partir de hello **votre charge de travail exécutant ?** menu déroulant, sélectionnez **local**.

    En effet, vous devez choisir l’option **Local**, car votre ordinateur Windows Server ou Windows est une machine physique, qui ne se trouve donc pas dans Azure.

3. À partir de hello **comment vous souhaitez toobackup ?** menu, sélectionnez **état du système**et cliquez sur **OK**.

    ![Configuration des fichiers et dossiers](./media/backup-azure-system-state/backup-goal-system-state.png)

    Après avoir cliqué sur OK, une coche apparaît en regard trop**objectif de sauvegarde**et hello **Prepare infrastructure** panneau s’ouvre.

    ![Objectif de sauvegarde configuré, début de préparation de l’infrastructure](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. Sur hello **Prepare infrastructure** panneau, cliquez sur **télécharger l’Agent pour Windows Server ou Windows Client**.

    ![Download Agent for Windows Server or Windows Client](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    Si vous utilisez Windows Server essentiels, puis choisissez toodownload hello agent essentielles de Windows Server. Un menu contextuel vous invite toorun ou enregistrer MARSAgentInstaller.exe.

    ![Boîte de dialogue MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. Dans le menu contextuel du téléchargement hello, cliquez sur **enregistrer**.

    Par défaut, hello **MARSagentinstaller.exe** fichier est enregistré le dossier Téléchargements de tooyour. Lorsque le programme d’installation hello est terminée, vous verrez un message vous demandant si vous souhaitez que le programme d’installation de toorun hello ou ouvrez le dossier de hello.

    ![Download Agent for Windows Server or Windows Client](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    Vous n’avez pas encore l’agent de tooinstall hello. Vous pouvez installer l’agent de hello après avoir téléchargé les informations d’identification de coffre hello.

6. Sur hello **Prepare infrastructure** panneau, cliquez sur **télécharger**.

    ![Télécharger les informations d’identification du coffre](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    informations d’identification de coffre Hello téléchargement le dossier Téléchargements de tooyour. Une fois les informations d’identification de coffre hello terminer le téléchargement, vous voyez un message vous demandant si vous souhaitez tooopen ou enregistrez les informations d’identification hello. Cliquez sur **Enregistrer**. Si vous cliquez accidentellement sur **ouvrir**, permettent de boîte de dialogue hello qui tente d’informations d’identification du coffre tooopen hello donc pas. Impossible d’ouvrir des informations d’identification de coffre hello. Passez maintenant toohello. informations d’identification de coffre Hello se trouvent dans le dossier Téléchargements de hello.   

    ![Fin du téléchargement des informations d’identification du coffre](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a>Installer et inscrire l’agent de hello

> [!NOTE]
> Activer la sauvegarde via hello portail Azure n’est pas encore disponible. Utilisez hello Microsoft Azure Recovery Services Agent tooback état du système Windows Server.
>

1. Recherchez et double-cliquez sur hello **MARSagentinstaller.exe** de téléchargements de hello dossier (ou tout autre emplacement enregistré).

    programme d’installation Hello fournit une série de messages qu’il extrait, installe et enregistre hello Recovery Services agent.

    ![Informations d’identification de programme d’installation de l’agent Recovery Services exécuté](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. Assistant Installation de Microsoft Azure Recovery Services Agent de hello terminée. Assistant de hello toocomplete, vous devez :

   * Choisissez un emplacement pour le dossier d’installation et de cache hello.
   * Fournir les informations du serveur de votre proxy si vous utilisez un toohello tooconnect du serveur proxy internet.
   * Fournir votre nom d’utilisateur et votre mot de passe si vous utilisez un proxy authentifié.
   * Fournir des informations d’identification de coffre hello téléchargé
   * Enregistrer la phrase secrète de chiffrement hello dans un emplacement sécurisé.

     > [!NOTE]
     > Si vous perdez ou oubliez le mot de passe hello, Microsoft ne peut pas aider à récupérer les données de sauvegarde hello. Enregistrez le fichier de hello dans un emplacement sécurisé. Il est requis toorestore une sauvegarde.
     >
     >

Hello agent est installé et que votre ordinateur est inscrit toohello coffre. Vous êtes prêt tooconfigure et planifiez votre sauvegarde.

## <a name="back-up-windows-server-system-state-preview"></a>Sauvegarder l’état du système Windows Server (préversion)
la sauvegarde initiale Hello inclut trois tâches :

* Activer la sauvegarde de l’état système à l’aide de l’agent de sauvegarde Azure hello
* Planifier la sauvegarde hello
* Sauvegarder des fichiers et des dossiers pour hello première fois

sauvegarde initiale toocomplete hello, utilisez hello Microsoft Azure Recovery Services agent.

### <a name="tooenable-system-state-backup-using-hello-azure-backup-agent"></a>sauvegarde de l’état du système de tooenable à l’aide de l’agent de sauvegarde Azure hello

1. Dans une session PowerShell, exécutez hello suivant du moteur de commande toostop hello Azure Backup.

  ```
  PS C:\> Net stop obengine
  ```

2. Ouvrez hello du Registre Windows.

  ```
  PS C:\> regedit.exe
  ```

3. Add hello clé de Registre avec hello suivante spécifiée de la valeur DWord.

  | Chemin d’accès au Registre | Clé de Registre | Valeur DWord |
  |---------------|--------------|-------------|
  | HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider | TurnOffSSBFeature | 2 |

4. Redémarrez le moteur de sauvegarde hello en exécutant hello suivant de commande dans une invite de commandes avec élévation de privilèges.

  ```
  PS C:\> Net start obengine
  ```

### <a name="tooschedule-hello-backup-job"></a>travail de sauvegarde hello tooschedule

1. Ouvrez l’agent de Microsoft Azure Recovery Services hello. Vous pouvez le trouver en recherchant **Sauvegarde Microsoft Azure**sur votre ordinateur.

    ![Lancer hello Azure Recovery Services agent](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. Dans l’agent Recovery Services hello, cliquez sur **planifier la sauvegarde**.

    ![Planifier une sauvegarde de Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. Sur hello mise en route de la page de hello Assistant Planification de sauvegarde, cliquez sur **suivant**.

4. Page de tooBackup hello sélectionner les éléments, cliquez sur **ajouter les éléments**.

5. Sélectionnez **État du système**, puis cliquez sur **OK**.

6. Cliquez sur **Suivant**.

7. Hello planification de rétention et de sauvegarde de l’état système est automatiquement définie tooback de tous les dimanches à 9 h 00, heure locale, et la valeur de période de rétention hello too60 jours.

   > [!NOTE]
   > La stratégie de sauvegarde et de rétention de l’état du système est configurée automatiquement. Si vous sauvegardez les fichiers et dossiers en outre état toohello du système de serveur Windows, spécifiez la stratégie de sauvegarde et de rétention hello uniquement pour les sauvegardes de fichiers à partir de l’Assistant de hello. 
   >

8. Sur la page de Confirmation hello, passez en revue les informations de hello, puis cliquez sur **Terminer**.

9. Une fois l’Assistant de hello ait fini de créer la planification de sauvegarde hello, cliquez sur **fermer**.

### <a name="tooback-up-windows-server-system-state-for-hello-first-time"></a>tooback état du système Windows Server pour hello première fois

1. Vérifiez qu’aucune mise à jour de Windows Server nécessitant un redémarrage n’est en attente.

2. Dans l’agent Recovery Services hello, cliquez sur **sauvegarder maintenant** hello toocomplete initiale d’amorçage réseau hello.

    ![Sauvegarder Windows Server maintenant](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. Sur la page de Confirmation hello, vérifier les paramètres hello qui hello Assistant sauvegarder maintenant utilisera tooback machine de hello. puis cliquez sur **Sauvegarder**.

4. Cliquez sur **fermer** Assistant de hello tooclose. Si vous fermez l’Assistant de hello avant la fin du processus de sauvegarde hello, Assistant de hello continue toorun en arrière-plan de hello.

5. Si vous sauvegardez des fichiers et dossiers sur votre serveur, en outre toohello Windows Server System State, Assistant sauvegarder maintenant hello sera uniquement sauvegarder les fichiers. tooperform un état du système ad hoc sauvegarder, utilisez hello suivant de commande PowerShell :

    ```
    PS C:\> Start-OBSystemStateBackup
    ```

  Une fois la sauvegarde initiale de hello est terminée, hello **fin du travail** état s’affiche dans la console de sauvegarde hello.

  ![RI terminé](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="frequently-asked-questions"></a>Forum Aux Questions

Hello questions et réponses suivantes fournissent des informations supplémentaires.

### <a name="what-is-hello-staging-volume"></a>Nouveautés hello Volume de mise en lots

Hello Volume de mise en lots représente un emplacement intermédiaire de hello où hello disponible en mode natif, sauvegarde de Windows Server prépare hello sauvegarde de l’état système. Azure Backup agent puis compresse et chiffre cette sauvegarde intermédiaire et envoie que via toohello de protocole HTTPS sécurisée configuré coffre Recovery Services. **Nous vous recommandons vivement de que vous établissez hello Volume de mise en lots dans un volume non--système d’exploitation Windows. Si vous notez des problèmes avec les sauvegardes d’état du système, la vérification d’emplacement hello de votre Volume de mise en lots est première étape de dépannage hello.** 

### <a name="how-can-i-change-hello-staging-volume-path-specified-in-hello-azure-backup-agent"></a>Comment puis-je modifier hello chemin d’accès du Volume intermédiaire spécifié dans l’agent de sauvegarde Azure hello ?

Hello Volume de mise en attente se trouve dans le dossier de cache hello par défaut. 

1. toochange cet emplacement, hello utilisez commande (dans une invite de commandes avec élévation de privilèges) suivante :
  ```
  PS C:\> Net stop obengine
  ```

2. Puis mettez à jour hello suivant des entrées de Registre avec hello chemin d’accès toohello nouveau Volume de mise en lots dossier.

  |Chemin d’accès au Registre|Clé de Registre|Valeur|
  |-------------|------------|-----|
  |HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider | SSBStagingPath | nouvel emplacement du volume intermédiaire |

Hello chemin d’accès de mise en lots respecte la casse et doit être hello même casse que celui qui existe sur le serveur de hello. 

3. Une fois que vous modifiez le chemin d’accès du volume hello intermédiaire, redémarrez le moteur de sauvegarde hello :
  ```
  PS C:\> Net start obengine
  ```
4. toopick chemin d’accès hello modifié, l’agent de Microsoft Azure Recovery Services hello ouvert et déclencheur une sauvegarde ad hoc de l’état du système.

### <a name="why-is-hello-system-state-default-retention-set-too60-days"></a>Pourquoi est-état du système hello rétention par défaut de définir les jours de too60 ?

Hello cycle de vie d’une sauvegarde de l’état système est hello identique au paramètre hello « tombstone lifetime » pour le rôle de Windows Server Active Directory hello. valeur par défaut de Hello pour l’entrée de durée de vie de temporisation hello est de 60 jours. Cette valeur peut être définie sur l’objet de configuration du Service d’annuaire (NTDS) hello.

### <a name="how-do-i-change-hello-default-backup-and-retention-policy-for-system-state"></a>Comment modifier la valeur par défaut de hello sauvegarde et de la stratégie de rétention pour l’état du système ?

valeur par défaut hello toochange sauvegarde et stratégie de rétention pour l’état du système :
1. Arrêter le moteur de sauvegarde hello. Exécutez hello de commande suivante à partir d’une invite de commandes avec élévation de privilèges.

  ```
  PS C:\> Net stop obengine
  ```

2. Ajouter ou mettre à jour hello suivant des entrées de clé de Registre dans HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider.

  |Nom de Registre|Description|Valeur|
  |-------------|-----------|-----|
  |SSBScheduleTime|Utilisation de hello tooconfigure de sauvegarde de hello. La valeur par défaut est 21h00 heure locale.|DWord : format HHMM (décimal), par exemple 2130 pour 21h30 heure locale.|
  |SSBScheduleDays|Jours de hello tooconfigure utilisé lorsque sauvegarde de l’état système doit être effectué au hello spécifié de fois. Des chiffres spécifient les jours de semaine de hello. 0 représente le dimanche, 1 le lundi, et ainsi de suite. Le jour de sauvegarde par défaut est le dimanche.|DWord : les jours de sauvegarde de toorun hello semaine (décimal), par exemple 1230 planifie les sauvegardes sur lundi, mardi, mercredi et dimanche.|
  |SSBRetentionDays|Sauvegarde de tooretain tooconfigure utilisé hello jours. La valeur par défaut est 60. La valeur maximale autorisée est 180.|DWord : La sauvegarde de tooretain jours (décimale).|

3. Utilisez hello suivant du moteur de sauvegarde commande toorestart hello.
    ```
    PS C:\> Net start obengine
    ```

4. Ouvrez hello Microsoft Recovery Services agent.

5. Cliquez sur **planifier la sauvegarde** puis cliquez sur **suivant** jusqu'à ce que vous voyiez modifications hello soient répercutées.

6. Cliquez sur **Terminer** modifications de hello tooapply.


## <a name="questions"></a>Des questions ?
Si vous avez des questions, ou s’il en existe toute fonctionnalité qui vous aimeriez toosee inclus, [envoyez-nous vos commentaires](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Étapes suivantes
* Approfondissez vos connaissances sur la [sauvegarde de machines Windows](backup-configure-vault.md).
* Maintenant que vous avez sauvegardé vos fichiers et vos dossiers, vous pouvez [gérer vos archivages et vos serveurs](backup-azure-manage-windows-server.md).
* Si vous devez toorestore une sauvegarde, utilisez cet article trop[restaurer la machine virtuelle Windows tooa fichiers](backup-azure-restore-windows-server.md).
