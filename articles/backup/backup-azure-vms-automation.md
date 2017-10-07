---
title: "aaaDeploy et gérer des sauvegardes pour les machines virtuelles déployées par le Gestionnaire de ressources à l’aide de PowerShell | Documents Microsoft"
description: "Utilisez PowerShell toodeploy et gérer des sauvegardes dans Azure pour les machines virtuelles déployées par le Gestionnaire de ressources"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 68606e4f-536d-4eac-9f80-8a198ea94d52
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/28/2017
ms.author: markgal;trinadhk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486fb3ae1902403fe6bf303df57244b76677ab17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azurermrecoveryservicesbackup-cmdlets-tooback-up-virtual-machines"></a>Utilisez tooback d’applets de commande AzureRM.RecoveryServices.Backup des machines virtuelles
> [!div class="op_single_selector"]
> * [Gestionnaire de ressources](backup-azure-vms-automation.md)
> * [Classique](backup-azure-vms-classic-automation.md)
>
>

Cet article explique comment tooback d’applets de commande de Azure PowerShell toouse haut et récupérer une machine virtuelle (VM) Azure à partir des Services de récupération de coffre. Un coffre Recovery Services est une ressource Azure Resource Manager et les données de tooprotect utilisés et des ressources dans Azure Backup et Azure Site Recovery services. Vous pouvez utiliser un tooprotect de coffre Recovery Services déployés au Gestionnaire des services Azure de machines virtuelles et les machines virtuelles de déploiement d’Azure Resource Manager.

> [!NOTE]
> Azure dispose de deux modèles de déploiement pour créer et utiliser des ressources : [Azure Resource Manager et Azure Classic](../azure-resource-manager/resource-manager-deployment-model.md). Cet article est pour une utilisation avec des machines virtuelles créées à l’aide du modèle de gestionnaire de ressources hello.
>
>

Cet article vous guide à l’aide de PowerShell tooprotect une machine virtuelle et restaurer des données à partir d’un point de récupération.

## <a name="concepts"></a>Concepts
Si vous n’êtes pas familiarisé avec hello service Azure Backup, pour une vue d’ensemble du service de hello, extraire [Nouveautés d’Azure Backup ?](backup-introduction-to-azure-backup.md) Avant de commencer, assurez-vous que vous couvrent essentials hello sur toowork de conditions préalables nécessaires hello avec Azure Backup et hello limitations de la solution de sauvegarde de machine virtuelle en cours hello.

toouse PowerShell efficacement, il est nécessaire toounderstand hello hiérarchie d’objets à partir de laquelle toostart.

![Hiérarchie des objets dans Recovery Services](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

tooview hello référence d’applet de commande PowerShell de AzureRm.RecoveryServices.Backup, consultez hello [Azure Backup - applets de commande de Services de récupération](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) Bonjour bibliothèque Azure.

## <a name="setup-and-registration"></a>Installation et inscription
toobegin :

1. [Télécharger la version la plus récente de PowerShell hello](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (hello version minimale requise est : 1.4.0)
2. Trouver hello Azure sauvegarde applets de commande PowerShell disponibles en tapant hello de commande suivante :

```
PS C:\> Get-Command *azurermrecoveryservices*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmRecoveryServicesBackupItem           1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Disable-AzureRmRecoveryServicesBackupProtection    1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Enable-AzureRmRecoveryServicesBackupProtection     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupContainer         1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupItem              1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupJob               1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupJobDetails        1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupManagementServer  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupProperties        1.4.0      AzureRM.RecoveryServices
Cmdlet          Get-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRMRecoveryServicesBackupRecoveryPoint     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupRetentionPolic... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupSchedulePolicy... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesVault                   1.4.0      AzureRM.RecoveryServices
Cmdlet          Get-AzureRmRecoveryServicesVaultSettingsFile       1.4.0      AzureRM.RecoveryServices
Cmdlet          New-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          New-AzureRmRecoveryServicesVault                   1.4.0      AzureRM.RecoveryServices
Cmdlet          Remove-AzureRmRecoveryServicesProtectionPolicy     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Remove-AzureRmRecoveryServicesVault                1.4.0      AzureRM.RecoveryServices
Cmdlet          Restore-AzureRMRecoveryServicesBackupItem          1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Set-AzureRmRecoveryServicesBackupProperties        1.4.0      AzureRM.RecoveryServices
Cmdlet          Set-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Set-AzureRmRecoveryServicesVaultContext            1.4.0      AzureRM.RecoveryServices
Cmdlet          Stop-AzureRmRecoveryServicesBackupJob              1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Unregister-AzureRmRecoveryServicesBackupContainer  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Unregister-AzureRmRecoveryServicesBackupManagem... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Wait-AzureRmRecoveryServicesBackupJob              1.4.0      AzureRM.RecoveryServices.Backup
```


Bonjour tâches suivantes peut être automatisée avec PowerShell :

* Créer un coffre Recovery Services
* Sauvegarder des machines virtuelles Azure
* Déclencher une tâche de sauvegarde
* Surveiller une tâche de sauvegarde
* Restauration d’une machine virtuelle Azure

## <a name="create-a-recovery-services-vault"></a>Créer un coffre Recovery Services
Hello suit vous guide lors de la création d’un coffre Recovery Services. Un coffre Recovery Services diffère d’un coffre de sauvegarde.

1. Si vous utilisez Azure Backup pour hello première fois, vous devez utiliser hello  **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)**  fournisseur de Service de récupération Azure hello applet de commande tooregister avec votre abonnement.

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. Hello coffre Recovery Services est une ressource de gestionnaire de ressources, vous devez donc tooplace dans un groupe de ressources. Vous pouvez utiliser un groupe de ressources existant ou créer un groupe de ressources avec hello  **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)**  applet de commande. Lorsque vous créez un groupe de ressources, spécifiez le nom de hello et un emplacement pour le groupe de ressources hello.  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. Hello d’utilisation  **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)**  hello de toocreate d’applet de commande de coffre Recovery Services. Veillez à toospecify hello même emplacement pour le coffre hello que celui utilisé pour le groupe de ressources hello.

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. Spécifiez le type hello de toouse de redondance de stockage ; Vous pouvez utiliser [stockage localement redondant (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) ou [stockage redondant de géo-réplication (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage). Hello suivant montre testvault hello BackupStorageRedundancy - option est la valeur tooGeoRedundant.

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > Nombreuses applets de commande Azure Backup nécessitent l’objet de coffre Recovery Services hello en tant qu’entrée. Pour cette raison, il est pratique toostore hello Services de récupération de sauvegarde coffre objet dans une variable.
   >
   >

## <a name="view-hello-vaults-in-a-subscription"></a>Affichage des coffres de hello dans un abonnement
Utilisez  **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)**  liste de hello tooview de tous les coffres dans l’abonnement actif de hello. Vous pouvez utiliser cette toocheck commande qu’un nouvel archivage a été créé ou toosee hello coffres disponibles dans l’abonnement de hello.

Exécutez la commande hello, Get-AzureRmRecoveryServicesVault, tooview tous les coffres dans l’abonnement de hello. Hello suivant montre les informations de hello affichées pour chaque archivage.

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="back-up-azure-vms"></a>Sauvegarder des machines virtuelles Azure
Utilisez un tooprotect de coffre Recovery Services vos machines virtuelles. Avant d’appliquer une protection hello, définir le contexte du coffre hello (type hello des données protégées dans le coffre hello) et vérifiez la stratégie de protection hello. stratégie de protection Hello est planification hello lors de l’exécution de travaux de sauvegarde hello et la durée de conservation de chaque instantané de sauvegarde.

### <a name="set-vault-context"></a>Définir le contexte du coffre
Avant d’activer la protection sur un ordinateur virtuel, utilisez  **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  contexte de coffre tooset hello. Une fois que le contexte de coffre hello est définie, elle s’applique tooall applets de commande suivantes. exemple Hello définit contexte de coffre hello pour le coffre hello, *testvault*.

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a>Création d’une stratégie de protection
Quand vous créez un coffre Recovery Services, il est fourni avec des stratégies de protection et de conservation par défaut. stratégie de protection par défaut Hello déclenche une opération de sauvegarde chaque jour à une heure spécifiée. stratégie de rétention par défaut Hello conserve le point de récupération quotidien hello pendant 30 jours. Vous pouvez utiliser la valeur par défaut hello stratégie tooquickly protéger votre machine virtuelle et la stratégie hello ultérieurement avec les détails de l’autres.

Utilisez  **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)**  tooview des stratégies de protection hello dans le coffre hello. Vous pouvez utiliser cette applet de commande tooget une stratégie spécifique, ou les stratégies de hello tooview associées à un type de charge de travail. Bonjour à l’exemple suivant obtient les stratégies pour le type de charge de travail, AzureVM.

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> fuseau horaire de Hello du champ de BackupTime hello dans PowerShell est UTC. Toutefois, lorsque les temps de sauvegarde hello sont affiché dans hello portail Azure, les temps de hello sont fuseau horaire local de tooyour ajustée.
>
>

Une stratégie de protection de la sauvegarde est associée à au moins une stratégie de rétention. La stratégie de conservation définit la durée de conservation d’un point de restauration avant sa suppression. Utilisez  **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)**  stratégie de rétention par défaut tooview hello.  De même, vous pouvez utiliser  **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)**  stratégie de planification par défaut tooobtain hello. Hello  **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  applet de commande crée un objet PowerShell qui contient des informations de stratégie de sauvegarde. Hello objets de stratégie de planification et de rétention sont utilisés comme entrées toohello  **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  applet de commande. Hello exemple suivant stocke hello planification hello politique de rétention et de variables. exemple de Hello utilise ces variables de paramètres de hello toodefine lors de la création d’une stratégie de protection, *NewPolicy*.

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a>Activer la protection
Une fois que vous avez défini la stratégie de protection des sauvegardes hello, vous devez toujours activer stratégie hello pour un élément. Utilisez  **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)**  tooenable protection. Activation de la protection nécessite deux objets - élément de hello et stratégie de hello. Une fois que la stratégie de hello a été associé au coffre de hello, flux de travail sauvegarde hello est déclenchée au moment de hello définie dans la planification de la stratégie hello.

Hello suivant l’exemple permet de protection pour l’élément hello, V2VM, à l’aide de la stratégie de hello, NewPolicy. protection de hello tooenable sur des machines virtuelles Resource Manager non chiffré

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

protection de hello tooenable sur chiffré (chiffrées à l’aide de BEK et KEK) de machines virtuelles, vous devez clés tooread autorisation du service Azure Backup toogive hello et les secrets à partir du coffre de clés.

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

protection de hello tooenable sur chiffré machines virtuelles (chiffrés à l’aide de BEK uniquement), vous devez toogive hello Azure Backup service autorisation tooread des secrets à partir du coffre de clés.

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> Si vous utilisez un cloud d’Azure Government hello, utilisez hello valeur ff281ffe-705c-4f53-9f37-a40e6f2c68f3 pour le paramètre hello **- ServicePrincipalName** dans [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) applet de commande .
>
>

Pour les machines virtuelles Classic

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a>Modifier une stratégie de protection
stratégie de protection toomodify hello, utilisez [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) toomodify hello SchedulePolicy ou RetentionPolicy objets.

Hello exemple suivant change hello recovery point rétention too365 jours.

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a>Déclencher une sauvegarde
Vous pouvez utiliser  **[sauvegarde-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)**  tootrigger un travail de sauvegarde. S’il s’agit de sauvegarde initiale de hello, il est une sauvegarde complète. Les sauvegardes suivantes prennent une copie incrémentielle. Être vraiment toouse  **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  tooset contexte de coffre hello avant de déclencher l’opération de sauvegarde hello. Bonjour à l’exemple suivant suppose coffre contexte a été défini.

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> fuseau horaire de Hello de champs de StartTime et EndTime hello dans PowerShell est UTC. Toutefois, lorsque l’heure de hello est affichée dans hello portail Azure, les temps de hello sont fuseau horaire local de tooyour ajustée.
>
>

## <a name="monitoring-a-backup-job"></a>Surveillance d’une tâche de sauvegarde
Vous pouvez surveiller les opérations longues, telles que les travaux de sauvegarde, sans utiliser de hello portail Azure. état de hello tooget d’une tâche en cours d’exécution, utilisez hello  **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)**  applet de commande. Cette applet de commande Obtient les travaux de sauvegarde hello pour un archivage spécifique, et ce coffre est spécifié dans le contexte de coffre hello. Bonjour exemple suivant obtient l’état de hello d’un travail en cours d’exécution sous forme de tableau et stocke l’état de hello dans la variable de hello $joblist.

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

Au lieu de l’interrogation de ces travaux pour la saisie semi-automatique, qui est un code superflu supplémentaire - utilisez hello  **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  applet de commande. Cette applet de commande suspend l’exécution de hello qu’hello tâche se termine ou hello spécifié la valeur de délai d’attente est atteinte.

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a>Restauration d’une machine virtuelle Azure
Il existe une différence fondamentale entre hello restauration d’une machine virtuelle à l’aide de hello portail Azure et la restauration d’une machine virtuelle à l’aide de PowerShell. Avec PowerShell, hello restauration est terminée une fois que les disques hello et les informations de configuration de point de récupération hello sont créés.

> [!NOTE]
> opération de restauration Hello ne crée pas d’un ordinateur virtuel.
>
>

toocreate un ordinateur virtuel à partir du disque, consultez la section hello [hello créer machine virtuelle à partir de disques stockées](backup-azure-vms-automation.md#create-a-vm-from-stored-disks). étapes de base de Hello toorestore une machine virtuelle Azure sont les suivantes :

* Sélectionnez hello machine virtuelle
* Choisir un point de récupération
* Restaurer des disques de hello
* Créer hello machine virtuelle à partir de disques stockées

Hello graphique suivant illustre hello objet hiérarchie hello RecoveryServicesVault toohello BackupRecoveryPoint vers le bas.

![Hiérarchie d’objets Recovery Services montrant BackupContainer](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

toorestore les données de sauvegarde, identifier l’élément de sauvegarde hello hello point de récupération et qui conserve les données de point-à-temps hello. Hello d’utilisation  **[restauration-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  données toorestore applet de commande hello coffre toohello du compte client.

### <a name="select-hello-vm"></a>Sélectionnez hello machine virtuelle
tooget hello PowerShell objet qui identifie hello droite sauvegarder élément démarrer à partir du conteneur hello dans le coffre hello et dont la hiérarchie d’objets hello. conteneur hello tooselect représentant hello machine virtuelle, utilisez hello  **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)**  applet de commande et redirigez cette toohello  **[ Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)**  applet de commande.

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a>Choisir un point de récupération
Hello d’utilisation  **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)**  toolist d’applet de commande points de récupération de tous les pour sauvegarder l’élément hello. Choisissez ensuite toorestore de point de récupération hello. Si vous ne savez pas quel toouse de point de récupération, il est une bonne approche en matière toochoose hello plus récente RecoveryPointType = point AppConsistent dans la liste de hello.

Bonjour le script suivant, hello variable, **$rp**, est un tableau de points de récupération pour hello sélectionné sauvegarder l’élément, à partir de hello sept derniers jours. tableau de Hello est trié dans l’ordre inverse de temps avec le dernier point de récupération hello à l’index 0. Utiliser le tableau PowerShell standard, l’indexation de point de récupération toopick hello. Dans l’exemple de hello, $rp [0] sélectionne le dernier point de récupération hello.

```
PS C:\> $startDate = (Get-Date).AddDays(-7)
PS C:\> $endDate = Get-Date
PS C:\> $rp = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $backupitem -StartDate $startdate.ToUniversalTime() -EndDate $enddate.ToUniversalTime()
PS C:\> $rp[0]
RecoveryPointAdditionalInfo :
SourceVMStorageType         : NormalStorage
Name                        : 15260861925810
ItemName                    : VM;iaasvmcontainer;RGName1;V2VM
RecoveryPointId             : /subscriptions/XX/resourceGroups/ RGName1/providers/Microsoft.RecoveryServices/vaults/testvault/backupFabrics/Azure/protectionContainers/IaasVMContainer;iaasvmcontainer;RGName1;V2VM/protectedItems/VM;iaasvmcontainer; RGName1;V2VM/recoveryPoints/15260861925810
RecoveryPointType           : AppConsistent
RecoveryPointTime           : 4/23/2016 5:02:04 PM
WorkloadType                : AzureVM
ContainerName               : IaasVMContainer;iaasvmcontainer; RGName1;V2VM
ContainerType               : AzureVM
BackupManagementType        : AzureVM
```



### <a name="restore-hello-disks"></a>Restaurer des disques de hello
Hello d’utilisation  **[restauration-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  toorestore de l’applet de commande les données d’un élément de sauvegarde et configuration tooa point de récupération. Une fois que vous avez identifié un point de récupération, utilisez-le comme valeur de hello pour hello **- RecoveryPoint** paramètre. Hello précédent exemple de code, **$rp [0]** a été toouse de point de récupération hello. Bonjour suivant l’exemple de code, **$rp [0]** est hello toouse de point de récupération pour la restauration du disque de hello.

les disques toorestore hello et les informations de configuration :

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

Hello d’utilisation  **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  toowait d’applet de commande pour toocomplete de travail de restauration hello.

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

Une fois le travail de restauration hello est terminé, utilisez hello  **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)**  détails hello tooget Hello l’opération de restauration. Hello JobDetails propriété a toorebuild nécessaires hello VM de hello plus d’informations.

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

Une fois que vous restaurez les disques hello, accédez hello toohello suivant section toocreate machine virtuelle.

## <a name="create-a-vm-from-restored-disks"></a>Créer une machine virtuelle à partir de disques restaurés
Après avoir restauré les disques hello, utilisez ces étapes toocreate et configurer l’ordinateur virtuel de hello à partir du disque.

> [!NOTE]
> toocreate chiffré des machines virtuelles à partir de disques restaurés, votre rôle Azure doit avoir l’action de hello autorisation tooperform, **Microsoft.KeyVault/vaults/deploy/action**. Si votre rôle ne dispose pas de cette autorisation, créez un rôle personnalisé avec cette action. Pour plus d’informations, consultez [Rôles personnalisés dans le contrôle d’accès en fonction du rôle (RBAC) Azure](../active-directory/role-based-access-control-custom-roles.md).
>
>

1. Hello de requête restauré les propriétés du disque pour les détails de la tâche hello.

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. Définir le contexte du stockage Azure hello et restaurez le fichier de configuration JSON hello.

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. Utilisez configuration d’ordinateur virtuel hello JSON configuration fichier toocreate hello.

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. Attachez le disque du système d’exploitation hello et des disques de données. Selon la configuration de hello de vos machines virtuelles, cliquez sur hello lien pertinent tooview applets de commande respectifs : 
    - [Machines virtuelles non gérés, non chiffré](#non-managed-non-encrypted-vms)
    - [Machines virtuelles non gérés, chiffrés (BEK uniquement)](#non-managed-encrypted-vms-bek-only)
    - [Machines virtuelles non gérés, chiffrés (BEK et KEK)](#non-managed-encrypted-vms-bek-and-kek)
    - [Ordinateurs virtuels gérés, non chiffré](#managed-non-encrypted-vms)
    - [Ordinateurs virtuels gérés, chiffrés (BEK et KEK)](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a>Machines virtuelles non gérées et non chiffrées

    Utilisez hello suivant l’exemple pour les ordinateurs virtuels non géré, non chiffré.

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a>Machines virtuelles non managées et chiffrées (BEK uniquement)

    Pour chiffrés, non géré des ordinateurs virtuels (chiffrés à l’aide de BEK uniquement), vous avez besoin de coffre de clés secrètes toohello hello toorestore avant que vous pouvez attacher des disques. Pour plus d’informations, consultez l’article hello, [restaurer un ordinateur virtuel chiffré à partir d’un point de récupération Azure Backup](backup-azure-restore-key-secret.md). Hello suivant l’exemple montre le mode de chiffrement de tooattach du système d’exploitation et des disques de données pour les machines virtuelles.

    ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.storageProfile'.osDisk.vhd.uri -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.storageProfile'.osDisk.osType
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a>Machines virtuelles non managées et chiffrées (BEK et KEK)

    Non gérés, chiffrés machines virtuelles (chiffrées à l’aide de BEK et KEK), vous devez clé de hello toorestore et coffre de clés secrètes toohello avant que vous pouvez attacher des disques. Pour plus d’informations, consultez l’article hello, [restaurer un ordinateur virtuel chiffré à partir d’un point de récupération Azure Backup](backup-azure-restore-key-secret.md). Hello suivant l’exemple montre le mode de chiffrement de tooattach du système d’exploitation et des disques de données pour les machines virtuelles.

    ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $kekUrl = "https://ContosoKeyVault.vault.azure.net:443/keys/ContosoKey007/x9xxx00000x0000x9b9949999xx0x006"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.storageProfile'.osDisk.vhd.uri -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -KeyEncryptionKeyUrl $kekUrl -KeyEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.storageProfile'.osDisk.osType
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

    #### <a name="managed-non-encrypted-vms"></a>Machines virtuelles gérées et non chiffrées

    Non chiffrées machines virtuelles gérées, vous allez peut-être disques toocreate géré depuis le stockage blob et puis attachez les disques hello. Pour plus d’informations, consultez l’article hello, [attacher un tooa de disque de données machine virtuelle Windows à l’aide de PowerShell](../virtual-machines/windows/attach-disk-ps.md). Hello suivant l’exemple de code montre comment tooattach hello des disques de données pour les machines virtuelles gérées non chiffré.

    ```
    PS C:\> $storageType = "StandardLRS"
    PS C:\> $osDiskName = $vm.Name + "_osdisk"
    PS C:\> $osVhdUri = $obj.'properties.storageProfile'.osDisk.vhd.uri
    PS C:\> $diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $osVhdUri
    PS C:\> $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk $diskConfig -ResourceGroupName "test"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -CreateOption "Attach" -Windows
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $dataDiskName = $vm.Name + $dd.name ;
     $dataVhdUri = $dd.vhd.uri ;
     $dataDiskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $dataVhdUri ;
     $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $dataDiskConfig -ResourceGroupName "test" ;
     Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -ManagedDiskId $dataDisk2.Id -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="managed-encrypted-vms-bek-and-kek"></a>Machines virtuelles managées et chiffrées (BEK et KEK)

    Chiffrées machines virtuelles gérées (chiffrées à l’aide de BEK et KEK), vous allez peut-être disques toocreate géré depuis le stockage blob et puis attachez les disques hello. Pour plus d’informations, consultez l’article hello, [attacher un tooa de disque de données machine virtuelle Windows à l’aide de PowerShell](../virtual-machines/windows/attach-disk-ps.md). Hello exemple de code suivant montre comment tooattach hello des disques de données pour les machines virtuelles chiffrées gérées.

     ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $kekUrl = "https://ContosoKeyVault.vault.azure.net:443/keys/ContosoKey007/x9xxx00000x0000x9b9949999xx0x006"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> $storageType = "StandardLRS"
    PS C:\> $osDiskName = $vm.Name + "_osdisk"
    PS C:\> $osVhdUri = $obj.'properties.storageProfile'.osDisk.vhd.uri
    PS C:\> $diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $osVhdUri
    PS C:\> $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk $diskConfig -ResourceGroupName "test"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -KeyEncryptionKeyUrl $kekUrl -KeyEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $dataDiskName = $vm.Name + $dd.name ;
     $dataVhdUri = $dd.vhd.uri ;
     $dataDiskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $dataVhdUri ;
     $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $dataDiskConfig -ResourceGroupName "test" ;
     Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -ManagedDiskId $dataDisk2.Id -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

5. Définir des paramètres de réseau hello.

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. Créer un ordinateur virtuel de hello.

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a>Étapes suivantes
Si vous préférez toouse PowerShell tooengage avec vos ressources Azure, consultez l’article de PowerShell hello, [déployer et gérer Backup pour Windows Server](backup-client-automation.md). Si vous gérez les sauvegardes DPM, consultez l’article hello, [déployer et gérer la sauvegarde de DPM](backup-dpm-automation.md). Ces deux articles ont une version concernant les déploiements avec le modèle Resource Manager et le modèle Classic.  
