---
title: aaaAutomated sauvegarde pour les Machines virtuelles Azure 2014 SQL Server | Documents Microsoft
description: "Explique la fonctionnalité de sauvegarde automatisée hello pour SQL Server 2014 machines virtuelles s’exécutant dans Azure. Cet article est tooVMs spécifique à l’aide de hello Gestionnaire de ressources."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: bdc63fd1-db49-4e76-87d5-b5c6a890e53c
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: c6803d8ef9f80e44a2f87918d87e099f1b562483
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a>Sauvegarde automatisée pour les machines virtuelles SQL Server 2014 (Resource Manager)

> [!div class="op_single_selector"]
> * [SQL Server 2014](virtual-machines-windows-sql-automated-backup.md)
> * [SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md)

Sauvegarde automatisée configure automatiquement [tooMicrosoft de gestion de sauvegarde Azure](https://msdn.microsoft.com/library/dn449496.aspx) pour toutes les bases de données nouvelles et existantes sur une machine virtuelle de Azure exécutant SQL Server 2014 Standard ou Enterprise. Cela vous permet de tooconfigure des sauvegardes régulières de la base de données qui utilisent le stockage d’objets blob Azure durable. Sauvegarde automatisée dépend hello [Extension de l’Agent SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>Composants requis
toouse la sauvegarde, tenez compte des hello suivant des conditions préalables :

**Système d’exploitation**:

- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016

**Édition/version de SQL Server**:

- SQL Server 2014 Standard
- SQL Server 2014 Enterprise

> [!IMPORTANT]
> La sauvegarde automatisée fonctionne avec SQL Server 2014. Si vous utilisez SQL Server 2016, vous pouvez utiliser la sauvegarde automatisée v2 tooback vos bases de données. Pour plus d’informations, consultez [Sauvegarde automatisée en version 2 pour les machines virtuelles Azure SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md).

**Configuration de la base de données**:

- Bases de données cible doivent utiliser le mode de récupération complète hello. Pour plus d’informations sur l’impact de hello hello complète du mode de récupération sur les sauvegardes, consultez [hello sauvegarde sous le mode de récupération complète](https://technet.microsoft.com/library/ms190217.aspx).
- Bases de données cible doivent être sur une instance de SQL Server par défaut hello. Hello IaaS Extension de SQL Server ne prend pas en charge les instances nommées.

**Modèle de déploiement Azure** :

- Gestionnaire de ressources

**Azure PowerShell**:

- [Installez les commandes Azure PowerShell dernière hello](/powershell/azure/overview) si vous envisagez de tooconfigure sauvegarde automatisée avec PowerShell.

> [!NOTE]
> Sauvegarde automatisée s’appuie sur hello Extension de l’Agent SQL Server IaaS. Les images actuelles de la galerie de machines virtuelles SQL ajoutent cette extension par défaut. Pour plus d’informations, consultez [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md)(Extension de l’agent IaaS SQL Server).

## <a name="settings"></a>Paramètres

Hello tableau suivant décrit les options de hello qui peuvent être configurées pour la sauvegarde automatisée. étapes de configuration réelles Hello varient selon que vous utilisez hello portail Azure ou des commandes PowerShell de Windows Azure.

| Paramètre | Plage (par défaut) | Description |
| --- | --- | --- |
| **Sauvegarde automatisée** | Activer/Désactiver (désactivé) | Active ou désactive la sauvegarde automatisée d’une machine virtuelle Azure exécutant SQL Server 2014 Standard ou Enterprise. |
| **Période de rétention** | 1 à 30 jours (30 jours) | nombre de Hello de jours tooretain une sauvegarde. |
| **Compte de stockage** | Compte Azure Storage | Un toouse de compte de stockage Azure pour stocker les fichiers de sauvegarde automatisée dans le stockage blob. Un conteneur est créé à cet emplacement toostore tous les fichiers de sauvegarde. fichier de sauvegarde Hello convention d’affectation de noms inclut hello date, heure et nom de l’ordinateur. |
| **Chiffrement** | Activer/Désactiver (désactivé) | Active ou désactive le chiffrement. Lorsque le chiffrement est activé, hello certificats utilisés toorestore hello sauvegarde se trouvent dans hello spécifié du compte de stockage Bonjour même `automaticbackup` conteneur à l’aide de hello même convention d’affectation de noms. Si le mot de passe hello change, un nouveau certificat est généré avec ce mot de passe, mais hello ancien certificat est conservé toorestore les sauvegardes antérieures. |
| **Mot de passe** | Texte du mot de passe | Mot de passe pour les clés de chiffrement. Il est uniquement requis si le chiffrement est activé. Dans l’ordre toorestore une sauvegarde chiffrée, vous devez avoir mot de passe correct hello et du certificat associé qui a été utilisé au moment de hello hello sauvegarde a été effectuée. |

## <a name="configuration-in-hello-portal"></a>Configuration Bonjour portail

Vous pouvez utiliser hello tooconfigure portail Azure la sauvegarde lors de la configuration ou de machines virtuelles SQL Server 2014 existantes.

### <a name="new-vms"></a>Nouvelles machines virtuelles

Utilisez hello tooconfigure portail Azure la sauvegarde lorsque vous créez une nouvelle Machine virtuelle SQL Server 2014 dans le modèle de déploiement du Gestionnaire de ressources hello.

Bonjour **paramètres SQL Server** panneau, sélectionnez **sauvegarde**. Bonjour Azure portail montre hello **sauvegarde automatisée SQL** panneau.

![Configuration d’une sauvegarde automatisée SQL dans le portail Azure](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

Pour le contexte, consultez la rubrique complète de hello relative [approvisionner un ordinateur virtuel de SQL Server dans Azure](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>Machines virtuelles existantes

Pour les machines virtuelles SQL Server existantes, sélectionnez votre machine virtuelle SQL Server. Puis sélectionnez hello **configuration de SQL Server** section Hello **paramètres** panneau.

![Sauvegarde automatisée SQL pour les machines virtuelles existantes](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

Bonjour **configuration de SQL Server** panneau, cliquez sur hello **modifier** bouton Bonjour automatisée de section de sauvegarde.

![Configurer la sauvegarde automatisée SQL pour les machines virtuelles existantes](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

Lorsque vous avez terminé, cliquez sur hello **OK** bouton bas hello Hello **configuration de SQL Server** panneau toosave vos modifications.

Si vous activez le sauvegarde automatisée pour hello première fois, Azure configure hello Agent SQL Server IaaS en arrière-plan de hello. Pendant ce temps, hello portail Azure peut ne pas affiche que la sauvegarde automatisée est configurée. Attendez quelques minutes pour hello toobe de l’agent installé, configuré. Après ce hello Azure portal reflètent les nouveaux paramètres de hello.

> [!NOTE]
> Vous pouvez également configurer la sauvegarde automatisée à l’aide d’un modèle. Pour plus d’informations, consultez l’article [Azure quickstart template for Automated Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update)(Modèle de démarrage rapide d’Azure pour la sauvegarde automatisée).

## <a name="configuration-with-powershell"></a>Configuration avec PowerShell

Vous pouvez utiliser PowerShell tooconfigure la sauvegarde. Avant de commencer, vous devez :

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
Enable                      : False
EnableEncryption            : False
RetentionPeriod             : -1
StorageUrl                  : NOTSET
StorageAccessKey            : 
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : 
FullBackupFrequency         : 
FullBackupStartTime         : 
FullBackupWindowHours       : 
LogBackupFrequency          : 
```

Si votre sortie montre que **activer** est défini trop**False**, vous devez effectuer des sauvegardes automatiques tooenable. Bonjour excellente est activer et configurer la sauvegarde automatisée Bonjour identique. Consultez hello la section suivante pour obtenir des informations.

> [!NOTE] 
> Si vous vérifiez les paramètres de hello immédiatement après une modification, il est possible que vous obtenez les valeurs de configuration anciennes hello. Attendez quelques minutes et vérifier les paramètres de hello à nouveau les toomake sûr que vos modifications ont été appliquées.

### <a name="configure-automated-backup"></a>Configurer une sauvegarde automatisée
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

Utilisez ensuite hello **New-AzureRmVMSqlServerAutoBackupConfig** tooenable de commande et de configurer des sauvegardes de toostore de paramètres de sauvegarde automatisée hello Bonjour compte de stockage Azure. Dans cet exemple, les sauvegardes de hello sont définies toobe conservée pendant 10 jours. Hello la deuxième commande, **Set-AzureRmVMSqlServerExtension**, hello de mises à jour spécifié de machine virtuelle Azure avec ces paramètres.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

Il peut prendre plusieurs minutes tooinstall et configurer hello IaaS Agent SQL Server.

> [!NOTE]
> Autres paramètres pour **New-AzureRmVMSqlServerAutoBackupConfig** qui s’appliquent uniquement tooSQL Server 2016 et v2 de sauvegarde automatisée. SQL Server 2014 ne prend pas en charge hello suivant paramètres : **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**,  **FullBackupStartHour**, **FullBackupWindowInHours**, et **LogBackupFrequencyInMinutes**. Si vous essayez de tooconfigure ces paramètres sur un ordinateur virtuel de SQL Server 2014, il n’existe aucune erreur, mais les paramètres hello ne sont pas appliquées. Si vous souhaitez que ces paramètres sur un ordinateur virtuel de SQL Server 2016 toouse, consultez [v2 de sauvegarde automatisée pour les Machines virtuelles Azure 2016 SQL Server](virtual-machines-windows-sql-automated-backup-v2.md).

le chiffrement tooenable, modifier hello toopass script précédent de hello **EnableEncryption** paramètre avec un mot de passe (chaîne sécurisée) hello **CertificatePassword** paramètre. Hello script suivant active les paramètres de sauvegarde automatisée hello dans l’exemple précédent de hello et ajoute le chiffrement.

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

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
    -ResourceGroupName $storage_resourcegroupname

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>Étapes suivantes

La sauvegarde automatisée configure une sauvegarde managée sur les machines virtuelles Azure. Il est donc important trop[passez en revue la documentation hello pour la gestion de sauvegarde](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello comportement et les implications.

Vous pouvez trouver de sauvegarde supplémentaire et restaurer des conseils pour SQL Server sur des machines virtuelles Azure dans la rubrique suivante de hello : [sauvegarde et de restauration pour SQL Server dans Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).

Pour plus d’informations sur les autres tâches d’automatisation disponibles, voir [Extension de l’agent IaaS SQL Server](virtual-machines-windows-sql-server-agent-extension.md).

Pour plus d’informations sur l’exécution de SQL Server sur des machines virtuelles Azure, voir [Vue d’ensemble de SQL Server sur les machines virtuelles Azure](virtual-machines-windows-sql-server-iaas-overview.md).

