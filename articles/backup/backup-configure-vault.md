---
title: aaaUse Azure Backup agent tooback les fichiers et dossiers | Documents Microsoft
description: "Utilisez hello Microsoft Azure Backup agent tooback des tooAzure de fichiers et dossiers de Windows. Créer un coffre Recovery Services, installez l’agent de sauvegarde hello, définir la stratégie de sauvegarde hello et exécuter la sauvegarde initiale de hello sur les dossiers et fichiers de hello."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: coffre de sauvegarde ; sauvegarder un serveur Windows ; sauvegarder windows ;
ms.assetid: 7f5b1943-b3c1-4ddb-8fb7-3560533c68d5
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: be203c24841971872b5c6e7cf260a2fa5c58ac47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-client-tooazure-using-hello-resource-manager-deployment-model"></a>Sauvegarder un tooAzure ou client Windows Server à l’aide du modèle de déploiement du Gestionnaire de ressources hello
> [!div class="op_single_selector"]
> * [Portail Azure](backup-configure-vault.md)
> * [Portail classique](backup-configure-vault-classic.md)
>
>

Cet article explique comment tooAzure de fichiers et dossiers tooback de votre client Windows Server (ou Windows) à l’aide de la sauvegarde Azure hello modèle de déploiement de gestionnaire de ressources.

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![Étapes du processus de sauvegarde](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a>Avant de commencer
tooback un serveur ou un client tooAzure, vous devez un compte Azure. Si vous n’en possédez pas, vous pouvez créer un [compte gratuit](https://azure.microsoft.com/free/) en quelques minutes.

## <a name="create-a-recovery-services-vault"></a>Créer un coffre Recovery Services
Un coffre Recovery Services est une entité qui stocke toutes les sauvegardes de hello et les points de récupération que vous créez au fil du temps. le coffre Recovery Services Hello contient également hello appliqué de stratégie de sauvegarde toohello protégé fichiers et dossiers. Lorsque vous créez un coffre Recovery Services, vous devez également sélectionner option de redondance de stockage approprié hello.

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


### <a name="set-storage-redundancy"></a>Définir la redondance du stockage
Lorsque vous créez un archivage de Recovery Services pour la première fois, vous devez spécifier le mode de réplication du stockage.

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

Maintenant que vous avez créé un coffre, préparez votre tooback infrastructure des fichiers et des dossiers en téléchargeant et installation hello Microsoft Azure Recovery Services agent, téléchargement des informations d’identification de coffre et ensuite à l’aide de ces informations d’identification tooregister hello agent coffre de Hello.

## <a name="configure-hello-vault"></a>Configurer le coffre de hello

1. On hello panneau du coffre Recovery Services (pour hello coffre vous venez de créer), dans la section prise en main de hello, cliquez sur **sauvegarde**, puis sur hello **mise en route de la sauvegarde** panneau, sélectionnez  **Objectif de sauvegarde**.

  ![Ouvrir le panneau Objectif de sauvegarde](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  Hello **sauvegarde objectif** panneau s’ouvre. Si hello de coffre Recovery Services a été configuré précédemment, puis hello **sauvegarde objectif** panneaux s’ouvre lorsque vous cliquez sur **sauvegarde** sur les Services de récupération hello coffre lame.

  ![Ouvrir le panneau Objectif de sauvegarde](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. À partir de hello **votre charge de travail exécutant ?** menu déroulant, sélectionnez **local**.

  En effet, vous devez choisir l’option **Local**, car votre ordinateur Windows Server ou Windows est une machine physique, qui ne se trouve donc pas dans Azure.

3. À partir de hello **comment vous souhaitez toobackup ?** menu, sélectionnez **fichiers et dossiers**et cliquez sur **OK**.

  ![Configuration des fichiers et dossiers](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

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
> Activer la sauvegarde via hello portail Azure n’est pas encore disponible. Utilisez tooback de Microsoft Azure Recovery Services Agent hello des fichiers et des dossiers.
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

## <a name="network-and-connectivity-requirements"></a>Conditions de connectivité et réseau

Si votre ordinateur/proxy est limitée à un accès à internet, assurez-vous que les paramètres du pare-feu sur hello/proxy de l’ordinateur sont hello tooallow configuré URL suivantes : <br>
    1. www.msftncsi.com
    2. *.Microsoft.com
    3. *.MicrosoftAzure.com
    4. *.microsoftonline.com
    5. *.windows.ne


## <a name="create-hello-backup-policy"></a>Créer une stratégie de sauvegarde hello
stratégie de sauvegarde Hello est planification de hello lorsque des points de récupération sont effectuées et hello de durée de conservation des points de récupération hello. Utilisez hello Microsoft Azure Backup agent toocreate hello stratégie de sauvegarde des fichiers et dossiers.

### <a name="toocreate-a-backup-schedule"></a>toocreate une planification de sauvegarde
1. Ouvrez hello Microsoft Azure Backup agent. Vous pouvez le trouver en recherchant **Sauvegarde Microsoft Azure**sur votre ordinateur.

    ![Lancez l’agent de sauvegarde Azure hello](./media/backup-configure-vault/snap-in-search.png)
2. Dans l’agent de sauvegarde hello **Actions** volet, cliquez sur **planifier la sauvegarde** toolaunch hello Assistant Planification de sauvegarde.

    ![Planifier une sauvegarde de Windows Server](./media/backup-configure-vault/schedule-first-backup.png)

3. Sur hello **mise en route** page Hello Assistant Planification de sauvegarde, cliquez sur **suivant**.
4. Sur hello **tooBackup de sélectionner les éléments** , cliquez sur **ajouter les éléments**.

  Ouvre la boîte de dialogue Sélectionner les éléments Hello.

5. Sélectionnez les fichiers de hello et dossiers que vous souhaitez tooprotect, puis cliquez sur **OK**.
6. Bonjour **tooBackup de sélectionner les éléments** , cliquez sur **suivant**.
7. Sur hello **spécifier la planification de sauvegarde** , spécifiez la planification de sauvegarde hello et cliquez sur **suivant**.

    Vous pouvez planifier des sauvegardes quotidiennes (au maximum 3 fois par jour) ou hebdomadaires.

    ![Éléments de sauvegarde de Windows Server](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > Pour plus d’informations sur comment toospecify hello planification de sauvegarde, voir l’article hello [tooreplace utilisez Azure Backup votre infrastructure de bande](backup-azure-backup-cloud-as-tape.md).
   >
   >

8. Sur hello **sélectionner la stratégie de rétention** page, choisissez hello de stratégies de rétention spécifique hello de copie de sauvegarde hello et cliquez sur **suivant**.

    stratégie de rétention Hello spécifie la durée hello quelle sauvegarde hello est stocké. Plutôt que de simplement spécifier « stratégie plate » pour tous les points de sauvegarde, vous pouvez spécifier des stratégies de rétention différentes basées sur lors de la sauvegarde de hello se produit. Vous pouvez modifier toomeet de stratégies de rétention quotidienne, hebdomadaire, mensuel et annuel hello à vos besoins.
9. Sur la page Choisir un Type de sauvegarde initiale de hello, choisissez le type de sauvegarde initiale hello. Conservez l’option hello **automatiquement sur le réseau de hello** sélectionné, puis cliquez sur **suivant**.

    Vous pouvez sauvegarder automatiquement sur le réseau de hello, ou vous pouvez sauvegarder en mode hors connexion. reste Hello de cet article décrit le processus hello pour sauvegarder automatiquement. Si vous préférez toodo une sauvegarde hors connexion, consultez l’article de hello [workflow de sauvegarde en mode hors connexion dans Azure Backup](backup-azure-backup-import-export.md) pour plus d’informations.
10. Sur la page de Confirmation hello, passez en revue les informations de hello, puis cliquez sur **Terminer**.
11. Une fois l’Assistant de hello ait fini de créer la planification de sauvegarde hello, cliquez sur **fermer**.

### <a name="enable-network-throttling"></a>Activation de la limitation du réseau
Hello Microsoft Azure Backup agent fournit la limitation du réseau. La limitation contrôle l’utilisation de la bande passante réseau durant le transfert de données. Ce contrôle peut être utile si vous devez tooback des données pendant les heures de travail mais que vous ne souhaitez pas que toointerfere du processus de sauvegarde hello avec tout autre trafic Internet. La limitation s’applique tooback des activités et de restauration.

> [!NOTE]
> La limitation du réseau n’est pas disponible sur Windows Server 2008 R2 SP1, Windows Server 2008 SP2 ou Windows 7 (avec service packs). fonctionnalité de limitation du réseau de sauvegarde Azure Hello engage une qualité de Service (QoS) sur le système d’exploitation local de hello. Bien que Azure Backup peut protéger ces systèmes d’exploitation, version hello de qualité de service disponibles sur ces plateformes ne fonctionne pas avec la limitation réseau Azure Backup. La limitation du réseau peut être utilisée sur tous les autres [systèmes d’exploitation pris en charge](backup-azure-backup-faq.md).
>
>

**la limitation réseau tooenable**

1. Dans l’agent Microsoft Azure Backup hello, cliquez sur **modifier les propriétés**.

    ![Modifier les propriétés](./media/backup-configure-vault/change-properties.png)
2. Sur hello **limitation** onglet, sélectionnez hello **activer l’utilisation de la bande passante internet pour les opérations de sauvegarde de limitation** case à cocher.

    ![Limitation du réseau](./media/backup-configure-vault/throttling-dialog.png)
3. Une fois que vous avez activé la limitation, spécifiez hello autorisée de la bande passante pour transférer des données de sauvegarde pendant **des heures de travail** et **heures chômées**.

    valeurs de la bande passante Hello commencent à 512 kilobits par seconde (Kbits/s) et peuvent atteindre la too1, 023 mégaoctets par seconde (Mbits/s). Vous pouvez également désigner le début de hello et de fin de **des heures de travail**, et les jours de semaine de hello sont des jours de travail pris en compte. Les heures non comprises dans les heures de travail définies sont considérées comme des heures chômées.
4. Cliquez sur **OK**.

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a>tooback des fichiers et des dossiers pour hello première fois
1. Dans l’agent de sauvegarde hello, cliquez sur **sauvegarder maintenant** hello toocomplete initiale d’amorçage réseau hello.

    ![Sauvegarder Windows Server maintenant](./media/backup-configure-vault/backup-now.png)
2. Sur la page de Confirmation hello, vérifier les paramètres hello qui hello Assistant sauvegarder maintenant utilisera tooback machine de hello. puis cliquez sur **Sauvegarder**.
3. Cliquez sur **fermer** Assistant de hello tooclose. Si vous procédez ainsi avant la fin du processus de sauvegarde hello, Assistant de hello continue toorun en arrière-plan de hello.

Une fois la sauvegarde initiale de hello est terminée, hello **fin du travail** état s’affiche dans la console de sauvegarde hello.

![RI terminé](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a>Des questions ?
Si vous avez des questions, ou s’il en existe toute fonctionnalité qui vous aimeriez toosee inclus, [envoyez-nous vos commentaires](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur la sauvegarde des machines virtuelles ou d’autres charges de travail, consultez les références suivantes :

* Maintenant que vous avez sauvegardé vos fichiers et vos dossiers, vous pouvez [gérer vos archivages et vos serveurs](backup-azure-manage-windows-server.md).
* Si vous devez toorestore une sauvegarde, utilisez cet article trop[restaurer la machine virtuelle Windows tooa fichiers](backup-azure-restore-windows-server.md).
