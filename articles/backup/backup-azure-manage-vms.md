---
title: "les sauvegardes déployées par le Gestionnaire de ressources des machines virtuelles aaaManage | Documents Microsoft"
description: "Découvrez comment toomanage et surveiller les sauvegardes déployées par le Gestionnaire de ressources des machines virtuelles"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: f3050283-d60f-472d-b464-cb844e70d67e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: trinadhk;markgal
ms.openlocfilehash: 241fc4b2a29c5cd8b8b0ee8efbf8ba4e96c6a7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-machine-backups"></a>Gestion des sauvegardes de machines virtuelles Azure
> [!div class="op_single_selector"]
> * [Gestion des sauvegardes de machines virtuelles Azure](backup-azure-manage-vms.md)
> * [Gestion des sauvegardes de machines virtuelles classiques](backup-azure-manage-vms-classic.md)
>
>

Cet article fournit des conseils sur la gestion des sauvegardes de la machine virtuelle et explique les informations d’alertes de sauvegarde hello disponibles dans le tableau de bord de portail hello. les instructions de Hello dans cet article s’appliquent VMs toousing avec les coffres des Services de récupération. Cet article ne couvre pas la création de hello d’ordinateurs virtuels, ni expliquent comment tooprotect virtual machines. Pour une introduction sur la protection Azure Resource Manager déployés de machines virtuelles dans Azure avec un coffre Recovery Services, consultez [tout d’abord rechercher : sauvegardez tooa de machines virtuelles de coffre Recovery Services](backup-azure-vms-first-look-arm.md).

## <a name="manage-vaults-and-protected-virtual-machines"></a>Gérer les coffres et les machines virtuelles protégées
Bonjour portail Azure, tableau de bord coffre de Services de récupération hello fournit tooinformation d’accès sur l’inclusion de coffre hello :

* Hello sauvegarde la plus récente d’instantané, qui est également dernier point de restauration hello < br\>
* stratégie de sauvegarde de Hello < br\>
* la taille totale de tous les instantanés de sauvegarde <br\>
* nombre d’ordinateurs virtuels qui sont protégées par le coffre hello < br\>

De nombreuses tâches de gestion avec une sauvegarde de l’ordinateur virtuel commencent avec ouverture hello coffre dans le tableau de bord hello. Toutefois, étant coffres tooprotect utilisé plusieurs éléments (ou plusieurs machines virtuelles), tooview des détails sur un ordinateur virtuel, ouvrez tableau de bord coffre hello. Hello procédure suivante vous montre comment tooopen hello *tableau de bord coffre* , puis continuer toohello *tableau de bord coffre*. Il existe des « conseils » dans les deux procédures qui désignent comment tooadd hello coffre et du coffre, toohello de l’élément du tableau de bord Azure à l’aide de commande de toodashboard hello Pin. Code confidentiel toodashboard est un moyen de créer un coffre toohello de raccourci ou d’un élément. Vous pouvez également exécuter des commandes courantes à partir du raccourci de hello.

> [!TIP]
> Si vous disposez de plusieurs tableaux de bord et ouvre des panneaux, utilisez le curseur de bleu foncé et de hello bas hello hello tooslide de fenêtre hello du tableau de bord Azure dans les deux sens.
>
>

![Vue complète avec curseur](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-hello-dashboard"></a>Ouvrez un coffre Recovery Services dans le tableau de bord hello :
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Dans le menu du Hub hello, cliquez sur **Parcourir** et, dans la liste hello des ressources, tapez **Recovery Services**. Comme vous commencez à taper, hello filtres de la liste en fonction de votre entrée. Cliquez sur **Coffre Recovery Services**.

    ![Créer un archivage de Recovery Services - Étape 1](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    liste Hello des archivages de Recovery Services s’affiche.

    ![Liste des coffres Recovery Services ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > Si vous épinglez un toohello coffre Azure le tableau de bord, ce coffre est immédiatement accessible lorsque vous ouvrez hello portail Azure. toopin un tableau de bord coffre toohello dans la liste de coffre hello, cliquez sur le coffre de hello, puis sélectionnez **toodashboard du code confidentiel**.
   >
   >
3. À partir de la liste de hello des coffres, sélectionnez hello coffre tooopen son tableau de bord. Lorsque vous sélectionnez le coffre de hello, tableau de bord coffre hello et hello **paramètres** panneau ouvert. Bonjour suivant image, hello **Contoso-coffre** tableau de bord est mis en surbrillance.

    ![Ouvrir le tableau de bord du coffre et le panneau Paramètres](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a>Ouvrir le tableau de bord d’un élément du coffre
Dans la procédure précédente de hello, vous avez ouvert le tableau de bord hello coffre. tooopen hello coffre tableau de bord :

1. Tableau de bord du coffre hello, sur hello **des éléments de sauvegarde** vignette, cliquez sur **des Machines virtuelles Azure**.

    ![Ouvrir la mosaïque Éléments de sauvegarde](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    Hello **des éléments de sauvegarde** panneau répertorie hello dernière tâche de sauvegarde de chaque élément. Dans cet exemple, une machine virtuelle nommée demovm-markgal est protégée par ce coffre.  

    ![Mosaïque Éléments de sauvegarde](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > Pour faciliter l’accès, vous pouvez épingler un toohello d’élément de coffre Azure le tableau de bord. toopin un élément de coffre, dans la liste d’éléments de coffre hello, élément de hello avec le bouton droit et sélectionnez **toodashboard du code confidentiel**.
   >
   >
2. Bonjour **des éléments de sauvegarde** panneau, cliquez sur hello élément tooopen hello coffre élément du tableau de bord.

    ![Mosaïque Éléments de sauvegarde](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    tableau de bord coffre Hello et son **paramètres** panneau ouvert.

    ![Tableau de bord Éléments de sauvegarde avec panneau Paramètres](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    À partir de hello coffre élément du tableau de bord, vous pouvez accomplir plusieurs tâches de gestion de clés, telles que :

   * modifier des stratégies ou créer une stratégie de sauvegarde <br\>
   * afficher les points de restauration et vérifier leur état de cohérence <br\>
   * sauvegarde à la demande d’une machine virtuelle <br\>
   * suspendre la protection des machines virtuelles <br\>
   * reprendre la protection d’une machine virtuelle <br\>
   * supprimer des données de sauvegarde (ou un point de récupération) <br\>
   * [restaurer des disques de sauvegarde](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  &lt;br\>

Pourquoi les procédures suivantes, hello point de départ est tableau de bord coffre hello.

## <a name="manage-backup-policies"></a>Gestion des stratégies de sauvegarde
1. Sur hello [tableau de bord coffre](backup-azure-manage-vms.md#open-a-vault-item-dashboard), cliquez sur **tous les paramètres** tooopen hello **paramètres** panneau.

    ![Panneau Stratégie de sauvegarde](./media/backup-azure-manage-vms/all-settings-button.png)
2. Sur hello **paramètres** panneau, cliquez sur **stratégie de sauvegarde** tooopen ce panneau.

    Dans Panneau de hello, hello sauvegarde fréquence et rétention détails de la plage sont affichés.

    ![Panneau Stratégie de sauvegarde](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. À partir de hello **choisir la stratégie de sauvegarde** menu :

   * sélectionner une autre stratégie de toochange stratégies, puis cliquez sur **enregistrer**. Hello nouvelle stratégie est appliquée immédiatement toohello coffre. <br\>
   * toocreate une stratégie, sélectionnez **créer un nouveau**.

     ![Sauvegarde de machine virtuelle](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     Pour savoir comment créer une stratégie de sauvegarde, consultez la section [Définition d’une stratégie de sauvegarde](backup-azure-manage-vms.md#defining-a-backup-policy).

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> Lors de la gestion des stratégies de sauvegarde, vérifiez que toofollow hello [meilleures pratiques](backup-azure-vms-introduction.md#best-practices) pour des performances optimales de sauvegarde
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a>Sauvegarde à la demande d’une machine virtuelle
Vous pouvez effectuer une sauvegarde à la demande d’une machine virtuelle une fois que celle-ci est configurée pour la protection. Si la sauvegarde initiale de hello est en attente, à la demande de sauvegarde crée une copie complète de la machine virtuelle de hello Bonjour de coffre Recovery Services. Si la sauvegarde initiale de hello est terminée, une sauvegarde à la demande envoyer uniquement les modifications à partir de l’instantané précédent hello, toohello le coffre Recovery Services. Autrement dit, les sauvegardes suivantes sont toujours incrémentielles.

> [!NOTE]
> Hello de rétention pour une sauvegarde à la demande est la valeur de rétention hello spécifié pour le point de sauvegarde quotidien hello dans la stratégie de hello. Si aucun point de sauvegarde quotidien n’est sélectionnée, point de sauvegarde hebdomadaire hello est utilisé.
>
>

sauvegarde tootrigger une demande d’un ordinateur virtuel :

* Sur hello [tableau de bord coffre](backup-azure-manage-vms.md#open-a-vault-item-dashboard), cliquez sur **sauvegarder maintenant**.

    ![Bouton Sauvegarder maintenant](./media/backup-azure-manage-vms/backup-now-button.png)

    portail de Hello permet de s’assurer que vous souhaitez toostart un travail de sauvegarde à la demande. Cliquez sur **Oui** toostart du travail de sauvegarde hello.

    ![Bouton Sauvegarder maintenant](./media/backup-azure-manage-vms/backup-now-check.png)

    travail de sauvegarde Hello crée un point de récupération. durée de rétention Hello hello du point de récupération est hello identique à la durée de rétention spécifiée dans la stratégie de hello associée à une machine virtuelle hello. progression de hello tootrack pour travail hello, dans le tableau de bord du coffre hello, cliquez sur hello **des tâches de sauvegarde** vignette.  

## <a name="stop-protecting-virtual-machines"></a>Arrêt de la protection des machines virtuelles
Si vous choisissez toostop protéger un ordinateur virtuel, vous êtes invité si vous souhaitez que les points de récupération tooretain hello. Il existe deux façons de machines virtuelles de la protection toostop :

* arrêter tous les travaux de sauvegarde à venir et supprimer tous les points de récupération, ou
* arrêter toutes les tâches futures de sauvegarde, mais laissez hello points de récupération <br/>

Il existe un coût associé en laissant hello des points de récupération dans le stockage. Toutefois, avantage hello de laisser des points de récupération hello est que vous pouvez restaurer une version ultérieure, hello virtual machine si vous le souhaitez. Pour plus d’informations sur les coûts de hello de laisser hello des points de récupération, consultez hello [tarification](https://azure.microsoft.com/pricing/details/backup/). Si vous choisissez toodelete tous les points de récupération, vous ne pouvez pas restaurer hello virtual machine.

protection toostop pour un ordinateur virtuel :

1. Sur hello [tableau de bord coffre](backup-azure-manage-vms.md#open-a-vault-item-dashboard), cliquez sur **arrêter la sauvegarde**.

    ![Bouton Arrêter la sauvegarde](./media/backup-azure-manage-vms/stop-backup-button.png)

    panneau d’arrêter la sauvegarde Hello s’ouvre.

    ![Panneau Arrêter la sauvegarde](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. Sur hello **arrêter la sauvegarde** panneau, choisissez si tooretain ou delete hello des données de sauvegarde. zone d’informations Hello fournit des détails sur votre choix.

    ![Arrêter la protection](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. Si vous avez choisi de données de sauvegarde tooretain hello, ignorez toostep 4. Si vous avez choisi de sauvegarder des données toodelete, confirmez que vous souhaitez que les travaux de sauvegarde toostop hello et supprimez des points de récupération hello - nom hello du type d’élément de hello.

    ![Arrêter la vérification](./media/backup-azure-manage-vms/item-verification-box.png)

    Si vous n’êtes pas sûr du nom de l’élément hello, pointez sur le nom de hello tooview hello point d’exclamation. En outre, le nom hello d’élément de hello est sous **arrêter la sauvegarde** haut hello du Panneau de hello.
4. Vous pouvez, si vous le souhaitez, indiquer une **Raison** ou un **Commentaire**.
5. Cliquez sur le travail de sauvegarde toostop hello pour l’élément en cours de hello, ![sauvegarde bouton d’arrêt](./media/backup-azure-manage-vms/stop-backup-button-blue.png)

    Un message de notification vous informe des travaux de sauvegarde hello ont été arrêtés.

    ![Confirmation l’arrêt de la protection](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a>Reprendre la protection d’une machine virtuelle
Si hello **conserver les données de sauvegarde** option choisie lors de la protection pour la machine virtuelle de hello a été arrêtée, il est possible de tooresume protection. Si hello **supprimer les données de sauvegarde** option a été choisie, puis ne peut pas reprendre la protection pour la machine virtuelle de hello.

protection tooresume pour la machine virtuelle de hello

1. Sur hello [tableau de bord coffre](backup-azure-manage-vms.md#open-a-vault-item-dashboard), cliquez sur **reprendre la sauvegarde**.

    ![Reprendre la protection](./media/backup-azure-manage-vms/resume-backup-button.png)

    Panneau de la stratégie de sauvegarde Hello s’ouvre.

   > [!NOTE]
   > Lors de la nouvelle protection hello virtual machine, vous pouvez choisir une autre stratégie que stratégie hello avec laquelle machine virtuelle a été initialement protégée.
   >
   >
2. Suivez les étapes de hello dans [gérer les stratégies de sauvegarde](backup-azure-manage-vms.md#manage-backup-policies) stratégie de hello tooassign pour la machine virtuelle de hello.

    Une fois appliqué toohello virtual machine, stratégie de sauvegarde hello vous consultez hello message suivant.

    ![Machine virtuelle protégée](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a>Suppression des données de sauvegarde
Vous pouvez supprimer les données de sauvegarde hello associées à un ordinateur virtuel pendant hello **arrêter la sauvegarde** travail, ou à tout moment après hello du travail de sauvegarde est terminée. Il peut même être bénéfiques toowait jours ou semaines avant de supprimer des points de récupération hello. Contrairement à la restauration des points de récupération, lors de la suppression des données de sauvegarde, vous ne pouvez pas choisir toodelete de points de récupération spécifique. Si vous choisissez toodelete vos données de sauvegarde, vous supprimez tous les points de récupération associés à des éléments de hello.

Hello procédure suivante suppose que le travail de sauvegarde hello pour la machine virtuelle de hello a été arrêté ou désactivé. Une fois le travail de sauvegarde hello est désactivé, hello **reprendre la sauvegarde** et **supprimer la sauvegarde** options sont disponibles dans le tableau de bord coffre hello.

![Boutons Reprendre et Supprimer](./media/backup-azure-manage-vms/resume-delete-buttons.png)

toodelete les données de sauvegarde sur un ordinateur virtuel avec hello *sauvegarde désactivé*:

1. Sur hello [tableau de bord coffre](backup-azure-manage-vms.md#open-a-vault-item-dashboard), cliquez sur **supprimer la sauvegarde**.

    ![Type de machine virtuelle](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    Hello **supprimer les données de sauvegarde** panneau s’ouvre.

    ![Type de machine virtuelle](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. Nom de type hello de hello élément tooconfirm vous souhaitez que les points de récupération toodelete hello.

    ![Arrêter la vérification](./media/backup-azure-manage-vms/item-verification-box.png)

    Si vous n’êtes pas sûr du nom de l’élément hello, pointez sur le nom de hello tooview hello point d’exclamation. En outre, le nom hello d’élément de hello est sous **supprimer les données de sauvegarde** haut hello du Panneau de hello.
3. Vous pouvez, si vous le souhaitez, indiquer une **Raison** ou un **Commentaire**.
4. Cliquez sur les données de sauvegarde toodelete hello pour l’élément en cours de hello, ![sauvegarde bouton d’arrêt](./media/backup-azure-manage-vms/delete-button.png)

    Un message de notification vous informe des données de sauvegarde hello a été supprimées.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur la manière de recréer une machine virtuelle à partir d’un point de récupération, consultez [Restauration de machines virtuelles Azure](backup-azure-restore-vms.md). Si vous avez besoin d’informations sur la protection de vos machines virtuelles, consultez [tout d’abord rechercher : sauvegardez tooa de machines virtuelles de coffre Recovery Services](backup-azure-vms-first-look-arm.md). Pour plus d’informations sur la surveillance des événements, consultez [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md)(Surveiller les alertes des sauvegardes de machines virtuelles Azure).
