---
title: aaaAutomated v2 de sauvegarde pour les Machines virtuelles Azure 2016 SQL Server | Documents Microsoft
description: "Explique la fonctionnalité de sauvegarde automatisée hello pour SQL Server 2016 machines virtuelles s’exécutant dans Azure. Cet article est tooVMs spécifique à l’aide de hello Gestionnaire de ressources."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: ebd23868-821c-475b-b867-06d4a2e310c7
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/05/2017
ms.author: jroth
ms.openlocfilehash: a322792fb22c76bfa74fafb711b8b1927a6e2b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-v2-for-sql-server-2016-azure-virtual-machines-resource-manager"></a>Sauvegarde automatisée version 2 pour SQL Server 2016 dans des machines virtuelles Azure (Resource Manager)

> [!div class="op_single_selector"]
> * [SQL Server 2014](virtual-machines-windows-sql-automated-backup.md)
> * [SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md)

V2 de sauvegarde automatisée configure automatiquement [tooMicrosoft de gestion de sauvegarde Azure](https://msdn.microsoft.com/library/dn449496.aspx) pour toutes les bases de données nouvelles et existantes sur une machine virtuelle de Azure exécutant les éditions de SQL Server 2016 : Standard, Enterprise ou Developer. Cela vous permet de tooconfigure des sauvegardes régulières de la base de données qui utilisent le stockage d’objets blob Azure durable. V2 de sauvegarde automatisée dépend hello [Extension de l’Agent SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>Composants requis
toouse v2 de sauvegarde automatisée, passez en revue les hello suivant des conditions préalables :

**Système d’exploitation**:

- Windows Server 2012 R2
- Windows Server 2016

**Édition/version de SQL Server**:

- SQL Server 2016 Standard
- SQL Server 2016 Enterprise
- SQL Server 2016 Developer

> [!IMPORTANT]
> La sauvegarde automatisée version 2 fonctionne avec SQL Server 2016. Si vous utilisez SQL Server 2014, vous pouvez utiliser la sauvegarde automatisée v1 tooback vos bases de données. Pour plus d’informations, voir [Sauvegarde automatisée pour SQL Server 2014 dans les machines virtuelles Azure](virtual-machines-windows-sql-automated-backup.md).

**Configuration de la base de données**:

- Bases de données cible doivent utiliser le mode de récupération complète hello. Pour plus d’informations sur l’impact de hello hello complète du mode de récupération sur les sauvegardes, consultez [hello sauvegarde sous le mode de récupération complète](https://technet.microsoft.com/library/ms190217.aspx).
- Bases de données système n’ont pas de mode de récupération complète toouse. Toutefois, si vous avez besoin toobe de sauvegardes de journal nécessaire pour le modèle ou MSDB, vous devez utiliser le mode de récupération complète.
- Bases de données cible doivent être sur une instance de SQL Server par défaut hello. Hello IaaS Extension de SQL Server ne prend pas en charge les instances nommées.

**Modèle de déploiement Azure** :

- Gestionnaire de ressources

> [!NOTE]
> Sauvegarde automatisée s’appuie sur hello **Extension de l’Agent SQL Server IaaS**. Les images actuelles de la galerie de machines virtuelles SQL ajoutent cette extension par défaut. Pour plus d’informations, consultez [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md)(Extension de l’agent IaaS SQL Server).

## <a name="settings"></a>Paramètres
Hello tableau suivant décrit les options de hello qui peuvent être configurées pour la sauvegarde automatisée v2. étapes de configuration réelles Hello varient selon que vous utilisez hello portail Azure ou des commandes PowerShell de Windows Azure.

### <a name="basic-settings"></a>Paramètres de base

| Paramètre | Plage (par défaut) | Description |
| --- | --- | --- |
| **Sauvegarde automatisée** | Activer/Désactiver (désactivé) | Active ou désactive la sauvegarde automatisée d’une machine virtuelle Azure exécutant SQL Server 2016 Standard ou Enterprise. |
| **Période de rétention** | 1 à 30 jours (30 jours) | nombre de Hello de sauvegardes de tooretain jours. |
| **Compte de stockage** | Compte Azure Storage | Un toouse de compte de stockage Azure pour stocker les fichiers de sauvegarde automatisée dans le stockage blob. Un conteneur est créé à cet emplacement toostore tous les fichiers de sauvegarde. fichier de sauvegarde Hello convention d’affectation de noms inclut hello date, heure et la base de données GUID. |
| **Chiffrement** |Activer/Désactiver (désactivé) | Active ou désactive le chiffrement. Lorsque le chiffrement est activé, hello certificats utilisés toorestore hello sauvegarde se trouvent dans hello spécifié du compte de stockage Bonjour même **automaticbackup** conteneur à l’aide de hello même convention d’affectation de noms. Si le mot de passe hello change, un nouveau certificat est généré avec ce mot de passe, mais hello ancien certificat est conservé toorestore les sauvegardes antérieures. |
| **Mot de passe** |Texte du mot de passe | Mot de passe pour les clés de chiffrement. Il est uniquement requis si le chiffrement est activé. Dans l’ordre toorestore une sauvegarde chiffrée, vous devez avoir mot de passe correct hello et du certificat associé qui a été utilisé au moment de hello hello sauvegarde a été effectuée. |

### <a name="advanced-settings"></a>Paramètres avancés

| Paramètre | Plage (par défaut) | Description |
| --- | --- | --- |
| **Sauvegardes de bases de données système** | Activer/Désactiver (désactivé) | Lorsque activé, cette fonctionnalité sera également sauvegarder les bases de données système hello : Master, MSDB et Model. Hello MSDB et des bases de données de modèle, vérifiez qu’ils sont en mode de récupération complète si vous souhaitez que toobe de sauvegardes de journal effectuée. Les sauvegardes de journaux ne sont jamais effectuées pour Master. Et aucune sauvegarde n’est effectuée pour TempDB. |
| **Planification de sauvegarde** | Manuelle/automatisée (automatisée) | Par défaut, planification de sauvegarde hello est automatiquement déterminée en fonction de la croissance du journal hello. Planification de la sauvegarde manuelle permet de fenêtre de temps hello utilisateur toospecify hello pour les sauvegardes. Dans ce cas, les sauvegardes seront uniquement n’aient lieu au moment de hello spécifié fréquence et pendant hello fenêtre de temps d’un jour donné. |
| **Fréquence de sauvegarde complète** | Quotidienne/hebdomadaire | Fréquence des sauvegardes complètes. Dans les deux cas, les sauvegardes complètes commence au cours de la fenêtre d’heure planifiée suivante hello. Si vous sélectionnez l’option Hebdomadaire, les sauvegardes peuvent s’étaler sur plusieurs jours jusqu'à ce que toutes les bases de données aient été sauvegardées avec succès. |
| **Heure de début de la sauvegarde complète** | 00:00 – 23:00 (01:00) | Heure de début d’un jour donné où des sauvegardes complètes peuvent être effectuées. |
| **Fenêtre de temps de la sauvegarde complète** | 1 à 23 heures (1 heure) | Durée hello de fenêtre de temps d’un jour donné au cours de laquelle les sauvegardes complètes peuvent avoir lieu. |
| **Fréquence de sauvegarde des journaux** | 5 à 60 minutes (60 minutes) | Fréquence des sauvegardes de journaux. |

## <a name="understanding-full-backup-frequency"></a>Présentation de la fréquence de sauvegarde complète
Il est la différence de hello toounderstand important entre les sauvegardes complètes quotidiennes ou hebdomadaires. Ici, nous étudierons deux exemples de scénarios.

### <a name="scenario-1-weekly-backups"></a>Scénario 1 : Sauvegardes hebdomadaires
Vous utilisez une machine virtuelle SQL Server qui contient plusieurs bases de données très volumineuses.

Lundi, vous activez v2 de sauvegarde automatisée avec hello suivant les paramètres :

- Planification de sauvegarde : **Manuelle**
- Fréquence de sauvegarde complète : **Hebdomadaire**
- Heure de début de la sauvegarde complète : **01:00**
- Fenêtre de temps de la sauvegarde complète : **1 heure**

Cela signifie que hello prochaine sauvegarde fenêtre disponible mardi à 1 h 00 pour 1 heure. À ce stade, la sauvegarde automatisée commence à sauvegarder vos bases de données une par une. Dans ce scénario, vos bases de données sont suffisamment grands pour que les sauvegardes complètes va s’achever pour hello abord deux bases de données. Toutefois, après une heure toutes les bases de données hello ont été sauvegardés.

Dans ce cas, sauvegarde automatisée commencera sauvegarde hello restant hello de bases de données à jour suivant, le mercredi à 1 h 00 pour 1 heure. Si pas toutes les bases de données ont été sauvegardés pendant cette période, il tentera à nouveau hello hello mise à jour même temps. Cette opération se poursuit jusqu'à ce que toutes les bases de données aient été correctement sauvegardées.

Le mardi suivant, la sauvegarde automatisée recommencera à sauvegarder toutes les bases de données.

Ce scénario montre que la sauvegarde automatisée ne fonctionnera que dans la fenêtre de temps spécifié hello, et chaque base de données est sauvegardé une fois par semaine. Il montre également qu’il est possible pour les sauvegardes toospan plusieurs jours Bonjour cas où il n’est pas possible de toocomplete toutes les sauvegardes en un seul jour.

### <a name="scenario-2-daily-backups"></a>Scénario 2 : Sauvegardes quotidiennes
Vous utilisez une machine virtuelle SQL Server qui contient plusieurs bases de données très volumineuses.

Lundi, vous activez v2 de sauvegarde automatisée avec hello suivant les paramètres :

- Planification de sauvegarde : Manuelle
- Fréquence de sauvegarde complète : Quotidienne
- Heure de début de la sauvegarde complète : 22:00
- Fenêtre de temps de la sauvegarde complète : 6 heures

Cela signifie que Hello suivant disponible fenêtre de sauvegarde est le lundi à 22 h 00 pendant 6 heures. À ce stade, la sauvegarde automatisée commence à sauvegarder vos bases de données une par une.

Puis des sauvegardes complètes de toutes les bases de données seront relancées mardi à 22 h 00 pendant 6 heures.

> [!IMPORTANT]
> Lors de la planification des sauvegardes quotidiennes, il est recommandé de planifier l’exécution d’une tooensure de fenêtre de temps large toutes les bases de données peuvent être sauvegardées dans ce délai. Cela est particulièrement important dans le cas de hello si vous avez une grande quantité de données tooback des.

## <a name="configuration-in-hello-portal"></a>Configuration Bonjour portail

Vous pouvez utiliser v2 de sauvegarde automatisée tooconfigure portail Azure hello lors de la configuration ou de SQL Server 2016 des machines virtuelles existantes.

### <a name="new-vms"></a>Nouvelles machines virtuelles

Utilisez v2 de sauvegarde automatisée hello tooconfigure portail Azure lorsque vous créez une nouvelle Machine virtuelle SQL Server 2016 dans le modèle de déploiement du Gestionnaire de ressources hello. 

Bonjour **paramètres SQL Server** panneau, sélectionnez **sauvegarde**. Bonjour Azure portail montre hello **sauvegarde automatisée SQL** panneau.

![Configuration d’une sauvegarde automatisée SQL dans le portail Azure](./media/virtual-machines-windows-sql-automated-backup-v2/automated-backup-blade.png)

> [!NOTE]
> La sauvegarde automatisée version 2 est désactivée par défaut.

Pour le contexte, consultez la rubrique complète de hello relative [approvisionner un ordinateur virtuel de SQL Server dans Azure](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>Machines virtuelles existantes

Pour les machines virtuelles SQL Server existantes, sélectionnez votre machine virtuelle SQL Server. Puis sélectionnez hello **configuration de SQL Server** section Hello **paramètres** panneau.

![Sauvegarde automatisée SQL pour les machines virtuelles existantes](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration.png)

Bonjour **configuration de SQL Server** panneau, cliquez sur hello **modifier** bouton Bonjour automatisée de section de sauvegarde.

![Configurer la sauvegarde automatisée SQL pour les machines virtuelles existantes](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration-edit.png)

Lorsque vous avez terminé, cliquez sur hello **OK** bouton bas hello Hello **configuration de SQL Server** panneau toosave vos modifications.

Si vous activez le sauvegarde automatisée pour hello première fois, Azure configure hello Agent SQL Server IaaS en arrière-plan de hello. Pendant ce temps, hello portail Azure peut ne pas affiche que la sauvegarde automatisée est configurée. Attendez quelques minutes pour hello toobe de l’agent installé, configuré. Après ce hello Azure portal reflètent les nouveaux paramètres de hello.

## <a name="configuration-with-powershell"></a>Configuration avec PowerShell

Vous pouvez utiliser PowerShell tooconfigure v2 de sauvegarde automatisée. Avant de commencer, vous devez :

- [Téléchargez et installez hello la dernière version d’Azure PowerShell](http://aka.ms/webpi-azps).
- Ouvrir Windows PowerShell et l’associer à votre compte. Vous pouvez faire cela hello comme suit dans hello [configurer votre abonnement](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section Hello rubrique de configuration.

### <a name="install-hello-sql-iaas-extension"></a>Installer hello IaaS Extension de SQL
Si vous avez configuré un ordinateur virtuel SQL Server hello portail Azure, hello IaaS Extension de SQL Server doit déjà être installé. Vous pouvez déterminer si elle est installée pour votre machine virtuelle en appelant **Get-AzureRmVM** commande et en examinant hello **Extensions** propriété.

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions 
```

Si hello extension SQL Server IaaS Agent est installé, vous devez voir qu'il répertorié comme « Sqliaasagent n’est » ou « SQLIaaSExtension ». **ProvisioningState** pour l’extension de hello doit également indiquer « Réussi ». 

S’il n’est pas installé ou a échoué toobe configuré, vous pouvez l’installer avec hello commande suivante. Dans Ajout toohello nom et ressource groupe virtuelle, vous devez également spécifier la région de hello (**$region**) où se trouve votre machine virtuelle.

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region 
```

### <a id="verifysettings"></a> Vérifier les paramètres actuels
Si vous avez activé la sauvegarde automatisée lors de la configuration, vous pouvez utiliser PowerShell toocheck votre configuration actuelle. Exécutez hello **Get-AzureRmVMSqlServerExtension** de commandes et examiner hello **AutoBackupSettings** propriété :

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

Vous devez obtenir suivant toohello similaire de sortie :

```
Enable                      : True
EnableEncryption            : False
RetentionPeriod             : 30
StorageUrl                  : https://test.blob.core.windows.net/
StorageAccessKey            :  
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : Manual
FullBackupFrequency         : WEEKLY
FullBackupStartTime         : 2
FullBackupWindowHours       : 2
LogBackupFrequency          : 60
```

Si votre sortie montre que **activer** est défini trop**False**, vous devez effectuer des sauvegardes automatiques tooenable. Bonjour excellente est activer et configurer la sauvegarde automatisée Bonjour identique. Consultez hello la section suivante pour obtenir des informations.

> [!NOTE] 
> Si vous vérifiez les paramètres de hello immédiatement après une modification, il est possible que vous obtenez les valeurs de configuration anciennes hello. Attendez quelques minutes et vérifier les paramètres de hello à nouveau les toomake sûr que vos modifications ont été appliquées.

### <a name="configure-automated-backup-v2"></a>Configurer une sauvegarde automatisée version 2
Vous pouvez utiliser les PowerShell tooenable la sauvegarde, ainsi que toomodify sa configuration et son comportement à tout moment. 

Tout d’abord, sélectionnez ou créez un compte de stockage hello pour les fichiers de sauvegarde. Hello script suivant sélectionne un compte de stockage ou la crée si elle n’existe pas.

```powershell
$storage_accountname = “yourstorageaccount”
$storage_resourcegroupname = $resourcegroupname

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region } 
```

> [!NOTE]
> La sauvegarde automatisée ne prend pas en charge le stockage des sauvegardes dans un stockage Premium, mais elle peut effectuer des sauvegardes à partir de disques de machines virtuelles qui utilisent le stockage Premium.

Utilisez ensuite hello **New-AzureRmVMSqlServerAutoBackupConfig** tooenable de commande et de configurer des sauvegardes de toostore paramètres hello v2 de sauvegarde automatisée dans le compte de stockage Azure hello. Dans cet exemple, les sauvegardes de hello sont définies toobe conservée pendant 10 jours. Les sauvegardes de bases de données système sont activées. Les sauvegardes complètes sont planifiées pour être effectuées toutes les semaines, avec une fenêtre de temps commençant à 20 h 00 pendant deux heures. Les sauvegardes de journaux sont planifiées pour être effectuées toutes les 30 minutes. Hello la deuxième commande, **Set-AzureRmVMSqlServerExtension**, hello de mises à jour spécifié de machine virtuelle Azure avec ces paramètres.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname 
```

Il peut prendre plusieurs minutes tooinstall et configurer hello IaaS Agent SQL Server. 

le chiffrement tooenable, modifier hello toopass script précédent de hello **EnableEncryption** paramètre avec un mot de passe (chaîne sécurisée) hello **CertificatePassword** paramètre. Hello script suivant active les paramètres de sauvegarde automatisée hello dans l’exemple précédent de hello et ajoute le chiffrement.

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

tooconfirm vos paramètres sont appliqués, [vérifier la configuration de sauvegarde automatisée hello](#verifysettings).

### <a name="disable-automated-backup"></a>Désactiver la sauvegarde automatisée
toodisable sauvegarde automatisée, exécution hello même script sans hello **-activer** paramètre toohello **New-AzureRmVMSqlServerAutoBackupConfig** commande. Hello absence de hello **-activer** fonctionnalité de paramètre signaux hello commande toodisable hello. Comme avec l’installation, il peut prendre plusieurs minutes toodisable la sauvegarde.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a>Exemple de script
Hello script suivant fournit un ensemble de variables que vous pouvez personnaliser tooenable et configurer la sauvegarde automatisée pour votre machine virtuelle. Dans ce cas, vous devrez peut-être le script de hello toocustomize selon vos besoins. Par exemple, vous auraient toomake modifications si vous souhaitez que la sauvegarde de hello toodisable de bases de données système ou activer le chiffrement.

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10
$backupscheduletype = "Manual"
$fullbackupfrequency = "Weekly"
$fullbackupstarthour = "20"
$fullbackupwindow = "2"
$logbackupfrequency = "30"

# ResourceGroupName is hello resource group which is hosting hello VM where you are deploying hello SQL IaaS Extension 

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account toostore hello backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType $backupscheduletype -FullBackupFrequency $fullbackupfrequency `
    -FullBackupStartHour $fullbackupstarthour -FullBackupWindowInHours $fullbackupwindow `
    -LogBackupFrequencyInMinutes $logbackupfrequency

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>Étapes suivantes
La sauvegarde automatisée v2 configure une sauvegarde managée sur les machines virtuelles Azure. Il est donc important trop[passez en revue la documentation hello pour la gestion de sauvegarde](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello comportement et les implications.

Vous pouvez trouver de sauvegarde supplémentaire et restaurer des conseils pour SQL Server sur des machines virtuelles Azure dans la rubrique suivante de hello : [sauvegarde et de restauration pour SQL Server dans Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).

Pour plus d’informations sur les autres tâches d’automatisation disponibles, voir [Extension de l’agent IaaS SQL Server](virtual-machines-windows-sql-server-agent-extension.md).

Pour plus d’informations sur l’exécution de SQL Server sur des machines virtuelles Azure, voir [Vue d’ensemble de SQL Server sur les machines virtuelles Azure](virtual-machines-windows-sql-server-iaas-overview.md).

