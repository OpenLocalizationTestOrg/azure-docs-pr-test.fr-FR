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
# <a name="automated-backup-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="e2249-103">Sauvegarde automatisée pour SQL Server dans les machines virtuelles Azure (classiques)</span><span class="sxs-lookup"><span data-stu-id="e2249-103">Automated Backup for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e2249-104">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="e2249-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="e2249-105">Classique</span><span class="sxs-lookup"><span data-stu-id="e2249-105">Classic</span></span>](../classic/sql-automated-backup.md)
> 
> 

<span data-ttu-id="e2249-106">Sauvegarde automatisée configure automatiquement [tooMicrosoft de gestion de sauvegarde Azure](https://msdn.microsoft.com/library/dn449496.aspx) pour toutes les bases de données nouvelles et existantes sur une machine virtuelle de Azure exécutant SQL Server 2014 Standard ou Enterprise.</span><span class="sxs-lookup"><span data-stu-id="e2249-106">Automated Backup automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="e2249-107">Cela vous permet de tooconfigure des sauvegardes régulières de la base de données qui utilisent le stockage d’objets blob Azure durable.</span><span class="sxs-lookup"><span data-stu-id="e2249-107">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="e2249-108">Sauvegarde automatisée dépend hello [Extension de l’Agent SQL Server IaaS](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e2249-108">Automated Backup depends on hello [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="e2249-109">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e2249-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e2249-110">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="e2249-110">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="e2249-111">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="e2249-111">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="e2249-112">version de gestionnaire de ressources hello tooview de cet article, consultez [sauvegarde automatisée pour SQL Server dans le Gestionnaire de ressources de Machines virtuelles Azure](../sql/virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="e2249-112">tooview hello Resource Manager version of this article, see [Automated Backup for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2249-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e2249-113">Prerequisites</span></span>
<span data-ttu-id="e2249-114">toouse la sauvegarde, tenez compte des hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="e2249-114">toouse Automated Backup, consider hello following prerequisites:</span></span>

<span data-ttu-id="e2249-115">**Système d’exploitation**:</span><span class="sxs-lookup"><span data-stu-id="e2249-115">**Operating System**:</span></span>

* <span data-ttu-id="e2249-116">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="e2249-116">Windows Server 2012</span></span>
* <span data-ttu-id="e2249-117">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="e2249-117">Windows Server 2012 R2</span></span>
* <span data-ttu-id="e2249-118">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="e2249-118">Windows Server 2016</span></span>

<span data-ttu-id="e2249-119">**Édition/version de SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="e2249-119">**SQL Server version/edition**:</span></span>

* <span data-ttu-id="e2249-120">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="e2249-120">SQL Server 2014 Standard</span></span>
* <span data-ttu-id="e2249-121">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="e2249-121">SQL Server 2014 Enterprise</span></span>

> [!NOTE]
> <span data-ttu-id="e2249-122">SQL Server 2016 n’est pas encore pris en charge pour la sauvegarde automatisée.</span><span class="sxs-lookup"><span data-stu-id="e2249-122">SQL Server 2016 is not yet supported for Automated Backup.</span></span>
> 
> 

<span data-ttu-id="e2249-123">**Configuration de la base de données**:</span><span class="sxs-lookup"><span data-stu-id="e2249-123">**Database configuration**:</span></span>

* <span data-ttu-id="e2249-124">Bases de données cible doivent utiliser le mode de récupération complète hello.</span><span class="sxs-lookup"><span data-stu-id="e2249-124">Target databases must use hello full recovery model.</span></span>

<span data-ttu-id="e2249-125">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="e2249-125">**Azure PowerShell**:</span></span>

* <span data-ttu-id="e2249-126">[Installez les commandes Azure PowerShell dernière hello](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e2249-126">[Install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="e2249-127">**Extension IaaS SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="e2249-127">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="e2249-128">[Installer l’IaaS Extension de SQL Server de hello](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="e2249-128">[Install hello SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="e2249-129">Paramètres</span><span class="sxs-lookup"><span data-stu-id="e2249-129">Settings</span></span>
<span data-ttu-id="e2249-130">Hello tableau suivant décrit les options de hello qui peuvent être configurées pour la sauvegarde automatisée.</span><span class="sxs-lookup"><span data-stu-id="e2249-130">hello following table describes hello options that can be configured for Automated Backup.</span></span> <span data-ttu-id="e2249-131">Pour les machines virtuelles classiques, vous devez utiliser PowerShell tooconfigure ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="e2249-131">For classic VMs, you must use PowerShell tooconfigure these settings.</span></span>

| <span data-ttu-id="e2249-132">Paramètre</span><span class="sxs-lookup"><span data-stu-id="e2249-132">Setting</span></span> | <span data-ttu-id="e2249-133">Plage (par défaut)</span><span class="sxs-lookup"><span data-stu-id="e2249-133">Range (Default)</span></span> | <span data-ttu-id="e2249-134">Description</span><span class="sxs-lookup"><span data-stu-id="e2249-134">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e2249-135">**Sauvegarde automatisée**</span><span class="sxs-lookup"><span data-stu-id="e2249-135">**Automated Backup**</span></span> |<span data-ttu-id="e2249-136">Activer/Désactiver (désactivé)</span><span class="sxs-lookup"><span data-stu-id="e2249-136">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="e2249-137">Active ou désactive la sauvegarde automatisée d’une machine virtuelle Azure exécutant SQL Server 2014 Standard ou Enterprise.</span><span class="sxs-lookup"><span data-stu-id="e2249-137">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="e2249-138">**Période de rétention**</span><span class="sxs-lookup"><span data-stu-id="e2249-138">**Retention Period**</span></span> |<span data-ttu-id="e2249-139">1 à 30 jours (30 jours)</span><span class="sxs-lookup"><span data-stu-id="e2249-139">1-30 days (30 days)</span></span> |<span data-ttu-id="e2249-140">nombre de Hello de jours tooretain une sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="e2249-140">hello number of days tooretain a backup.</span></span> |
| <span data-ttu-id="e2249-141">**Compte de stockage**</span><span class="sxs-lookup"><span data-stu-id="e2249-141">**Storage Account**</span></span> |<span data-ttu-id="e2249-142">Compte de stockage Azure (compte de stockage hello créé pour hello spécifié de machine virtuelle)</span><span class="sxs-lookup"><span data-stu-id="e2249-142">Azure storage account (hello storage account created for hello specified VM)</span></span> |<span data-ttu-id="e2249-143">Un toouse de compte de stockage Azure pour stocker les fichiers de sauvegarde automatisée dans le stockage blob.</span><span class="sxs-lookup"><span data-stu-id="e2249-143">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="e2249-144">Un conteneur est créé à cet emplacement toostore tous les fichiers de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="e2249-144">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="e2249-145">fichier de sauvegarde Hello convention d’affectation de noms inclut hello date, heure et nom de l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e2249-145">hello backup file naming convention includes hello date, time, and machine name.</span></span> |
| <span data-ttu-id="e2249-146">**Chiffrement**</span><span class="sxs-lookup"><span data-stu-id="e2249-146">**Encryption**</span></span> |<span data-ttu-id="e2249-147">Activer/Désactiver (désactivé)</span><span class="sxs-lookup"><span data-stu-id="e2249-147">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="e2249-148">Active ou désactive le chiffrement.</span><span class="sxs-lookup"><span data-stu-id="e2249-148">Enables or disables encryption.</span></span> <span data-ttu-id="e2249-149">Lorsque le chiffrement est activé, les certificats hello sauvegarde de hello toorestore utilisés sont situés dans hello spécifié compte de stockage Bonjour à l’aide du même automaticbackup conteneur hello même convention d’affectation de noms.</span><span class="sxs-lookup"><span data-stu-id="e2249-149">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same automaticbackup container using hello same naming convention.</span></span> <span data-ttu-id="e2249-150">Si le mot de passe hello change, un nouveau certificat est généré avec ce mot de passe, mais hello ancien certificat est conservé toorestore les sauvegardes antérieures.</span><span class="sxs-lookup"><span data-stu-id="e2249-150">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="e2249-151">**Mot de passe**</span><span class="sxs-lookup"><span data-stu-id="e2249-151">**Password**</span></span> |<span data-ttu-id="e2249-152">Texte du mot de passe (aucun)</span><span class="sxs-lookup"><span data-stu-id="e2249-152">Password text (None)</span></span> |<span data-ttu-id="e2249-153">Mot de passe pour les clés de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="e2249-153">A password for encryption keys.</span></span> <span data-ttu-id="e2249-154">Il est uniquement requis si le chiffrement est activé.</span><span class="sxs-lookup"><span data-stu-id="e2249-154">This is only required if encryption is enabled.</span></span> <span data-ttu-id="e2249-155">Dans l’ordre toorestore une sauvegarde chiffrée, vous devez avoir mot de passe correct hello et du certificat associé qui a été utilisé au moment de hello hello sauvegarde a été effectuée.</span><span class="sxs-lookup"><span data-stu-id="e2249-155">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> | <span data-ttu-id="e2249-156">**Sauvegarde des bases de données système**</span><span class="sxs-lookup"><span data-stu-id="e2249-156">**Backup system databases**</span></span> | <span data-ttu-id="e2249-157">Activer/Désactiver (désactivé)</span><span class="sxs-lookup"><span data-stu-id="e2249-157">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="e2249-158">Effectue des sauvegardes complètes des bases de données Master, Model et MSDB</span><span class="sxs-lookup"><span data-stu-id="e2249-158">Take full backups of Master, Model, and MSDB</span></span> |
| <span data-ttu-id="e2249-159">**Configuration de la planification de sauvegarde**</span><span class="sxs-lookup"><span data-stu-id="e2249-159">**Configure backup schedule**</span></span> | <span data-ttu-id="e2249-160">Manuelle/automatisée (automatisée)</span><span class="sxs-lookup"><span data-stu-id="e2249-160">Manual/Automated (Automated)</span></span> | <span data-ttu-id="e2249-161">Sélectionnez **automatisée** tooautomatically exploiter pleinement et en fonction de la croissance du journal des sauvegardes de journaux.</span><span class="sxs-lookup"><span data-stu-id="e2249-161">Select **Automated** tooautomatically take full and log backups based on log growth.</span></span> <span data-ttu-id="e2249-162">Sélectionnez **manuel** planification de hello toospecify pour complète et sauvegardes de journaux.</span><span class="sxs-lookup"><span data-stu-id="e2249-162">Select **Manual** toospecify hello schedule for full and log backups.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="e2249-163">Configuration avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2249-163">Configuration with PowerShell</span></span>
<span data-ttu-id="e2249-164">Bonjour PowerShell l’exemple suivant, la sauvegarde automatisée est configurée pour un ordinateur SQL Server 2014 virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="e2249-164">In hello following PowerShell example, Automated Backup is configured for an existing SQL Server 2014 VM.</span></span> <span data-ttu-id="e2249-165">Hello **New-AzureVMSqlServerAutoBackupConfig** commande configure les sauvegardes de toostore de paramètres de sauvegarde automatisée hello de compte de stockage Azure hello spécifié par la variable de hello $storageaccount.</span><span class="sxs-lookup"><span data-stu-id="e2249-165">hello **New-AzureVMSqlServerAutoBackupConfig** command configures hello Automated Backup settings toostore backups in hello Azure storage account specified by hello $storageaccount variable.</span></span> <span data-ttu-id="e2249-166">Ces sauvegardes sont conservées pendant 10 jours.</span><span class="sxs-lookup"><span data-stu-id="e2249-166">These backups will be retained for 10 days.</span></span> <span data-ttu-id="e2249-167">Hello **Set-AzureVMSqlServerExtension** commande hello de mises à jour spécifié de machine virtuelle Azure avec ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="e2249-167">hello **Set-AzureVMSqlServerExtension** command updates hello specified Azure VM with these settings.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="e2249-168">Il peut prendre plusieurs minutes tooinstall et configurer hello IaaS Agent SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e2249-168">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="e2249-169">le chiffrement tooenable, modifier hello précédent script toopass hello paramètre EnableEncryption et un mot de passe (chaîne sécurisée) pour le paramètre CertificatePassword de hello.</span><span class="sxs-lookup"><span data-stu-id="e2249-169">tooenable encryption, modify hello previous script toopass hello EnableEncryption parameter along with a password (secure string) for hello CertificatePassword parameter.</span></span> <span data-ttu-id="e2249-170">Hello script suivant active les paramètres de sauvegarde automatisée hello dans l’exemple précédent de hello et ajoute le chiffrement.</span><span class="sxs-lookup"><span data-stu-id="e2249-170">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="e2249-171">sauvegarde automatique de toodisable, exécution hello même script sans hello **-activer** paramètre toohello **New-AzureVMSqlServerAutoBackupConfig**.</span><span class="sxs-lookup"><span data-stu-id="e2249-171">toodisable automatic backup, run hello same script without hello **-Enable** parameter toohello **New-AzureVMSqlServerAutoBackupConfig**.</span></span> <span data-ttu-id="e2249-172">Comme avec l’installation, il peut prendre plusieurs minutes toodisable la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="e2249-172">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

> [!NOTE]
> <span data-ttu-id="e2249-173">Désactivation et désinstallation hello IaaS Agent SQL Server ne suppriment pas les paramètres de sauvegarde managée hello précédemment configuré.</span><span class="sxs-lookup"><span data-stu-id="e2249-173">Disabling and uninstalling hello SQL Server IaaS Agent does not remove hello previously configured Managed Backup settings.</span></span> <span data-ttu-id="e2249-174">Vous devez désactiver la sauvegarde automatisée avant la désactivation ou la désinstallation de hello IaaS Agent SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e2249-174">You should disable Automated Backup before disabling or uninstalling hello SQL Server IaaS Agent.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e2249-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e2249-175">Next steps</span></span>
<span data-ttu-id="e2249-176">La sauvegarde automatisée configure une sauvegarde managée sur les machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="e2249-176">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="e2249-177">Il est donc important trop[passez en revue la documentation hello pour la gestion de sauvegarde](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello comportement et les implications.</span><span class="sxs-lookup"><span data-stu-id="e2249-177">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="e2249-178">Vous pouvez trouver de sauvegarde supplémentaire et restaurer des conseils pour SQL Server sur des machines virtuelles Azure dans la rubrique suivante de hello : [sauvegarde et de restauration pour SQL Server dans Azure Virtual Machines](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e2249-178">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="e2249-179">Pour plus d’informations sur les autres tâches d’automatisation disponibles, voir [Extension de l’agent IaaS SQL Server](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="e2249-179">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="e2249-180">Pour plus d’informations sur l’exécution de SQL Server sur des machines virtuelles Azure, voir [Vue d’ensemble de SQL Server sur les machines virtuelles Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e2249-180">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

