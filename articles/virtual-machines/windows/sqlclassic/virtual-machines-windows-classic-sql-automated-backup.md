---
title: aaaAutomated sauvegarde pour les Machines virtuelles SQL Server (classiques) | Documents Microsoft
description: "Explique la fonctionnalité de sauvegarde automatisée hello pour SQL Server s’exécutant dans des Machines virtuelles Azure à l’aide du Gestionnaire de ressources. "
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 3333e830-8a60-42f5-9f44-8e02e9868d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 5d8f0412578c2d86edc6e54093a5da4891d3847e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-in-azure-virtual-machines-classic"></a>Sauvegarde automatisée pour SQL Server dans les machines virtuelles Azure (classiques)
> [!div class="op_single_selector"]
> * [Gestionnaire de ressources](../sql/virtual-machines-windows-sql-automated-backup.md)
> * [Classique](../classic/sql-automated-backup.md)
> 
> 

Sauvegarde automatisée configure automatiquement [tooMicrosoft de gestion de sauvegarde Azure](https://msdn.microsoft.com/library/dn449496.aspx) pour toutes les bases de données nouvelles et existantes sur une machine virtuelle de Azure exécutant SQL Server 2014 Standard ou Enterprise. Cela vous permet de tooconfigure des sauvegardes régulières de la base de données qui utilisent le stockage d’objets blob Azure durable. Sauvegarde automatisée dépend hello [Extension de l’Agent SQL Server IaaS](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../azure-resource-manager/resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. version de gestionnaire de ressources hello tooview de cet article, consultez [sauvegarde automatisée pour SQL Server dans le Gestionnaire de ressources de Machines virtuelles Azure](../sql/virtual-machines-windows-sql-automated-backup.md).

## <a name="prerequisites"></a>Composants requis
toouse la sauvegarde, tenez compte des hello suivant des conditions préalables :

**Système d’exploitation**:

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**Édition/version de SQL Server**:

* SQL Server 2014 Standard
* SQL Server 2014 Enterprise

> [!NOTE]
> SQL Server 2016 n’est pas encore pris en charge pour la sauvegarde automatisée.
> 
> 

**Configuration de la base de données**:

* Bases de données cible doivent utiliser le mode de récupération complète hello.

**Azure PowerShell**:

* [Installez les commandes Azure PowerShell dernière hello](/powershell/azure/overview).

**Extension IaaS SQL Server**:

* [Installer l’IaaS Extension de SQL Server de hello](../classic/sql-server-agent-extension.md).

## <a name="settings"></a>Paramètres
Hello tableau suivant décrit les options de hello qui peuvent être configurées pour la sauvegarde automatisée. Pour les machines virtuelles classiques, vous devez utiliser PowerShell tooconfigure ces paramètres.

| Paramètre | Plage (par défaut) | Description |
| --- | --- | --- |
| **Sauvegarde automatisée** |Activer/Désactiver (désactivé) |Active ou désactive la sauvegarde automatisée d’une machine virtuelle Azure exécutant SQL Server 2014 Standard ou Enterprise. |
| **Période de rétention** |1 à 30 jours (30 jours) |nombre de Hello de jours tooretain une sauvegarde. |
| **Compte de stockage** |Compte de stockage Azure (compte de stockage hello créé pour hello spécifié de machine virtuelle) |Un toouse de compte de stockage Azure pour stocker les fichiers de sauvegarde automatisée dans le stockage blob. Un conteneur est créé à cet emplacement toostore tous les fichiers de sauvegarde. fichier de sauvegarde Hello convention d’affectation de noms inclut hello date, heure et nom de l’ordinateur. |
| **Chiffrement** |Activer/Désactiver (désactivé) |Active ou désactive le chiffrement. Lorsque le chiffrement est activé, les certificats hello sauvegarde de hello toorestore utilisés sont situés dans hello spécifié compte de stockage Bonjour à l’aide du même automaticbackup conteneur hello même convention d’affectation de noms. Si le mot de passe hello change, un nouveau certificat est généré avec ce mot de passe, mais hello ancien certificat est conservé toorestore les sauvegardes antérieures. |
| **Mot de passe** |Texte du mot de passe (aucun) |Mot de passe pour les clés de chiffrement. Il est uniquement requis si le chiffrement est activé. Dans l’ordre toorestore une sauvegarde chiffrée, vous devez avoir mot de passe correct hello et du certificat associé qui a été utilisé au moment de hello hello sauvegarde a été effectuée. | **Sauvegarde des bases de données système** | Activer/Désactiver (désactivé) | Effectue des sauvegardes complètes des bases de données Master, Model et MSDB |
| **Configuration de la planification de sauvegarde** | Manuelle/automatisée (automatisée) | Sélectionnez **automatisée** tooautomatically exploiter pleinement et en fonction de la croissance du journal des sauvegardes de journaux. Sélectionnez **manuel** planification de hello toospecify pour complète et sauvegardes de journaux. |

## <a name="configuration-with-powershell"></a>Configuration avec PowerShell
Bonjour PowerShell l’exemple suivant, la sauvegarde automatisée est configurée pour un ordinateur SQL Server 2014 virtuel existant. Hello **New-AzureVMSqlServerAutoBackupConfig** commande configure les sauvegardes de toostore de paramètres de sauvegarde automatisée hello de compte de stockage Azure hello spécifié par la variable de hello $storageaccount. Ces sauvegardes sont conservées pendant 10 jours. Hello **Set-AzureVMSqlServerExtension** commande hello de mises à jour spécifié de machine virtuelle Azure avec ces paramètres.

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

Il peut prendre plusieurs minutes tooinstall et configurer hello IaaS Agent SQL Server.

le chiffrement tooenable, modifier hello précédent script toopass hello paramètre EnableEncryption et un mot de passe (chaîne sécurisée) pour le paramètre CertificatePassword de hello. Hello script suivant active les paramètres de sauvegarde automatisée hello dans l’exemple précédent de hello et ajoute le chiffrement.

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

sauvegarde automatique de toodisable, exécution hello même script sans hello **-activer** paramètre toohello **New-AzureVMSqlServerAutoBackupConfig**. Comme avec l’installation, il peut prendre plusieurs minutes toodisable la sauvegarde.

> [!NOTE]
> Désactivation et désinstallation hello IaaS Agent SQL Server ne suppriment pas les paramètres de sauvegarde managée hello précédemment configuré. Vous devez désactiver la sauvegarde automatisée avant la désactivation ou la désinstallation de hello IaaS Agent SQL Server.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
La sauvegarde automatisée configure une sauvegarde managée sur les machines virtuelles Azure. Il est donc important trop[passez en revue la documentation hello pour la gestion de sauvegarde](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello comportement et les implications.

Vous pouvez trouver de sauvegarde supplémentaire et restaurer des conseils pour SQL Server sur des machines virtuelles Azure dans la rubrique suivante de hello : [sauvegarde et de restauration pour SQL Server dans Azure Virtual Machines](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).

Pour plus d’informations sur les autres tâches d’automatisation disponibles, voir [Extension de l’agent IaaS SQL Server](../classic/sql-server-agent-extension.md).

Pour plus d’informations sur l’exécution de SQL Server sur des machines virtuelles Azure, voir [Vue d’ensemble de SQL Server sur les machines virtuelles Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

