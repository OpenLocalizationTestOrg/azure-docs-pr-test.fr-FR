---
title: "aaaDeploy et gérer des sauvegardes pour les machines virtuelles déployées par le Gestionnaire de ressources à l’aide de PowerShell | Documents Microsoft"
description: "Utilisez PowerShell toodeploy et gérer des sauvegardes dans Azure pour les machines virtuelles déployées par le Gestionnaire de ressources"
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
ms.openlocfilehash: 486fb3ae1902403fe6bf303df57244b76677ab17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azurermrecoveryservicesbackup-cmdlets-tooback-up-virtual-machines"></a><span data-ttu-id="4db2c-103">Utilisez tooback d’applets de commande AzureRM.RecoveryServices.Backup des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="4db2c-103">Use AzureRM.RecoveryServices.Backup cmdlets tooback up virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4db2c-104">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="4db2c-104">Resource Manager</span></span>](backup-azure-vms-automation.md)
> * [<span data-ttu-id="4db2c-105">Classique</span><span class="sxs-lookup"><span data-stu-id="4db2c-105">Classic</span></span>](backup-azure-vms-classic-automation.md)
>
>

<span data-ttu-id="4db2c-106">Cet article explique comment tooback d’applets de commande de Azure PowerShell toouse haut et récupérer une machine virtuelle (VM) Azure à partir des Services de récupération de coffre.</span><span class="sxs-lookup"><span data-stu-id="4db2c-106">This article shows you how toouse Azure PowerShell cmdlets tooback up and recover an Azure virtual machine (VM) from a Recovery Services vault.</span></span> <span data-ttu-id="4db2c-107">Un coffre Recovery Services est une ressource Azure Resource Manager et les données de tooprotect utilisés et des ressources dans Azure Backup et Azure Site Recovery services.</span><span class="sxs-lookup"><span data-stu-id="4db2c-107">A Recovery Services vault is an Azure Resource Manager resource and is used tooprotect data and assets in both Azure Backup and Azure Site Recovery services.</span></span> <span data-ttu-id="4db2c-108">Vous pouvez utiliser un tooprotect de coffre Recovery Services déployés au Gestionnaire des services Azure de machines virtuelles et les machines virtuelles de déploiement d’Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4db2c-108">You can use a Recovery Services vault tooprotect Azure Service Manager-deployed VMs, and Azure Resource Manager-deployed VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="4db2c-109">Azure dispose de deux modèles de déploiement pour créer et utiliser des ressources : [Azure Resource Manager et Azure Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4db2c-109">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4db2c-110">Cet article est pour une utilisation avec des machines virtuelles créées à l’aide du modèle de gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-110">This article is for use with VMs created using hello Resource Manager model.</span></span>
>
>

<span data-ttu-id="4db2c-111">Cet article vous guide à l’aide de PowerShell tooprotect une machine virtuelle et restaurer des données à partir d’un point de récupération.</span><span class="sxs-lookup"><span data-stu-id="4db2c-111">This article walks you through using PowerShell tooprotect a VM, and restore data from a recovery point.</span></span>

## <a name="concepts"></a><span data-ttu-id="4db2c-112">Concepts</span><span class="sxs-lookup"><span data-stu-id="4db2c-112">Concepts</span></span>
<span data-ttu-id="4db2c-113">Si vous n’êtes pas familiarisé avec hello service Azure Backup, pour une vue d’ensemble du service de hello, extraire [Nouveautés d’Azure Backup ?](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="4db2c-113">If you are not familiar with hello Azure Backup service, for an overview of hello service, check out [What is Azure Backup?](backup-introduction-to-azure-backup.md)</span></span> <span data-ttu-id="4db2c-114">Avant de commencer, assurez-vous que vous couvrent essentials hello sur toowork de conditions préalables nécessaires hello avec Azure Backup et hello limitations de la solution de sauvegarde de machine virtuelle en cours hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-114">Before you start, ensure that you cover hello essentials about hello prerequisites needed toowork with Azure Backup, and hello limitations of hello current VM backup solution.</span></span>

<span data-ttu-id="4db2c-115">toouse PowerShell efficacement, il est nécessaire toounderstand hello hiérarchie d’objets à partir de laquelle toostart.</span><span class="sxs-lookup"><span data-stu-id="4db2c-115">toouse PowerShell effectively, it is necessary toounderstand hello hierarchy of objects and from where toostart.</span></span>

![Hiérarchie des objets dans Recovery Services](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

<span data-ttu-id="4db2c-117">tooview hello référence d’applet de commande PowerShell de AzureRm.RecoveryServices.Backup, consultez hello [Azure Backup - applets de commande de Services de récupération](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) Bonjour bibliothèque Azure.</span><span class="sxs-lookup"><span data-stu-id="4db2c-117">tooview hello AzureRm.RecoveryServices.Backup PowerShell cmdlet reference, see hello [Azure Backup - Recovery Services Cmdlets](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) in hello Azure library.</span></span>

## <a name="setup-and-registration"></a><span data-ttu-id="4db2c-118">Installation et inscription</span><span class="sxs-lookup"><span data-stu-id="4db2c-118">Setup and Registration</span></span>
<span data-ttu-id="4db2c-119">toobegin :</span><span class="sxs-lookup"><span data-stu-id="4db2c-119">toobegin:</span></span>

1. <span data-ttu-id="4db2c-120">[Télécharger la version la plus récente de PowerShell hello](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (hello version minimale requise est : 1.4.0)</span><span class="sxs-lookup"><span data-stu-id="4db2c-120">[Download hello latest version of PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (hello minimum version required is: 1.4.0)</span></span>
2. <span data-ttu-id="4db2c-121">Trouver hello Azure sauvegarde applets de commande PowerShell disponibles en tapant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4db2c-121">Find hello Azure Backup PowerShell cmdlets available by typing hello following command:</span></span>

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


<span data-ttu-id="4db2c-122">Bonjour tâches suivantes peut être automatisée avec PowerShell :</span><span class="sxs-lookup"><span data-stu-id="4db2c-122">hello following tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="4db2c-123">Créer un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="4db2c-123">Create a Recovery Services vault</span></span>
* <span data-ttu-id="4db2c-124">Sauvegarder des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="4db2c-124">Back up Azure VMs</span></span>
* <span data-ttu-id="4db2c-125">Déclencher une tâche de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="4db2c-125">Trigger a backup job</span></span>
* <span data-ttu-id="4db2c-126">Surveiller une tâche de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="4db2c-126">Monitor a backup job</span></span>
* <span data-ttu-id="4db2c-127">Restauration d’une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="4db2c-127">Restore an Azure VM</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="4db2c-128">Créer un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="4db2c-128">Create a recovery services vault</span></span>
<span data-ttu-id="4db2c-129">Hello suit vous guide lors de la création d’un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="4db2c-129">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="4db2c-130">Un coffre Recovery Services diffère d’un coffre de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="4db2c-130">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="4db2c-131">Si vous utilisez Azure Backup pour hello première fois, vous devez utiliser hello  **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)**  fournisseur de Service de récupération Azure hello applet de commande tooregister avec votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="4db2c-131">If you are using Azure Backup for hello first time, you must use hello **[Register-AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="4db2c-132">Hello coffre Recovery Services est une ressource de gestionnaire de ressources, vous devez donc tooplace dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="4db2c-132">hello Recovery Services vault is a Resource Manager resource, so you need tooplace it within a resource group.</span></span> <span data-ttu-id="4db2c-133">Vous pouvez utiliser un groupe de ressources existant ou créer un groupe de ressources avec hello  **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)**  applet de commande.</span><span class="sxs-lookup"><span data-stu-id="4db2c-133">You can use an existing resource group, or create a resource group with hello **[New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)** cmdlet.</span></span> <span data-ttu-id="4db2c-134">Lorsque vous créez un groupe de ressources, spécifiez le nom de hello et un emplacement pour le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-134">When creating a resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="4db2c-135">Hello d’utilisation  **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)**  hello de toocreate d’applet de commande de coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="4db2c-135">Use hello **[New-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)** cmdlet toocreate hello Recovery Services vault.</span></span> <span data-ttu-id="4db2c-136">Veillez à toospecify hello même emplacement pour le coffre hello que celui utilisé pour le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-136">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="4db2c-137">Spécifiez le type hello de toouse de redondance de stockage ; Vous pouvez utiliser [stockage localement redondant (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) ou [stockage redondant de géo-réplication (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="4db2c-137">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="4db2c-138">Hello suivant montre testvault hello BackupStorageRedundancy - option est la valeur tooGeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="4db2c-138">hello following example shows hello -BackupStorageRedundancy option for testvault is set tooGeoRedundant.</span></span>

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > <span data-ttu-id="4db2c-139">Nombreuses applets de commande Azure Backup nécessitent l’objet de coffre Recovery Services hello en tant qu’entrée.</span><span class="sxs-lookup"><span data-stu-id="4db2c-139">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="4db2c-140">Pour cette raison, il est pratique toostore hello Services de récupération de sauvegarde coffre objet dans une variable.</span><span class="sxs-lookup"><span data-stu-id="4db2c-140">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="4db2c-141">Affichage des coffres de hello dans un abonnement</span><span class="sxs-lookup"><span data-stu-id="4db2c-141">View hello vaults in a subscription</span></span>
<span data-ttu-id="4db2c-142">Utilisez  **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)**  liste de hello tooview de tous les coffres dans l’abonnement actif de hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-142">Use **[Get-AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="4db2c-143">Vous pouvez utiliser cette toocheck commande qu’un nouvel archivage a été créé ou toosee hello coffres disponibles dans l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-143">You can use this command toocheck that a new vault was created, or toosee hello available vaults in hello subscription.</span></span>

<span data-ttu-id="4db2c-144">Exécutez la commande hello, Get-AzureRmRecoveryServicesVault, tooview tous les coffres dans l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-144">Run hello command, Get-AzureRmRecoveryServicesVault, tooview all vaults in hello subscription.</span></span> <span data-ttu-id="4db2c-145">Hello suivant montre les informations de hello affichées pour chaque archivage.</span><span class="sxs-lookup"><span data-stu-id="4db2c-145">hello following example shows hello information displayed for each vault.</span></span>

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


## <a name="back-up-azure-vms"></a><span data-ttu-id="4db2c-146">Sauvegarder des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="4db2c-146">Back up Azure VMs</span></span>
<span data-ttu-id="4db2c-147">Utilisez un tooprotect de coffre Recovery Services vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="4db2c-147">Use a Recovery Services vault tooprotect your virtual machines.</span></span> <span data-ttu-id="4db2c-148">Avant d’appliquer une protection hello, définir le contexte du coffre hello (type hello des données protégées dans le coffre hello) et vérifiez la stratégie de protection hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-148">Before you apply hello protection, set hello vault context (hello type of data protected in hello vault), and verify hello protection policy.</span></span> <span data-ttu-id="4db2c-149">stratégie de protection Hello est planification hello lors de l’exécution de travaux de sauvegarde hello et la durée de conservation de chaque instantané de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="4db2c-149">hello protection policy is hello schedule when hello backup jobs run, and how long each backup snapshot is retained.</span></span>

### <a name="set-vault-context"></a><span data-ttu-id="4db2c-150">Définir le contexte du coffre</span><span class="sxs-lookup"><span data-stu-id="4db2c-150">Set vault context</span></span>
<span data-ttu-id="4db2c-151">Avant d’activer la protection sur un ordinateur virtuel, utilisez  **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  contexte de coffre tooset hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-151">Before enabling protection on a VM, use **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** tooset hello vault context.</span></span> <span data-ttu-id="4db2c-152">Une fois que le contexte de coffre hello est définie, elle s’applique tooall applets de commande suivantes.</span><span class="sxs-lookup"><span data-stu-id="4db2c-152">Once hello vault context is set, it applies tooall subsequent cmdlets.</span></span> <span data-ttu-id="4db2c-153">exemple Hello définit contexte de coffre hello pour le coffre hello, *testvault*.</span><span class="sxs-lookup"><span data-stu-id="4db2c-153">hello following example sets hello vault context for hello vault, *testvault*.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a><span data-ttu-id="4db2c-154">Création d’une stratégie de protection</span><span class="sxs-lookup"><span data-stu-id="4db2c-154">Create a protection policy</span></span>
<span data-ttu-id="4db2c-155">Quand vous créez un coffre Recovery Services, il est fourni avec des stratégies de protection et de conservation par défaut.</span><span class="sxs-lookup"><span data-stu-id="4db2c-155">When you create a Recovery Services vault, it comes with default protection and retention policies.</span></span> <span data-ttu-id="4db2c-156">stratégie de protection par défaut Hello déclenche une opération de sauvegarde chaque jour à une heure spécifiée.</span><span class="sxs-lookup"><span data-stu-id="4db2c-156">hello default protection policy triggers a backup job each day at a specified time.</span></span> <span data-ttu-id="4db2c-157">stratégie de rétention par défaut Hello conserve le point de récupération quotidien hello pendant 30 jours.</span><span class="sxs-lookup"><span data-stu-id="4db2c-157">hello default retention policy retains hello daily recovery point for 30 days.</span></span> <span data-ttu-id="4db2c-158">Vous pouvez utiliser la valeur par défaut hello stratégie tooquickly protéger votre machine virtuelle et la stratégie hello ultérieurement avec les détails de l’autres.</span><span class="sxs-lookup"><span data-stu-id="4db2c-158">You can use hello default policy tooquickly protect your VM and edit hello policy later with different details.</span></span>

<span data-ttu-id="4db2c-159">Utilisez  **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)**  tooview des stratégies de protection hello dans le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-159">Use **[Get-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)** tooview hello protection policies in hello vault.</span></span> <span data-ttu-id="4db2c-160">Vous pouvez utiliser cette applet de commande tooget une stratégie spécifique, ou les stratégies de hello tooview associées à un type de charge de travail.</span><span class="sxs-lookup"><span data-stu-id="4db2c-160">You can use this cmdlet tooget a specific policy, or tooview hello policies associated with a workload type.</span></span> <span data-ttu-id="4db2c-161">Bonjour à l’exemple suivant obtient les stratégies pour le type de charge de travail, AzureVM.</span><span class="sxs-lookup"><span data-stu-id="4db2c-161">hello following example gets policies for workload type, AzureVM.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> <span data-ttu-id="4db2c-162">fuseau horaire de Hello du champ de BackupTime hello dans PowerShell est UTC.</span><span class="sxs-lookup"><span data-stu-id="4db2c-162">hello timezone of hello BackupTime field in PowerShell is UTC.</span></span> <span data-ttu-id="4db2c-163">Toutefois, lorsque les temps de sauvegarde hello sont affiché dans hello portail Azure, les temps de hello sont fuseau horaire local de tooyour ajustée.</span><span class="sxs-lookup"><span data-stu-id="4db2c-163">However, when hello backup time is shown in hello Azure portal, hello time is adjusted tooyour local timezone.</span></span>
>
>

<span data-ttu-id="4db2c-164">Une stratégie de protection de la sauvegarde est associée à au moins une stratégie de rétention.</span><span class="sxs-lookup"><span data-stu-id="4db2c-164">A backup protection policy is associated with at least one retention policy.</span></span> <span data-ttu-id="4db2c-165">La stratégie de conservation définit la durée de conservation d’un point de restauration avant sa suppression.</span><span class="sxs-lookup"><span data-stu-id="4db2c-165">Retention policy defines how long a recovery point is kept before it is deleted.</span></span> <span data-ttu-id="4db2c-166">Utilisez  **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)**  stratégie de rétention par défaut tooview hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-166">Use **[Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)** tooview hello default retention policy.</span></span>  <span data-ttu-id="4db2c-167">De même, vous pouvez utiliser  **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)**  stratégie de planification par défaut tooobtain hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-167">Similarly you can use **[Get-AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)** tooobtain hello default schedule policy.</span></span> <span data-ttu-id="4db2c-168">Hello  **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  applet de commande crée un objet PowerShell qui contient des informations de stratégie de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="4db2c-168">hello **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet creates a PowerShell object that holds backup policy information.</span></span> <span data-ttu-id="4db2c-169">Hello objets de stratégie de planification et de rétention sont utilisés comme entrées toohello  **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  applet de commande.</span><span class="sxs-lookup"><span data-stu-id="4db2c-169">hello schedule and retention policy objects are used as inputs toohello **[New-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)** cmdlet.</span></span> <span data-ttu-id="4db2c-170">Hello exemple suivant stocke hello planification hello politique de rétention et de variables.</span><span class="sxs-lookup"><span data-stu-id="4db2c-170">hello following example stores hello schedule policy and hello retention policy in variables.</span></span> <span data-ttu-id="4db2c-171">exemple de Hello utilise ces variables de paramètres de hello toodefine lors de la création d’une stratégie de protection, *NewPolicy*.</span><span class="sxs-lookup"><span data-stu-id="4db2c-171">hello example uses those variables toodefine hello parameters when creating a protection policy, *NewPolicy*.</span></span>

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a><span data-ttu-id="4db2c-172">Activer la protection</span><span class="sxs-lookup"><span data-stu-id="4db2c-172">Enable protection</span></span>
<span data-ttu-id="4db2c-173">Une fois que vous avez défini la stratégie de protection des sauvegardes hello, vous devez toujours activer stratégie hello pour un élément.</span><span class="sxs-lookup"><span data-stu-id="4db2c-173">Once you have defined hello backup protection policy, you still must enable hello policy for an item.</span></span> <span data-ttu-id="4db2c-174">Utilisez  **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)**  tooenable protection.</span><span class="sxs-lookup"><span data-stu-id="4db2c-174">Use **[Enable-AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)** tooenable protection.</span></span> <span data-ttu-id="4db2c-175">Activation de la protection nécessite deux objets - élément de hello et stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-175">Enabling protection requires two objects - hello item and hello policy.</span></span> <span data-ttu-id="4db2c-176">Une fois que la stratégie de hello a été associé au coffre de hello, flux de travail sauvegarde hello est déclenchée au moment de hello définie dans la planification de la stratégie hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-176">Once hello policy has been associated with hello vault, hello backup workflow is triggered at hello time defined in hello policy schedule.</span></span>

<span data-ttu-id="4db2c-177">Hello suivant l’exemple permet de protection pour l’élément hello, V2VM, à l’aide de la stratégie de hello, NewPolicy.</span><span class="sxs-lookup"><span data-stu-id="4db2c-177">hello following example enables protection for hello item, V2VM, using hello policy, NewPolicy.</span></span> <span data-ttu-id="4db2c-178">protection de hello tooenable sur des machines virtuelles Resource Manager non chiffré</span><span class="sxs-lookup"><span data-stu-id="4db2c-178">tooenable hello protection on non-encrypted Resource Manager VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="4db2c-179">protection de hello tooenable sur chiffré (chiffrées à l’aide de BEK et KEK) de machines virtuelles, vous devez clés tooread autorisation du service Azure Backup toogive hello et les secrets à partir du coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="4db2c-179">tooenable hello protection on encrypted VMs (encrypted using BEK and KEK), you need toogive hello Azure Backup service permission tooread keys and secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

<span data-ttu-id="4db2c-180">protection de hello tooenable sur chiffré machines virtuelles (chiffrés à l’aide de BEK uniquement), vous devez toogive hello Azure Backup service autorisation tooread des secrets à partir du coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="4db2c-180">tooenable hello protection on encrypted VMs (encrypted using BEK only), you need toogive hello Azure Backup service permission tooread secrets from key vault.</span></span>

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> <span data-ttu-id="4db2c-181">Si vous utilisez un cloud d’Azure Government hello, utilisez hello valeur ff281ffe-705c-4f53-9f37-a40e6f2c68f3 pour le paramètre hello **- ServicePrincipalName** dans [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) applet de commande .</span><span class="sxs-lookup"><span data-stu-id="4db2c-181">If you are using hello Azure Government cloud, then use hello value ff281ffe-705c-4f53-9f37-a40e6f2c68f3 for hello parameter **-ServicePrincipalName** in [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.</span></span>
>
>

<span data-ttu-id="4db2c-182">Pour les machines virtuelles Classic</span><span class="sxs-lookup"><span data-stu-id="4db2c-182">For classic VMs</span></span>

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a><span data-ttu-id="4db2c-183">Modifier une stratégie de protection</span><span class="sxs-lookup"><span data-stu-id="4db2c-183">Modify a protection policy</span></span>
<span data-ttu-id="4db2c-184">stratégie de protection toomodify hello, utilisez [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) toomodify hello SchedulePolicy ou RetentionPolicy objets.</span><span class="sxs-lookup"><span data-stu-id="4db2c-184">toomodify hello protection policy, use [Set-AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) toomodify hello SchedulePolicy or RetentionPolicy objects.</span></span>

<span data-ttu-id="4db2c-185">Hello exemple suivant change hello recovery point rétention too365 jours.</span><span class="sxs-lookup"><span data-stu-id="4db2c-185">hello following example changes hello recovery point retention too365 days.</span></span>

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a><span data-ttu-id="4db2c-186">Déclencher une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="4db2c-186">Trigger a backup</span></span>
<span data-ttu-id="4db2c-187">Vous pouvez utiliser  **[sauvegarde-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)**  tootrigger un travail de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="4db2c-187">You can use **[Backup-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)** tootrigger a backup job.</span></span> <span data-ttu-id="4db2c-188">S’il s’agit de sauvegarde initiale de hello, il est une sauvegarde complète.</span><span class="sxs-lookup"><span data-stu-id="4db2c-188">If it is hello initial backup, it is a full backup.</span></span> <span data-ttu-id="4db2c-189">Les sauvegardes suivantes prennent une copie incrémentielle.</span><span class="sxs-lookup"><span data-stu-id="4db2c-189">Subsequent backups take an incremental copy.</span></span> <span data-ttu-id="4db2c-190">Être vraiment toouse  **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  tooset contexte de coffre hello avant de déclencher l’opération de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-190">Be sure toouse **[Set-AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)** tooset hello vault context before triggering hello backup job.</span></span> <span data-ttu-id="4db2c-191">Bonjour à l’exemple suivant suppose coffre contexte a été défini.</span><span class="sxs-lookup"><span data-stu-id="4db2c-191">hello following example assumes vault context was set.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> <span data-ttu-id="4db2c-192">fuseau horaire de Hello de champs de StartTime et EndTime hello dans PowerShell est UTC.</span><span class="sxs-lookup"><span data-stu-id="4db2c-192">hello timezone of hello StartTime and EndTime fields in PowerShell is UTC.</span></span> <span data-ttu-id="4db2c-193">Toutefois, lorsque l’heure de hello est affichée dans hello portail Azure, les temps de hello sont fuseau horaire local de tooyour ajustée.</span><span class="sxs-lookup"><span data-stu-id="4db2c-193">However, when hello time is shown in hello Azure portal, hello time is adjusted tooyour local timezone.</span></span>
>
>

## <a name="monitoring-a-backup-job"></a><span data-ttu-id="4db2c-194">Surveillance d’une tâche de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="4db2c-194">Monitoring a backup job</span></span>
<span data-ttu-id="4db2c-195">Vous pouvez surveiller les opérations longues, telles que les travaux de sauvegarde, sans utiliser de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4db2c-195">You can monitor long-running operations, such as backup jobs, without using hello Azure portal.</span></span> <span data-ttu-id="4db2c-196">état de hello tooget d’une tâche en cours d’exécution, utilisez hello  **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)**  applet de commande.</span><span class="sxs-lookup"><span data-stu-id="4db2c-196">tooget hello status of an in-progress job, use hello **[Get-AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="4db2c-197">Cette applet de commande Obtient les travaux de sauvegarde hello pour un archivage spécifique, et ce coffre est spécifié dans le contexte de coffre hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-197">This cmdlet gets hello backup jobs for a specific vault, and that vault is specified in hello vault context.</span></span> <span data-ttu-id="4db2c-198">Bonjour exemple suivant obtient l’état de hello d’un travail en cours d’exécution sous forme de tableau et stocke l’état de hello dans la variable de hello $joblist.</span><span class="sxs-lookup"><span data-stu-id="4db2c-198">hello following example gets hello status of an in-progress job as an array, and stores hello status in hello $joblist variable.</span></span>

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="4db2c-199">Au lieu de l’interrogation de ces travaux pour la saisie semi-automatique, qui est un code superflu supplémentaire - utilisez hello  **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  applet de commande.</span><span class="sxs-lookup"><span data-stu-id="4db2c-199">Instead of polling these jobs for completion - which is unnecessary additional code - use hello **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet.</span></span> <span data-ttu-id="4db2c-200">Cette applet de commande suspend l’exécution de hello qu’hello tâche se termine ou hello spécifié la valeur de délai d’attente est atteinte.</span><span class="sxs-lookup"><span data-stu-id="4db2c-200">This cmdlet pauses hello execution until either hello job completes or hello specified timeout value is reached.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a><span data-ttu-id="4db2c-201">Restauration d’une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="4db2c-201">Restore an Azure VM</span></span>
<span data-ttu-id="4db2c-202">Il existe une différence fondamentale entre hello restauration d’une machine virtuelle à l’aide de hello portail Azure et la restauration d’une machine virtuelle à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4db2c-202">There is a key difference between hello restoring a VM using hello Azure portal and restoring a VM using PowerShell.</span></span> <span data-ttu-id="4db2c-203">Avec PowerShell, hello restauration est terminée une fois que les disques hello et les informations de configuration de point de récupération hello sont créés.</span><span class="sxs-lookup"><span data-stu-id="4db2c-203">With PowerShell, hello restore operation is complete once hello disks and configuration information from hello recovery point are created.</span></span>

> [!NOTE]
> <span data-ttu-id="4db2c-204">opération de restauration Hello ne crée pas d’un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="4db2c-204">hello restore operation does not create a virtual machine.</span></span>
>
>

<span data-ttu-id="4db2c-205">toocreate un ordinateur virtuel à partir du disque, consultez la section hello [hello créer machine virtuelle à partir de disques stockées](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span><span class="sxs-lookup"><span data-stu-id="4db2c-205">toocreate a virtual machine from disk, see hello section, [Create hello VM from stored disks](backup-azure-vms-automation.md#create-a-vm-from-stored-disks).</span></span> <span data-ttu-id="4db2c-206">étapes de base de Hello toorestore une machine virtuelle Azure sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="4db2c-206">hello basic steps toorestore an Azure VM are:</span></span>

* <span data-ttu-id="4db2c-207">Sélectionnez hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="4db2c-207">Select hello VM</span></span>
* <span data-ttu-id="4db2c-208">Choisir un point de récupération</span><span class="sxs-lookup"><span data-stu-id="4db2c-208">Choose a recovery point</span></span>
* <span data-ttu-id="4db2c-209">Restaurer des disques de hello</span><span class="sxs-lookup"><span data-stu-id="4db2c-209">Restore hello disks</span></span>
* <span data-ttu-id="4db2c-210">Créer hello machine virtuelle à partir de disques stockées</span><span class="sxs-lookup"><span data-stu-id="4db2c-210">Create hello VM from stored disks</span></span>

<span data-ttu-id="4db2c-211">Hello graphique suivant illustre hello objet hiérarchie hello RecoveryServicesVault toohello BackupRecoveryPoint vers le bas.</span><span class="sxs-lookup"><span data-stu-id="4db2c-211">hello following graphic shows hello object hierarchy from hello RecoveryServicesVault down toohello BackupRecoveryPoint.</span></span>

![Hiérarchie d’objets Recovery Services montrant BackupContainer](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

<span data-ttu-id="4db2c-213">toorestore les données de sauvegarde, identifier l’élément de sauvegarde hello hello point de récupération et qui conserve les données de point-à-temps hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-213">toorestore backup data, identify hello backed-up item and hello recovery point that holds hello point-in-time data.</span></span> <span data-ttu-id="4db2c-214">Hello d’utilisation  **[restauration-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  données toorestore applet de commande hello coffre toohello du compte client.</span><span class="sxs-lookup"><span data-stu-id="4db2c-214">Use hello **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet toorestore data from hello vault toohello customer's account.</span></span>

### <a name="select-hello-vm"></a><span data-ttu-id="4db2c-215">Sélectionnez hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="4db2c-215">Select hello VM</span></span>
<span data-ttu-id="4db2c-216">tooget hello PowerShell objet qui identifie hello droite sauvegarder élément démarrer à partir du conteneur hello dans le coffre hello et dont la hiérarchie d’objets hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-216">tooget hello PowerShell object that identifies hello right backup item, start from hello container in hello vault, and work your way down hello object hierarchy.</span></span> <span data-ttu-id="4db2c-217">conteneur hello tooselect représentant hello machine virtuelle, utilisez hello  **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)**  applet de commande et redirigez cette toohello  **[ Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)**  applet de commande.</span><span class="sxs-lookup"><span data-stu-id="4db2c-217">tooselect hello container that represents hello VM, use hello **[Get-AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)** cmdlet and pipe that toohello **[Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)** cmdlet.</span></span>

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a><span data-ttu-id="4db2c-218">Choisir un point de récupération</span><span class="sxs-lookup"><span data-stu-id="4db2c-218">Choose a recovery point</span></span>
<span data-ttu-id="4db2c-219">Hello d’utilisation  **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)**  toolist d’applet de commande points de récupération de tous les pour sauvegarder l’élément hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-219">Use hello **[Get-AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)** cmdlet toolist all recovery points for hello backup item.</span></span> <span data-ttu-id="4db2c-220">Choisissez ensuite toorestore de point de récupération hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-220">Then choose hello recovery point toorestore.</span></span> <span data-ttu-id="4db2c-221">Si vous ne savez pas quel toouse de point de récupération, il est une bonne approche en matière toochoose hello plus récente RecoveryPointType = point AppConsistent dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-221">If you are unsure which recovery point toouse, it is a good practice toochoose hello most recent RecoveryPointType = AppConsistent point in hello list.</span></span>

<span data-ttu-id="4db2c-222">Bonjour le script suivant, hello variable, **$rp**, est un tableau de points de récupération pour hello sélectionné sauvegarder l’élément, à partir de hello sept derniers jours.</span><span class="sxs-lookup"><span data-stu-id="4db2c-222">In hello following script, hello variable, **$rp**, is an array of recovery points for hello selected backup item, from hello past seven days.</span></span> <span data-ttu-id="4db2c-223">tableau de Hello est trié dans l’ordre inverse de temps avec le dernier point de récupération hello à l’index 0.</span><span class="sxs-lookup"><span data-stu-id="4db2c-223">hello array is sorted in reverse order of time with hello latest recovery point at index 0.</span></span> <span data-ttu-id="4db2c-224">Utiliser le tableau PowerShell standard, l’indexation de point de récupération toopick hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-224">Use standard PowerShell array indexing toopick hello recovery point.</span></span> <span data-ttu-id="4db2c-225">Dans l’exemple de hello, $rp [0] sélectionne le dernier point de récupération hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-225">In hello example, $rp[0] selects hello latest recovery point.</span></span>

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



### <a name="restore-hello-disks"></a><span data-ttu-id="4db2c-226">Restaurer des disques de hello</span><span class="sxs-lookup"><span data-stu-id="4db2c-226">Restore hello disks</span></span>
<span data-ttu-id="4db2c-227">Hello d’utilisation  **[restauration-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  toorestore de l’applet de commande les données d’un élément de sauvegarde et configuration tooa point de récupération.</span><span class="sxs-lookup"><span data-stu-id="4db2c-227">Use hello **[Restore-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)** cmdlet toorestore a backup item's data and configuration tooa recovery point.</span></span> <span data-ttu-id="4db2c-228">Une fois que vous avez identifié un point de récupération, utilisez-le comme valeur de hello pour hello **- RecoveryPoint** paramètre.</span><span class="sxs-lookup"><span data-stu-id="4db2c-228">Once you have identified a recovery point, use it as hello value for hello **-RecoveryPoint** parameter.</span></span> <span data-ttu-id="4db2c-229">Hello précédent exemple de code, **$rp [0]** a été toouse de point de récupération hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-229">In hello previous sample code, **$rp[0]** was hello recovery point toouse.</span></span> <span data-ttu-id="4db2c-230">Bonjour suivant l’exemple de code, **$rp [0]** est hello toouse de point de récupération pour la restauration du disque de hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-230">In hello following sample code, **$rp[0]** is hello recovery point toouse for restoring hello disk.</span></span>

<span data-ttu-id="4db2c-231">les disques toorestore hello et les informations de configuration :</span><span class="sxs-lookup"><span data-stu-id="4db2c-231">toorestore hello disks and configuration information:</span></span>

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

<span data-ttu-id="4db2c-232">Hello d’utilisation  **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  toowait d’applet de commande pour toocomplete de travail de restauration hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-232">Use hello **[Wait-AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)** cmdlet toowait for hello Restore job toocomplete.</span></span>

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

<span data-ttu-id="4db2c-233">Une fois le travail de restauration hello est terminé, utilisez hello  **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)**  détails hello tooget Hello l’opération de restauration.</span><span class="sxs-lookup"><span data-stu-id="4db2c-233">Once hello Restore job has completed, use hello **[Get-AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)** cmdlet tooget hello details of hello restore operation.</span></span> <span data-ttu-id="4db2c-234">Hello JobDetails propriété a toorebuild nécessaires hello VM de hello plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="4db2c-234">hello JobDetails property has hello information needed toorebuild hello VM.</span></span>

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

<span data-ttu-id="4db2c-235">Une fois que vous restaurez les disques hello, accédez hello toohello suivant section toocreate machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4db2c-235">Once you restore hello disks, go toohello next section toocreate hello VM.</span></span>

## <a name="create-a-vm-from-restored-disks"></a><span data-ttu-id="4db2c-236">Créer une machine virtuelle à partir de disques restaurés</span><span class="sxs-lookup"><span data-stu-id="4db2c-236">Create a VM from restored disks</span></span>
<span data-ttu-id="4db2c-237">Après avoir restauré les disques hello, utilisez ces étapes toocreate et configurer l’ordinateur virtuel de hello à partir du disque.</span><span class="sxs-lookup"><span data-stu-id="4db2c-237">After you have restored hello disks, use these steps toocreate and configure hello virtual machine from disk.</span></span>

> [!NOTE]
> <span data-ttu-id="4db2c-238">toocreate chiffré des machines virtuelles à partir de disques restaurés, votre rôle Azure doit avoir l’action de hello autorisation tooperform, **Microsoft.KeyVault/vaults/deploy/action**.</span><span class="sxs-lookup"><span data-stu-id="4db2c-238">toocreate encrypted VMs from restored disks, your Azure role must have permission tooperform hello action, **Microsoft.KeyVault/vaults/deploy/action**.</span></span> <span data-ttu-id="4db2c-239">Si votre rôle ne dispose pas de cette autorisation, créez un rôle personnalisé avec cette action.</span><span class="sxs-lookup"><span data-stu-id="4db2c-239">If your role does not have this permission, create a custom role with this action.</span></span> <span data-ttu-id="4db2c-240">Pour plus d’informations, consultez [Rôles personnalisés dans le contrôle d’accès en fonction du rôle (RBAC) Azure](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="4db2c-240">For more information, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>
>
>

1. <span data-ttu-id="4db2c-241">Hello de requête restauré les propriétés du disque pour les détails de la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-241">Query hello restored disk properties for hello job details.</span></span>

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. <span data-ttu-id="4db2c-242">Définir le contexte du stockage Azure hello et restaurez le fichier de configuration JSON hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-242">Set hello Azure storage context and restore hello JSON configuration file.</span></span>

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. <span data-ttu-id="4db2c-243">Utilisez configuration d’ordinateur virtuel hello JSON configuration fichier toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-243">Use hello JSON configuration file toocreate hello VM configuration.</span></span>

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. <span data-ttu-id="4db2c-244">Attachez le disque du système d’exploitation hello et des disques de données.</span><span class="sxs-lookup"><span data-stu-id="4db2c-244">Attach hello OS disk and data disks.</span></span> <span data-ttu-id="4db2c-245">Selon la configuration de hello de vos machines virtuelles, cliquez sur hello lien pertinent tooview applets de commande respectifs :</span><span class="sxs-lookup"><span data-stu-id="4db2c-245">Depending on hello configuration of your VMs, click on hello relevant link tooview respective cmdlets:</span></span> 
    - [<span data-ttu-id="4db2c-246">Machines virtuelles non gérés, non chiffré</span><span class="sxs-lookup"><span data-stu-id="4db2c-246">Non-managed, non-encrypted VMs</span></span>](#non-managed-non-encrypted-vms)
    - [<span data-ttu-id="4db2c-247">Machines virtuelles non gérés, chiffrés (BEK uniquement)</span><span class="sxs-lookup"><span data-stu-id="4db2c-247">Non-managed, encrypted VMs (BEK only)</span></span>](#non-managed-encrypted-vms-bek-only)
    - [<span data-ttu-id="4db2c-248">Machines virtuelles non gérés, chiffrés (BEK et KEK)</span><span class="sxs-lookup"><span data-stu-id="4db2c-248">Non-managed, encrypted VMs (BEK and KEK)</span></span>](#non-managed-encrypted-vms-bek-and-kek)
    - [<span data-ttu-id="4db2c-249">Ordinateurs virtuels gérés, non chiffré</span><span class="sxs-lookup"><span data-stu-id="4db2c-249">Managed, non-encrypted VMs</span></span>](#managed-non-encrypted-vms)
    - [<span data-ttu-id="4db2c-250">Ordinateurs virtuels gérés, chiffrés (BEK et KEK)</span><span class="sxs-lookup"><span data-stu-id="4db2c-250">Managed, encrypted VMs (BEK and KEK)</span></span>](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a><span data-ttu-id="4db2c-251">Machines virtuelles non gérées et non chiffrées</span><span class="sxs-lookup"><span data-stu-id="4db2c-251">Non-managed, non-encrypted VMs</span></span>

    <span data-ttu-id="4db2c-252">Utilisez hello suivant l’exemple pour les ordinateurs virtuels non géré, non chiffré.</span><span class="sxs-lookup"><span data-stu-id="4db2c-252">Use hello following sample for non-managed, non-encrypted VMs.</span></span>

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a><span data-ttu-id="4db2c-253">Machines virtuelles non managées et chiffrées (BEK uniquement)</span><span class="sxs-lookup"><span data-stu-id="4db2c-253">Non-managed, encrypted VMs (BEK only)</span></span>

    <span data-ttu-id="4db2c-254">Pour chiffrés, non géré des ordinateurs virtuels (chiffrés à l’aide de BEK uniquement), vous avez besoin de coffre de clés secrètes toohello hello toorestore avant que vous pouvez attacher des disques.</span><span class="sxs-lookup"><span data-stu-id="4db2c-254">For non-managed, encrypted VMs (encrypted using BEK only), you need toorestore hello secret toohello key vault before you can attach disks.</span></span> <span data-ttu-id="4db2c-255">Pour plus d’informations, consultez l’article hello, [restaurer un ordinateur virtuel chiffré à partir d’un point de récupération Azure Backup](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="4db2c-255">For more information, please see hello article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="4db2c-256">Hello suivant l’exemple montre le mode de chiffrement de tooattach du système d’exploitation et des disques de données pour les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="4db2c-256">hello following sample shows how tooattach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="4db2c-257">Machines virtuelles non managées et chiffrées (BEK et KEK)</span><span class="sxs-lookup"><span data-stu-id="4db2c-257">Non-managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="4db2c-258">Non gérés, chiffrés machines virtuelles (chiffrées à l’aide de BEK et KEK), vous devez clé de hello toorestore et coffre de clés secrètes toohello avant que vous pouvez attacher des disques.</span><span class="sxs-lookup"><span data-stu-id="4db2c-258">For non-managed, encrypted VMs (encrypted using BEK and KEK), you need toorestore hello key and secret toohello key vault before you can attach disks.</span></span> <span data-ttu-id="4db2c-259">Pour plus d’informations, consultez l’article hello, [restaurer un ordinateur virtuel chiffré à partir d’un point de récupération Azure Backup](backup-azure-restore-key-secret.md).</span><span class="sxs-lookup"><span data-stu-id="4db2c-259">For more information, please see hello article, [Restore an encrypted virtual machine from an Azure Backup recovery point](backup-azure-restore-key-secret.md).</span></span> <span data-ttu-id="4db2c-260">Hello suivant l’exemple montre le mode de chiffrement de tooattach du système d’exploitation et des disques de données pour les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="4db2c-260">hello following sample shows how tooattach OS and data disks for encrypted VMs.</span></span>

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

    #### <a name="managed-non-encrypted-vms"></a><span data-ttu-id="4db2c-261">Machines virtuelles gérées et non chiffrées</span><span class="sxs-lookup"><span data-stu-id="4db2c-261">Managed, non-encrypted VMs</span></span>

    <span data-ttu-id="4db2c-262">Non chiffrées machines virtuelles gérées, vous allez peut-être disques toocreate géré depuis le stockage blob et puis attachez les disques hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-262">For managed non-encrypted VMs, you'll need toocreate managed disks from blob storage, and then attach hello disks.</span></span> <span data-ttu-id="4db2c-263">Pour plus d’informations, consultez l’article hello, [attacher un tooa de disque de données machine virtuelle Windows à l’aide de PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4db2c-263">For in-depth information, see hello article, [Attach a data disk tooa Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="4db2c-264">Hello suivant l’exemple de code montre comment tooattach hello des disques de données pour les machines virtuelles gérées non chiffré.</span><span class="sxs-lookup"><span data-stu-id="4db2c-264">hello following sample code shows how tooattach hello data disks for managed non-encrypted VMs.</span></span>

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

    #### <a name="managed-encrypted-vms-bek-and-kek"></a><span data-ttu-id="4db2c-265">Machines virtuelles managées et chiffrées (BEK et KEK)</span><span class="sxs-lookup"><span data-stu-id="4db2c-265">Managed, encrypted VMs (BEK and KEK)</span></span>

    <span data-ttu-id="4db2c-266">Chiffrées machines virtuelles gérées (chiffrées à l’aide de BEK et KEK), vous allez peut-être disques toocreate géré depuis le stockage blob et puis attachez les disques hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-266">For managed encrypted VMs (encrypted using BEK and KEK), you'll need toocreate managed disks from blob storage, and then attach hello disks.</span></span> <span data-ttu-id="4db2c-267">Pour plus d’informations, consultez l’article hello, [attacher un tooa de disque de données machine virtuelle Windows à l’aide de PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4db2c-267">For in-depth information, see hello article, [Attach a data disk tooa Windows VM using PowerShell](../virtual-machines/windows/attach-disk-ps.md).</span></span> <span data-ttu-id="4db2c-268">Hello exemple de code suivant montre comment tooattach hello des disques de données pour les machines virtuelles chiffrées gérées.</span><span class="sxs-lookup"><span data-stu-id="4db2c-268">hello following sample code shows how tooattach hello data disks for managed encrypted VMs.</span></span>

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

5. <span data-ttu-id="4db2c-269">Définir des paramètres de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-269">Set hello Network settings.</span></span>

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. <span data-ttu-id="4db2c-270">Créer un ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="4db2c-270">Create hello virtual machine.</span></span>

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a><span data-ttu-id="4db2c-271">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4db2c-271">Next steps</span></span>
<span data-ttu-id="4db2c-272">Si vous préférez toouse PowerShell tooengage avec vos ressources Azure, consultez l’article de PowerShell hello, [déployer et gérer Backup pour Windows Server](backup-client-automation.md).</span><span class="sxs-lookup"><span data-stu-id="4db2c-272">If you prefer toouse PowerShell tooengage with your Azure resources, see hello PowerShell article, [Deploy and Manage Backup for Windows Server](backup-client-automation.md).</span></span> <span data-ttu-id="4db2c-273">Si vous gérez les sauvegardes DPM, consultez l’article hello, [déployer et gérer la sauvegarde de DPM](backup-dpm-automation.md).</span><span class="sxs-lookup"><span data-stu-id="4db2c-273">If you manage DPM backups, see hello article, [Deploy and Manage Backup for DPM](backup-dpm-automation.md).</span></span> <span data-ttu-id="4db2c-274">Ces deux articles ont une version concernant les déploiements avec le modèle Resource Manager et le modèle Classic.</span><span class="sxs-lookup"><span data-stu-id="4db2c-274">Both of these articles have a version for Resource Manager deployments and Classic deployments.</span></span>  
