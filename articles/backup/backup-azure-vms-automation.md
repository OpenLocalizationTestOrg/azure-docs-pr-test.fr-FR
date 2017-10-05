---
title: "Déploiement et gestion des sauvegardes de machines virtuelles déployées avec le modèle Resource Manager à l’aide de PowerShell | Microsoft Docs"
description: "Utilisation de PowerShell pour déployer et gérer des sauvegardes dans Azure pour les machines virtuelles déployées avec le modèle Resource Manager"
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
ms.openlocfilehash: 861346a50df6641abb9e454644228146e14b4078
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azurermrecoveryservicesbackup-cmdlets-to-back-up-virtual-machines"></a><span data-ttu-id="39102-103">Utilisez les applets de commande AzureRM.RecoveryServices.Backup pour sauvegarder des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="39102-103">Use AzureRM.RecoveryServices.Backup cmdlets to back up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="39102-104">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="39102-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="39102-105">Classique</span><span class="sxs-lookup"><span data-stu-id="39102-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="39102-106">Cet article vous montre comment utiliser des applets de commande Azure PowerShell pour sauvegarder et restaurer une machine virtuelle Azure à partir d’un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="39102-106">This article shows you how to use Azure PowerShell cmdlets to back up and recover an Azure virtual machine (VM) from a Recovery Services vault.</span></span> <span data-ttu-id="39102-107">Un coffre Recovery Services est une ressource Azure Resource Manager utilisée pour protéger les données et les actifs dans Azure Backup et Azure Site Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="39102-107">A Recovery Services vault is an Azure Resource Manager resource and is used to protect data and assets in both Azure Backup and Azure Site Recovery services.</span></span> <span data-ttu-id="39102-108">Vous pouvez utiliser un coffre Recovery Services pour protéger des machines virtuelles déployées avec Azure Service Manager, ainsi que des machines virtuelles déployées avec le modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="39102-108">You can use a Recovery Services vault to protect Azure Service Manager-deployed VMs, and Azure Resource Manager-deployed VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="39102-109">Azure dispose de deux modèles de déploiement pour créer et utiliser des ressources : [Azure Resource Manager et Azure Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="39102-109">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="39102-110">Cet article concerne l’utilisation avec des machines virtuelles créées à l’aide du modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="39102-110">This article is for use with VMs created using the Resource Manager model.</span></span>
>
>

<span data-ttu-id="39102-111">Cet article vous guide tout au long de l’utilisation de PowerShell pour protéger une machine virtuelle et la restauration de données à partir d’un point de récupération.</span><span class="sxs-lookup"><span data-stu-id="39102-111">This article walks you through using PowerShell to protect a VM, and restore data from a recovery point.</span></span>

## <a name="concepts"></a><span data-ttu-id="39102-112">Concepts</span><span class="sxs-lookup"><span data-stu-id="39102-112">Concepts</span></span>
<span data-ttu-id="39102-113">Si vous n’êtes pas familiarisé avec le service de sauvegarde Azure, consultez [Qu’est-ce que la Sauvegarde Azure ?](backup-introduction-to-azure-backup.md) pour obtenir une vue d’ensemble du service.</span><span class="sxs-lookup"><span data-stu-id="39102-113">If you are not familiar with the Azure Backup service, for an overview of the service, check out [What is Azure Backup?](backup-introduction-to-azure-backup.md)</span></span> <span data-ttu-id="39102-114">Avant de commencer, assurez-vous de connaître les conditions préalables de base nécessaires pour travailler avec Azure Backup et les limitations de la solution actuelle de sauvegarde de la machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="39102-114">Before you start, ensure that you cover the essentials about the prerequisites needed to work with Azure Backup, and the limitations of the current VM backup solution.</span></span>

<span data-ttu-id="39102-115">Pour pouvoir utiliser efficacement PowerShell, il est nécessaire de comprendre la hiérarchie des objets et par où commencer.</span><span class="sxs-lookup"><span data-stu-id="39102-115">To use PowerShell effectively, it is necessary to understand the hierarchy of objects and from where to start.</span></span>

![Hiérarchie des objets dans Recovery Services](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

<span data-ttu-id="39102-117">Pour voir les informations de référence sur l’applet de commande PowerShell AzureRmRecoveryServicesBackup, consultez [Sauvegarde Azure - Applets de commande de Recovery Services](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) dans la bibliothèque Azure.</span><span class="sxs-lookup"><span data-stu-id="39102-117">To view the AzureRm.RecoveryServices.Backup PowerShell cmdlet reference, see the [Azure Backup - Recovery Services Cmdlets](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) in the Azure library.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="39102-118">Installation et inscription</span><span class="sxs-lookup"><span data-stu-id="39102-118">Setup and Registration</span></span>
<span data-ttu-id="39102-119">Pour commencer :</span><span class="sxs-lookup"><span data-stu-id="39102-119">To begin:</span></span>

1. <span data-ttu-id="39102-120">[Téléchargez la dernière version de PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (version minimale requise : 1.4.0)</span><span class="sxs-lookup"><span data-stu-id="39102-120">[Download the latest version of PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (the minimum version required is: 1.4.0)</span></span>
2. <span data-ttu-id="39102-121">Rechercher les applets de commande PowerShell Azure Backup disponibles en tapant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="39102-121">Find the Azure Backup PowerShell cmdlets available by typing the following command:</span></span>

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


<span data-ttu-id="39102-122">Les tâches ci-après peuvent être automatisées avec PowerShell :</span><span class="sxs-lookup"><span data-stu-id="39102-122">The following tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="39102-123">Créer un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="39102-123">Create a Recovery Services vault</span></span>
* <span data-ttu-id="39102-124">Sauvegarder des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="39102-124">Back up Azure VMs</span></span>
* <span data-ttu-id="39102-125">Déclencher une tâche de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="39102-125">Trigger a backup job</span></span>
* <span data-ttu-id="39102-126">Surveiller une tâche de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="39102-126">Monitor a backup job</span></span>
* <span data-ttu-id="39102-127">Restauration d’une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="39102-127">Restore an Azure VM</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="39102-128">Créer un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="39102-128">Create a recovery services vault</span></span>
<span data-ttu-id="39102-129">Les étapes suivantes vous montrent comment créer un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="39102-129">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="39102-130">Un coffre Recovery Services diffère d’un coffre Backup.</span><span class="sxs-lookup"><span data-stu-id="39102-130">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="39102-131">Si vous utilisez Sauvegarde Azure pour la première fois, vous devez utiliser l’applet de commande **[Register-AzureRMResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)** pour inscrire le fournisseur Azure Recovery Service auprès de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="39102-131">If you are using Azure Backup for the first time, you must use the **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="39102-132">Le coffre Recovery Services étant une ressource Resource Manager, vous devez le placer dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="39102-132">The Recovery Services vault is a Resource Manager resource, so you need to place it within a resource group.</span></span> <span data-ttu-id="39102-133">Si vous ne disposez pas d’un groupe de ressources, créez-en un avec la cmdlet **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)**.</span><span class="sxs-lookup"><span data-stu-id="39102-133">You can use an existing resource group, or create a resource group with the **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)** cmdlet.</span></span> <span data-ttu-id="39102-134">Quand vous créez un groupe de ressources, spécifiez son nom et son emplacement.</span><span class="sxs-lookup"><span data-stu-id="39102-134">When creating a resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="39102-135">Utilisez l’applet de commande **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)** pour créer un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="39102-135">Use the **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)** cmdlet to create the Recovery Services vault.</span></span> <span data-ttu-id="39102-136">Spécifiez pour le coffre le même emplacement que pour le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="39102-136">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="39102-137">Spécifiez le type de redondance de stockage à utiliser : [Stockage localement redondant (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) ou [Stockage géo-redondant (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="39102-137">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="39102-138">L’exemple suivant montre que l’option -BackupStorageRedundancy pour testvault est définie sur GeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="39102-138">The following example shows the -BackupStorageRedundancy option for testvault is set to GeoRedundant.</span></span>

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > <span data-ttu-id="39102-139">De nombreuses applets de commande Azure Backup nécessitent l’objet coffre Recovery Services en tant qu’entrée.</span><span class="sxs-lookup"><span data-stu-id="39102-139">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span></span> <span data-ttu-id="39102-140">Pour cette raison, il est pratique de stocker l’objet coffre Backup Recovery Services dans une variable.</span><span class="sxs-lookup"><span data-stu-id="39102-140">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span></span>
   >
   >

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="39102-141">Afficher les coffres dans un abonnement</span><span class="sxs-lookup"><span data-stu-id="39102-141">View the vaults in a subscription</span></span>
<span data-ttu-id="39102-142">Utilisez **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)** pour afficher la liste de tous les coffres dans l’abonnement actuel.</span><span class="sxs-lookup"><span data-stu-id="39102-142">Use **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="39102-143">Vous pouvez utiliser cette commande pour vérifier qu’un coffre a été créé ou pour voir les coffres disponibles dans l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="39102-143">You can use this command to check that a new vault was created, or to see the available vaults in the subscription.</span></span>

<span data-ttu-id="39102-144">Exécutez la commande Get-AzureRmRecoveryServicesVault pour afficher tous les coffres de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="39102-144">Run the command, Get-AzureRmRecoveryServicesVault, to view all vaults in the subscription.</span></span> <span data-ttu-id="39102-145">L’exemple suivant montre les informations affichées pour chaque coffre.</span><span class="sxs-lookup"><span data-stu-id="39102-145">The following example shows the information displayed for each vault.</span></span>

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


## <a name="back-up-azure-vms"></a><span data-ttu-id="39102-146">Sauvegarder des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="39102-146">Back up Azure VMs</span></span>
<span data-ttu-id="39102-147">Utilisez un coffre Recovery Services pour protéger vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="39102-147">Use a Recovery Services vault to protect your virtual machines.</span></span> <span data-ttu-id="39102-148">Avant d’appliquer la protection, définissez le contexte du coffre (le type de données qu’il protège) et vérifiez la stratégie de protection.</span><span class="sxs-lookup"><span data-stu-id="39102-148">Before you apply the protection, set the vault context (the type of data protected in the vault), and verify the protection policy.</span></span> <span data-ttu-id="39102-149">La stratégie de protection consiste à planifier l’exécution du travail de sauvegarde et la durée de conservation de chaque instantané de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="39102-149">The protection policy is the schedule when the backup jobs run, and how long each backup snapshot is retained.</span></span>

### <a name="set-vault-context"></a><span data-ttu-id="39102-150">Définir le contexte du coffre</span><span class="sxs-lookup"><span data-stu-id="39102-150">Set vault context</span></span>
<span data-ttu-id="39102-151">Avant d’activer la protection sur une machine virtuelle, utilisez  **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  pour définir le contexte du coffre.</span><span class="sxs-lookup"><span data-stu-id="39102-151">Before enabling protection on a VM, use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** to set the vault context.</span></span> <span data-ttu-id="39102-152">Une fois le contexte du coffre défini, il s’applique à toutes les applets de commande suivantes.</span><span class="sxs-lookup"><span data-stu-id="39102-152">Once the vault context is set, it applies to all subsequent cmdlets.</span></span> <span data-ttu-id="39102-153">L’exemple suivant définit le contexte du coffre pour le coffre *testvault*.</span><span class="sxs-lookup"><span data-stu-id="39102-153">The following example sets the vault context for the vault, *testvault*.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a><span data-ttu-id="39102-154">Création d’une stratégie de protection</span><span class="sxs-lookup"><span data-stu-id="39102-154">Create a protection policy</span></span>
<span data-ttu-id="39102-155">Quand vous créez un coffre Recovery Services, il est fourni avec des stratégies de protection et de conservation par défaut.</span><span class="sxs-lookup"><span data-stu-id="39102-155">When you create a Recovery Services vault, it comes with default protection and retention policies.</span></span> <span data-ttu-id="39102-156">La stratégie de protection par défaut déclenche une tâche de sauvegarde chaque jour à une heure spécifiée.</span><span class="sxs-lookup"><span data-stu-id="39102-156">The default protection policy triggers a backup job each day at a specified time.</span></span> <span data-ttu-id="39102-157">La stratégie de conservation par défaut conserve le point de récupération quotidien pendant 30 jours.</span><span class="sxs-lookup"><span data-stu-id="39102-157">The default retention policy retains the daily recovery point for 30 days.</span></span> <span data-ttu-id="39102-158">Vous pouvez utiliser la stratégie par défaut pour protéger rapidement votre machine virtuelle et modifier la stratégie ultérieurement avec différents détails.</span><span class="sxs-lookup"><span data-stu-id="39102-158">You can use the default policy to quickly protect your VM and edit the policy later with different details.</span></span>

<span data-ttu-id="39102-159">Utilisez **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)** pour afficher les stratégies de protection du coffre.</span><span class="sxs-lookup"><span data-stu-id="39102-159">Use **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)** to view the protection policies in the vault.</span></span> <span data-ttu-id="39102-160">Vous pouvez utiliser cette applet de commande pour obtenir une stratégie spécifique ou pour afficher les stratégies associées à un type de charge de travail.</span><span class="sxs-lookup"><span data-stu-id="39102-160">You can use this cmdlet to get a specific policy, or to view the policies associated with a workload type.</span></span> <span data-ttu-id="39102-161">L’exemple suivant obtient les stratégies pour le type de charge de travail AzureVM.</span><span class="sxs-lookup"><span data-stu-id="39102-161">The following example gets policies for workload type, AzureVM.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> <span data-ttu-id="39102-162">Le fuseau horaire du champ BackupTime dans PowerShell est UTC.</span><span class="sxs-lookup"><span data-stu-id="39102-162">The timezone of the BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="39102-163">Toutefois, lorsque l’heure de sauvegarde s’affiche dans le portail Azure, elle est alignée sur votre fuseau horaire.</span><span class="sxs-lookup"><span data-stu-id="39102-163">However, when the backup time is shown in the Azure portal, the time is adjusted to your local timezone.</span></span>
>
>

<span data-ttu-id="39102-164">Une stratégie de protection de la sauvegarde est associée à au moins une stratégie de rétention.</span><span class="sxs-lookup"><span data-stu-id="39102-164">A backup protection policy is associated with at least one retention policy.</span></span> <span data-ttu-id="39102-165">La stratégie de conservation définit la durée de conservation d’un point de restauration avant sa suppression.</span><span class="sxs-lookup"><span data-stu-id="39102-165">Retention policy defines how long a recovery point is kept before it is deleted.</span></span> <span data-ttu-id="39102-166">Utilisez **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)** pour afficher la stratégie de conservation par défaut.</span><span class="sxs-lookup"><span data-stu-id="39102-166">Use **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)** to view the default retention policy.</span></span>  <span data-ttu-id="39102-167">De même, vous pouvez utiliser **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)** pour obtenir la stratégie de planification par défaut.</span><span class="sxs-lookup"><span data-stu-id="39102-167">Similarly you can use **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)** to obtain the default schedule policy.</span></span> <span data-ttu-id="39102-168">L’applet de commande **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** crée un objet PowerShell contenant des informations sur la stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="39102-168">The **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="39102-169">Les objets de la stratégie de planification et de conservation sont utilisés comme entrées pour l’applet de commande **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**.</span><span class="sxs-lookup"><span data-stu-id="39102-169">The schedule and retention policy objects are used as inputs to the **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet.</span></span> <span data-ttu-id="39102-170">L’exemple suivant stocke la stratégie de planification et la stratégie de conservation dans des variables.</span><span class="sxs-lookup"><span data-stu-id="39102-170">The following example stores the schedule policy and the retention policy in variables.</span></span> <span data-ttu-id="39102-171">L’exemple utilise ces variables pour définir les paramètres lors de la création d’une stratégie de protection, *NewPolicy*.</span><span class="sxs-lookup"><span data-stu-id="39102-171">The example uses those variables to define the parameters when creating a protection policy, *NewPolicy*.</span></span>

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a><span data-ttu-id="39102-172">Activer la protection</span><span class="sxs-lookup"><span data-stu-id="39102-172">Enable protection</span></span>
<span data-ttu-id="39102-173">Une fois que vous avez défini la stratégie de protection de la sauvegarde, vous devez encore activer la stratégie pour un élément.</span><span class="sxs-lookup"><span data-stu-id="39102-173">Once you have defined the backup protection policy, you still must enable the policy for an item.</span></span> <span data-ttu-id="39102-174">Utilisez  **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)**  pour activer la protection.</span><span class="sxs-lookup"><span data-stu-id="39102-174">Use **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)** to enable protection.</span></span> <span data-ttu-id="39102-175">L’activation de la protection nécessite deux objets : l’élément et la stratégie.</span><span class="sxs-lookup"><span data-stu-id="39102-175">Enabling protection requires two objects - the item and the policy.</span></span> <span data-ttu-id="39102-176">Une fois que la stratégie a été associée au coffre, le flux de travail de la sauvegarde est déclenché à l’heure planifiée dans la planification de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="39102-176">Once the policy has been associated with the vault, the backup workflow is triggered at the time defined in the policy schedule.</span></span>

<span data-ttu-id="39102-177">L’exemple suivant active la protection pour l’élément V2VM avec la stratégie NewPolicy.</span><span class="sxs-lookup"><span data-stu-id="39102-177">The following example enables protection for the item, V2VM, using the policy, NewPolicy.</span></span> <span data-ttu-id="39102-178">Pour activer la protection sur des machines virtuelles Resource Manager non chiffrées</span><span class="sxs-lookup"><span data-stu-id="39102-178">To enable the protection on non-encrypted Resource Manager VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="39102-179">Pour activer la protection sur des machines virtuelles chiffrées (à l’aide de clés BEK et KEK), vous devez accorder au service Sauvegarde Azure l’autorisation de lire les clés et les secrets dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="39102-179">To enable the protection on encrypted VMs (encrypted using BEK and KEK), you need to give the Azure Backup service permission to read keys and secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="39102-180">Pour activer la protection sur les machines virtuelles chiffrées (à l’aide de clés BEK uniquement), vous devez accorder au service Sauvegarde Azure l’autorisation de lire les secrets dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="39102-180">To enable the protection on encrypted VMs (encrypted using BEK only), you need to give the Azure Backup service permission to read secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> <span data-ttu-id="39102-181">Si vous êtes sur le cloud Azure Government, utilisez la valeur ff281ffe-705c-4f53-9f37-a40e6f2c68f3 pour le paramètre **- ServicePrincipalName** dans l’applet de commande [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy).</span><span class="sxs-lookup"><span data-stu-id="39102-181">If you are using the Azure Government cloud, then use the value ff281ffe-705c-4f53-9f37-a40e6f2c68f3 for the parameter **-ServicePrincipalName** in [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.</span></span>
>
>

<span data-ttu-id="39102-182">Pour les machines virtuelles Classic</span><span class="sxs-lookup"><span data-stu-id="39102-182">For classic VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a><span data-ttu-id="39102-183">Modifier une stratégie de protection</span><span class="sxs-lookup"><span data-stu-id="39102-183">Modify a protection policy</span></span>
<span data-ttu-id="39102-184">Pour modifier la stratégie de protection, utilisez [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) pour modifier les objets SchedulePolicy ou RetentionPolicy.</span><span class="sxs-lookup"><span data-stu-id="39102-184">To modify the protection policy, use [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) to modify the SchedulePolicy or RetentionPolicy objects.</span></span>

<span data-ttu-id="39102-185">L’exemple suivant change la conservation des points de récupération en 365 jours.</span><span class="sxs-lookup"><span data-stu-id="39102-185">The following example changes the recovery point retention to 365 days.</span></span>

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a><span data-ttu-id="39102-186">Déclencher une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="39102-186">Trigger a backup</span></span>
<span data-ttu-id="39102-187">Vous pouvez utiliser  **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)** pour déclencher une tâche de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="39102-187">You can use **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)** to trigger a backup job.</span></span> <span data-ttu-id="39102-188">S’il s’agit de la sauvegarde initiale, c’est une sauvegarde complète.</span><span class="sxs-lookup"><span data-stu-id="39102-188">If it is the initial backup, it is a full backup.</span></span> <span data-ttu-id="39102-189">Les sauvegardes suivantes prennent une copie incrémentielle.</span><span class="sxs-lookup"><span data-stu-id="39102-189">Subsequent backups take an incremental copy.</span></span> <span data-ttu-id="39102-190">Veillez à utiliser  **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  pour définir le contexte du coffre avant de déclencher la tâche de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="39102-190">Be sure to use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** to set the vault context before triggering the backup job.</span></span> <span data-ttu-id="39102-191">L’exemple suivant suppose que la valeur du contexte du coffre a été définie.</span><span class="sxs-lookup"><span data-stu-id="39102-191">The following example assumes vault context was set.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> <span data-ttu-id="39102-192">Le fuseau horaire des champs StartTime et EndTime affichés dans PowerShell est UTC.</span><span class="sxs-lookup"><span data-stu-id="39102-192">The timezone of the StartTime and EndTime fields in PowerShell is UTC.</span></span> <span data-ttu-id="39102-193">Toutefois, lorsque l’heure s’affiche dans le portail Azure, elle est alignée sur votre fuseau horaire.</span><span class="sxs-lookup"><span data-stu-id="39102-193">However, when the time is shown in the Azure portal, the time is adjusted to your local timezone.</span></span>
>
>

## <a name="monitoring-a-backup-job"></a><span data-ttu-id="39102-194">Surveillance d’une tâche de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="39102-194">Monitoring a backup job</span></span>
<span data-ttu-id="39102-195">Vous pouvez surveiller les opérations à exécution longue, comme les tâches de sauvegarde, sans utiliser le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="39102-195">You can monitor long-running operations, such as backup jobs, without using the Azure portal.</span></span> <span data-ttu-id="39102-196">Pour obtenir l’état d’une tâche en cours d’exécution, utilisez l’applet de commande **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)**.</span><span class="sxs-lookup"><span data-stu-id="39102-196">To get the status of an in-progress job, use the **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="39102-197">Cette applet de commande obtient les tâches de sauvegarde pour un coffre spécifique, et ce coffre est spécifié dans le contexte du coffre.</span><span class="sxs-lookup"><span data-stu-id="39102-197">This cmdlet gets the backup jobs for a specific vault, and that vault is specified in the vault context.</span></span> <span data-ttu-id="39102-198">L’exemple suivant obtient l’état d’une tâche en cours d’exécution sous forme de tableau et stocke l’état dans la variable $joblist.</span><span class="sxs-lookup"><span data-stu-id="39102-198">The following example gets the status of an in-progress job as an array, and stores the status in the $joblist variable.</span></span>

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="39102-199">Au lieu d’interroger ces travaux pour connaître leur état d’avancement, ce qui implique du code supplémentaire inutile, utilisez l’applet de commande **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**.</span><span class="sxs-lookup"><span data-stu-id="39102-199">Instead of polling these jobs for completion - which is unnecessary additional code - use the **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="39102-200">Cette applet de commande suspend l’exécution jusqu’à la fin de la tâche ou jusqu’à ce que la valeur spécifiée pour l’expiration du délai soit atteinte.</span><span class="sxs-lookup"><span data-stu-id="39102-200">This cmdlet pauses the execution until either the job completes or the specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a><span data-ttu-id="39102-201">Restauration d’une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="39102-201">Restore an Azure VM</span></span>
<span data-ttu-id="39102-202">Il existe une différence clé entre la restauration d’une machine virtuelle à l’aide du portail Azure et la restauration d’une machine virtuelle à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="39102-202">There is a key difference between the restoring a VM using the Azure portal and restoring a VM using PowerShell.</span></span> <span data-ttu-id="39102-203">Avec PowerShell, l’opération de restauration est terminée dès que sont créés les disques et les informations de configuration à partir d’un point de restauration.</span><span class="sxs-lookup"><span data-stu-id="39102-203">With PowerShell, the restore operation is complete once the disks and configuration information from the recovery point are created.</span></span>

> [!NOTE]
> <span data-ttu-id="39102-204">L’opération de restauration ne crée pas de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="39102-204">The restore operation does not create a virtual machine.</span></span>
>
>

<span data-ttu-id="39102-205">Pour créer une machine virtuelle à partir d’un disque, consultez la section [Créer la machine virtuelle à partir de disques stockés](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span><span class="sxs-lookup"><span data-stu-id="39102-205">To create a virtual machine from disk, see the section, [Create the VM from stored disks](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span></span> <span data-ttu-id="39102-206">Les étapes de base pour restaurer une machine virtuelle Azure sont :</span><span class="sxs-lookup"><span data-stu-id="39102-206">The basic steps to restore an Azure VM are:</span></span>

* <span data-ttu-id="39102-207">Sélection de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="39102-207">Select the VM</span></span>
* <span data-ttu-id="39102-208">Choisir un point de récupération</span><span class="sxs-lookup"><span data-stu-id="39102-208">Choose a recovery point</span></span>
* <span data-ttu-id="39102-209">Restaurer les disques</span><span class="sxs-lookup"><span data-stu-id="39102-209">Restore the disks</span></span>
* <span data-ttu-id="39102-210">Créer la machine virtuelle à partir des disques stockés</span><span class="sxs-lookup"><span data-stu-id="39102-210">Create the VM from stored disks</span></span>

<span data-ttu-id="39102-211">L’illustration suivante montre la hiérarchie d’objets à partir de RecoveryServicesVault jusqu’à BackupRecoveryPoint.</span><span class="sxs-lookup"><span data-stu-id="39102-211">The following graphic shows the object hierarchy from the RecoveryServicesVault down to the BackupRecoveryPoint.</span></span>

![Hiérarchie d’objets Recovery Services montrant BackupContainer](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

<span data-ttu-id="39102-213">Pour restaurer les données de sauvegarde, identifiez l’élément sauvegardé et le point de récupération contenant les données ponctuelles.</span><span class="sxs-lookup"><span data-stu-id="39102-213">To restore backup data, identify the backed-up item and the recovery point that holds the point-in-time data.</span></span> <span data-ttu-id="39102-214">Utilisez l’applet de commande **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** pour restaurer les données à partir du coffre vers le compte du client.</span><span class="sxs-lookup"><span data-stu-id="39102-214">Use the **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet to restore data from the vault to the customer's account.</span></span>

### <a name="select-the-vm"></a><span data-ttu-id="39102-215">Sélection de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="39102-215">Select the VM</span></span>
<span data-ttu-id="39102-216">Pour obtenir l’objet PowerShell permettant d’identifier l’élément à restaurer, vous devez commencer au niveau du conteneur dans le coffre et descendre dans la hiérarchie d’objets.</span><span class="sxs-lookup"><span data-stu-id="39102-216">To get the PowerShell object that identifies the right backup item, start from the container in the vault, and work your way down the object hierarchy.</span></span> <span data-ttu-id="39102-217">Pour sélectionner le conteneur qui représente la machine virtuelle, utilisez l’applet de commande **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)** et dirigez-la vers l’applet de commande **[Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)**.</span><span class="sxs-lookup"><span data-stu-id="39102-217">To select the container that represents the VM, use the **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)** cmdlet and pipe that to the **[Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)** cmdlet.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="39102-218">Choisir un point de récupération</span><span class="sxs-lookup"><span data-stu-id="39102-218">Choose a recovery point</span></span>
<span data-ttu-id="39102-219">Utilisez l’applet de commande **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)** pour répertorier tous les points de récupération pour l’élément de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="39102-219">Use the **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)** cmdlet to list all recovery points for the backup item.</span></span> <span data-ttu-id="39102-220">Ensuite, choisissez le point de récupération à restaurer.</span><span class="sxs-lookup"><span data-stu-id="39102-220">Then choose the recovery point to restore.</span></span> <span data-ttu-id="39102-221">Si vous ne savez pas quel point de récupération utiliser, nous vous conseillons de choisir le point RecoveryPointType = AppConsistent le plus récent dans la liste.</span><span class="sxs-lookup"><span data-stu-id="39102-221">If you are unsure which recovery point to use, it is a good practice to choose the most recent RecoveryPointType = AppConsistent point in the list.</span></span>

<span data-ttu-id="39102-222">Dans le script suivant, la variable **$rp**est un tableau de points de récupération des 7 derniers jours pour l’élément de sauvegarde sélectionné.</span><span class="sxs-lookup"><span data-stu-id="39102-222">In the following script, the variable, **$rp**, is an array of recovery points for the selected backup item, from the past seven days.</span></span> <span data-ttu-id="39102-223">Le tableau est trié dans l’ordre chronologique inverse, le point de récupération le plus récent détenant l’index 0.</span><span class="sxs-lookup"><span data-stu-id="39102-223">The array is sorted in reverse order of time with the latest recovery point at index 0.</span></span> <span data-ttu-id="39102-224">Utilisez l'indexation de tableau PowerShell standard pour sélectionner le point de récupération.</span><span class="sxs-lookup"><span data-stu-id="39102-224">Use standard PowerShell array indexing to pick the recovery point.</span></span> <span data-ttu-id="39102-225">Dans l’exemple, $rp[0] sélectionne le dernier point de récupération.</span><span class="sxs-lookup"><span data-stu-id="39102-225">In the example, $rp[0] selects the latest recovery point.</span></span>

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



### <a name="restore-the-disks"></a><span data-ttu-id="39102-226">Restaurer les disques</span><span class="sxs-lookup"><span data-stu-id="39102-226">Restore the disks</span></span>
<span data-ttu-id="39102-227">Utilisez l’applet de commande **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** pour restaurer les données et la configuration d’un élément de sauvegarde à un point de récupération.</span><span class="sxs-lookup"><span data-stu-id="39102-227">Use the **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet to restore a backup item's data and configuration to a recovery point.</span></span> <span data-ttu-id="39102-228">Lorsque vous avez identifié un point de récupération, utilisez-le comme valeur du paramètre **-RecoveryPoint** .</span><span class="sxs-lookup"><span data-stu-id="39102-228">Once you have identified a recovery point, use it as the value for the **-RecoveryPoint** parameter.</span></span> <span data-ttu-id="39102-229">Dans l’exemple de code précédent, **$rp[0]** était le point de récupération à utiliser.</span><span class="sxs-lookup"><span data-stu-id="39102-229">In the previous sample code, **$rp[0]** was the recovery point to use.</span></span> <span data-ttu-id="39102-230">Dans l’exemple de code suivant, **$rp [0]** est le point de récupération à utiliser pour restaurer le disque.</span><span class="sxs-lookup"><span data-stu-id="39102-230">In the following sample code, **$rp[0]** is the recovery point to use for restoring the disk.</span></span>

<span data-ttu-id="39102-231">Pour restaurer les disques et les informations de configuration :</span><span class="sxs-lookup"><span data-stu-id="39102-231">To restore the disks and configuration information:</span></span>

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="39102-232">Utilisez l’applet de commande **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** pour attendre que la tâche de restauration soit terminée.</span><span class="sxs-lookup"><span data-stu-id="39102-232">Use the **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet to wait for the Restore job to complete.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

<span data-ttu-id="39102-233">Une fois le travail de restauration terminé, utilisez l’applet de commande **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)** pour obtenir les détails du travail de restauration.</span><span class="sxs-lookup"><span data-stu-id="39102-233">Once the Restore job has completed, use the **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)** cmdlet to get the details of the restore operation.</span></span> <span data-ttu-id="39102-234">La propriété JobDetails contient les informations nécessaires pour régénérer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="39102-234">The JobDetails property has the information needed to rebuild the VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

<span data-ttu-id="39102-235">Une fois que vous avez restauré les disques, accédez à la section suivante pour créer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="39102-235">Once you restore the disks, go to the next section to create the VM.</span></span>

## <a name="create-a-vm-from-restored-disks"></a><span data-ttu-id="39102-236">Créer une machine virtuelle à partir de disques restaurés</span><span class="sxs-lookup"><span data-stu-id="39102-236">Create a VM from restored disks</span></span>
<span data-ttu-id="39102-237">Après avoir restauré les disques, exécutez les étapes ci-après pour créer et configurer la machine virtuelle à partir du disque.</span><span class="sxs-lookup"><span data-stu-id="39102-237">After you have restored the disks, use these steps to create and configure the virtual machine from disk.</span></span>

> [!NOTE]
> <span data-ttu-id="39102-238">Pour créer des machines virtuelles chiffrées à partir de disques restaurés, votre rôle Azure doit avoir l’autorisation d’effectuer l’action **Microsoft.KeyVault/vaults/deploy/action**.</span><span class="sxs-lookup"><span data-stu-id="39102-238">To create encrypted VMs from restored disks, your Azure role must have permission to perform the action, **Microsoft.KeyVault/vaults/deploy/action**.</span></span> <span data-ttu-id="39102-239">Si votre rôle ne dispose pas de cette autorisation, créez un rôle personnalisé avec cette action.</span><span class="sxs-lookup"><span data-stu-id="39102-239">If your role does not have this permission, create a custom role with this action.</span></span> <span data-ttu-id="39102-240">Pour plus d’informations, consultez [Rôles personnalisés dans le contrôle d’accès en fonction du rôle (RBAC) Azure](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="39102-240">For more information, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>
>
>

1. <span data-ttu-id="39102-241">Interrogez les propriétés des disques restaurés pour obtenir les détails du travail.</span><span class="sxs-lookup"><span data-stu-id="39102-241">Query the restored disk properties for the job details.</span></span>

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. <span data-ttu-id="39102-242">Définissez le contexte de stockage Azure et restaurez le fichier de configuration JSON.</span><span class="sxs-lookup"><span data-stu-id="39102-242">Set the Azure storage context and restore the JSON configuration file.</span></span>

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. <span data-ttu-id="39102-243">Utilisez le fichier de configuration JSON pour créer la configuration de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="39102-243">Use the JSON configuration file to create the VM configuration.</span></span>

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. <span data-ttu-id="39102-244">Attachez le disque du système d’exploitation et les disques de données.</span><span class="sxs-lookup"><span data-stu-id="39102-244">Attach the OS disk and data disks.</span></span> <span data-ttu-id="39102-245">Selon la configuration de vos machines virtuelles, cliquez sur le lien approprié pour afficher les applets de commande respectifs :</span><span class="sxs-lookup"><span data-stu-id="39102-245">Depending on the configuration of your VMs, click on the relevant link to view respective cmdlets:</span></span> 
    - [<span data-ttu-id="39102-246">Machines virtuelles non gérés, non chiffré</span><span class="sxs-lookup"><span data-stu-id="39102-246">Non-managed, non-encrypted VMs</span></span>](#non-managed-non-encrypted-vms)
    - [<span data-ttu-id="39102-247">Machines virtuelles non gérés, chiffrés (BEK uniquement)</span><span class="sxs-lookup"><span data-stu-id="39102-247">Non-managed, encrypted VMs (BEK only)</span></span>](#non-managed-encrypted-vms-bek-only)
    - [<span data-ttu-id="39102-248">Machines virtuelles non gérés, chiffrés (BEK et KEK)</span><span class="sxs-lookup"><span data-stu-id="39102-248">Non-managed, encrypted VMs (BEK and KEK)</span></span>](#non-managed-encrypted-vms-bek-and-kek)
    - [<span data-ttu-id="39102-249">Ordinateurs virtuels gérés, non chiffré</span><span class="sxs-lookup"><span data-stu-id="39102-249">Managed, non-encrypted VMs</span></span>](#managed-non-encrypted-vms)
    - [<span data-ttu-id="39102-250">Ordinateurs virtuels gérés, chiffrés (BEK et KEK)</span><span class="sxs-lookup"><span data-stu-id="39102-250">Managed, encrypted VMs (BEK and KEK)</span></span>](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a><span data-ttu-id="39102-251">Machines virtuelles non gérées et non chiffrées</span><span class="sxs-lookup"><span data-stu-id="39102-251">Non-managed, non-encrypted VMs</span></span>

    <span data-ttu-id="39102-252">Utilisez l’exemple suivant pour une machine virtuelle non gérée et non chiffrée.</span><span class="sxs-lookup"><span data-stu-id="39102-252">Use the following sample for non-managed, non-encrypted VMs.</span></span>

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a><span data-ttu-id="39102-253">Machines virtuelles non managées et chiffrées (BEK uniquement)</span><span class="sxs-lookup"><span data-stu-id="39102-253">Non-managed, encrypted VMs (BEK only)</span></span>

    <span data-ttu-id="39102-254">Pour les machines virtuelles non managées et chiffrées (à l’aide de BEK uniquement), vous devez restaurer le secret dans le coffre de clés avant d’attacher des disques.</span><span class="sxs-lookup"><span data-stu-id="39102-254">For non-managed, encrypted VMs (encrypted using BEK only), you need to restore the secret to the key vault before you can attach disks.</span></span> <span data-ttu-id="39102-255">Pour plus d’informations, consultez l’article [Restaurer une machine virtuelle chiffrée à partir d’un point de récupération Sauvegarde Azure](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="39102-255">For more information, please see the article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="39102-256">L’exemple suivant montre comment attacher des disques de système d’exploitation et de données pour les machines virtuelles chiffrées.</span><span class="sxs-lookup"><span data-stu-id="39102-256">The following sample shows how to attach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="39102-257">Machines virtuelles non managées et chiffrées (BEK et KEK)</span><span class="sxs-lookup"><span data-stu-id="39102-257">Non-managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="39102-258">Pour les machines virtuelles non managées et chiffrées (à l’aide de BEK et de KEK), vous devez restaurer la clé et le secret dans le coffre de clés avant d’attacher des disques.</span><span class="sxs-lookup"><span data-stu-id="39102-258">For non-managed, encrypted VMs (encrypted using BEK and KEK), you need to restore the key and secret to the key vault before you can attach disks.</span></span> <span data-ttu-id="39102-259">Pour plus d’informations, consultez l’article [Restaurer une machine virtuelle chiffrée à partir d’un point de récupération Sauvegarde Azure](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="39102-259">For more information, please see the article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="39102-260">L’exemple suivant montre comment attacher des disques de système d’exploitation et de données pour les machines virtuelles chiffrées.</span><span class="sxs-lookup"><span data-stu-id="39102-260">The following sample shows how to attach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="managed-non-encrypted-vms"></a><span data-ttu-id="39102-261">Machines virtuelles gérées et non chiffrées</span><span class="sxs-lookup"><span data-stu-id="39102-261">Managed, non-encrypted VMs</span></span>

    <span data-ttu-id="39102-262">Pour les machines virtuelles gérées et non chiffrées, vous devez créer des disques managés à partir de Stockage Blob, puis attacher les disques.</span><span class="sxs-lookup"><span data-stu-id="39102-262">For managed non-encrypted VMs, you'll need to create managed disks from blob storage, and then attach the disks.</span></span> <span data-ttu-id="39102-263">Pour plus d’informations, consultez l’article [Attacher un disque de données à une machine virtuelle Windows à l’aide de PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="39102-263">For in-depth information, see the article, [Attach a data disk to a Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="39102-264">L’exemple de code suivant montre comment attacher les disques de données pour des machines virtuelles non chiffrées et gérées.</span><span class="sxs-lookup"><span data-stu-id="39102-264">The following sample code shows how to attach the data disks for managed non-encrypted VMs.</span></span>

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

    #### <a name="managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="39102-265">Machines virtuelles managées et chiffrées (BEK et KEK)</span><span class="sxs-lookup"><span data-stu-id="39102-265">Managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="39102-266">Pour les machines virtuelles managées et chiffrées (à l’aide de BEK et de KEK), vous devez créer des disques managés depuis Stockage Blob, puis attacher les disques.</span><span class="sxs-lookup"><span data-stu-id="39102-266">For managed encrypted VMs (encrypted using BEK and KEK), you'll need to create managed disks from blob storage, and then attach the disks.</span></span> <span data-ttu-id="39102-267">Pour plus d’informations, consultez l’article [Attacher un disque de données à une machine virtuelle Windows à l’aide de PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="39102-267">For in-depth information, see the article, [Attach a data disk to a Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="39102-268">L’exemple de code suivant montre comment attacher les disques de données pour des machines virtuelles chiffrées et gérées.</span><span class="sxs-lookup"><span data-stu-id="39102-268">The following sample code shows how to attach the data disks for managed encrypted VMs.</span></span>

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

5. <span data-ttu-id="39102-269">Définissez les paramètres réseau.</span><span class="sxs-lookup"><span data-stu-id="39102-269">Set the Network settings.</span></span>

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. <span data-ttu-id="39102-270">Créez la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="39102-270">Create the virtual machine.</span></span>

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a><span data-ttu-id="39102-271">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="39102-271">Next steps</span></span>
<span data-ttu-id="39102-272">Si vous préférez utiliser PowerShell pour gérer vos ressources Azure, consultez l’article PowerShell [Déployer et gérer une sauvegarde pour Windows Server](backup-client-automation.md).</span><span class="sxs-lookup"><span data-stu-id="39102-272">If you prefer to use PowerShell to engage with your Azure resources, see the PowerShell article, [Deploy and Manage Backup for Windows Server](backup-client-automation.md).</span></span> <span data-ttu-id="39102-273">Si vous gérez des sauvegardes DPM, consultez l’article [Déployer et gérer la sauvegarde pour DPM](backup-dpm-automation.md).</span><span class="sxs-lookup"><span data-stu-id="39102-273">If you manage DPM backups, see the article, [Deploy and Manage Backup for DPM](backup-dpm-automation.md).</span></span> <span data-ttu-id="39102-274">Ces deux articles ont une version concernant les déploiements avec le modèle Resource Manager et le modèle Classic.</span><span class="sxs-lookup"><span data-stu-id="39102-274">Both of these articles have a version for Resource Manager deployments and Classic deployments.</span></span>  
