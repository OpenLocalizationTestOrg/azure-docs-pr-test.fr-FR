---
title: "Sauvegarde Azure : Restaurer l’état du système sur un serveur Windows | Microsoft Docs"
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
ms.openlocfilehash: 320c85f8045d9b72cf7f430d2e2736ba8e5ec269
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="restore-system-state-to-windows-server"></a>Restaurer l’état du système sur Windows Server

Cet article explique comment restaurer des sauvegardes de l’état du système Windows Server à partir d’un coffre Azure Recovery Services. Pour restaurer l’état du système, vous devez disposer d’une sauvegarde de l’état du système (créée en suivant les instructions fournies dans [Sauvegarder l’état du système](backup-azure-system-state.md#back-up-windows-server-system-state-preview)) et vérifier que vous avez installé la [version la plus récente de l’agent Microsoft Azure Recovery Services (MARS)](http://aka.ms/azurebackup_agent). La récupération des données d’état du système Windows Server à partir d’un coffre Azure Recovery Services est un processus en deux étapes :

1. Restaurer l’état du système sous forme de fichiers à partir de Sauvegarde Azure. Lors de la restauration de l’état du système sous forme de fichiers à partir de Sauvegarde Azure, vous pouvez :
  * Restaurer l’état du système sur le même serveur que celui où les sauvegardes ont été effectuées, ou
  * Restaurer le fichier d’état du système sur un autre serveur

2. Appliquer les fichiers d’état du système restaurés à un serveur Windows.


## <a name="recover-system-state-files-to-the-same-server"></a>Récupérer les fichiers d’état du système sur le même serveur
Les étapes suivantes expliquent comment restaurer votre configuration Windows Server à un état antérieur. La restauration de votre configuration de serveur à un état stable connu peut être extrêmement utile. Les étapes suivantes restaurent l’état du système du serveur à partir d’un coffre Recovery Services. 

1. Ouvrez le composant logiciel enfichable **Sauvegarde Microsoft Azure**. Si vous ne savez pas où il a été installé, recherchez **Sauvegarde Microsoft Azure** sur l’ordinateur ou le serveur.

    L’application de bureau devrait apparaître dans les résultats de recherche.

2. Cliquez sur **Récupérer des données** pour lancer l’Assistant.

    ![Récupérer des données](./media/backup-azure-restore-windows-server/recover.png)

3. Sur le volet **Prise en main**, pour restaurer les données sur le même serveur ou ordinateur, sélectionnez **Ce serveur (`<server name>`)** et cliquez sur **Suivant**.

    ![Choisissez l’option Ce serveur pour restaurer les données sur le même ordinateur](./media/backup-azure-restore-system-state/samemachine.png)

4. Dans le volet **Sélectionnez le mode de récupération**, choisissez **État du système**, puis cliquez sur **Suivant**.

    ![Parcourir les fichiers](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. Sur le calendrier dans le volet **Sélectionner un volume et une date**, sélectionnez un point de récupération. 

    Vous pouvez effectuer la restauration à partir du point de récupération de votre choix dans le temps. Les dates **en gras** indiquent la disponibilité d’au moins un point de récupération. Une fois que vous avez sélectionné une date, si plusieurs points de récupération sont disponibles, cliquez sur l’un d’entre eux dans le menu déroulant **Temps**.

    ![Volume et date](./media/backup-azure-restore-system-state/select-date.png)

6. Une fois que vous avez choisi le point de récupération à restaurer, cliquez sur **Suivant**.

    La Sauvegarde Azure monte le point de récupération local et l’utilise comme volume de récupération.

7. Dans le volet suivant, spécifiez la destination des fichiers d’état du système récupérés, cliquez sur **Parcourir** pour ouvrir l’Explorateur Windows et recherchez les fichiers et les dossiers souhaités. L’option **Créer des copies pour avoir les deux versions** permet de créer des copies des différents fichiers dans une archive de fichiers d’état du système existante, au lieu de créer la copie de la totalité de l’archive d’état du système.

    ![Options de récupération](./media/backup-azure-restore-system-state/recover-as-files.png)

8. Vérifiez les détails de la récupération dans le volet **Confirmation** et cliquez sur **Récupérer**.

   ![cliquer sur Récupérer pour accuser réception de l’action de récupération](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. Copiez le répertoire *WindowsImageBackup* dans la destination de récupération sur un volume non critique du serveur. En règle générale, le volume de système d’exploitation Windows est le volume critique.

10. Une fois la récupération réussie, suivez les étapes décrites dans la section [Appliquer des fichiers d’état du système restaurés au serveur Windows](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server) pour terminer le processus de récupération de l’état du système.

## <a name="recover-system-state-files-to-an-alternate-server"></a>Récupérer les fichiers d’état du système sur un autre serveur

Si votre serveur Windows est endommagé ou inaccessible et que vous voulez le restaurer à un état stable en récupérant l’état du système Windows Server, vous pouvez restaurer l’état du système du serveur endommagé à partir d’un autre serveur. Pour restaurer l’état du système sur un autre serveur, effectuez les étapes suivantes.  

Les termes ci-après sont utilisés pour cette procédure :

- *Ordinateur source* : ordinateur d’origine à partir duquel la sauvegarde a été effectuée et qui est actuellement indisponible.
- *Ordinateur cible* : ordinateur sur lequel les données sont récupérées.
- *Exemple d’archivage* – coffre Recovery Services dans lequel *l’ordinateur source* et *l’ordinateur cible* sont enregistrés. <br/>

> [!NOTE]
> Les sauvegardes effectuées à partir d’un ordinateur ne peuvent pas être restaurées sur un ordinateur qui exécute une version antérieure du système d’exploitation. Par exemple, les sauvegardes effectuées à partir d’un ordinateur Windows Server 2016 ne peut pas être restaurées vers Windows Server 2012 R2. Toutefois, l’inverse est possible. Vous pouvez utiliser des sauvegardes de Windows Server 2012 R2 pour restaurer Windows Server 2016.
>

1. Ouvrez le composant logiciel enfichable **Sauvegarde Microsoft Azure** sur l’*Ordinateur cible*.
2. Vérifiez que *l’ordinateur cible* et *l’ordinateur source* sont inscrits auprès du même coffre Recovery Services.
3. Cliquez sur **Récupérer des données** pour lancer le flux de travail.

    ![Récupérer des données](./media/backup-azure-restore-windows-server-classic/recover.png)

4. Sélectionnez **Un autre serveur**

    ![Un autre serveur](./media/backup-azure-restore-system-state/anotherserver.png)

5. Fournissez le fichier d’informations d’identification de coffre qui correspond à l’ *exemple d’archivage*. Si le fichier d’informations d’identification du coffre n’est pas valide (ou a expiré), téléchargez un nouveau fichier d’informations d’identification de coffre à partir de *l’Exemple de coffre* dans le Portail Azure. Une fois le fichier d’informations d’identification de coffre fourni, le coffre Recovery Services associé au fichier d’informations d’identification de coffre apparaît.

6. Dans le volet Sélectionner un serveur de sauvegarde, sélectionnez l’*Ordinateur source* dans la liste des ordinateurs affichés.

    ![Liste des ordinateurs](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. Dans le volet Sélectionnez le mode de récupération, choisissez **État du système**, puis cliquez sur **Suivant**. 

    ![Search](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. Sur le calendrier dans le volet **Sélectionner un volume et une date**, sélectionnez un point de récupération. Vous pouvez effectuer la restauration à partir du point de récupération de votre choix dans le temps. Les dates **en gras** indiquent la disponibilité d’au moins un point de récupération. Une fois que vous avez sélectionné une date, si plusieurs points de récupération sont disponibles, cliquez sur l’un d’entre eux dans le menu déroulant **Temps**. 

    ![Éléments de recherche](./media/backup-azure-restore-system-state/select-date.png)

9. Une fois que vous avez choisi le point de récupération à restaurer, cliquez sur **Suivant**.

10. Dans le volet **Sélectionner le mode de récupération de l’état du système**, spécifiez la destination où vous souhaitez récupérer les fichiers d’état du système, puis cliquez sur **Suivant**.

    ![Chiffrement](./media/backup-azure-restore-system-state/recover-as-files.png)

    L’option **Créer des copies pour avoir les deux versions** permet de créer des copies des différents fichiers dans une archive de fichiers d’état du système existante, au lieu de créer la copie de la totalité de l’archive d’état du système.

11. Vérifiez les détails de la récupération dans le volet Confirmation et cliquez sur **Récupérer**. 

    ![cliquer sur le bouton Récupérer pour confirmer le processus de récupération](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. Copiez le répertoire *WindowsImageBackup* sur un volume non critique du serveur (par exemple D:\). En règle générale, le volume de système d’exploitation Windows est le volume critique.

13. Pour terminer le processus de récupération, utilisez la section suivante pour [appliquer les fichiers d’état du système restaurés sur un serveur Windows](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).




## <a name="apply-restored-system-state-on-a-windows-server"></a>Appliquer l’état du système restauré sur un serveur Windows

Une fois que vous avez récupéré l’état du système sous forme de fichiers à l’aide de l’Agent Azure Recovery Services, utilisez l’utilitaire Sauvegarde Windows Server pour appliquer l’état du système récupéré à Windows Server. L’utilitaire Sauvegarde Windows Server est déjà disponible sur le serveur. Les étapes suivantes expliquent comment appliquer l’état du système récupéré.

1. Exécutez les commandes suivantes pour redémarrer votre serveur en *Mode de réparation des services d’annuaire*. À partir d’une invite de commandes avec élévation de privilèges :

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. Après le redémarrage, ouvrez le composant logiciel enfichable Sauvegarde Windows Server. Si vous ne savez pas où il a été installé, recherchez **Sauvegarde Windows Server** sur l’ordinateur ou le serveur.

    L’application de bureau s’affiche dans les résultats de recherche.

3. Dans le composant logiciel enfichable, sélectionnez **Sauvegarde locale**.

    ![sélectionner Sauvegarde locale pour restaurer à partir de là](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. Dans la console Sauvegarde locale, dans le volet **Actions**, cliquez sur **Récupérer** pour ouvrir l’Assistant Récupération.

5. Sélectionnez l’option **Un autre emplacement**, puis cliquez sur **Suivant**.

   ![choisir de récupérer sur un autre serveur](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. Quand vous spécifiez le type d’emplacement, sélectionnez **Dossier partagé distant** si votre sauvegarde de l’état du système a été récupérée sur un autre serveur. Si l’état du système a été récupéré localement, sélectionnez **Lecteurs locaux**. 

    ![sélectionner s’il faut récupérer à partir d’un serveur local ou autre](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. Entrez le chemin du répertoire *WindowsImageBackup* ou choisissez le lecteur local contenant ce répertoire (par exemple, D:\WindowsImageBackup), récupéré dans le cadre de la récupération des fichiers d’état du système à l’aide de l’Agent Azure Recovery Services, puis cliquez sur **Suivant**.

    ![chemin du fichier partagé](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. Sélectionnez la version de l’état du système que vous souhaitez restaurer, puis cliquez sur **Suivant**.

9. Dans le volet Sélectionner le type de récupération, sélectionnez **État du système**, puis cliquez sur **Suivant**.

10. Comme emplacement de récupération de l’état du système, sélectionnez **Emplacement d’origine**, puis cliquez sur **Suivant**.

11. Passez en revue les détails de confirmation, vérifiez les paramètres de redémarrage, puis cliquez sur **Récupérer** pour appliquer les fichiers d’état du système restaurés.

    ![lancez la restauration des fichiers d’état du système](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a>Considérations spéciales pour la récupération de l’état du système sur le serveur Active Directory

La sauvegarde de l’état du système inclut les données Active Directory. Effectuez les étapes suivantes pour restaurer les services de domaine Active Directory (AD DS) de leur état actuel vers un état antérieur.

1. Redémarrez le contrôleur de domaine en Mode restauration des services d’annuaire (DSRM).
2. Suivez les étapes [ici](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) pour utiliser les applets de commande Windows Server Backup afin de récupérer AD DS.


## <a name="troubleshoot-failed-system-state-restore"></a>Résoudre les problèmes d’échec de restauration de l’état du système

Si le processus précédent d’application de l’état du système ne se termine pas correctement, utilisez l’Environnement de récupération Windows (WinRE) pour récupérer votre serveur Windows. Les étapes suivantes expliquent comment récupérer à l’aide de l’Environnement de récupération Windows (WinRE). Utilisez cette option uniquement si Windows Server ne démarre pas normalement après une restauration de l’état du système. Le processus suivant efface les données autres que les données système. Soyez prudent. 

1. Démarrez votre ordinateur Windows Server dans l’Environnement de récupération Windows (WinRE).

2. Sélectionnez Dépanner parmi les trois options disponibles.

    ![ouverture du menu](./media/backup-azure-restore-system-state/winre-1.png)

3. Dans l’écran **Options avancées**, sélectionnez **Invite de commandes** et fournissez le nom d’utilisateur et le mot de passe de l’administrateur de serveur.

   ![ouverture du menu](./media/backup-azure-restore-system-state/winre-2.png)

4. Fournissez le nom d’utilisateur et le mot de passe de l’administrateur de serveur.

    ![ouverture du menu](./media/backup-azure-restore-system-state/winre-3.png)

5. Quand vous ouvrez l’invite de commandes en mode administrateur, exécutez la commande suivante pour obtenir les versions de sauvegarde de l’état du système.

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![obtenir les versions de sauvegarde de l’état du système](./media/backup-azure-restore-system-state/winre-4.png)

6. Exécutez la commande suivante pour obtenir tous les volumes disponibles dans la sauvegarde.

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![obtenir les versions de sauvegarde de l’état du système](./media/backup-azure-restore-system-state/winre-5.png)

7. La commande suivante récupère tous les volumes qui font partie de la sauvegarde de l’état du système. Notez que cette étape récupère uniquement les volumes critiques qui font partie de l’état du système. Toutes les données autres que les données système sont effacées.

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![obtenir les versions de sauvegarde de l’état du système](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a>Étapes suivantes
* Maintenant que vous avez restauré vos fichiers et vos dossiers, vous pouvez [gérer vos sauvegardes](backup-azure-manage-windows-server.md).
