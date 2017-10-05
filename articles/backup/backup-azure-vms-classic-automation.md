---
title: "Déploiement et gestion d’une sauvegarde pour les machines virtuelles Azure à l’aide de PowerShell | Microsoft Docs"
description: "Découvrez comment déployer et gérer Sauvegarde Azure à l’aide de PowerShell."
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
ms.openlocfilehash: 5f0f06adb8177ce2d17aa0b40666470279c04e22
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="use-azurermbackup-cmdlets-to-back-up-virtual-machines"></a><span data-ttu-id="0eda4-103">Utilisation des applets de commande AzureRM.Backup pour sauvegarder des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="0eda4-103">Use AzureRM.Backup cmdlets to back up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0eda4-104">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="0eda4-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="0eda4-105">Classique</span><span class="sxs-lookup"><span data-stu-id="0eda4-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="0eda4-106">Cet article vous montre comment utiliser Azure PowerShell pour la sauvegarde et la restauration des machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="0eda4-106">This article shows you how to use Azure PowerShell for backup and recovery of Azure VMs.</span></span> <span data-ttu-id="0eda4-107">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : Resource Manager et classique.</span><span class="sxs-lookup"><span data-stu-id="0eda4-107">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="0eda4-108">Cet article traite de l’utilisation du modèle de déploiement classique pour sauvegarder des données dans un coffre de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="0eda4-108">This article covers using the Classic deployment model to back up data to a Backup vault.</span></span> <span data-ttu-id="0eda4-109">Si vous n’avez pas créé de coffre de sauvegarde dans votre abonnement, consultez la version du Gestionnaire des ressources de cet article, [Utilisez les applets de commande AzureRM.RecoveryServices.Backup pour sauvegarder des machines virtuelles](backup-azure-vms-automation.md).</span><span class="sxs-lookup"><span data-stu-id="0eda4-109">If you have not created a Backup vault in your subscription, see the Resource Manager version of this article, [Use AzureRM.RecoveryServices.Backup cmdlets to back up virtual machines](backup-azure-vms-automation.md).</span></span> <span data-ttu-id="0eda4-110">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0eda4-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0eda4-111">Vous pouvez désormais mettre à niveau vos coffres de sauvegarde vers des coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="0eda4-111">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="0eda4-112">Pour en savoir plus, consultez l’article [Mettre à niveau un coffre de sauvegarde vers un coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="0eda4-112">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="0eda4-113">Microsoft vous recommande de mettre à niveau vos coffres de sauvegarde vers des coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="0eda4-113">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="0eda4-114">À compter du 15 octobre 2017, vous ne pourrez plus vous servir de PowerShell pour créer des coffres de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="0eda4-114">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="0eda4-115">**D’ici au 1er novembre 2017** :</span><span class="sxs-lookup"><span data-stu-id="0eda4-115">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="0eda4-116">tous les coffres de sauvegarde restants seront automatiquement mis à niveau vers des coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="0eda4-116">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="0eda4-117">Vous ne pourrez plus accéder à vos données de sauvegarde depuis le portail Classic.</span><span class="sxs-lookup"><span data-stu-id="0eda4-117">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="0eda4-118">Au lieu de cela, vous devrez utiliser le portail Azure pour accéder à ces données au sein de coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="0eda4-118">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="concepts"></a><span data-ttu-id="0eda4-119">Concepts</span><span class="sxs-lookup"><span data-stu-id="0eda4-119">Concepts</span></span>
<span data-ttu-id="0eda4-120">Cet article fournit des informations spécifiques aux applets de commande PowerShell utilisées pour sauvegarder des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="0eda4-120">This article provides information specific to the PowerShell cmdlets used to back up virtual machines.</span></span> <span data-ttu-id="0eda4-121">Pour obtenir des informations sur la protection des machines virtuelles Azure, consultez [Planification de votre infrastructure de sauvegarde de machines virtuelles dans Azure](backup-azure-vms-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0eda4-121">For introductory information about protecting Azure VMs, please see [Plan your VM backup infrastructure in Azure](backup-azure-vms-introduction.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0eda4-122">Avant de commencer, lisez les [conditions préalables](backup-azure-vms-prepare.md) nécessaires pour utiliser Sauvegarde Azure et les [limitations](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) de la solution actuelle de sauvegarde de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="0eda4-122">Before you start, read the [prerequisites](backup-azure-vms-prepare.md) required to work with Azure Backup, and the [limitations](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) of the current VM backup solution.</span></span>
>
>

<span data-ttu-id="0eda4-123">Pour pouvoir utiliser efficacement PowerShell, il est nécessaire de comprendre la hiérarchie d’objets et par où commencer.</span><span class="sxs-lookup"><span data-stu-id="0eda4-123">To use PowerShell effectively, take a moment to understand the hierarchy of objects and from where to start.</span></span>

![Hiérarchie des objets](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

<span data-ttu-id="0eda4-125">Les deux processus les plus importants permettent la protection des machines virtuelles et la restauration des données à partir d’un point de restauration.</span><span class="sxs-lookup"><span data-stu-id="0eda4-125">The two most important flows are enabling protection for a VM, and restoring data from a recovery point.</span></span> <span data-ttu-id="0eda4-126">L’objectif de cet article est de vous apprendre à utiliser les applets de commande PowerShell pour permettre ces deux scénarios.</span><span class="sxs-lookup"><span data-stu-id="0eda4-126">The focus of this article is to help you become adept at working with the PowerShell cmdlets to enable these two scenarios.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="0eda4-127">Installation et inscription</span><span class="sxs-lookup"><span data-stu-id="0eda4-127">Setup and Registration</span></span>
<span data-ttu-id="0eda4-128">Pour commencer :</span><span class="sxs-lookup"><span data-stu-id="0eda4-128">To begin:</span></span>

1. <span data-ttu-id="0eda4-129">[Téléchargez la dernière version de PowerShell](https://github.com/Azure/azure-powershell/releases) (version minimale requise : 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="0eda4-129">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="0eda4-130">Rechercher les applets de commande PowerShell Azure Backup disponibles en tapant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0eda4-130">Find the Azure Backup PowerShell cmdlets available by typing the following command:</span></span>

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

<span data-ttu-id="0eda4-131">Les tâches de configuration et d’inscription ci-après peuvent être automatisées avec PowerShell :</span><span class="sxs-lookup"><span data-stu-id="0eda4-131">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="0eda4-132">Créer un coffre de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="0eda4-132">Create a backup vault</span></span>
* <span data-ttu-id="0eda4-133">Inscription des machines virtuelles auprès du service Sauvegarde Azure</span><span class="sxs-lookup"><span data-stu-id="0eda4-133">Registering the VMs with the Azure Backup service</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="0eda4-134">Créer un coffre de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="0eda4-134">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="0eda4-135">Pour les clients utilisant Sauvegarde Azure pour la première fois, vous devez enregistrer le fournisseur Sauvegarde Azure à utiliser avec votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="0eda4-135">For customers using Azure Backup for the first time, you need to register the Azure Backup provider to be used with your subscription.</span></span> <span data-ttu-id="0eda4-136">Pour ce faire, exécutez la commande suivante : Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="0eda4-136">This can be done by running the following command: Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="0eda4-137">Vous pouvez créer un coffre de sauvegarde en utilisant l’applet de commande **New-AzureRmBackupVault** .</span><span class="sxs-lookup"><span data-stu-id="0eda4-137">You can create a new backup vault using the **New-AzureRmBackupVault** cmdlet.</span></span> <span data-ttu-id="0eda4-138">Le coffre de sauvegarde constituant une ressource ARM, vous devez le placer dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="0eda4-138">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="0eda4-139">Dans une console Azure PowerShell avec élévation de privilèges, exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="0eda4-139">In an elevated Azure PowerShell console, run the following commands:</span></span>

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="0eda4-140">Vous pouvez obtenir la liste de tous les coffres de sauvegarde d’un abonnement donné à l’aide de l’applet de commande **Get-AzureRmBackupVault** .</span><span class="sxs-lookup"><span data-stu-id="0eda4-140">You can get a list of all the backup vaults in a given subscription using the **Get-AzureRmBackupVault** cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="0eda4-141">Il est pratique de stocker l’objet du coffre de sauvegarde dans une variable.</span><span class="sxs-lookup"><span data-stu-id="0eda4-141">It is convenient to store the backup vault object into a variable.</span></span> <span data-ttu-id="0eda4-142">L’objet coffre est nécessaire comme entrée de nombreuses applets de commande Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="0eda4-142">The vault object is needed as an input for many Azure Backup cmdlets.</span></span>
>
>

### <a name="registering-the-vms"></a><span data-ttu-id="0eda4-143">Enregistrement des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="0eda4-143">Registering the VMs</span></span>
<span data-ttu-id="0eda4-144">La première étape de la configuration de la sauvegarde avec Sauvegarde Azure consiste à enregistrer votre ordinateur ou machine virtuelle avec un coffre de sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="0eda4-144">The first step towards configuring backup with Azure Backup is to register your machine or VM with an Azure Backup vault.</span></span> <span data-ttu-id="0eda4-145">L’applet de commande **Register-AzureRmBackupContainer** collecte les informations d’entrée d’une machine virtuelle IaaS Azure et les enregistre dans le coffre spécifié.</span><span class="sxs-lookup"><span data-stu-id="0eda4-145">The **Register-AzureRmBackupContainer** cmdlet takes the input information of an Azure IaaS virtual machine and registers it with the specified vault.</span></span> <span data-ttu-id="0eda4-146">L’opération d’enregistrement associe la machine virtuelle Azure avec le coffre de sauvegarde et effectue le suivi de la machine virtuelle tout au long du cycle de vie de la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="0eda4-146">The register operation associates the Azure virtual machine with the backup vault and tracks the VM through the backup lifecycle.</span></span>

<span data-ttu-id="0eda4-147">L’enregistrement de votre machine virtuelle auprès du service Sauvegarde Azure crée un objet conteneur de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="0eda4-147">Registering your VM with the Azure Backup service creates a top-level container object.</span></span> <span data-ttu-id="0eda4-148">Un conteneur contient généralement plusieurs éléments qui peuvent être sauvegardés, mais dans le cas de machines virtuelles, il n’y a qu’un élément de sauvegarde pour le conteneur.</span><span class="sxs-lookup"><span data-stu-id="0eda4-148">A container typically contains multiple items that can be backed up, but in the case of VMs there will be only one backup item for the container.</span></span>

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a><span data-ttu-id="0eda4-149">Sauvegarde des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="0eda4-149">Backup Azure VMs</span></span>
### <a name="create-a-protection-policy"></a><span data-ttu-id="0eda4-150">Création d’une stratégie de protection</span><span class="sxs-lookup"><span data-stu-id="0eda4-150">Create a protection policy</span></span>
<span data-ttu-id="0eda4-151">Il n’est pas obligatoire de créer une nouvelle stratégie de protection pour démarrer la sauvegarde de vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="0eda4-151">It is not mandatory to create a new protection policy to start backup of your VMs.</span></span> <span data-ttu-id="0eda4-152">Le coffre est fourni avec une stratégie par défaut qui peut être utilisée pour activer la protection, puis modifiée ultérieurement avec les bonnes informations.</span><span class="sxs-lookup"><span data-stu-id="0eda4-152">The vault comes with a 'Default Policy' that can be used to quickly enable protection, and then edited later with the right details.</span></span> <span data-ttu-id="0eda4-153">Vous pouvez obtenir la liste des stratégies disponibles dans le coffre à l’aide de l’applet de commande **Get-AzureRmBackupProtectionPolicy** :</span><span class="sxs-lookup"><span data-stu-id="0eda4-153">You can get a list of the policies available in the vault by using the **Get-AzureRmBackupProtectionPolicy** cmdlet:</span></span>

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> <span data-ttu-id="0eda4-154">Le fuseau horaire du champ BackupTime dans PowerShell est UTC.</span><span class="sxs-lookup"><span data-stu-id="0eda4-154">The timezone of the BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="0eda4-155">Toutefois, lorsque l'heure de sauvegarde s’affiche dans le portail Azure, le fuseau horaire est aligné sur votre système local, tout comme le décalage UTC.</span><span class="sxs-lookup"><span data-stu-id="0eda4-155">However, when the backup time is shown in the Azure portal, the timezone is aligned to your local system along with the UTC offset.</span></span>
>
>

<span data-ttu-id="0eda4-156">Une stratégie de sauvegarde est associée à au moins une stratégie de rétention.</span><span class="sxs-lookup"><span data-stu-id="0eda4-156">A backup policy is associated with at least one retention policy.</span></span> <span data-ttu-id="0eda4-157">La stratégie de rétention définit la durée de conservation d’un point de restauration avec Sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="0eda4-157">The retention policy defines how long a recovery point is kept with Azure Backup.</span></span> <span data-ttu-id="0eda4-158">L’applet de commande **New-AzureRmBackupRetentionPolicy** crée des objets PowerShell qui contiennent des informations sur la stratégie de rétention.</span><span class="sxs-lookup"><span data-stu-id="0eda4-158">The **New-AzureRmBackupRetentionPolicy** cmdlet creates PowerShell objects that hold retention policy information.</span></span> <span data-ttu-id="0eda4-159">Ces objets de stratégie de rétention sont utilisés comme entrées dans l’applet de commande *New-AzureRmBackupProtectionPolicy* ou directement dans le cas de l’applet de commande *Enable-AzureRmBackupProtection*.</span><span class="sxs-lookup"><span data-stu-id="0eda4-159">These retention policy objects are used as inputs to the *New-AzureRmBackupProtectionPolicy* cmdlet, or directly with the *Enable-AzureRmBackupProtection* cmdlet.</span></span>

<span data-ttu-id="0eda4-160">Une stratégie de sauvegarde définit quand et à quelle fréquence la sauvegarde d’un élément doit être effectuée.</span><span class="sxs-lookup"><span data-stu-id="0eda4-160">A backup policy defines when and how often the backup of an item is done.</span></span> <span data-ttu-id="0eda4-161">L’applet de commande **New-AzureRmBackupProtectionPolicy** crée un objet PowerShell contenant des informations sur la stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="0eda4-161">The **New-AzureRmBackupProtectionPolicy** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="0eda4-162">La stratégie de sauvegarde est utilisée comme entrée dans l’applet de commande *Enable-AzureRmBackupProtection* .</span><span class="sxs-lookup"><span data-stu-id="0eda4-162">The backup policy is used as an input to the *Enable-AzureRmBackupProtection* cmdlet.</span></span>

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a><span data-ttu-id="0eda4-163">Activer la protection</span><span class="sxs-lookup"><span data-stu-id="0eda4-163">Enable protection</span></span>
<span data-ttu-id="0eda4-164">L’activation de la protection implique deux objets : l’élément et la stratégie, et les deux doivent appartenir au même coffre.</span><span class="sxs-lookup"><span data-stu-id="0eda4-164">Enabling protection involves two objects - the Item and the Policy, and both need to belong to the same vault.</span></span> <span data-ttu-id="0eda4-165">Une fois que la stratégie a été associée à l’élément, le flux de travail de la sauvegarde se lancera à l’heure planifiée.</span><span class="sxs-lookup"><span data-stu-id="0eda4-165">Once the policy has been associated with the item, the backup workflow will kick in at the defined schedule.</span></span>

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a><span data-ttu-id="0eda4-166">Sauvegarde initiale</span><span class="sxs-lookup"><span data-stu-id="0eda4-166">Initial backup</span></span>
<span data-ttu-id="0eda4-167">La planification de sauvegarde se charge d’effectuer la copie initiale complète de l’élément et la copie incrémentielle pour les sauvegardes suivantes.</span><span class="sxs-lookup"><span data-stu-id="0eda4-167">The backup schedule will take care of doing the full initial copy for the item and the incremental copy for the subsequent backups.</span></span> <span data-ttu-id="0eda4-168">Cependant, si vous voulez forcer l’exécution de la sauvegarde initiale à un moment déterminé, voire immédiatement, utilisez l’applet de commande **Backup-AzureRmBackupItem** :</span><span class="sxs-lookup"><span data-stu-id="0eda4-168">However, if you want to force the initial backup to happen at a certain time or even immediately then use the **Backup-AzureRmBackupItem** cmdlet:</span></span>

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="0eda4-169">Le fuseau horaire des champs StartTime et EndTime affichés dans PowerShell est UTC.</span><span class="sxs-lookup"><span data-stu-id="0eda4-169">The timezone of the StartTime and EndTime fields shown in PowerShell is UTC.</span></span> <span data-ttu-id="0eda4-170">Toutefois, lorsque des informations similaires s'affichent dans le portail Azure, le fuseau horaire est aligné sur l'horloge de votre système local.</span><span class="sxs-lookup"><span data-stu-id="0eda4-170">However, when the similar information is shown in the Azure portal, the timezone is aligned to your local system clock.</span></span>
>
>

### <a name="monitoring-a-backup-job"></a><span data-ttu-id="0eda4-171">Surveillance d’une tâche de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="0eda4-171">Monitoring a backup job</span></span>
<span data-ttu-id="0eda4-172">La plupart des opérations longues dans Sauvegarde Azure sont reproduites en tant que tâche.</span><span class="sxs-lookup"><span data-stu-id="0eda4-172">Most long-running operations in Azure Backup are modelled as a job.</span></span> <span data-ttu-id="0eda4-173">Cela permet de suivre facilement la progression sans avoir à garder le portail Azure ouvert en permanence.</span><span class="sxs-lookup"><span data-stu-id="0eda4-173">This makes it easy to track progress without having to keep the Azure portal open at all times.</span></span>

<span data-ttu-id="0eda4-174">Pour connaître l’état récent d’une tâche en cours de traitement, utilisez l’applet de commande **Get-AzureRmBackupJob** .</span><span class="sxs-lookup"><span data-stu-id="0eda4-174">To get the latest status of an in-progress job, use the **Get-AzureRmBackupJob** cmdlet.</span></span>

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

<span data-ttu-id="0eda4-175">Au lieu d’interroger ces tâches pour connaître leur état d’avancement, ce qui implique du code supplémentaire inutile, il est plus simple d’utiliser l’applet de commande **Wait-AzureRmBackupJob** .</span><span class="sxs-lookup"><span data-stu-id="0eda4-175">Instead of polling these jobs for completion - which is unnecessary, additional code - it is simpler to use the **Wait-AzureRmBackupJob** cmdlet.</span></span> <span data-ttu-id="0eda4-176">Lorsqu’elle est utilisée dans un script, l’applet de commande suspend l’exécution jusqu’à la fin de la tâche ou jusqu’à ce que la valeur spécifiée pour l’expiration du délai soit atteinte.</span><span class="sxs-lookup"><span data-stu-id="0eda4-176">When used in a script, the cmdlet will pause the execution until either the job completes or the specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a><span data-ttu-id="0eda4-177">Restauration d’une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="0eda4-177">Restore an Azure VM</span></span>
<span data-ttu-id="0eda4-178">Pour restaurer les données de sauvegarde, vous devez identifier l’élément sauvegardé et le point de restauration contenant les données ponctuelles.</span><span class="sxs-lookup"><span data-stu-id="0eda4-178">In order to restore backup data, you need to identify the backed-up Item and the Recovery Point that holds the point-in-time data.</span></span> <span data-ttu-id="0eda4-179">Ces informations sont fournies à l’applet de commande Restore-AzureRmBackupItem pour lancer une restauration des données du coffre vers le compte du client.</span><span class="sxs-lookup"><span data-stu-id="0eda4-179">This information is supplied to the Restore-AzureRmBackupItem cmdlet to initiate a restore of data from the vault to the customer's account.</span></span>

### <a name="select-the-vm"></a><span data-ttu-id="0eda4-180">Sélection de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="0eda4-180">Select the VM</span></span>
<span data-ttu-id="0eda4-181">Pour obtenir l’objet PowerShell permettant d’identifier l’élément à restaurer, vous devez commencer au niveau du conteneur dans le coffre et descendre dans la hiérarchie d’objets.</span><span class="sxs-lookup"><span data-stu-id="0eda4-181">To get the PowerShell object that identifies the right backup Item, you need to start from the Container in the vault, and work your way down object hierarchy.</span></span> <span data-ttu-id="0eda4-182">Pour sélectionner le conteneur qui représente la machine virtuelle, utilisez l’applet de commande **Get-AzureRmBackupContainer** et dirigez-la vers l’applet de commande **Get-AzureRmBackupItem**.</span><span class="sxs-lookup"><span data-stu-id="0eda4-182">To select the container that represents the VM, use the **Get-AzureRmBackupContainer** cmdlet and pipe that to the **Get-AzureRmBackupItem** cmdlet.</span></span>

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="0eda4-183">Choisir un point de récupération</span><span class="sxs-lookup"><span data-stu-id="0eda4-183">Choose a recovery point</span></span>
<span data-ttu-id="0eda4-184">Vous pouvez maintenant répertorier tous les points de restauration pour l’élément de sauvegarde via l’applet de commande **Get-AzureRmBackupRecoveryPoint** et choisir le point de récupération à restaurer.</span><span class="sxs-lookup"><span data-stu-id="0eda4-184">You can now list all the recovery points for the backup item using the **Get-AzureRmBackupRecoveryPoint** cmdlet, and choose the recovery point to restore.</span></span> <span data-ttu-id="0eda4-185">En général, les utilisateurs choisissent le point *AppConsistent* le plus récent dans la liste.</span><span class="sxs-lookup"><span data-stu-id="0eda4-185">Typically users pick the most recent *AppConsistent* point in the list.</span></span>

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

<span data-ttu-id="0eda4-186">La variable ```$rp``` est un tableau de points de récupération pour l’élément de sauvegarde sélectionné et triés par ordre chronologique inverse, le dernier point de récupération étant fixé sur l’index 0.</span><span class="sxs-lookup"><span data-stu-id="0eda4-186">The variable ```$rp``` is an array of recovery points for the selected backup item, sorted in reverse order of time - the latest recovery point is at index 0.</span></span> <span data-ttu-id="0eda4-187">Utilisez l'indexation de tableau PowerShell standard pour sélectionner le point de récupération.</span><span class="sxs-lookup"><span data-stu-id="0eda4-187">Use standard PowerShell array indexing to pick the recovery point.</span></span> <span data-ttu-id="0eda4-188">Par exemple : ```$rp[0]``` sélectionnera le point de récupération le plus récent.</span><span class="sxs-lookup"><span data-stu-id="0eda4-188">For example: ```$rp[0]``` will select the latest recovery point.</span></span>

### <a name="restoring-disks"></a><span data-ttu-id="0eda4-189">Restauration de disques</span><span class="sxs-lookup"><span data-stu-id="0eda4-189">Restoring disks</span></span>
<span data-ttu-id="0eda4-190">Il existe une différence essentielle entre les opérations de restauration effectuées par le biais du portail Azure et celles effectuées via Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0eda4-190">There is a key difference between the restore operations done through the Azure portal and through Azure PowerShell.</span></span> <span data-ttu-id="0eda4-191">Avec PowerShell, l’opération de restauration se limite à la restauration des disques et informations de configuration à partir d’un point de restauration.</span><span class="sxs-lookup"><span data-stu-id="0eda4-191">With PowerShell, the restore operation stops at restoring the disks and config information from the recovery point.</span></span> <span data-ttu-id="0eda4-192">Il n’y a pas de création de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0eda4-192">It does not create a virtual machine.</span></span>

> [!WARNING]
> <span data-ttu-id="0eda4-193">L’applet de commande Restore-AzureRmBackupItem ne crée pas une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0eda4-193">The Restore-AzureRmBackupItem does not create a VM.</span></span> <span data-ttu-id="0eda4-194">Elle restaure uniquement les disques dans le compte de stockage spécifié.</span><span class="sxs-lookup"><span data-stu-id="0eda4-194">It only restores the disks to the specified storage account.</span></span> <span data-ttu-id="0eda4-195">Vous ne constaterez pas le même comportement avec le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0eda4-195">This is not the same behavior you will experience in the Azure portal.</span></span>
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

<span data-ttu-id="0eda4-196">Vous pouvez obtenir les détails de l’opération de restauration à l’aide de l’applet de commande **Get-AzureRmBackupJobDetails** une fois la tâche de restauration terminée.</span><span class="sxs-lookup"><span data-stu-id="0eda4-196">You can get the details of the restore operation using the **Get-AzureRmBackupJobDetails** cmdlet once the Restore job has completed.</span></span> <span data-ttu-id="0eda4-197">La propriété *ErrorDetails* contient les informations nécessaires pour régénérer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0eda4-197">The *ErrorDetails* property will have the information needed to rebuild the VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-the-vm"></a><span data-ttu-id="0eda4-198">Création de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="0eda4-198">Build the VM</span></span>
<span data-ttu-id="0eda4-199">La création de la machine virtuelle à partir de disques restaurés peut être effectuée à l’aide d’applets de commande Azure Service Management PowerShell plus anciennes, des nouveaux modèles Azure Resource Manager ou même à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0eda4-199">Building the VM out of the restored disks can be done using the older Azure Service Management PowerShell cmdlets, the new Azure Resource Manager templates, or even using the Azure portal.</span></span> <span data-ttu-id="0eda4-200">Dans un exemple rapide, nous allons montrer comment y parvenir via les applets de commande Azure Service Management.</span><span class="sxs-lookup"><span data-stu-id="0eda4-200">In a quick example, we will show how to get there using the Azure Service Management cmdlets.</span></span>

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

<span data-ttu-id="0eda4-201">Pour plus d’informations sur la création d’une machine virtuelle à partir des disques restaurés, découvrez les applets de commande suivantes :</span><span class="sxs-lookup"><span data-stu-id="0eda4-201">For more information on how to build a VM from the restored disks, read about the following cmdlets:</span></span>

* [<span data-ttu-id="0eda4-202">Add-AzureDisk</span><span class="sxs-lookup"><span data-stu-id="0eda4-202">Add-AzureDisk</span></span>](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [<span data-ttu-id="0eda4-203">New-AzureVMConfig</span><span class="sxs-lookup"><span data-stu-id="0eda4-203">New-AzureVMConfig</span></span>](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [<span data-ttu-id="0eda4-204">New-AzureVM</span><span class="sxs-lookup"><span data-stu-id="0eda4-204">New-AzureVM</span></span>](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a><span data-ttu-id="0eda4-205">Exemples de code</span><span class="sxs-lookup"><span data-stu-id="0eda4-205">Code samples</span></span>
### <a name="1-get-the-completion-status-of-job-sub-tasks"></a><span data-ttu-id="0eda4-206">1. Obtenir l'état d'achèvement des sous-tâches de travail</span><span class="sxs-lookup"><span data-stu-id="0eda4-206">1. Get the completion status of job sub-tasks</span></span>
<span data-ttu-id="0eda4-207">Pour suivre l’état d’achèvement de sous-tâches individuelles, vous pouvez utiliser l’applet de commande **Get-AzureRmBackupJobDetails** :</span><span class="sxs-lookup"><span data-stu-id="0eda4-207">To track the completion status of individual sub-tasks, you can use the **Get-AzureRmBackupJobDetails** cmdlet:</span></span>

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data to Backup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a><span data-ttu-id="0eda4-208">2. Création d’un rapport quotidien/hebdomadaire des travaux de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="0eda4-208">2. Create a daily/weekly report of backup jobs</span></span>
<span data-ttu-id="0eda4-209">En général, les administrateurs souhaitent connaître les travaux de sauvegarde exécutés au cours des dernières 24 heures ainsi que l'état de ces travaux de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="0eda4-209">Administrators typically want to know what backup jobs ran in the last 24 hours, the status of those backup jobs.</span></span> <span data-ttu-id="0eda4-210">En outre, la quantité de données transférées offre aux administrateurs une manière d'évaluer leur utilisation mensuelle de données.</span><span class="sxs-lookup"><span data-stu-id="0eda4-210">Additionally, the amount of data transferred gives administrators a way to estimate their monthly data usage.</span></span> <span data-ttu-id="0eda4-211">Le script ci-dessous extrait les données brutes à partir du service de sauvegarde Azure et affiche les informations sur la console PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0eda4-211">The script below pulls the raw data from the Azure Backup service and displays the information in the PowerShell console.</span></span>

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
    $dailyjoblist = Get-AzureRmBackupJob -Vault $backupvault -From $startdate -To $enddate -Type AzureVM -Operation Backup
    Write-Progress -Activity "Getting job information for the last $numberofdays days" -Status "Day -$i" -PercentComplete ([int]([decimal]$i*100/$numberofdays))

    foreach( $job in $dailyjoblist )
    {
        #Extract the information for the reports
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

<span data-ttu-id="0eda4-212">Si vous souhaitez ajouter des fonctionnalités graphiques à ce rapport, consultez le billet de blog TechNet sur [Fonctionnalités graphiques avec PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span><span class="sxs-lookup"><span data-stu-id="0eda4-212">If you want to add charting capabilities to this report output, learn from the TechNet blog post [Charting with PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="0eda4-213">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0eda4-213">Next steps</span></span>
<span data-ttu-id="0eda4-214">Si vous préférez utiliser PowerShell pour gérer vos ressources Azure, consultez l’article de PowerShell pour la protection de Windows Server : [Déployer et gérer une sauvegarde pour Windows Server](backup-client-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="0eda4-214">If you prefer using PowerShell to engage with your Azure resources, check out the PowerShell article for protecting Windows Server, [Deploy and Manage Backup for Windows Server](backup-client-automation-classic.md).</span></span> <span data-ttu-id="0eda4-215">Il existe également un article PowerShell sur la gestion des sauvegardes DPM : [Déployer et gérer une sauvegarde pour DPM](backup-dpm-automation-classic.md).</span><span class="sxs-lookup"><span data-stu-id="0eda4-215">There is also a PowerShell article for managing DPM backups, [Deploy and Manage Backup for DPM](backup-dpm-automation-classic.md).</span></span> <span data-ttu-id="0eda4-216">Ces deux articles ont une version concernant les déploiements avec le modèle Resource Manager et le modèle Classic.</span><span class="sxs-lookup"><span data-stu-id="0eda4-216">Both of these articles have a version for Resource Manager deployments as well as Classic deployments.</span></span>
