---
title: sauvegardes de Windows Server aaaUse PowerShell toomanage dans Azure | Documents Microsoft
description: "Déployez et gérez des sauvegardes Windows Server à l’aide de PowerShell."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: e7e269e2-1f11-41a9-957b-a2155de6a1e0
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: saurse;markgal;nkolli;trinadhk
ms.openlocfilehash: 72292e510b0f059102440bd49a195be4ef700a6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a>Déployer et gérer la sauvegarde tooAzure pour le Client Windows Server et Windows à l’aide de PowerShell
> [!div class="op_single_selector"]
> * [ARM](backup-client-automation.md)
> * [Classique](backup-client-automation-classic.md)
>
>

Cet article explique comment tooback de PowerShell toouse Windows Server ou Windows workstation données tooa coffre de sauvegarde. Microsoft recommande d’utiliser des coffres Recovery Services pour tous les nouveaux déploiements. Si vous êtes un nouvel utilisateur Azure Backup et que vous n’avez pas créé un coffre de sauvegarde dans votre abonnement, utilisez l’article hello, [déployer et gérer des tooAzure de données de Data Protection Manager à l’aide de PowerShell](backup-client-automation.md) afin de vous stockez vos données dans un coffre Recovery Services. 

> [!IMPORTANT]
> Vous pouvez maintenant mettre à niveau vos archivages de sauvegarde coffres tooRecovery Services. Pour plus d’informations, voir l’article hello [mise à niveau d’un tooa de coffre de sauvegarde de coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft vous encourage tooupgrade coffres des Services tooRecovery les coffres de votre sauvegarde.<br/> Après le 15 octobre 2017, vous ne pouvez pas utiliser les coffres de sauvegarde toocreate PowerShell. **D’ici au 1er novembre 2017** :
>- Tous les coffres de sauvegarde restants seront les coffres des Services de tooRecovery automatiquement mis à niveau.
>- Vous ne pourra plus être en mesure de tooaccess vos données de sauvegarde dans le portail classique de hello. Au lieu de cela, utilisez hello tooaccess portail Azure vos données de sauvegarde dans les coffres des Services de récupération.
>

## <a name="install-azure-powershell"></a>Installation d'Azure PowerShell
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

Azure PowerShell 1.0 a été publié en octobre 2015. Cette version a réussi la mise en production hello 0.9.8 et résultant des modifications importantes, notamment dans le modèle de désignation hello d’applets de commande hello. Suivez d’applets de commande 1.0 hello modèle d’affectation de noms {verbe}-Azure Resource Manager {nom} ; alors que les noms de hello 0.9.8 n’incluent pas **Rm** (par exemple, New-AzureRmResourceGroup au lieu de New-AzureResourceGroup). Lorsque vous utilisez Azure PowerShell 0.9.8, vous devez d’abord activer le mode Gestionnaire de ressources hello en exécutant hello **Switch-AzureMode AzureResourceManager** commande. Cette commande n’est pas nécessaire dans les versions 1.0 ou ultérieures.

Si vous souhaitez toouse vos scripts écrits pour hello 0.9.8 environnement hello 1.0 ou ultérieure environnement, vous devez tester soigneusement les scripts hello dans un environnement de préproduction avant de les utiliser dans la production tooavoid impact inattendu.

[Télécharger la dernière version de PowerShell hello](https://github.com/Azure/azure-powershell/releases) (version minimale requise est : 1.0.0)

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-backup-vault"></a>Créer un coffre de sauvegarde
> [!WARNING]
> Pour les clients à l’aide de la sauvegarde Azure pour hello première fois, vous devez tooregister hello Azure Backup fournisseur toobe utilisé avec votre abonnement. Cela est possible en exécutant hello de commande suivante : Register-AzureProvider - ProviderNamespace « Microsoft.Backup »
>
>

Vous pouvez créer un coffre de sauvegarde à l’aide de hello **New-AzureRMBackupVault** applet de commande. coffre de sauvegarde Hello est une ressource ARM, par conséquent, vous devez tooplace dans un groupe de ressources. Dans une console Azure PowerShell avec élévation de privilèges, exécutez hello suivant de commandes :

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

Hello d’utilisation **Get-AzureRMBackupVault** les coffres de sauvegarde de hello toolist applet de commande dans un abonnement.

## <a name="installing-hello-azure-backup-agent"></a>Installation de l’agent Azure Backup hello
Avant d’installer l’agent de sauvegarde Azure hello, vous devez le programme d’installation de toohave hello téléchargés et présent sur hello Windows Server. Vous pouvez obtenir la version la plus récente du programme d’installation hello hello de hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) ou à partir de la page du tableau de bord du coffre de sauvegarde hello. Enregistrer le programme d’installation de hello tooan les emplacement facilement accessible, tel que * C:\Downloads\*.

tooinstall hello exécution de l’agent, hello suivant de commande dans une console PowerShell avec élévation de privilèges :

```
PS C:\> MARSAgentInstaller.exe /q
```

Cette commande installe l’agent de hello avec toutes les options par défaut de hello. installation de Hello prend quelques minutes en arrière-plan de hello. Si vous ne spécifiez pas hello */nu* option puis hello **mise à jour Windows** fenêtre s’ouvre à fin hello de toocheck d’installation hello pour les mises à jour. Une fois installé, l’agent de hello s’affichent dans la liste hello des programmes installés.

liste de hello toosee des programmes installés, passez trop**le panneau de configuration** > **programmes** > **programmes et fonctionnalités**.

![Agent installé](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a>Options d’installation
toosee tous hello options disponibles via hello de ligne de commande, utilisez les hello de commande suivante :

```
PS C:\> MARSAgentInstaller.exe /?
```

les options disponibles Hello sont les suivantes :

| Option | Détails | Default |
| --- | --- | --- |
| /q |Installation silencieuse |- |
| /p:"emplacement" |Chemin d’accès toohello dossier d’installation de l’agent de sauvegarde Azure hello. |C:\Program Files\Microsoft Azure Recovery Services Agent |
| /s:"emplacement" |Chemin d’accès toohello dossier de cache de l’agent de sauvegarde Azure hello. |C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch |
| /m |Acceptation de la mise à jour tooMicrosoft |- |
| /nu |Ne pas vérifier les mises à jour une fois l’installation terminée |- |
| /d |Désinstalle l’agent Microsoft Azure Recovery Services |- |
| /ph |Adresse de l’hôte proxy |- |
| /po |Numéro de port de l’hôte proxy |- |
| /pu |Nom d’utilisateur de l’hôte proxy |- |
| /pw |Mot de passe du proxy |- |

## <a name="registering-with-hello-azure-backup-service"></a>L’inscription auprès de hello service Azure Backup
Avant de pouvoir inscrire avec hello service Azure Backup, vous devez tooensure que hello [conditions préalables](backup-configure-vault.md) sont remplies. Vous devez respecter les consignes suivantes :

* Avoir un abonnement Azure valide
* Disposer d’un coffre de sauvegarde

informations d’identification d’archivage toodownload hello, exécutez hello **Get-AzureRMBackupVaultCredentials** applet de commande dans une console Azure PowerShell et le magasin dans un emplacement pratique comme * C:\Downloads\*.

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

L’enregistrement machine hello avec le coffre de hello est effectuée à l’aide de hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) applet de commande :

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration -VaultCredentials $cred -Confirm:$false

CertThumbprint      : 7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName : test-vault
Region              : West US

Machine registration succeeded.
```

> [!IMPORTANT]
> N’utilisez pas le fichier d’informations d’identification de chemins d’accès relatifs toospecify hello coffre. Vous devez fournir un chemin d’accès absolu comme une applet de commande toohello d’entrée.
>
>

## <a name="networking-settings"></a>Paramètres de mise en réseau
Lors de la connectivité hello Hello toohello qu'internet se fait via un serveur proxy d’ordinateur Windows, les paramètres de proxy hello peuvent également être fournies toohello agent. Dans cet exemple, il n’y a aucun serveur proxy. Nous effaçons donc explicitement toutes informations concernant un proxy.

L’utilisation de la bande passante peut également être contrôlée avec options hello ```work hour bandwidth``` et ```non-work hour bandwidth``` pour un ensemble donné de jours de semaine de hello.

Définition des détails de la bande passante et de proxy hello est effectuée à l’aide de hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) applet de commande :

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a>Paramètres de chiffrement
tooAzure de données de sauvegarde envoyées Hello sauvegarde est la confidentialité de hello tooprotect chiffré des données de hello. phrase secrète de chiffrement Hello donnée hello « mot de passe » toodecrypt hello au moment de la restauration de hello.

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
Server properties updated successfully
```

> [!IMPORTANT]
> Conserver les informations de mot de passe hello sûre et sécurisée une fois qu’elle est définie. Vous ne serez pas toorestore en mesure des données à partir d’Azure sans cette phrase secrète.
>
>

## <a name="back-up-files-and-folders"></a>Sauvegarde des fichiers et dossiers
Toutes les sauvegardes à partir de serveurs et clients Windows tooAzure sauvegarde sont régies par une stratégie. stratégie de Hello comprend trois parties :

1. A **planification de sauvegarde** qui spécifie quand les sauvegardes doivent toobe prises et synchronisé avec le service de hello.
2. A **planification de rétention** qui spécifie la durée pendant laquelle des points de récupération de hello tooretain dans Azure.
3. Une **spécification d'inclusion/exclusion de fichier** qui dicte ce qui doit être sauvegardé.

Dans ce document, comme nous automatisons la sauvegarde, nous supposons que rien n'a été configuré. Nous commençons par créer une stratégie de sauvegarde à l’aide de hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) applet de commande et son utilisation.

```
PS C:\> $newpolicy = New-OBPolicy
```

À ce hello temps stratégie est vide et autres applets de commande sont nécessaire toodefine quels éléments seront inclus ou exclus, lorsque les sauvegardes sont exécutées et hello où les sauvegardes seront stockées.

### <a name="configuring-hello-backup-schedule"></a>Configuration de planification de sauvegarde hello
Hello tout d’abord de hello 3 parties d’une stratégie est hello planification de sauvegarde est créée à l’aide de hello [New-OBSchedule](https://technet.microsoft.com/library/hh770401) applet de commande. planification de sauvegarde Hello définit lorsque les sauvegardes doivent toobe prise. Lors de la création d’une planification, vous devez toospecify 2 des paramètres d’entrée :

* **Jours de semaine de hello** cette sauvegarde hello doit s’exécuter. Vous pouvez exécuter la tâche de sauvegarde hello sur une seule journée, ou tous les jours de semaine de hello ou n’importe quelle combinaison entre les deux.
* **Heures de la journée de hello** quand la sauvegarde de hello doit s’exécuter. Vous pouvez définir des too3 différents moments de la journée hello déclenchement de sauvegarde de hello.

Par exemple, vous pouvez configurer une stratégie de sauvegarde qui s'exécute à 16 h 00 chaque samedi et chaque dimanche.

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

planification de sauvegarde Hello doit toobe associé à une stratégie, et cela peut être obtenue à l’aide de hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) applet de commande.

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a>Configuration d'une stratégie de rétention
stratégie de rétention Hello définit la durée de récupération points créés à partir des travaux de sauvegarde sont conservés. Lorsque vous créez une nouvelle stratégie de rétention à l’aide de hello [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) applet de commande, vous pouvez spécifier plusieurs hello jours pendant lesquels les points de récupération d’une sauvegarde de hello doivent toobe avec Azure Backup. exemple Hello ci-dessous définit une stratégie de rétention de 7 jours.

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

Hello stratégie de rétention doit être associé à stratégie de principal de hello à l’aide d’applet de commande hello [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):

```
PS C:\> Set-OBRetentionPolicy -Policy $newpolicy -RetentionPolicy $retentionpolicy

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          :
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```
### <a name="including-and-excluding-files-toobe-backed-up"></a>Inclusion et exclusion de toobe de fichiers sauvegardé
Un ```OBFileSpec``` objet définit hello fichiers toobe inclus et exclu dans une sauvegarde. Il s’agit d’un ensemble de règles que les fichiers et dossiers sur un ordinateur protégés par étendue out hello. Vous pouvez avoir de nombreuses règles d'inclusion ou d’exclusion en fonction de vos besoins, et les associer à une stratégie. Lorsque vous créez un objet OBFileSpec, vous pouvez :

* Spécifiez hello toobe fichiers et dossiers inclus
* Spécifiez hello toobe fichiers et dossiers exclu
* Spécifiez la sauvegarde récursive de données dans un dossier (ou) si uniquement hello fichiers de niveau supérieur dans le dossier spécifié de hello doivent être sauvegardées jusqu'à.

Hello ce dernier est obtenue à l’aide d’indicateur de non récursives - hello dans la commande hello New-OBFileSpec.

Dans l’exemple hello ci-dessous, nous sauvegarder volume C: et D: et exclure les fichiers binaires du système d’exploitation hello dans le dossier de Windows hello et tous les dossiers temporaires. toodo afin que nous allons créer deux spécifications de fichier à l’aide de hello [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) applet de commande - un pour inclusion et un pour l’exclusion. Une fois les spécifications de fichier hello ont été créées, ils sont associés avec stratégie hello hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) applet de commande.

```
PS C:\> $inclusions = New-OBFileSpec -FileSpec @("C:\", "D:\")

PS C:\> $exclusions = New-OBFileSpec -FileSpec @("C:\windows", "C:\temp") -Exclude

PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $inclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid


PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $exclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\windows
                  IsExclude:True
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\temp
                  IsExclude:True
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```

### <a name="applying-hello-policy"></a>Appliquer la stratégie de hello
Maintenant, objet de stratégie de hello est terminée et a une planification de sauvegarde associée, la stratégie de rétention et une liste d’inclusion/exclusion de fichiers. Cette stratégie peut maintenant être validée pour Azure Backup toouse. Avant d’appliquer hello nouvellement créé stratégie Assurez-vous qu’il n’y a aucune stratégie de sauvegarde existant associé avec le serveur de hello à l’aide de hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) applet de commande. Suppression de la stratégie de hello invitera à confirmer l’opération. confirmation de hello tooskip utiliser hello ```-Confirm:$false``` indicateur avec l’applet de commande hello.

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

Objet de stratégie de validation hello est effectuée à l’aide de hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) applet de commande. Une confirmation vous est également demandée. confirmation de hello tooskip utiliser hello ```-Confirm:$false``` indicateur avec l’applet de commande hello.

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want toosave this backup policy ? [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s)
DsList : {DataSource
         DatasourceId:4508156004108672185
         Name:C:\
         FileSpec:FileSpec
         FileSpec:C:\
         IsExclude:False
         IsRecursive:True,

         FileSpec
         FileSpec:C:\windows
         IsExclude:True
         IsRecursive:True,

         FileSpec
         FileSpec:C:\temp
         IsExclude:True
         IsRecursive:True,

         DataSource
         DatasourceId:4508156005178868542
         Name:D:\
         FileSpec:FileSpec
         FileSpec:D:\
         IsExclude:False
         IsRecursive:True
    }
PolicyName : c2eb6568-8a06-49f4-a20e-3019ae411bac
RetentionPolicy : Retention Days : 7
              WeeklyLTRSchedule :
              Weekly schedule is not set

              MonthlyLTRSchedule :
              Monthly schedule is not set

              YearlyLTRSchedule :
              Yearly schedule is not set
State : Existing PolicyState : Valid
```

Vous pouvez afficher les détails de hello hello existant stratégie de sauvegarde à l’aide de hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) applet de commande. Vous pouvez Explorer à l’aide des hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) applet de commande pour la planification de sauvegarde hello et hello [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) applet de commande pour les stratégies de rétention hello

```
PS C:> Get-OBPolicy | Get-OBSchedule
SchedulePolicyName : 71944081-9950-4f7e-841d-32f0a0a1359a
ScheduleRunDays : {Saturday, Sunday}
ScheduleRunTimes : {16:00:00}
State : Existing

PS C:> Get-OBPolicy | Get-OBRetentionPolicy
RetentionDays : 7
RetentionPolicyName : ca3574ec-8331-46fd-a605-c01743a5265e
State : Existing

PS C:> Get-OBPolicy | Get-OBFileSpec
FileName : *
FilePath : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
FileSpec : D:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\
FileSpec : C:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\windows
FileSpec : C:\windows
IsExclude : True
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\temp
FileSpec : C:\temp
IsExclude : True
IsRecursive : True
```

### <a name="performing-an-ad-hoc-backup"></a>Exécution d'une sauvegarde ad hoc
Une fois qu’une stratégie de sauvegarde a été définie hello sauvegardes par la planification de hello. Déclenchement d’une sauvegarde ad hoc est également possible à l’aide de hello [OBBackup de début](https://technet.microsoft.com/library/hh770426) applet de commande :

```
PS C:> Get-OBPolicy | Start-OBBackup
Taking snapshot of volumes...
Preparing storage...
Estimating size of backup items...
Estimating size of backup items...
Transferring data...
Verifying backup...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a>Restauration des données à partir de Sauvegarde Azure
Cette section vous guidera tout au long des étapes hello pour automatiser la récupération des données à partir d’Azure Backup. Cette opération implique hello comme suit :

1. Sélectionnez hello source volume
2. Choisissez un toorestore de point de sauvegarde
3. Choisissez un élément de toorestore
4. Processus de restauration hello déclencheur

### <a name="picking-hello-source-volume"></a>Volume de prélèvement hello source
Dans l’ordre toorestore un élément à partir d’Azure Backup, vous devez d’abord source de hello tooidentify d’élément de hello. Étant donné que nous allons l’exécution de commandes hello dans le contexte de hello d’un serveur Windows ou d’un client Windows, hello ordinateur est déjà identifié. étape suivante de Hello pour identifier la source de hello est volume de hello tooidentify qui le contient. Une liste des volumes ou des sources en cours de sauvegarde à partir de cet ordinateur peut être récupérée en exécutant hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) applet de commande. Cette commande retourne un tableau de toutes les sources de hello sauvegardés à partir de ce serveur/client.

```
PS C:> $source = Get-OBRecoverableSource
PS C:> $source
FriendlyName : C:\
RecoverySourceName : C:\
ServerName : myserver.microsoft.com

FriendlyName : D:\
RecoverySourceName : D:\
ServerName : myserver.microsoft.com
```

### <a name="choosing-a-backup-point-toorestore"></a>Choix d’un toorestore de point de sauvegarde
Hello liste de points de sauvegarde peut être récupérée en exécutant hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) applet de commande avec les paramètres appropriés. Dans notre exemple, nous allons choisir hello sauvegarde les plus récentes pour le volume source de hello *D:* et utilisez-le toorecover un fichier spécifique.

```
PS C:> $rps = Get-OBRecoverableItem -Source $source[1]
IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :

IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 17-Jun-15 6:31:31 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :
```
objet de Hello ```$rps``` est un tableau de points de sauvegarde. premier élément de Hello est plus récentes hello et Nième élément de hello est le point le plus ancien hello. toochoose hello les plus récentes, nous allons utiliser ```$rps[0]```.

### <a name="choosing-an-item-toorestore"></a>Choix d’un élément de toorestore
tooidentify hello exact ou du fichier toorestore du dossier, récursive utiliser hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) applet de commande. Cette hiérarchie de dossiers de manière hello peut être parcourue uniquement à l’aide de hello ```Get-OBRecoverableItem```.

Dans cet exemple, si nous voulons que le fichier de hello toorestore *finances.xls* nous pouvons font référence à l’aide de cet objet de hello ```$filesFolders[1]```.

```
PS C:> $filesFolders = Get-OBRecoverableItem $rps[0]
PS C:> $filesFolders
IsDir : True
ItemNameFriendly : D:\MyData\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\
LocalMountPoint : D:\
MountPointName : D:\
Name : MyData
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime : 15-Jun-15 8:49:29 AM

PS C:> $filesFolders = Get-OBRecoverableItem $filesFolders[0]
PS C:> $filesFolders
IsDir : False
ItemNameFriendly : D:\MyData\screenshot.oxps
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\screenshot.oxps
LocalMountPoint : D:\
MountPointName : D:\
Name : screenshot.oxps
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 228313
ItemLastModifiedTime : 21-Jun-14 6:45:09 AM

IsDir : False
ItemNameFriendly : D:\MyData\finances.xls
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\finances.xls
LocalMountPoint : D:\
MountPointName : D:\
Name : finances.xls
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 96256
ItemLastModifiedTime : 21-Jun-14 6:43:02 AM
```

Vous pouvez également rechercher des toorestore d’éléments à l’aide de hello ```Get-OBRecoverableItem``` applet de commande. Dans notre exemple, toosearch pour *finances.xls* nous aurions pu obtenir un descripteur sur un fichier hello en exécutant cette commande :

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a>Processus de restauration hello déclenchement
processus de restauration tootrigger hello, nous devons tout d’abord les options de récupération toospecify hello. Cela est possible à l’aide de hello [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) applet de commande. Pour cet exemple, supposons que nous souhaitons que les fichiers de hello toorestore trop*C:\temp*. Supposons également que nous souhaitons tooskip fichiers qui existent déjà sur le dossier de destination hello *C:\temp*. toocreate telle une option de récupération, utilisez hello de commande suivante :

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

Déclenchement de la restauration à l’aide de hello maintenant [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) commande hello sélectionné ```$item``` à partir de la sortie de hello Hello ```Get-OBRecoverableItem``` applet de commande :

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a>Désinstallation de l’agent de sauvegarde Azure hello
Désinstaller l’agent de sauvegarde Azure hello est possible à l’aide de hello de commande suivante :

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

Désinstallation des fichiers binaires hello à partir de l’ordinateur de hello a certaines tooconsider conséquences :

* Elle supprime le filtre de fichier hello à partir de l’ordinateur de hello et le suivi des modifications est arrêté.
* Toutes les informations de stratégie sont supprimées de la machine de hello, mais les informations de stratégie hello continuent toobe stockée dans le service hello.
* Toutes les planifications de sauvegarde sont supprimées, et aucune autre sauvegarde n'est effectuée.

Toutefois, hello des données stockées dans le reste de Azure et sont conservées conformément aux paramètres de stratégie de rétention hello par vous. Les points plus anciens deviennent automatiquement obsolètes.

## <a name="remote-management"></a>Gestion à distance
Toute la gestion hello autour de l’agent de sauvegarde Azure hello, les stratégies et les sources de données peut être effectuée à distance via PowerShell. ordinateur Hello qui est géré à distance doit toobe correctement préparé.

Par défaut, hello service WinRM est configuré pour un démarrage manuel. type de démarrage de Hello doit être défini trop*automatique* et hello service doit être démarré. tooverify qui hello service WinRM est en cours d’exécution, la valeur de la propriété Status de hello hello doit être *en cours d’exécution*.

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

PowerShell doit être configuré pour la communication à distance.

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

machine de Hello désormais peut être géré à distance, en commençant à partir de l’installation Bonjour de l’agent de hello. Par exemple, hello script suivant copie de l’ordinateur distant hello agent toohello et l’installe.

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur Sauvegarde Azure pour client/serveur Windows, consultez

* [Introduction tooAzure sauvegarde](backup-introduction-to-azure-backup.md)
* [Sauvegarder des serveurs Windows](backup-configure-vault.md)
