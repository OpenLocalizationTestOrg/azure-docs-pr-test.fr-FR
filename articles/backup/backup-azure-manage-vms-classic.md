---
title: les sauvegardes de machine virtuelle Azure aaaManage et analyse | Documents Microsoft
description: "Découvrez comment toomanage et analyse Azure virtual machine de sauvegardes"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 4372944e-d33a-4f6a-bd5f-d04af2842713
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: trinadhk;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cb95e0b3760c96f7fd563c42cb4c635553f48957
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-common-azure-backup-jobs-and-trigger-alerts-in-hello-classic-portal"></a>Gérer les travaux de sauvegarde Azure courants et de déclencher des alertes dans le portail classique de hello
> [!div class="op_single_selector"]
> * [Gestion des sauvegardes de machines virtuelles Azure](backup-azure-manage-vms.md)
> * [Gestion des sauvegardes de machines virtuelles classiques](backup-azure-manage-vms-classic.md)
>
>

Cet article fournit des informations sur les tâches de gestion et de surveillance courantes des machines virtuelles déployées avec le modèle Classic protégées dans Azure.  

> [!NOTE]
> Azure dispose de deux modèles de déploiement pour créer et utiliser des ressources : [Azure Resource Manager et Azure Classic](../azure-resource-manager/resource-manager-deployment-model.md). Consultez [préparer votre tooback environnement des machines virtuelles](backup-azure-vms-prepare.md) pour plus d’informations sur l’utilisation de déploiement de classique des machines virtuelles de modèle.
>
> [!IMPORTANT]
>À partir de mars 2017, vous pouvez utiliser n’est plus les coffres de sauvegarde hello toocreate portail classique.
>
> Vous pouvez maintenant mettre à niveau vos archivages de sauvegarde coffres tooRecovery Services. Pour plus d’informations, voir l’article hello [mise à niveau d’un tooa de coffre de sauvegarde de coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft vous encourage tooupgrade coffres des Services tooRecovery les coffres de votre sauvegarde.<br/> Après le 15 octobre 2017, vous ne pouvez pas utiliser les coffres de sauvegarde toocreate PowerShell. **D’ici au 1er novembre 2017** :
>- Tous les coffres de sauvegarde restants seront les coffres des Services de tooRecovery automatiquement mis à niveau.
>- Vous ne pourra plus être en mesure de tooaccess vos données de sauvegarde dans le portail classique de hello. Au lieu de cela, utilisez hello tooaccess portail Azure vos données de sauvegarde dans les coffres des Services de récupération.

## <a name="manage-protected-virtual-machines"></a>Gérer des machines virtuelles protégées
toomanage des ordinateurs virtuels protégés :

1. tooview et gérer les paramètres de sauvegarde pour un ordinateur virtuel, cliquez sur hello **éléments protégés** onglet.
2. Cliquez sur le nom hello un Hello de toosee élément protégé **détails de la sauvegarde** onglet, qui présente des informations sur la dernière sauvegarde de hello.

    ![Sauvegarde de machine virtuelle](./media/backup-azure-manage-vms/backup-vmdetails.png)
3. tooview et gérer les paramètres de stratégie de sauvegarde pour un ordinateur virtuel, cliquez sur hello **stratégies** onglet.

    ![Stratégie de machine virtuelle](./media/backup-azure-manage-vms/manage-policy-settings.png)

    Hello **stratégies de sauvegarde** onglet affiche hello de stratégie existante. Vous pouvez la modifier en fonction de vos besoins. Si vous avez besoin d’une nouvelle stratégie de toocreate cliquez sur **créer** sur hello **stratégies** page. Notez que si vous souhaitez tooremove une stratégie qu’il ne doit pas avoir toutes les machines virtuelles associées.

    ![Stratégie de machine virtuelle](./media/backup-azure-manage-vms/backup-vmpolicy.png)
4. Vous pouvez obtenir plus d’informations sur l’état ou les actions pour un ordinateur virtuel sur hello **travaux** page. Cliquez sur une tâche dans hello liste tooget davantage de détails ou filtre les travaux pour un ordinateur virtuel spécifique.

    ![Tâches](./media/backup-azure-manage-vms/backup-job.png)

## <a name="on-demand-backup-of-a-virtual-machine"></a>Sauvegarde à la demande d’une machine virtuelle
Vous pouvez effectuer une sauvegarde à la demande d’une machine virtuelle une fois que celle-ci est configurée pour la protection. Si la sauvegarde initiale hello est en attente pour l’ordinateur virtuel de hello, sauvegarde créera une copie complète de la machine virtuelle de hello dans le coffre de sauvegarde Azure. Si la première sauvegarde est terminée, à la demande de sauvegarde aura uniquement l’envoi des modifications à partir de la sauvegarde tooAzure sauvegarde précédente de coffre autrement dit, il est toujours incrémentiel.

> [!NOTE]
> Durée de rétention d’une sauvegarde à la demande est valeur tooretention spécifiée pour le délai de rétention quotidienne toohello correspondante de stratégie de sauvegarde virtuelle.  
>
>

sauvegarde tootake une demande d’un ordinateur virtuel :

1. Accédez toohello **éléments protégés** page et sélectionnez **Machine virtuelle Azure** en tant que **Type** (le cas échéant), puis cliquez sur **sélectionnez**bouton.

    ![Type de machine virtuelle](./media/backup-azure-manage-vms/vm-type.png)
2. Sélectionnez la machine virtuelle hello sur lequel vous souhaitez tootake une demande de sauvegarde et cliquez sur **sauvegarder maintenant** bouton bas hello de page de hello.

    ![Sauvegarder maintenant](./media/backup-azure-manage-vms/backup-now.png)

    Cela crée un travail de sauvegarde sur l’ordinateur virtuel de hello sélectionné. Durée de rétention du point de récupération créé via ce travail sera identique à celui spécifié dans la stratégie hello associé avec l’ordinateur virtuel de hello.

    ![Création du travail de sauvegarde](./media/backup-azure-manage-vms/creating-job.png)

   > [!NOTE]
   > stratégie de hello tooview associé à un ordinateur virtuel, exploration vers le bas dans la machine virtuelle dans hello **éléments protégés** page et l’onglet de stratégie toobackup accédez.
   >
   >
3. Une fois le travail de hello est créé, vous pouvez cliquer sur **afficher le travail** bouton toast hello barre la tâche de hello toosee correspondante dans la page des travaux hello.

    ![Travail de sauvegarde créé](./media/backup-azure-manage-vms/created-job.png)
4. Après l’achèvement réussi de la tâche de hello, un point de récupération sera créé que vous pouvez utiliser toorestore hello virtual machine. Cela permet également d’incrémenter la valeur de la colonne de hello de point de récupération par 1 dans **éléments protégés** page.

## <a name="stop-protecting-virtual-machines"></a>Arrêt de la protection des machines virtuelles
Vous pouvez choisir toostop hello futures sauvegardes d’une machine virtuelle avec hello options suivantes :

* Conserver les données de sauvegarde associées à la machine virtuelle dans l’archivage de sauvegarde Azure
* Supprimer les données de sauvegarde associées à la machine virtuelle

Si vous avez sélectionné des données de sauvegarde tooretain associées avec l’ordinateur virtuel, vous pouvez utiliser hello les données de sauvegarde toorestore hello virtual machine. Pour connaître les détails de la tarification de ces machines virtuelles, cliquez [ici](https://azure.microsoft.com/pricing/details/backup/).

protection tooStop pour un ordinateur virtuel :

1. Accédez trop**éléments protégés** page et sélectionnez **machine virtuelle Azure** en tant que type de filtre hello (le cas échéant), puis cliquez sur **sélectionnez** bouton.

    ![Type de machine virtuelle](./media/backup-azure-manage-vms/vm-type.png)
2. Sélectionnez l’ordinateur virtuel de hello et cliquez sur **arrêter la Protection** bas hello de page de hello.

    ![Arrêter la protection](./media/backup-azure-manage-vms/stop-protection.png)
3. Par défaut, Azure Backup ne supprime pas les données de sauvegarde hello associées avec l’ordinateur virtuel de hello.

    ![Confirmation l’arrêt de la protection](./media/backup-azure-manage-vms/confirm-stop-protection.png)

    Si vous souhaitez que les données de sauvegarde toodelete, sélectionnez la case hello.

    ![Case à cocher](./media/backup-azure-manage-vms/checkbox.png)

    Sélectionnez la raison de l’arrêt de la sauvegarde de hello. Bien que cela soit facultatif, fournir une raison aideront toowork Azure Backup sur les commentaires hello et hiérarchiser les scénarios de client hello.
4. Cliquez sur **Submit** hello toosubmit de bouton **arrêter la protection** travail. Cliquez sur **afficher le travail** toosee hello travail hello correspondant dans **travaux** page.

    ![Arrêter la protection](./media/backup-azure-manage-vms/stop-protect-success.png)

    Si vous n’avez pas sélectionné **supprimer les données de sauvegarde associées** option pendant **arrêter la Protection** Assistant, puis sur Poste de travail terminé, de protection devient trop**Protection arrêtée**. les données de salutation restent avec Azure Backup jusqu'à ce qu’il est supprimé explicitement. Vous pouvez toujours supprimer les données de salutation en sélectionnant la machine virtuelle de hello Bonjour **éléments protégés** page, en cliquant sur **supprimer**.

    ![Protection arrêtée](./media/backup-azure-manage-vms/protection-stopped-status.png)

    Si vous avez sélectionné hello **supprimer les données de sauvegarde associées** option, hello machine virtuelle ne seront pas partie de hello **éléments protégés** page.

## <a name="re-protect-virtual-machine"></a>Application d’une nouvelle protection à la machine virtuelle
Si vous n’avez pas sélectionné de hello **les données de sauvegarde associer Delete** option dans **arrêter la Protection**, vous pouvez protéger de nouveau hello virtual machine en suivant toobacking similaire de hello suit les inscrit virtuel machines. Une fois protégé, cet ordinateur virtuel, les données de sauvegarde conservées toostop préalable la protection est et points de récupération créé après la protéger de nouveau.

Protégez de nouveau après l’état de protection de l’ordinateur virtuel de hello est modifiée trop**protégé** s’il existe des points de récupération antérieurs trop**arrêter la Protection**.

  ![Machine virtuelle à nouveau protégée](./media/backup-azure-manage-vms/reprotected-status.png)

> [!NOTE]
> Lors de la nouvelle protection hello virtual machine, vous pouvez choisir une autre stratégie que stratégie hello avec laquelle machine virtuelle a été initialement protégée.
>
>

## <a name="unregister-virtual-machines"></a>Annulation de l’inscription des machines virtuelles
Si vous souhaitez virtuels tooremove hello hello coffre de sauvegarde :

1. Cliquez sur hello **UNREGISTER** bouton bas hello de page de hello.

    ![Désactiver la protection](./media/backup-azure-manage-vms/unregister-button.png)

    Une notification toast s’affiche en bas hello d’écran hello demander la confirmation. Cliquez sur **Oui** toocontinue.

    ![Désactiver la protection](./media/backup-azure-manage-vms/confirm-unregister.png)

## <a name="delete-backup-data"></a>Suppression des données de sauvegarde
Vous pouvez supprimer les données de sauvegarde hello associées à un ordinateur virtuel, soit :

* Au cours du travail Arrêter la protection
* Après la fin du travail d’arrêt de la protection sur une machine virtuelle

toodelete les données de sauvegarde sur un ordinateur virtuel, qui se trouve dans hello *Protection arrêtée* état valider la réussite d’une **arrêter la sauvegarde** travail :

1. Accédez toohello **éléments protégés** page et sélectionnez **Machine virtuelle Azure** en tant que *type* et cliquez sur hello **sélectionnez** bouton.

    ![Type de machine virtuelle](./media/backup-azure-manage-vms/vm-type.png)
2. Sélectionnez la machine virtuelle de hello. machine virtuelle de Hello sera dans **Protection arrêtée** état.

    ![Protection arrêtée](./media/backup-azure-manage-vms/protection-stopped-b.png)
3. Cliquez sur hello **supprimer** bouton bas hello de page de hello.

    ![Supprimer la sauvegarde](./media/backup-azure-manage-vms/delete-backup.png)
4. Bonjour **supprimer les données de sauvegarde** Assistant, sélectionnez un motif pour la suppression des données de sauvegarde (hautement recommandées), cliquez sur **Submit**.

    ![Supprimer les données de sauvegarde](./media/backup-azure-manage-vms/delete-backup-data.png)
5. Cela va créer un travail toodelete sauvegarde de données de la machine virtuelle sélectionnée. Cliquez sur **afficher le travail** toosee la tâche correspondante dans la page tâches.

    ![Suppression de données réussie](./media/backup-azure-manage-vms/delete-data-success.png)

    Une fois le travail de hello est terminé, hello entrée de machine virtuelle de toohello correspondante sera retiré **éléments protégés** page.

## <a name="dashboard"></a>tableau de bord
Sur hello **tableau de bord** page, vous pouvez consulter des informations sur les machines virtuelles, de leur stockage et les travaux qui s’y rapportent dans hello des dernières 24 heures. Vous pouvez afficher l’état de la sauvegarde et les éventuelles erreurs de sauvegarde associées.

![tableau de bord](./media/backup-azure-manage-vms/dashboard-protectedvms.png)

> [!NOTE]
> Les valeurs dans le tableau de bord hello sont actualisés toutes les 24 heures.
>
>

## <a name="auditing-operations"></a>Audit des opérations
Azure backup offre la révision de hello « journaux des opérations « des opérations de sauvegarde déclenchées par le client hello rend facile toosee exactement les opérations de gestion ont été effectuées sur le coffre de sauvegarde hello. Journaux des opérations d’audit prise en charge des opérations de sauvegarde hello et activer excellent post-mortem.

Hello opérations suivantes est consignée dans les journaux des opérations :

* S’inscrire
* Unregister 
* Configurer la protection
* Sauvegarde (planifiée et à la demande via BackupNow)
* Restauration
* Arrêter la protection
* Supprimer les données de sauvegarde
* Add policy
* Supprimer la stratégie
* Mettre à jour la stratégie
* Annuler le travail

tooview opération enregistre le coffre de sauvegarde tooa correspondante :

1. Accédez trop**des services de gestion** dans le portail Azure, puis cliquez sur hello **journaux des opérations** onglet.

    ![Journaux des opérations](./media/backup-azure-manage-vms/ops-logs.png)
2. Dans les filtres de hello, sélectionnez **sauvegarde** en tant que *Type* et spécifiez le nom de coffre de sauvegarde hello dans *nom du service* , puis cliquez sur **Submit**.

    ![Filtre des journaux des opérations](./media/backup-azure-manage-vms/ops-logs-filter.png)
3. Dans les journaux des opérations de hello, sélectionnez n’importe quelle opération, puis cliquez sur **détails** toosee détails opération tooan correspondante.

    ![Détails de l’extraction des journaux d’opérations](./media/backup-azure-manage-vms/ops-logs-details.png)

    Hello **Assistant de détails** contient des informations sur l’opération de hello déclenchée, tâche, Id de ressource sur lequel cette opération est déclenchée et l’heure de début de l’opération de hello.

    ![Détails de l'opération](./media/backup-azure-manage-vms/ops-logs-details-window.png)

## <a name="alert-notifications"></a>Notifications d’alerte
Vous pouvez obtenir des notifications d’alerte personnalisées pour les travaux de hello dans le portail. Pour cela, vous devez définir des règles d’alerte basées sur PowerShell sur les événements de journaux des opérations. Nous vous recommandons d’utiliser *PowerShell version 1.3.0 ou version ultérieure*.

toodefine un tooalert de notification personnalisée pour les échecs de sauvegarde, un exemple de commande doit ressembler à :

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.Backup/backupVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/microsoft.backupbvtd2/BackupVault/trinadhVault -Actions $actionEmail
```

**ResourceId**: vous pouvez obtenir cela à partir de la fenêtre contextuelle Journaux des opérations, comme indiqué dans la section ci-dessus. ResourceUri dans la fenêtre contextuelle de détails d’une opération est hello ResourceId toobe est fournie pour cette applet de commande.

**NomOpération**: il s’agit du format de hello « Microsoft.Backup/backupvault/<EventName>» où EventName est inscrire, désinscrire, ConfigureProtection, sauvegarde, restauration, StopProtection, DeleteBackupData, CreateProtectionPolicy, DeleteProtectionPolicy, UpdateProtectionPolicy

**État**: les valeurs prises en charge sont Démarré, Réussi et Échec.

**Le groupe de ressources**: le groupe de ressources de ressource hello sur lequel l’opération est déclenchée. Vous pouvez l’obtenir à partir de la valeur ResourceId. Valeur comprise entre les champs */resourceGroups/* et */providers/* dans ResourceId valeur est hello pour le groupe de ressources.

**Nom**: nom de la règle d’alerte de hello.

**CustomEmail**: spécifiez toowhich d’adresse e-mail personnalisé hello souhaité toosend notification d’alerte

**SendToServiceOwners**: cette option envoie la notification d’alerte tooall administrateurs et coadministrateurs d’abonnement de hello. Elle peut être utilisée dans l’applet de commande **New-AzureRmAlertRuleEmail** .

### <a name="limitations-on-alerts"></a>Limitations sur les alertes
Alertes basées sur les événements sont soumis toohello limites suivantes :

1. Des alertes sont déclenchées sur tous les ordinateurs virtuels dans le coffre de sauvegarde hello. Vous ne pouvez pas personnaliser tooget des alertes pour un ensemble spécifique d’ordinateurs virtuels dans un coffre de sauvegarde.
2. Cette fonctionnalité est en version préliminaire. [En savoir plus](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. Vous recevez des alertes de « alerts-noreply@mail.windowsazure.com ». Actuellement, vous ne pouvez pas modifier expéditeur du courrier électronique hello.

## <a name="next-steps"></a>Étapes suivantes
* [Restauration de machines virtuelles Azure](backup-azure-restore-vms.md)
