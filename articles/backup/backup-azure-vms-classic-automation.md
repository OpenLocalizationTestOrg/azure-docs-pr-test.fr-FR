---
title: "aaaDeploy et gérer la sauvegarde pour les machines virtuelles Azure à l’aide de PowerShell | Documents Microsoft"
description: "Découvrez comment toodeploy et gérer la sauvegarde Azure à l’aide de PowerShell."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 2e24b1d9-4375-4049-a28d-e3bc01152f32
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;trinadhk;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f3ecd3f94c5e3e8fc8018e8786302edd4847744b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azurermbackup-cmdlets-tooback-up-virtual-machines"></a>Utilisez tooback d’applets de commande AzureRM.Backup des machines virtuelles
> [!div class="op_single_selector"]
> * [Gestionnaire de ressources](backup-azure-vms-automation.md)
> * [Classique](backup-azure-vms-classic-automation.md)
>
>

Cet article vous montre comment toouse Azure PowerShell pour la sauvegarde et récupération des machines virtuelles Azure. Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : Resource Manager et classique. Cet article couvre l’utilisation de tooback de modèle de déploiement de classique hello de coffre de sauvegarde de données tooa. Si vous n’avez pas créé un coffre de sauvegarde dans votre abonnement, consultez la version du Gestionnaire de ressources hello de cet article, [tooback d’applets de commande AzureRM.RecoveryServices.Backup d’utilisation des machines virtuelles](backup-azure-vms-automation.md). Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.

> [!IMPORTANT]
> Vous pouvez maintenant mettre à niveau vos archivages de sauvegarde coffres tooRecovery Services. Pour plus d’informations, voir l’article hello [mise à niveau d’un tooa de coffre de sauvegarde de coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft vous encourage tooupgrade coffres des Services tooRecovery les coffres de votre sauvegarde.<br/> Après le 15 octobre 2017, vous ne pouvez pas utiliser les coffres de sauvegarde toocreate PowerShell. **D’ici au 1er novembre 2017** :
>- Tous les coffres de sauvegarde restants seront les coffres des Services de tooRecovery automatiquement mis à niveau.
>- Vous ne pourra plus être en mesure de tooaccess vos données de sauvegarde dans le portail classique de hello. Au lieu de cela, utilisez hello tooaccess portail Azure vos données de sauvegarde dans les coffres des Services de récupération.
>

## <a name="concepts"></a>Concepts
Cet article fournit des informations spécifique toohello applets de commande PowerShell utilisées tooback des machines virtuelles. Pour obtenir des informations sur la protection des machines virtuelles Azure, consultez [Planification de votre infrastructure de sauvegarde de machines virtuelles dans Azure](backup-azure-vms-introduction.md).

> [!NOTE]
> Avant de commencer, lisez hello [conditions préalables](backup-azure-vms-prepare.md) toowork requise avec Azure Backup et hello [limitations](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) de solution de sauvegarde de machine virtuelle en cours hello.
>
>

toouse PowerShell prendre efficacement, une hiérarchie de hello toounderstand moment des objets et à quel endroit toostart.

![Hiérarchie des objets](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

Bonjour deux flux les plus importants sont activer la protection sur une machine virtuelle et restaurer les données à partir d’un point de récupération. focus Hello de cet article est toohelp vous deviendriez performants pour travailler avec tooenable d’applets de commande PowerShell hello ces deux scénarios.

## <a name="setup-and-registration"></a>Installation et inscription
toobegin :

1. [Téléchargez la dernière version de PowerShell](https://github.com/Azure/azure-powershell/releases) (version minimale requise : 1.0.0)
2. Trouver hello Azure sauvegarde applets de commande PowerShell disponibles en tapant hello de commande suivante :

```
PS C:\> Get-Command *azurermbackup*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmBackupItem                           1.0.1      AzureRM.Backup
Cmdlet          Disable-AzureRmBackupProtection                    1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupContainerReregistration        1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupProtection                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupContainer                         1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupItem                              1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJob                               1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJobDetails                        1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupRecoveryPoint                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVaultCredentials                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupRetentionPolicyObject             1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Register-AzureRmBackupContainer                    1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupProtectionPolicy               1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupVault                          1.0.1      AzureRM.Backup
Cmdlet          Restore-AzureRmBackupItem                          1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Stop-AzureRmBackupJob                              1.0.1      AzureRM.Backup
Cmdlet          Unregister-AzureRmBackupContainer                  1.0.1      AzureRM.Backup
Cmdlet          Wait-AzureRmBackupJob                              1.0.1      AzureRM.Backup
```

Hello suivant le programme d’installation et tâches d’enregistrement peuvent être automatisées avec PowerShell :

* Créer un coffre de sauvegarde
* L’inscription d’ordinateurs virtuels de hello avec hello service Azure Backup

### <a name="create-a-backup-vault"></a>Créer un coffre de sauvegarde
> [!WARNING]
> Pour les clients à l’aide de la sauvegarde Azure pour hello première fois, vous devez tooregister hello Azure Backup fournisseur toobe utilisé avec votre abonnement. Cela est possible en exécutant hello de commande suivante : Register-AzureRmResourceProvider - ProviderNamespace « Microsoft.Backup »
>
>

Vous pouvez créer un coffre de sauvegarde à l’aide de hello **New-AzureRmBackupVault** applet de commande. coffre de sauvegarde Hello est une ressource ARM, par conséquent, vous devez tooplace dans un groupe de ressources. Dans une console Azure PowerShell avec élévation de privilèges, exécutez hello suivant de commandes :

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

Vous pouvez obtenir une liste de tous les coffres de sauvegarde hello dans un abonnement donné à l’aide de hello **Get-AzureRmBackupVault** applet de commande.

> [!NOTE]
> Il est pratique de toostore objet de coffre de sauvegarde hello dans une variable. objet de coffre Hello est nécessaire en tant qu’entrée de nombreuses applets de commande Azure Backup.
>
>

### <a name="registering-hello-vms"></a>L’inscription d’ordinateurs virtuels de hello
Hello première étape de configuration de sauvegarde avec Azure Backup est tooregister votre ordinateur ou une machine virtuelle avec un coffre Azure Backup. Hello **Register-AzureRmBackupContainer** applet de commande prend les informations d’entrée de hello d’une machine virtuelle Azure IaaS et inscrit avec le coffre hello spécifié. opération de Registre Hello associe hello machine virtuelle Azure avec le coffre de sauvegarde hello et assure le suivi hello machine virtuelle via le cycle de vie de sauvegarde hello.

L’inscription de votre machine virtuelle avec hello service Azure Backup crée un objet conteneur de niveau supérieur. Un conteneur contient généralement plusieurs éléments qui peuvent être sauvegardées, mais dans les cas de hello de machines virtuelles il y aura qu’un seul élément de sauvegarde pour le conteneur de hello.

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a>Sauvegarde des machines virtuelles Azure
### <a name="create-a-protection-policy"></a>Création d’une stratégie de protection
Il n’est pas obligatoire toocreate une nouvelle stratégie toostart la sauvegarde de protection de vos machines virtuelles. coffre de Hello est fourni avec un « stratégie par défaut' peut être utilisé tooquickly activer la protection, puis le modifier ultérieurement avec les informations de droite hello. Vous pouvez obtenir la liste des stratégies de hello disponibles dans le coffre hello à l’aide de hello **Get-AzureRmBackupProtectionPolicy** applet de commande :

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> fuseau horaire de Hello du champ de BackupTime hello dans PowerShell est UTC. Toutefois, lorsque les temps de sauvegarde hello sont affiché dans hello portail Azure, fuseau horaire de hello est alignée tooyour le système local, ainsi que le décalage de hello UTC.
>
>

Une stratégie de sauvegarde est associée à au moins une stratégie de rétention. stratégie de rétention Hello définit la durée pendant laquelle un point de récupération est conservé avec Azure Backup. Hello **New-AzureRmBackupRetentionPolicy** applet de commande crée les objets PowerShell qui contiennent les informations de stratégie de rétention. Ces objets de stratégie de rétention sont utilisés comme entrées toohello *New-AzureRmBackupProtectionPolicy* applet de commande, ou directement avec hello *Enable-AzureRmBackupProtection* applet de commande.

Une stratégie de sauvegarde définit quand et à quelle fréquence hello sauvegarde d’un élément est effectuée. Hello **New-AzureRmBackupProtectionPolicy** applet de commande crée un objet PowerShell qui contient des informations de stratégie de sauvegarde. stratégie de sauvegarde Hello est utilisée comme une entrée toohello *Enable-AzureRmBackupProtection* applet de commande.

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a>Activer la protection
L’activation de protection implique deux objets : hello élément et hello stratégie et les deux toohello de toobelong besoin même coffre. Une fois que la stratégie de hello a été associé avec un élément de hello, flux de travail sauvegarde hello lancera conformément au calendrier défini de hello.

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a>Sauvegarde initiale
planification de sauvegarde Hello s’occupe une copie initiale complète de hello pour l’élément de hello et hello incrémentielles pour les sauvegardes ultérieures hello. Toutefois, si vous souhaitez tooforce hello initiale sauvegarde toohappen à un moment donné ou même immédiatement utiliser hello **AzureRmBackupItem de sauvegarde** applet de commande :

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> Hello fuseau horaire de hello StartTime et EndTime les champs affichés dans PowerShell en UTC. Toutefois, lorsque des informations similaires hello sont affichées dans hello portail Azure, fuseau horaire de hello est alignée tooyour horloge du système local.
>
>

### <a name="monitoring-a-backup-job"></a>Surveillance d’une tâche de sauvegarde
La plupart des opérations longues dans Sauvegarde Azure sont reproduites en tant que tâche. Il est ainsi facile tootrack progression sans avoir tookeep hello ouvrir portail Azure en permanence.

état le plus récent hello tooget d’une tâche en cours d’exécution, utilisez hello **Get-AzureRmBackupJob** applet de commande.

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

Au lieu de l’interrogation de ces travaux pour la saisie semi-automatique, qui est un code inutile, supplémentaire - il est plus simple toouse hello **AzureRmBackupJob-attente** applet de commande. Lorsqu’il est utilisé dans un script, applet de commande hello suspend l’exécution de hello qu’hello tâche se termine ou hello spécifié la valeur de délai d’attente est atteinte.

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a>Restauration d’une machine virtuelle Azure
Dans les données de sauvegarde toorestore ordre, vous devez tooidentify hello sauvegardé élément, et Point de récupération hello qui contient les données de point-à-temps hello. Ces informations sont fournies toohello AzureRmBackupItem de restauration applet de commande tooinitiate une restauration de données à partir de hello coffre toohello du client.

### <a name="select-hello-vm"></a>Sélectionnez hello machine virtuelle
objet PowerShell hello tooget identifiant hello droit de sauvegarder l’élément, vous devez toostart de hello conteneur dans le coffre de hello et dont la hiérarchie d’objets. conteneur hello tooselect représentant hello machine virtuelle, utilisez hello **Get-AzureRmBackupContainer** applet de commande et redirigez cette toohello **Get-AzureRmBackupItem** applet de commande.

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a>Choisir un point de récupération
Vous pouvez maintenant mettre tous les points de récupération hello pour sauvegarder l’élément hello à l’aide de hello **Get-AzureRmBackupRecoveryPoint** applet de commande, puis choisissez toorestore de point de récupération hello. En général, les utilisateurs choisir hello plus récente *AppConsistent* point dans la liste de hello.

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

variable de Hello ```$rp``` est un tableau de points de récupération pour hello l’élément de sauvegarde, trié dans l’ordre inverse de temps sélectionné - dernier point de récupération hello est à l’index 0. Utiliser le tableau PowerShell standard, l’indexation de point de récupération toopick hello. Par exemple : ```$rp[0]``` sélectionnera le dernier point de récupération hello.

### <a name="restoring-disks"></a>Restauration de disques
Il existe une différence fondamentale entre les opérations de restauration hello effectuée par le biais hello portail Azure et Azure PowerShell. Avec PowerShell, hello restauration s’arrête à la restauration des disques de hello et les informations de configuration de point de récupération hello. Il n’y a pas de création de machine virtuelle.

> [!WARNING]
> Hello AzureRmBackupItem de restauration ne crée pas une machine virtuelle. Il restaure uniquement les disques hello toohello spécifié de compte de stockage. Cela n’est pas hello même comportement que vous rencontrerez dans hello portail Azure.
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

Vous pouvez obtenir les détails de hello hello d’opération de restauration à l’aide de hello **Get-AzureRmBackupJobDetails** applet de commande une fois que le travail de restauration hello est terminée. Hello *ErrorDetails* propriété hello des informations sont nécessaires toorebuild hello machine virtuelle.

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-hello-vm"></a>Build hello machine virtuelle
Hello construction machine virtuelle hors des disques hello restauré peut être effectuée à l’aide des applets de commande PowerShell Azure Service Management plus anciennes de hello, hello nouveaux modèles Azure Resource Manager, ou même à l’aide de hello portail Azure. Dans l’exemple ci-dessous, nous allons montrer comment tooget là à l’aide des applets de commande de gestion des services Azure hello.

```
$properties  = $details.Properties

$storageAccountName = $properties["Target Storage Account Name"]
$containerName = $properties["Config Blob Container Name"]
$blobName = $properties["Config Blob Name"]

$keys = Get-AzureStorageKey -StorageAccountName $storageAccountName
$storageAccountKey = $keys.Primary
$storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey


$destination_path = "C:\Users\admin\Desktop\vmconfig.xml"
Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path -Context $storageContext


$obj = [xml](((Get-Content -Path $destination_path -Encoding UniCode)).TrimEnd([char]0x00))
$pvr = $obj.PersistentVMRole
$os = $pvr.OSVirtualHardDisk
$dds = $pvr.DataVirtualHardDisks
$osDisk = Add-AzureDisk -MediaLocation $os.MediaLink -OS $os.OS -DiskName "panbhaosdisk"
$vm = New-AzureVMConfig -Name $pvr.RoleName -InstanceSize $pvr.RoleSize -DiskName $osDisk.DiskName

if (!($dds -eq $null))
{
    foreach($d in $dds.DataVirtualHardDisk)
    {
        $lun = 0
        if(!($d.Lun -eq $null))
        {
            $lun = $d.Lun
        }
        $name = "panbhadataDisk" + $lun
        Add-AzureDisk -DiskName $name -MediaLocation $d.MediaLink
        $vm | Add-AzureDataDisk -Import -DiskName $name -LUN $lun
    }
}

New-AzureVM -ServiceName "panbhasample" -Location "SouthEast Asia" -VM $vm
```

Pour plus d’informations sur la façon dont les disques restaurés toobuild une machine virtuelle à partir de hello, consultez hello suivant d’applets de commande :

* [Add-AzureDisk](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [New-AzureVMConfig](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [New-AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a>Exemples de code
### <a name="1-get-hello-completion-status-of-job-sub-tasks"></a>1. Obtenir l’état d’achèvement hello de travail des tâches subordonnées
état d’achèvement hello tootrack, de sous-tâches individuels, vous pouvez utiliser hello **Get-AzureRmBackupJobDetails** applet de commande :

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data tooBackup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a>2. Création d’un rapport quotidien/hebdomadaire des travaux de sauvegarde
En règle générale, les administrateurs souhaitent tooknow les travaux de sauvegarde exécutés hello des dernières 24 heures, état hello de ces tâches de sauvegarde. En outre, quantité hello de données transférées donne aux administrateurs un moyen tooestimate leur utilisation des données mensuelles. script Hello ci-dessous extrait des données brutes hello hello service Azure Backup et affiche des informations de hello dans la console PowerShell hello.

```
param(  [Parameter(Mandatory=$True,Position=1)]
        [string]$backupvaultname,

        [Parameter(Mandatory=$False,Position=2)]
        [int]$numberofdays = 7)


#Initialize variables
$DAILYBACKUPSTATS = @()
$backupvault = Get-AzureRmBackupVault -Name $backupvaultname
$enddate = ([datetime]::Today).AddDays(1)
$startdate = ([datetime]::Today)

for( $i = 1; $i -le $numberofdays; $i++ )
{
    # We query one day at a time because pulling 7 days of data might be too much
    $dailyjoblist = Get-AzureRmBackupJob -Vault $backupvault -From $startdate -too$enddate -Type AzureVM -Operation Backup
    Write-Progress -Activity "Getting job information for hello last $numberofdays days" -Status "Day -$i" -PercentComplete ([int]([decimal]$i*100/$numberofdays))

    foreach( $job in $dailyjoblist )
    {
        #Extract hello information for hello reports
        $newstatsobj = New-Object System.Object
        $newstatsobj | Add-Member -Type NoteProperty -Name Date -Value $startdate
        $newstatsobj | Add-Member -Type NoteProperty -Name VMName -Value $job.WorkloadName
        $newstatsobj | Add-Member -Type NoteProperty -Name Duration -Value $job.Duration
        $newstatsobj | Add-Member -Type NoteProperty -Name Status -Value $job.Status

        $details = Get-AzureRmBackupJobDetails -Job $job
        $newstatsobj | Add-Member -Type NoteProperty -Name BackupSize -Value $details.Properties["Backup Size"]
        $DAILYBACKUPSTATS += $newstatsobj
    }

    $enddate = $enddate.AddDays(-1)
    $startdate = $startdate.AddDays(-1)
}

$DAILYBACKUPSTATS | Out-GridView
```

Si vous souhaitez tooadd le résultat du rapport toothis fonctionnalités de création de graphiques, obtenir des informations à partir du billet de blog TechNet hello [graphiques avec PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)

## <a name="next-steps"></a>Étapes suivantes
Si vous préférez utiliser PowerShell tooengage avec vos ressources Azure, consultez l’article de PowerShell hello pour protéger Windows Server, [déployer et gérer Backup pour Windows Server](backup-client-automation-classic.md). Il existe également un article PowerShell sur la gestion des sauvegardes DPM : [Déployer et gérer une sauvegarde pour DPM](backup-dpm-automation-classic.md). Ces deux articles ont une version concernant les déploiements avec le modèle Resource Manager et le modèle Classic.
