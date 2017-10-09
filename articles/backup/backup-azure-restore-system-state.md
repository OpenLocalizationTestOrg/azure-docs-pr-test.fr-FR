---
title: "Sauvegarde Azure : Tooa de restaurer l’état système Windows Server | Documents Microsoft"
description: "Explication étape par étape pour la restauration de l’état du système de Windows Server à partir d’une sauvegarde dans Azure."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/18/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: a45506507f53e2744350d3b6b2e52f1db415de4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-system-state-toowindows-server"></a>Restaurer l’état système tooWindows Server

Cet article explique comment les sauvegardes d’état du système Windows Server toorestore à partir d’un Azure Recovery Services coffre. toorestore état du système, doit avoir une sauvegarde de l’état du système (créé à l’aide d’instructions hello dans [sauvegarder l’état du système](backup-azure-system-state.md#back-up-windows-server-system-state-preview)) et vérifiez que vous avez installé hello [version la plus récente de Microsoft Azure Recovery de hello L’agent de services (MARS)](http://aka.ms/azurebackup_agent). La récupération des données d’état du système Windows Server à partir d’un coffre Azure Recovery Services est un processus en deux étapes :

1. Restaurer l’état du système sous forme de fichiers à partir de Sauvegarde Azure. Lors de la restauration de l’état du système sous forme de fichiers à partir de Sauvegarde Azure, vous pouvez :
  * Restaurer l’état système toohello même serveur sur lequel les sauvegardes hello ont été effectuées, ou
  * Restaurer l’état système fichier tooan autre serveur.

2. Appliquer tooa de fichiers hello restauré l’état du système Windows Server.


## <a name="recover-system-state-files-toohello-same-server"></a>Récupération de l’état système de fichiers toohello même serveur
Hello suit explique comment tooroll sauvegarder votre état précédent de tooa de configuration de Windows Server. Restauration de votre serveur tooa arrière de configuration connu, l’état stable, peut être extrêmement utile. Hello suivant l’état du système du serveur hello étapes restauration à partir d’un coffre Recovery Services. 

1. Ouvrez hello **Microsoft Azure Backup** enfichable. Si vous ne savez pas où le composant logiciel enfichable hello a été installé, recherchez hello ordinateur ou un serveur pour **Microsoft Azure Backup**.

    application de bureau Hello doit apparaître dans les résultats de la recherche hello.

2. Cliquez sur **récupérer les données** Assistant de hello toostart.

    ![Récupérer des données](./media/backup-azure-restore-windows-server/recover.png)

3. Sur hello **mise en route** volet, toorestore hello données toohello même serveur ou ordinateur, sélectionnez **ce serveur (`<server name>`)** et cliquez sur **suivant**.

    ![Choisissez cette toohello de données de serveur option toorestore hello même ordinateur](./media/backup-azure-restore-system-state/samemachine.png)

4. Sur hello **sélectionner le Mode de récupération** volet, choisissez **état du système** puis cliquez sur **suivant**.

    ![Parcourir les fichiers](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. Calendrier hello dans **sélectionner le Volume et la Date** point du volet, sélectionnez une récupération. 

    Vous pouvez effectuer la restauration à partir du point de récupération de votre choix dans le temps. Les dates dans **gras** indiquer la disponibilité de hello d’au moins un point de récupération. Une fois que vous sélectionnez une date, si plusieurs points de récupération sont disponibles, choisissez le point de récupération spécifique hello dans hello **temps** menu déroulant.

    ![Volume et date](./media/backup-azure-restore-system-state/select-date.png)

6. Une fois que vous avez choisi toorestore de point de récupération hello, cliquez sur **suivant**.

    Sauvegarde Azure monte le point de récupération locaux hello et l’utilise comme un volume de reprise.

7. Dans le volet suivant de hello, spécifiez la destination hello pour hello récupérées des fichiers d’état du système, puis cliquez sur **Parcourir** tooopen l’Explorateur Windows et hello rechercher des fichiers et dossiers que vous souhaitez. Hello option, **créer des copies pour avoir les deux versions**, crée des copies des fichiers individuels dans une archive de fichier de l’état du système existante au lieu de créer la copie de hello de hello totalité l’état du système de l’archive.

    ![Options de récupération](./media/backup-azure-restore-system-state/recover-as-files.png)

8. Vérifiez les détails de la récupération sur hello hello **Confirmation** volet et cliquez sur **récupérer**.

   ![Cliquez sur récupérer tooacknowledge hello recover action](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. Hello de copie *WindowsImageBackup* répertoire hello volume non critiques tooa destination récupération du serveur de hello. Hello volume du système d’exploitation Windows est généralement un volume critique de hello.

10. Une fois la récupération de hello a réussi, suivez les étapes de hello dans la section de hello, [appliquer restauré toohello de fichiers d’état du système Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), toocomplete hello les processus de récupération de l’état du système.

## <a name="recover-system-state-files-tooan-alternate-server"></a>Récupération de l’état système de fichiers sur un autre serveur tooan

Si votre serveur Windows est endommagé ou est inaccessible, et vous souhaitez toorestore il état stable de tooa en récupérant hello état du système Windows Server, vous pouvez restaurer l’état du système du serveur hello endommagé à partir d’un autre serveur. Utilisez hello suivant les étapes permettant de restaurer toohello état du système sur un serveur distinct.  

terminologie Hello utilisée dans cette procédure inclut :

- *Ordinateur source* : ordinateur d’origine hello quelle sauvegarde hello a été effectuée et qui est actuellement indisponible.
- *Ordinateur cible* – hello machine toowhich hello données sont récupérées.
- *Archivage de l’exemple* – Bonjour Recovery Services coffre toowhich Bonjour *machine Source* et *de l’ordinateur cible* sont enregistrés. <br/>

> [!NOTE]
> Les sauvegardes effectuées à partir d’un ordinateur ne peut pas être ordinateur restauré tooa exécutant une version antérieure du système d’exploitation de hello. Par exemple, les sauvegardes effectuées à partir d’un ordinateur Windows Server 2016 ordinateur ne peut pas être restaurée tooWindows Server 2012 R2. Toutefois, l’inverse de hello est possible. Vous pouvez utiliser les sauvegardes à partir de Windows Server 2012 R2 toorestore Windows Server 2016.
>

1. Ouvrez hello **Microsoft Azure Backup** enfichable sur hello *de l’ordinateur cible*.
2. Vérifiez que hello *de l’ordinateur cible* et hello *machine Source* sont toohello des Services de récupération même coffre.
3. Cliquez sur **récupérer les données** flux de travail tooinitiate hello.

    ![Récupérer des données](./media/backup-azure-restore-windows-server-classic/recover.png)

4. Sélectionnez **Un autre serveur**

    ![Un autre serveur](./media/backup-azure-restore-system-state/anotherserver.png)

5. Fournissez le fichier d’informations d’identification de coffre hello correspondant toohello *coffre d’exemple*. Si le fichier d’informations d’identification de coffre hello est non valide (ou a expiré), téléchargez un nouveau fichier d’informations d’identification de coffre à partir de hello *coffre d’exemple* Bonjour portail Azure. Une fois que le fichier d’informations d’identification de coffre hello est fourni, le coffre Recovery Services hello associé au fichier d’informations d’identification de coffre hello s’affiche.

6. Dans le volet de sélectionner un serveur de sauvegarde hello, sélectionnez hello *machine Source* à partir de la liste hello des ordinateurs affichés.

    ![Liste des ordinateurs](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. Dans le volet Sélectionner un Mode de récupération de hello, choisissez **état du système** et cliquez sur **suivant**. 

    ![Search](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. Sur hello calendrier Bonjour **sélectionner le Volume et la Date** point du volet, sélectionnez une récupération. Vous pouvez effectuer la restauration à partir du point de récupération de votre choix dans le temps. Les dates dans **gras** indiquer la disponibilité de hello d’au moins un point de récupération. Une fois que vous sélectionnez une date, si plusieurs points de récupération sont disponibles, choisissez le point de récupération spécifique hello dans hello **temps** menu déroulant. 

    ![Éléments de recherche](./media/backup-azure-restore-system-state/select-date.png)

9. Une fois que vous avez choisi toorestore de point de récupération hello, cliquez sur **suivant**.

10. Sur hello **sélectionner le Mode de récupération système état** volet, hello destination de l’état du système de fichiers toobe récupérée, puis cliquez sur **suivant**.

    ![Chiffrement](./media/backup-azure-restore-system-state/recover-as-files.png)

    Hello option, **créer des copies pour avoir les deux versions**, crée des copies des fichiers individuels dans une archive de fichier de l’état du système existante au lieu de créer la copie de hello de hello totalité l’état du système de l’archive.

11. Vérifiez les détails de la récupération sur le volet de Confirmation hello hello, puis cliquez sur **récupérer**. 

    ![Cliquez sur le processus de récupération du bouton tooconfirm hello hello récupérer](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. Hello de copie *WindowsImageBackup* répertoire tooa non critiques volume sur hello serveur (par exemple D:\). Hello volume du système d’exploitation Windows est généralement un volume critique de hello.

13. processus de récupération toocomplete hello, suivant de hello utilisez section trop[appliquer hello restauré les fichiers de l’état du système sur un serveur Windows](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).




## <a name="apply-restored-system-state-on-a-windows-server"></a>Appliquer l’état du système restauré sur un serveur Windows

Une fois que vous avez récupéré l’état du système sous forme de fichiers à l’aide d’Azure Recovery Services Agent, utilisez hello sauvegarde Windows Server utilitaire tooapply hello récupéré tooWindows d’état du système serveur. Hello utilitaire sauvegarde Windows Server est déjà disponible sur le serveur de hello. Hello suit explique comment tooapply hello récupérées à l’état du système.

1. Les commandes suivantes de hello utilisation tooreboot votre serveur dans *Mode réparation Services d’annuaire*. À partir d’une invite de commandes avec élévation de privilèges :

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. Après le redémarrage de hello, ouvrez le composant logiciel enfichable Sauvegarde Windows Server des hello. Si vous ne savez pas où le composant logiciel enfichable hello a été installé, recherchez hello ordinateur ou un serveur pour **sauvegarde Windows Server**.

    application de bureau Hello s’affiche dans les résultats de recherche hello.

3. Dans le composant logiciel enfichable hello, sélectionnez **sauvegarde locale**.

    ![Sélectionnez la sauvegarde locale toorestore à partir de là](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. Dans la console de sauvegarde locale hello, Bonjour **volet Actions**, cliquez sur **récupérer** tooopen hello Assistant récupération.

5. Sélectionnez l’option de hello, **une sauvegarde stockée dans un autre emplacement**, puis cliquez sur **suivant**.

   ![Choisissez toorecover tooa autre serveur](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. Lorsque vous spécifiez le type d’emplacement hello, sélectionnez **dossier partagé distant** si votre sauvegarde de l’état du système a été récupérée tooanother server. Si l’état du système a été récupéré localement, sélectionnez **Lecteurs locaux**. 

    ![Sélectionnez si toorecovery de serveur local ou un autre](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. Entrez hello chemin d’accès toohello *WindowsImageBackup* active, ou cliquez sur le disque local hello contenant ce répertoire (par exemple, D:\WindowsImageBackup), récupéré en tant que partie de la récupération de fichiers hello état du système à l’aide de la récupération d’Azure L’Agent et cliquez sur services **suivant**.

    ![chemin d’accès fichier partagé toohello](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. Version de l’état du système hello SELECT que vous souhaitez toorestore, puis cliquez sur **suivant**.

9. Dans le volet de sélectionner le Type de récupération hello, sélectionnez **état du système** et cliquez sur **suivant**.

10. Pour l’emplacement de hello Hello récupérer l’état du système, sélectionnez **emplacement d’origine**, puis cliquez sur **suivant**.

11. Passez en revue les détails de confirmation hello, vérifiez les paramètres de redémarrage hello, puis cliquez sur **récupérer** tooapplly hello restauration des fichiers de l’état du système.

    ![lancement hello restaurer les fichiers de l’état du système](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a>Considérations spéciales pour la récupération de l’état du système sur le serveur Active Directory

La sauvegarde de l’état du système inclut les données Active Directory. Utilisez hello suivant les étapes toorestore Service de domaine Active Directory (AD DS) dans son état précédent du tooa état actuel.

1. Redémarrez le contrôleur de domaine hello dans le Mode restauration des Services d’annuaire (DSRM).
2. Suivez les étapes de hello [ici](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toorecover applets de commande de sauvegarde de Windows Server toouse les services AD DS.


## <a name="troubleshoot-failed-system-state-restore"></a>Résoudre les problèmes d’échec de restauration de l’état du système

Si le processus précédent de hello de l’application de l’état du système ne se termine pas correctement, vous pouvez utiliser hello environnement de récupération Windows (Windows RE) toorecover votre serveur Windows. Hello étapes suivantes expliquent comment toorecover à l’aide de remporter de RE. Utilisez cette option uniquement si Windows Server ne démarre pas normalement après une restauration de l’état du système. Hello suivant processus efface les données non système, soyez prudent. 

1. Démarre votre serveur Windows hello environnement de récupération Windows (Windows RE).

2. Sélectionnez le dépannage de hello trois options.

    ![ouverture du menu](./media/backup-azure-restore-system-state/winre-1.png)

3. À partir de hello **Options avancées** écran, sélectionnez **invite de commandes** et fournir le nom d’utilisateur administrateur hello serveur et le mot de passe.

   ![ouverture du menu](./media/backup-azure-restore-system-state/winre-2.png)

4. Fournir le mot de passe et le nom d’utilisateur administrateur hello serveur.

    ![ouverture du menu](./media/backup-azure-restore-system-state/winre-3.png)

5. Lorsque vous ouvrez l’invite de commandes hello en mode administrateur, exécutez après les versions de sauvegarde de l’état du système de commande tooget hello.

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![obtenir les versions de sauvegarde de l’état du système](./media/backup-azure-restore-system-state/winre-4.png)

6. Exécutez hello suivant commande tooget tous les volumes disponibles dans la sauvegarde de hello.

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![obtenir les versions de sauvegarde de l’état du système](./media/backup-azure-restore-system-state/winre-5.png)

7. Hello commande suivante récupère tous les volumes qui font partie de la sauvegarde de l’état système de hello. Notez que cette étape récupère uniquement hello volumes critiques qui font partie de l’état du système hello. Toutes les données autres que les données système sont effacées.

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![obtenir les versions de sauvegarde de l’état du système](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a>Étapes suivantes
* Maintenant que vous avez restauré vos fichiers et vos dossiers, vous pouvez [gérer vos sauvegardes](backup-azure-manage-windows-server.md).
