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
# <a name="use-azurermbackup-cmdlets-tooback-up-virtual-machines"></a><span data-ttu-id="e860b-103">Utilisez tooback d’applets de commande AzureRM.Backup des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="e860b-103">Use AzureRM.Backup cmdlets tooback up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e860b-104">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="e860b-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="e860b-105">Classique</span><span class="sxs-lookup"><span data-stu-id="e860b-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="e860b-106">Cet article vous montre comment toouse Azure PowerShell pour la sauvegarde et récupération des machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="e860b-106">This article shows you how toouse Azure PowerShell for backup and recovery of Azure VMs.</span></span> <span data-ttu-id="e860b-107">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : Resource Manager et classique.</span><span class="sxs-lookup"><span data-stu-id="e860b-107">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="e860b-108">Cet article couvre l’utilisation de tooback de modèle de déploiement de classique hello de coffre de sauvegarde de données tooa.</span><span class="sxs-lookup"><span data-stu-id="e860b-108">This article covers using hello Classic deployment model tooback up data tooa Backup vault.</span></span> <span data-ttu-id="e860b-109">Si vous n’avez pas créé un coffre de sauvegarde dans votre abonnement, consultez la version du Gestionnaire de ressources hello de cet article, [tooback d’applets de commande AzureRM.RecoveryServices.Backup d’utilisation des machines virtuelles](backup-azure-vms-automation.md).</span><span class="sxs-lookup"><span data-stu-id="e860b-109">If you have not created a Backup vault in your subscription, see hello Resource Manager version of this article, [Use AzureRM.RecoveryServices.Backup cmdlets tooback up virtual machines](backup-azure-vms-automation.md).</span></span> <span data-ttu-id="e860b-110">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="e860b-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e860b-111">Vous pouvez maintenant mettre à niveau vos archivages de sauvegarde coffres tooRecovery Services.</span><span class="sxs-lookup"><span data-stu-id="e860b-111">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="e860b-112">Pour plus d’informations, voir l’article hello [mise à niveau d’un tooa de coffre de sauvegarde de coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="e860b-112">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="e860b-113">Microsoft vous encourage tooupgrade coffres des Services tooRecovery les coffres de votre sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="e860b-113">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="e860b-114">Après le 15 octobre 2017, vous ne pouvez pas utiliser les coffres de sauvegarde toocreate PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e860b-114">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="e860b-115">**D’ici au 1er novembre 2017** :</span><span class="sxs-lookup"><span data-stu-id="e860b-115">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="e860b-116">Tous les coffres de sauvegarde restants seront les coffres des Services de tooRecovery automatiquement mis à niveau.</span><span class="sxs-lookup"><span data-stu-id="e860b-116">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="e860b-117">Vous ne pourra plus être en mesure de tooaccess vos données de sauvegarde dans le portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="e860b-117">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="e860b-118">Au lieu de cela, utilisez hello tooaccess portail Azure vos données de sauvegarde dans les coffres des Services de récupération.</span><span class="sxs-lookup"><span data-stu-id="e860b-118">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="concepts"></a><span data-ttu-id="e860b-119">Concepts</span><span class="sxs-lookup"><span data-stu-id="e860b-119">Concepts</span></span>
<span data-ttu-id="e860b-120">Cet article fournit des informations spécifique toohello applets de commande PowerShell utilisées tooback des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="e860b-120">This article provides information specific toohello PowerShell cmdlets used tooback up virtual machines.</span></span> <span data-ttu-id="e860b-121">Pour obtenir des informations sur la protection des machines virtuelles Azure, consultez [Planification de votre infrastructure de sauvegarde de machines virtuelles dans Azure](backup-azure-vms-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e860b-121">For introductory information about protecting Azure VMs, please see [Plan your VM backup infrastructure in Azure](backup-azure-vms-introduction.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e860b-122">Avant de commencer, lisez hello [conditions préalables](backup-azure-vms-prepare.md) toowork requise avec Azure Backup et hello [limitations](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) de solution de sauvegarde de machine virtuelle en cours hello.</span><span class="sxs-lookup"><span data-stu-id="e860b-122">Before you start, read hello [prerequisites](backup-azure-vms-prepare.md) required toowork with Azure Backup, and hello [limitations](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) of hello current VM backup solution.</span></span>
>
>

<span data-ttu-id="e860b-123">toouse PowerShell prendre efficacement, une hiérarchie de hello toounderstand moment des objets et à quel endroit toostart.</span><span class="sxs-lookup"><span data-stu-id="e860b-123">toouse PowerShell effectively, take a moment toounderstand hello hierarchy of objects and from where toostart.</span></span>

![Hiérarchie des objets](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

<span data-ttu-id="e860b-125">Bonjour deux flux les plus importants sont activer la protection sur une machine virtuelle et restaurer les données à partir d’un point de récupération.</span><span class="sxs-lookup"><span data-stu-id="e860b-125">hello two most important flows are enabling protection for a VM, and restoring data from a recovery point.</span></span> <span data-ttu-id="e860b-126">focus Hello de cet article est toohelp vous deviendriez performants pour travailler avec tooenable d’applets de commande PowerShell hello ces deux scénarios.</span><span class="sxs-lookup"><span data-stu-id="e860b-126">hello focus of this article is toohelp you become adept at working with hello PowerShell cmdlets tooenable these two scenarios.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="e860b-127">Installation et inscription</span><span class="sxs-lookup"><span data-stu-id="e860b-127">Setup and Registration</span></span>
<span data-ttu-id="e860b-128">toobegin :</span><span class="sxs-lookup"><span data-stu-id="e860b-128">toobegin:</span></span>

1. <span data-ttu-id="e860b-129">[Téléchargez la dernière version de PowerShell](https://github.com/Azure/azure-powershell/releases) (version minimale requise : 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="e860b-129">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="e860b-130">Trouver hello Azure sauvegarde applets de commande PowerShell disponibles en tapant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e860b-130">Find hello Azure Backup PowerShell cmdlets available by typing hello following command:</span></span>

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

<span data-ttu-id="e860b-131">Hello suivant le programme d’installation et tâches d’enregistrement peuvent être automatisées avec PowerShell :</span><span class="sxs-lookup"><span data-stu-id="e860b-131">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="e860b-132">Créer un coffre de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="e860b-132">Create a backup vault</span></span>
* <span data-ttu-id="e860b-133">L’inscription d’ordinateurs virtuels de hello avec hello service Azure Backup</span><span class="sxs-lookup"><span data-stu-id="e860b-133">Registering hello VMs with hello Azure Backup service</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="e860b-134">Créer un coffre de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="e860b-134">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="e860b-135">Pour les clients à l’aide de la sauvegarde Azure pour hello première fois, vous devez tooregister hello Azure Backup fournisseur toobe utilisé avec votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="e860b-135">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="e860b-136">Cela est possible en exécutant hello de commande suivante : Register-AzureRmResourceProvider - ProviderNamespace « Microsoft.Backup »</span><span class="sxs-lookup"><span data-stu-id="e860b-136">This can be done by running hello following command: Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="e860b-137">Vous pouvez créer un coffre de sauvegarde à l’aide de hello **New-AzureRmBackupVault** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="e860b-137">You can create a new backup vault using hello **New-AzureRmBackupVault** cmdlet.</span></span> <span data-ttu-id="e860b-138">coffre de sauvegarde Hello est une ressource ARM, par conséquent, vous devez tooplace dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="e860b-138">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="e860b-139">Dans une console Azure PowerShell avec élévation de privilèges, exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="e860b-139">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="e860b-140">Vous pouvez obtenir une liste de tous les coffres de sauvegarde hello dans un abonnement donné à l’aide de hello **Get-AzureRmBackupVault** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="e860b-140">You can get a list of all hello backup vaults in a given subscription using hello **Get-AzureRmBackupVault** cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="e860b-141">Il est pratique de toostore objet de coffre de sauvegarde hello dans une variable.</span><span class="sxs-lookup"><span data-stu-id="e860b-141">It is convenient toostore hello backup vault object into a variable.</span></span> <span data-ttu-id="e860b-142">objet de coffre Hello est nécessaire en tant qu’entrée de nombreuses applets de commande Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="e860b-142">hello vault object is needed as an input for many Azure Backup cmdlets.</span></span>
>
>

### <a name="registering-hello-vms"></a><span data-ttu-id="e860b-143">L’inscription d’ordinateurs virtuels de hello</span><span class="sxs-lookup"><span data-stu-id="e860b-143">Registering hello VMs</span></span>
<span data-ttu-id="e860b-144">Hello première étape de configuration de sauvegarde avec Azure Backup est tooregister votre ordinateur ou une machine virtuelle avec un coffre Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="e860b-144">hello first step towards configuring backup with Azure Backup is tooregister your machine or VM with an Azure Backup vault.</span></span> <span data-ttu-id="e860b-145">Hello **Register-AzureRmBackupContainer** applet de commande prend les informations d’entrée de hello d’une machine virtuelle Azure IaaS et inscrit avec le coffre hello spécifié.</span><span class="sxs-lookup"><span data-stu-id="e860b-145">hello **Register-AzureRmBackupContainer** cmdlet takes hello input information of an Azure IaaS virtual machine and registers it with hello specified vault.</span></span> <span data-ttu-id="e860b-146">opération de Registre Hello associe hello machine virtuelle Azure avec le coffre de sauvegarde hello et assure le suivi hello machine virtuelle via le cycle de vie de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="e860b-146">hello register operation associates hello Azure virtual machine with hello backup vault and tracks hello VM through hello backup lifecycle.</span></span>

<span data-ttu-id="e860b-147">L’inscription de votre machine virtuelle avec hello service Azure Backup crée un objet conteneur de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="e860b-147">Registering your VM with hello Azure Backup service creates a top-level container object.</span></span> <span data-ttu-id="e860b-148">Un conteneur contient généralement plusieurs éléments qui peuvent être sauvegardées, mais dans les cas de hello de machines virtuelles il y aura qu’un seul élément de sauvegarde pour le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="e860b-148">A container typically contains multiple items that can be backed up, but in hello case of VMs there will be only one backup item for hello container.</span></span>

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a><span data-ttu-id="e860b-149">Sauvegarde des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="e860b-149">Backup Azure VMs</span></span>
### <a name="create-a-protection-policy"></a><span data-ttu-id="e860b-150">Création d’une stratégie de protection</span><span class="sxs-lookup"><span data-stu-id="e860b-150">Create a protection policy</span></span>
<span data-ttu-id="e860b-151">Il n’est pas obligatoire toocreate une nouvelle stratégie toostart la sauvegarde de protection de vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="e860b-151">It is not mandatory toocreate a new protection policy toostart backup of your VMs.</span></span> <span data-ttu-id="e860b-152">coffre de Hello est fourni avec un « stratégie par défaut' peut être utilisé tooquickly activer la protection, puis le modifier ultérieurement avec les informations de droite hello.</span><span class="sxs-lookup"><span data-stu-id="e860b-152">hello vault comes with a 'Default Policy' that can be used tooquickly enable protection, and then edited later with hello right details.</span></span> <span data-ttu-id="e860b-153">Vous pouvez obtenir la liste des stratégies de hello disponibles dans le coffre hello à l’aide de hello **Get-AzureRmBackupProtectionPolicy** applet de commande :</span><span class="sxs-lookup"><span data-stu-id="e860b-153">You can get a list of hello policies available in hello vault by using hello **Get-AzureRmBackupProtectionPolicy** cmdlet:</span></span>

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> <span data-ttu-id="e860b-154">fuseau horaire de Hello du champ de BackupTime hello dans PowerShell est UTC.</span><span class="sxs-lookup"><span data-stu-id="e860b-154">hello timezone of hello BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="e860b-155">Toutefois, lorsque les temps de sauvegarde hello sont affiché dans hello portail Azure, fuseau horaire de hello est alignée tooyour le système local, ainsi que le décalage de hello UTC.</span><span class="sxs-lookup"><span data-stu-id="e860b-155">However, when hello backup time is shown in hello Azure portal, hello timezone is aligned tooyour local system along with hello UTC offset.</span></span>
>
>

<span data-ttu-id="e860b-156">Une stratégie de sauvegarde est associée à au moins une stratégie de rétention.</span><span class="sxs-lookup"><span data-stu-id="e860b-156">A backup policy is associated with at least one retention policy.</span></span> <span data-ttu-id="e860b-157">stratégie de rétention Hello définit la durée pendant laquelle un point de récupération est conservé avec Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="e860b-157">hello retention policy defines how long a recovery point is kept with Azure Backup.</span></span> <span data-ttu-id="e860b-158">Hello **New-AzureRmBackupRetentionPolicy** applet de commande crée les objets PowerShell qui contiennent les informations de stratégie de rétention.</span><span class="sxs-lookup"><span data-stu-id="e860b-158">hello **New-AzureRmBackupRetentionPolicy** cmdlet creates PowerShell objects that hold retention policy information.</span></span> <span data-ttu-id="e860b-159">Ces objets de stratégie de rétention sont utilisés comme entrées toohello *New-AzureRmBackupProtectionPolicy* applet de commande, ou directement avec hello *Enable-AzureRmBackupProtection* applet de commande.</span><span class="sxs-lookup"><span data-stu-id="e860b-159">These retention policy objects are used as inputs toohello *New-AzureRmBackupProtectionPolicy* cmdlet, or directly with hello *Enable-AzureRmBackupProtection* cmdlet.</span></span>

<span data-ttu-id="e860b-160">Une stratégie de sauvegarde définit quand et à quelle fréquence hello sauvegarde d’un élément est effectuée.</span><span class="sxs-lookup"><span data-stu-id="e860b-160">A backup policy defines when and how often hello backup of an item is done.</span></span> <span data-ttu-id="e860b-161">Hello **New-AzureRmBackupProtectionPolicy** applet de commande crée un objet PowerShell qui contient des informations de stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="e860b-161">hello **New-AzureRmBackupProtectionPolicy** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="e860b-162">stratégie de sauvegarde Hello est utilisée comme une entrée toohello *Enable-AzureRmBackupProtection* applet de commande.</span><span class="sxs-lookup"><span data-stu-id="e860b-162">hello backup policy is used as an input toohello *Enable-AzureRmBackupProtection* cmdlet.</span></span>

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a><span data-ttu-id="e860b-163">Activer la protection</span><span class="sxs-lookup"><span data-stu-id="e860b-163">Enable protection</span></span>
<span data-ttu-id="e860b-164">L’activation de protection implique deux objets : hello élément et hello stratégie et les deux toohello de toobelong besoin même coffre.</span><span class="sxs-lookup"><span data-stu-id="e860b-164">Enabling protection involves two objects - hello Item and hello Policy, and both need toobelong toohello same vault.</span></span> <span data-ttu-id="e860b-165">Une fois que la stratégie de hello a été associé avec un élément de hello, flux de travail sauvegarde hello lancera conformément au calendrier défini de hello.</span><span class="sxs-lookup"><span data-stu-id="e860b-165">Once hello policy has been associated with hello item, hello backup workflow will kick in at hello defined schedule.</span></span>

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a><span data-ttu-id="e860b-166">Sauvegarde initiale</span><span class="sxs-lookup"><span data-stu-id="e860b-166">Initial backup</span></span>
<span data-ttu-id="e860b-167">planification de sauvegarde Hello s’occupe une copie initiale complète de hello pour l’élément de hello et hello incrémentielles pour les sauvegardes ultérieures hello.</span><span class="sxs-lookup"><span data-stu-id="e860b-167">hello backup schedule will take care of doing hello full initial copy for hello item and hello incremental copy for hello subsequent backups.</span></span> <span data-ttu-id="e860b-168">Toutefois, si vous souhaitez tooforce hello initiale sauvegarde toohappen à un moment donné ou même immédiatement utiliser hello **AzureRmBackupItem de sauvegarde** applet de commande :</span><span class="sxs-lookup"><span data-stu-id="e860b-168">However, if you want tooforce hello initial backup toohappen at a certain time or even immediately then use hello **Backup-AzureRmBackupItem** cmdlet:</span></span>

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="e860b-169">Hello fuseau horaire de hello StartTime et EndTime les champs affichés dans PowerShell en UTC.</span><span class="sxs-lookup"><span data-stu-id="e860b-169">hello timezone of hello StartTime and EndTime fields shown in PowerShell is UTC.</span></span> <span data-ttu-id="e860b-170">Toutefois, lorsque des informations similaires hello sont affichées dans hello portail Azure, fuseau horaire de hello est alignée tooyour horloge du système local.</span><span class="sxs-lookup"><span data-stu-id="e860b-170">However, when hello similar information is shown in hello Azure portal, hello timezone is aligned tooyour local system clock.</span></span>
>
>

### <a name="monitoring-a-backup-job"></a><span data-ttu-id="e860b-171">Surveillance d’une tâche de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="e860b-171">Monitoring a backup job</span></span>
<span data-ttu-id="e860b-172">La plupart des opérations longues dans Sauvegarde Azure sont reproduites en tant que tâche.</span><span class="sxs-lookup"><span data-stu-id="e860b-172">Most long-running operations in Azure Backup are modelled as a job.</span></span> <span data-ttu-id="e860b-173">Il est ainsi facile tootrack progression sans avoir tookeep hello ouvrir portail Azure en permanence.</span><span class="sxs-lookup"><span data-stu-id="e860b-173">This makes it easy tootrack progress without having tookeep hello Azure portal open at all times.</span></span>

<span data-ttu-id="e860b-174">état le plus récent hello tooget d’une tâche en cours d’exécution, utilisez hello **Get-AzureRmBackupJob** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="e860b-174">tooget hello latest status of an in-progress job, use hello **Get-AzureRmBackupJob** cmdlet.</span></span>

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

<span data-ttu-id="e860b-175">Au lieu de l’interrogation de ces travaux pour la saisie semi-automatique, qui est un code inutile, supplémentaire - il est plus simple toouse hello **AzureRmBackupJob-attente** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="e860b-175">Instead of polling these jobs for completion - which is unnecessary, additional code - it is simpler toouse hello **Wait-AzureRmBackupJob** cmdlet.</span></span> <span data-ttu-id="e860b-176">Lorsqu’il est utilisé dans un script, applet de commande hello suspend l’exécution de hello qu’hello tâche se termine ou hello spécifié la valeur de délai d’attente est atteinte.</span><span class="sxs-lookup"><span data-stu-id="e860b-176">When used in a script, hello cmdlet will pause hello execution until either hello job completes or hello specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a><span data-ttu-id="e860b-177">Restauration d’une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="e860b-177">Restore an Azure VM</span></span>
<span data-ttu-id="e860b-178">Dans les données de sauvegarde toorestore ordre, vous devez tooidentify hello sauvegardé élément, et Point de récupération hello qui contient les données de point-à-temps hello.</span><span class="sxs-lookup"><span data-stu-id="e860b-178">In order toorestore backup data, you need tooidentify hello backed-up Item and hello Recovery Point that holds hello point-in-time data.</span></span> <span data-ttu-id="e860b-179">Ces informations sont fournies toohello AzureRmBackupItem de restauration applet de commande tooinitiate une restauration de données à partir de hello coffre toohello du client.</span><span class="sxs-lookup"><span data-stu-id="e860b-179">This information is supplied toohello Restore-AzureRmBackupItem cmdlet tooinitiate a restore of data from hello vault toohello customer's account.</span></span>

### <a name="select-hello-vm"></a><span data-ttu-id="e860b-180">Sélectionnez hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e860b-180">Select hello VM</span></span>
<span data-ttu-id="e860b-181">objet PowerShell hello tooget identifiant hello droit de sauvegarder l’élément, vous devez toostart de hello conteneur dans le coffre de hello et dont la hiérarchie d’objets.</span><span class="sxs-lookup"><span data-stu-id="e860b-181">tooget hello PowerShell object that identifies hello right backup Item, you need toostart from hello Container in hello vault, and work your way down object hierarchy.</span></span> <span data-ttu-id="e860b-182">conteneur hello tooselect représentant hello machine virtuelle, utilisez hello **Get-AzureRmBackupContainer** applet de commande et redirigez cette toohello **Get-AzureRmBackupItem** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="e860b-182">tooselect hello container that represents hello VM, use hello **Get-AzureRmBackupContainer** cmdlet and pipe that toohello **Get-AzureRmBackupItem** cmdlet.</span></span>

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="e860b-183">Choisir un point de récupération</span><span class="sxs-lookup"><span data-stu-id="e860b-183">Choose a recovery point</span></span>
<span data-ttu-id="e860b-184">Vous pouvez maintenant mettre tous les points de récupération hello pour sauvegarder l’élément hello à l’aide de hello **Get-AzureRmBackupRecoveryPoint** applet de commande, puis choisissez toorestore de point de récupération hello.</span><span class="sxs-lookup"><span data-stu-id="e860b-184">You can now list all hello recovery points for hello backup item using hello **Get-AzureRmBackupRecoveryPoint** cmdlet, and choose hello recovery point toorestore.</span></span> <span data-ttu-id="e860b-185">En général, les utilisateurs choisir hello plus récente *AppConsistent* point dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="e860b-185">Typically users pick hello most recent *AppConsistent* point in hello list.</span></span>

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

<span data-ttu-id="e860b-186">variable de Hello ```$rp``` est un tableau de points de récupération pour hello l’élément de sauvegarde, trié dans l’ordre inverse de temps sélectionné - dernier point de récupération hello est à l’index 0.</span><span class="sxs-lookup"><span data-stu-id="e860b-186">hello variable ```$rp``` is an array of recovery points for hello selected backup item, sorted in reverse order of time - hello latest recovery point is at index 0.</span></span> <span data-ttu-id="e860b-187">Utiliser le tableau PowerShell standard, l’indexation de point de récupération toopick hello.</span><span class="sxs-lookup"><span data-stu-id="e860b-187">Use standard PowerShell array indexing toopick hello recovery point.</span></span> <span data-ttu-id="e860b-188">Par exemple : ```$rp[0]``` sélectionnera le dernier point de récupération hello.</span><span class="sxs-lookup"><span data-stu-id="e860b-188">For example: ```$rp[0]``` will select hello latest recovery point.</span></span>

### <a name="restoring-disks"></a><span data-ttu-id="e860b-189">Restauration de disques</span><span class="sxs-lookup"><span data-stu-id="e860b-189">Restoring disks</span></span>
<span data-ttu-id="e860b-190">Il existe une différence fondamentale entre les opérations de restauration hello effectuée par le biais hello portail Azure et Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e860b-190">There is a key difference between hello restore operations done through hello Azure portal and through Azure PowerShell.</span></span> <span data-ttu-id="e860b-191">Avec PowerShell, hello restauration s’arrête à la restauration des disques de hello et les informations de configuration de point de récupération hello.</span><span class="sxs-lookup"><span data-stu-id="e860b-191">With PowerShell, hello restore operation stops at restoring hello disks and config information from hello recovery point.</span></span> <span data-ttu-id="e860b-192">Il n’y a pas de création de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e860b-192">It does not create a virtual machine.</span></span>

> [!WARNING]
> <span data-ttu-id="e860b-193">Hello AzureRmBackupItem de restauration ne crée pas une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e860b-193">hello Restore-AzureRmBackupItem does not create a VM.</span></span> <span data-ttu-id="e860b-194">Il restaure uniquement les disques hello toohello spécifié de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="e860b-194">It only restores hello disks toohello specified storage account.</span></span> <span data-ttu-id="e860b-195">Cela n’est pas hello même comportement que vous rencontrerez dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e860b-195">This is not hello same behavior you will experience in hello Azure portal.</span></span>
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

<span data-ttu-id="e860b-196">Vous pouvez obtenir les détails de hello hello d’opération de restauration à l’aide de hello **Get-AzureRmBackupJobDetails** applet de commande une fois que le travail de restauration hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="e860b-196">You can get hello details of hello restore operation using hello **Get-AzureRmBackupJobDetails** cmdlet once hello Restore job has completed.</span></span> <span data-ttu-id="e860b-197">Hello *ErrorDetails* propriété hello des informations sont nécessaires toorebuild hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e860b-197">hello *ErrorDetails* property will have hello information needed toorebuild hello VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-hello-vm"></a><span data-ttu-id="e860b-198">Build hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e860b-198">Build hello VM</span></span>
<span data-ttu-id="e860b-199">Hello construction machine virtuelle hors des disques hello restauré peut être effectuée à l’aide des applets de commande PowerShell Azure Service Management plus anciennes de hello, hello nouveaux modèles Azure Resource Manager, ou même à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e860b-199">Building hello VM out of hello restored disks can be done using hello older Azure Service Management PowerShell cmdlets, hello new Azure Resource Manager templates, or even using hello Azure portal.</span></span> <span data-ttu-id="e860b-200">Dans l’exemple ci-dessous, nous allons montrer comment tooget là à l’aide des applets de commande de gestion des services Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e860b-200">In a quick example, we will show how tooget there using hello Azure Service Management cmdlets.</span></span>

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

<span data-ttu-id="e860b-201">Pour plus d’informations sur la façon dont les disques restaurés toobuild une machine virtuelle à partir de hello, consultez hello suivant d’applets de commande :</span><span class="sxs-lookup"><span data-stu-id="e860b-201">For more information on how toobuild a VM from hello restored disks, read about hello following cmdlets:</span></span>

* [<span data-ttu-id="e860b-202">Add-AzureDisk</span><span class="sxs-lookup"><span data-stu-id="e860b-202">Add-AzureDisk</span></span>](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [<span data-ttu-id="e860b-203">New-AzureVMConfig</span><span class="sxs-lookup"><span data-stu-id="e860b-203">New-AzureVMConfig</span></span>](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [<span data-ttu-id="e860b-204">New-AzureVM</span><span class="sxs-lookup"><span data-stu-id="e860b-204">New-AzureVM</span></span>](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a><span data-ttu-id="e860b-205">Exemples de code</span><span class="sxs-lookup"><span data-stu-id="e860b-205">Code samples</span></span>
### <a name="1-get-hello-completion-status-of-job-sub-tasks"></a><span data-ttu-id="e860b-206">1. Obtenir l’état d’achèvement hello de travail des tâches subordonnées</span><span class="sxs-lookup"><span data-stu-id="e860b-206">1. Get hello completion status of job sub-tasks</span></span>
<span data-ttu-id="e860b-207">état d’achèvement hello tootrack, de sous-tâches individuels, vous pouvez utiliser hello **Get-AzureRmBackupJobDetails** applet de commande :</span><span class="sxs-lookup"><span data-stu-id="e860b-207">tootrack hello completion status of individual sub-tasks, you can use hello **Get-AzureRmBackupJobDetails** cmdlet:</span></span>

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data tooBackup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a><span data-ttu-id="e860b-208">2. Création d’un rapport quotidien/hebdomadaire des travaux de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="e860b-208">2. Create a daily/weekly report of backup jobs</span></span>
<span data-ttu-id="e860b-209">En règle générale, les administrateurs souhaitent tooknow les travaux de sauvegarde exécutés hello des dernières 24 heures, état hello de ces tâches de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="e860b-209">Administrators typically want tooknow what backup jobs ran in hello last 24 hours, hello status of those backup jobs.</span></span> <span data-ttu-id="e860b-210">En outre, quantité hello de données transférées donne aux administrateurs un moyen tooestimate leur utilisation des données mensuelles.</span><span class="sxs-lookup"><span data-stu-id="e860b-210">Additionally, hello amount of data transferred gives administrators a way tooestimate their monthly data usage.</span></span> <span data-ttu-id="e860b-211">script Hello ci-dessous extrait des données brutes hello hello service Azure Backup et affiche des informations de hello dans la console PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="e860b-211">hello script below pulls hello raw data from hello Azure Backup service and displays hello information in hello PowerShell console.</span></span>

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

<span data-ttu-id="e860b-212">Si vous souhaitez tooadd le résultat du rapport toothis fonctionnalités de création de graphiques, obtenir des informations à partir du billet de blog TechNet hello [graphiques avec PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span><span class="sxs-lookup"><span data-stu-id="e860b-212">If you want tooadd charting capabilities toothis report output, learn from hello TechNet blog post [Charting with PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="e860b-213">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e860b-213">Next steps</span></span>
<span data-ttu-id="e860b-214">Si vous préférez utiliser PowerShell tooengage avec vos ressources Azure, consultez l’article de PowerShell hello pour protéger Windows Server, [déployer et gérer Backup pour Windows Server](backup-client-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="e860b-214">If you prefer using PowerShell tooengage with your Azure resources, check out hello PowerShell article for protecting Windows Server, [Deploy and Manage Backup for Windows Server](backup-client-automation-classic.md).</span></span> <span data-ttu-id="e860b-215">Il existe également un article PowerShell sur la gestion des sauvegardes DPM : [Déployer et gérer une sauvegarde pour DPM](backup-dpm-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="e860b-215">There is also a PowerShell article for managing DPM backups, [Deploy and Manage Backup for DPM](backup-dpm-automation-classic.md).</span></span> <span data-ttu-id="e860b-216">Ces deux articles ont une version concernant les déploiements avec le modèle Resource Manager et le modèle Classic.</span><span class="sxs-lookup"><span data-stu-id="e860b-216">Both of these articles have a version for Resource Manager deployments as well as Classic deployments.</span></span>
