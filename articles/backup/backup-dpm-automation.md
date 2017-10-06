---
title: aaaAzure sauvegarde - tooback utiliser PowerShell des charges de travail DPM | Documents Microsoft
description: "Découvrez comment toodeploy et gérer la sauvegarde de Azure pour Data Protection Manager (DPM) à l’aide de PowerShell"
services: backup
documentationcenter: 
author: NKolli1
manager: shreeshd
editor: 
ms.assetid: e9bd223c-2398-4eb1-9bf3-50e08970fea7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: adigan;anuragm;trinadhk;markgal
ms.openlocfilehash: 27d2b4b3127b68c9da564697eb61dc3ccbc34b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a>Déployer et gérer la sauvegarde tooAzure pour les serveurs Data Protection Manager (DPM) à l’aide de PowerShell
> [!div class="op_single_selector"]
> * [ARM](backup-dpm-automation.md)
> * [Classique](backup-dpm-automation-classic.md)
>
>

Cet article vous montre comment toouse PowerShell toosetup Azure Backup sur un serveur DPM et toomanage sauvegarde et de récupération.

## <a name="setting-up-hello-powershell-environment"></a>Configurer l’environnement PowerShell de hello
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

Avant de pouvoir utiliser des sauvegardes de toomanage PowerShell à partir de Data Protection Manager tooAzure, vous avez besoin d’environnement de droite hello toohave dans PowerShell. Au début de hello de session de PowerShell hello, assurez-vous que vous exécutez hello suivant modules bon de commande tooimport hello et vous permettre d’applets de commande DPM toocorrectly référence hello :

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome toohello DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a>Installation et inscription
toobegin :

1. [Téléchargez la dernière version de PowerShell](https://github.com/Azure/azure-powershell/releases) (version minimale requise : 1.0.0)
2. Activer les applets de commande de sauvegarde Azure hello en basculant trop*AzureResourceManager* mode à l’aide de hello **Switch-AzureMode** applet de commande :

```
PS C:\> Switch-AzureMode AzureResourceManager
```

Hello suivant le programme d’installation et tâches d’enregistrement peuvent être automatisées avec PowerShell :

* Créer un coffre Recovery Services
* Installation de l’agent Azure Backup hello
* L’inscription auprès de hello service Azure Backup
* Paramètres de mise en réseau
* Paramètres de chiffrement

## <a name="create-a-recovery-services-vault"></a>Créer un coffre Recovery Services
Hello suit vous guide lors de la création d’un coffre Recovery Services. Un coffre Recovery Services diffère d’un coffre de sauvegarde.

1. Si vous utilisez Azure Backup pour hello première fois, vous devez utiliser hello **Register-AzureRMResourceProvider** fournisseur de Service de récupération Azure hello applet de commande tooregister avec votre abonnement.

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. Hello coffre Recovery Services est une ressource ARM, vous devez donc tooplace dans un groupe de ressources. Vous pouvez utiliser un groupe de ressources existant ou en créer un. Lorsque vous créez un nouveau groupe de ressources, spécifiez le nom de hello et un emplacement pour le groupe de ressources hello.  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. Hello d’utilisation **New-AzureRmRecoveryServicesVault** toocreate de l’applet de commande un coffre. Veillez à toospecify hello même emplacement pour le coffre hello que celui utilisé pour le groupe de ressources hello.

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. Spécifiez le type hello de toouse de redondance de stockage ; Vous pouvez utiliser [stockage localement redondant (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) ou [stockage redondant de géo-réplication (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage). Hello suivant montre testVault hello BackupStorageRedundancy - option est la valeur tooGeoRedundant.

   > [!TIP]
   > Nombreuses applets de commande Azure Backup nécessitent l’objet de coffre Recovery Services hello en tant qu’entrée. Pour cette raison, il est pratique toostore hello Services de récupération de sauvegarde coffre objet dans une variable.
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a>Affichage des coffres de hello dans un abonnement
Utilisez **Get-AzureRmRecoveryServicesVault** liste de hello tooview de tous les coffres dans l’abonnement actif de hello. Vous pouvez utiliser cette toocheck commande qu’un nouvel archivage a été créé ou toosee les coffres sont disponibles dans l’abonnement de hello.

Exécutez la commande hello, Get-AzureRmRecoveryServicesVault, et tous les archivages dans l’abonnement de hello sont répertoriées.

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


## <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a>Agent de sauvegarde Azure hello lors de l’installation sur un serveur DPM
Avant d’installer l’agent de sauvegarde Azure hello, vous devez le programme d’installation de toohave hello téléchargés et présent sur hello Windows Server. Vous pouvez obtenir la version la plus récente du programme d’installation hello hello de hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) ou à partir de la page du tableau de bord du coffre de Services de récupération hello. Enregistrer le programme d’installation de hello tooan les emplacement facilement accessible, tel que * C:\Downloads\*.

tooinstall hello exécution de l’agent, hello suivant de commande dans une console PowerShell avec élévation de privilèges **sur le serveur DPM hello**:

```
PS C:\> MARSAgentInstaller.exe /q
```

Cette commande installe l’agent de hello avec toutes les options par défaut de hello. installation de Hello prend quelques minutes en arrière-plan de hello. Si vous ne spécifiez pas hello */nu* hello d’option **mise à jour Windows** fenêtre s’ouvre à la fin de hello de toocheck d’installation hello pour les mises à jour.

l’agent de Hello s’affiche dans la liste hello des programmes installés. liste de hello toosee des programmes installés, passez trop**le panneau de configuration** > **programmes** > **programmes et fonctionnalités**.

![Agent installé](./media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a>Options d’installation
toosee toutes les options de hello disponibles via hello commandline, hello utilisation suivant de commandes :

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

## <a name="registering-dpm-tooa-recovery-services-vault"></a>L’enregistrement DPM tooa coffre Recovery Services
Une fois que vous avez créé le coffre Recovery Services hello, téléchargez l’agent plus récent hello et les informations d’identification de coffre hello et stockez-le dans un emplacement pratique comme C:\Downloads.

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

Sur le serveur DPM hello, exécutez hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) machine de hello tooregister applet de commande avec le coffre de hello.

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a>Paramètres de la configuration initiale
Une fois hello serveur DPM est enregistré avec hello de coffre Recovery Services, il commence par les paramètres par défaut de l’abonnement. Ces paramètres d’abonnement incluent la mise en réseau, le chiffrement et hello zone de transit. paramètres d’abonnement toochange vous devez toofirst obtenez un descripteur sur paramètres hello existants (par défaut) à l’aide de hello [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) applet de commande :

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

Toutes les modifications sont apportées toothis local PowerShell objet ```$setting``` puis complet de l’objet hello est validée tooDPM et Azure Backup toosave les à l’aide de hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) applet de commande. Vous devez toouse hello ```–Commit``` tooensure indicateur qui hello les modifications sont conservées. paramètres de Hello ne seront pas appliqués et utilisés par Azure Backup, sauf si la validation.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a>Mise en réseau
Si la connexion de hello de hello DPM machine toohello service Azure Backup sur hello internet est via un serveur proxy, paramètres hello du serveur proxy doivent être fournies pour les sauvegardes réussies. Il incombe à l’aide de hello ```-ProxyServer```et ```-ProxyPort```, ```-ProxyUsername``` et hello ```ProxyPassword``` paramètres avec hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) applet de commande. Dans cet exemple, il n’y a aucun serveur proxy. Nous effaçons donc explicitement toutes informations concernant un proxy.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

L’utilisation de la bande passante peut également être contrôlée avec les options de ```-WorkHourBandwidth``` et ```-NonWorkHourBandwidth``` pour un ensemble donné de jours de semaine de hello. Dans cet exemple, nous ne fixons aucune limitation.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-hello-staging-area"></a>Configuration de la zone de transit hello
Bonjour Azure Backup agent en cours d’exécution sur le serveur DPM hello a besoin de stockage temporaire pour les données restaurées à partir du cloud de hello (zone de transit local). Configurer la zone de transit à l’aide de hello hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) applet de commande et hello ```-StagingAreaPath``` paramètre.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

Dans l’exemple hello ci-dessus, la zone de transit hello sera définie trop*C:\StagingArea* dans l’objet de PowerShell hello ```$setting```. Vérifiez que hello le dossier spécifié existe déjà, sinon la validation finale de paramètres d’abonnement hello hello échouera.

### <a name="encryption-settings"></a>Paramètres de chiffrement
tooAzure de données de sauvegarde envoyées Hello sauvegarde est la confidentialité de hello tooprotect chiffré des données de hello. phrase secrète de chiffrement Hello donnée hello « mot de passe » toodecrypt hello au moment de la restauration de hello. Il est important tookeep cette sécurisé des informations et sécuriser une fois qu’elle est définie.

Dans l’exemple hello ci-dessous, commande premier hello convertit la chaîne de hello ```passphrase123456789``` tooa sécurisée chaîne et lui affecte hello sécurisé toohello variable chaîne nommée ```$Passphrase```. commande deuxième Hello définit la chaîne sécurisée de hello ```$Passphrase``` comme mot de passe hello pour le chiffrement des sauvegardes.

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> Conserver les informations de mot de passe hello sûre et sécurisée une fois qu’elle est définie. Vous ne serez pas toorestore en mesure des données à partir d’Azure sans cette phrase secrète.
>
>

À ce stade, vous aurait dû effectuer tous les toohello de modifications hello requis ```$setting``` objet. N’oubliez pas de modifications de hello toocommit.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a>Protéger les données tooAzure sauvegarde
Dans cette section, vous ajoutez un tooDPM de serveur de production et puis protégez hello toolocal DPM stockage et des données puis tooAzure sauvegarde. Dans les exemples hello, nous allons vous montrer comment tooback des fichiers et des dossiers. Hello logique peut facilement être étendu toobackup n’importe quelle source de données pris en charge de DPM. Toutes vos sauvegardes DPM sont régies par un groupe de protection constitué de quatre parties :

1. **Membres du groupe** est une liste de tous les objets protégeables hello (également appelé *sources de données* dans DPM) que vous souhaitez tooprotect Bonjour même groupe de protection. Par exemple, vous voudrez tooprotect production machines virtuelles dans un groupe de protection et de bases de données SQL Server dans un autre groupe de protection d’avoir différentes exigences de sauvegarde. Avant que vous puissiez sauvegarder toute source de données sur un serveur de production, vous devez toomake hello que l’Agent DPM est installé sur le serveur de hello et est géré par DPM. Suivez les étapes de hello pour [installation hello Agent DPM](https://technet.microsoft.com/library/bb870935.aspx) et en le liant toohello approprié du serveur DPM.
2. **Méthode de protection des données** spécifie hello cible emplacements de sauvegarde - bande, disque et cloud. Dans notre exemple, nous protégera données toohello local disque et toohello dans le cloud.
3. A **planification de sauvegarde** qui spécifie quand les sauvegardes doivent toobe prise et la fréquence à laquelle hello données doivent être synchronisées entre hello serveur DPM et le serveur de production hello.
4. A **planification de rétention** qui spécifie la durée pendant laquelle des points de récupération de hello tooretain dans Azure.

### <a name="creating-a-protection-group"></a>Création d’un groupe de protection
Commencez par créer un nouveau groupe de Protection à l’aide de hello [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) applet de commande.

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

Hello ci-dessus crée un groupe de Protection nommée *ProtectGroup01*. Ultérieures tooadd toohello à sauvegarde Azure cloud peut également être modifié à un groupe de protection existant. Toutefois, toomake toutes les modifications toohello - groupe de Protection nouveau ou existant - nous avons besoin d’un handle de tooget sur un *modifiable* objet à l’aide de hello [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) applet de commande.

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a>Ajout de membres de groupe toohello groupe de Protection
Chaque Agent DPM sait liste hello de sources de données sur le serveur hello lequel il est installé. tooadd un toohello de source de données groupe de Protection, hello toofirst des besoins de l’Agent DPM envoyer une liste de serveur DPM toohello arrière hello sources de données. Une ou plusieurs sources de données sont sélectionnées et ajoutées toohello groupe de Protection. étapes de PowerShell Hello nécessaires tooachieve cela sont :

1. Extraire une liste de tous les serveurs gérés par DPM via hello Agent DPM.
2. Choisissez un serveur spécifique.
3. Extraire une liste de toutes les sources de données sur le serveur de hello.
4. Choisissez une ou plusieurs sources de données et de les ajouter toohello groupe de Protection

Hello la liste des serveurs sur le hello Agent DPM est installé et est géré par le serveur DPM de hello est acquis par hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) applet de commande. Dans cet exemple, nous allons filtrer et configurer uniquement PS avec une sauvegarde nommée *productionserver01* .

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

Liste hello de sources de données d’extraire maintenant sur ```$server``` à l’aide de hello [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) applet de commande. Dans cet exemple, nous allons filtrage pour le volume de hello * D:\* que nous souhaitons tooconfigure pour la sauvegarde. Cette source de données est ensuite ajouté toohello groupe de Protection à l’aide de hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) applet de commande. N’oubliez pas de toouse hello *modifiable* objet du groupe de protection ```$MPG``` ajouts de hello toomake.

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

Répétez cette étape autant de fois en fonction des besoins, jusqu'à ce que vous avez ajouté tous les hello choisi le groupe de protection toohello de sources de données. Vous pouvez également commencer par qu’une seule source de données et flux de travail hello complète pour la création de hello groupe de Protection et à un moment ultérieur ajouter plusieurs sources de données toohello groupe de Protection.

### <a name="selecting-hello-data-protection-method"></a>Méthode de protection des données en sélectionnant hello
Après ont ajouté les sources de données hello toohello groupe de Protection, hello prochaine étape consiste à l’aide de hello la méthode de protection hello toospecify [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) applet de commande. Dans cet exemple, hello groupe de Protection est configurée pour le disque local et de sauvegarde sur le cloud. Vous devez également datasource de hello toospecify que vous souhaitez toocloud tooprotect à l’aide de hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) applet de commande avec l’indicateur en ligne-.

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a>Définition de la plage de rétention hello
Définir la rétention hello pour les points de sauvegarde hello à l’aide de hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) applet de commande. Il peut sembler rétention de hello impair tooset avant de la planification de sauvegarde hello a été définie, à l’aide de hello ```Set-DPMPolicyObjective``` applet de commande définit automatiquement une planification de sauvegarde par défaut qui peut ensuite être modifiée. Il est toujours possible tooset planification de sauvegarde hello en premier et hello après la période de rétention.

Dans l’exemple hello ci-dessous, hello définit des paramètres de rétention hello pour les sauvegardes sur disque. Cela conservera sauvegardes pendant 10 jours, les données de synchronisation toutes les 6 heures entre le serveur de production hello et le serveur DPM hello. Hello ```SynchronizationFrequencyMinutes``` ne définit pas la fréquence à laquelle un point de sauvegarde est créé, mais la fréquence à laquelle les données sont copié toohello le serveur DPM.  Ce paramètre évite que les sauvegardes soient trop volumineuses.

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

Pour les sauvegardes tooAzure (DPM fait référence toothem en tant que les sauvegardes en ligne) des plages de rétention hello peuvent être configurées pour [à long terme rétention à l’aide d’un schéma grand-père-Father-Son (GFS)](backup-azure-backup-cloud-as-tape.md). Autrement dit, vous pouvez définir une stratégie de rétention combinée incluant des stratégies de rétention quotidiennes, hebdomadaires, mensuelles et annuelles. Dans cet exemple, nous créer un tableau représentant le schéma de rétention complexes hello que nous souhaitons, puis configurez la durée de rétention hello à l’aide de hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) applet de commande.

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a>Planification de sauvegarde hello ensemble
DPM définit automatiquement une planification de sauvegarde par défaut si vous spécifiez l’objectif de protection hello à l’aide de hello ```Set-DPMPolicyObjective``` applet de commande. les planifications par défaut toochange hello, utilisez hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) applet de commande suivie hello [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) applet de commande.

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

Bonjour au-dessus de l’exemple, ```$onlineSch``` est un tableau qui contient la planification de protection en ligne existante hello pour hello groupe de Protection dans le schéma GFS hello avec quatre éléments :

1. ```$onlineSch[0]```contient la planification quotidienne de hello
2. ```$onlineSch[1]```contient la planification hebdomadaire hello
3. ```$onlineSch[2]```contient la planification mensuelle de hello
4. ```$onlineSch[3]```contient la planification annuelle de hello

Si vous avez besoin de la planification hebdomadaire toomodify hello, vous devez toorefer toohello ```$onlineSch[1]```.

### <a name="initial-backup"></a>Sauvegarde initiale
Lorsque la sauvegarde un datasource de hello première fois, DPM doit crée réplica initial qui crée une copie complète de hello toobe de source de données protégée sur le volume du réplica DPM. Cette activité peuvent être planifiée pour une durée spécifique, ou peut être déclenchée manuellement, à l’aide de hello [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) applet de commande avec le paramètre hello ```-NOW```.

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a>Modification de la taille de hello du réplica DPM et le volume des points de récupération
Vous pouvez également modifier la taille du volume du réplica DPM et le volume de cliché instantané à l’aide de hello [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) applet de commande comme hello l’exemple suivant : Get-DatasourceDiskAllocation - source de données $DS Set-DatasourceDiskAllocation - Datasource $DS - ProtectionGroup $MPG-manuel - ReplicaArea (2 Go) - ShadowCopyArea (2 Go)

### <a name="committing-hello-changes-toohello-protection-group"></a>Validation hello change toohello groupe de Protection
Enfin, les modifications de hello doivent toobe validée que DPM puisse être sauvegarde hello par la nouvelle configuration de groupe de Protection hello. Cela peut être obtenue à l’aide de hello [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) applet de commande.

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a>Afficher des points de sauvegarde hello
Vous pouvez utiliser hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) tooget de l’applet de commande une liste de tous les points de récupération pour une source de données. Dans cet exemple, nous allons :

* FETCH tous hello pages sur le serveur DPM hello et stockées dans un tableau```$PG```
* obtenir toohello correspondante de sources de données hello```$PG[0]```
* obtenir tous les points de récupération hello pour une source de données.

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a>Restaurer des données protégées sur Azure
La restauration des données est une combinaison d'un objet ```RecoverableItem``` et d’un objet ```RecoveryOption```. Dans la section précédente de hello, nous avons obtenu une liste de points de sauvegarde hello pour une source de données.

Dans l’exemple hello ci-dessous, nous allons montrer comment la machine virtuelle de toorestore Hyper-V à partir d’Azure Backup en combinant les points de sauvegarde avec hello cibler pour la récupération. Cet exemple inclut :

* Création d’une option de récupération à l’aide de hello [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) applet de commande.
* Tableau de hello l’extraction des points de sauvegarde à l’aide de hello ```Get-DPMRecoveryPoint``` applet de commande.
* Choix d’un toorestore de point de sauvegarde à partir de.

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

commandes Hello peuvent facilement être étendus pour n’importe quel type de source de données.

## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur DPM tooAzure sauvegarde consultez [Introduction tooDPM sauvegarde](backup-azure-dpm-introduction.md)
