---
title: "machines virtuelles à l’aide d’Azure Backup de chiffrement de clé de coffre de clés aaaRestore et secret pour | Documents Microsoft"
description: "Découvrez comment le coffre de clé toorestore secret dans Azure Backup à l’aide de PowerShell et la clé"
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 45214083-d5fc-4eb3-a367-0239dc59e0f6
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 659b2f647493ffcc9494caee111c8bd584ef9c7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a><span data-ttu-id="f9e40-103">Restaurer la clé et le secret du Key Vault pour les machines virtuelles chiffrées à l’aide d’Azure Backup</span><span class="sxs-lookup"><span data-stu-id="f9e40-103">Restore Key Vault key and secret for encrypted VMs using Azure Backup</span></span>
<span data-ttu-id="f9e40-104">Cet article traite d’à l’aide de restauration tooperform de sauvegarde de machine virtuelle Azure de chiffrée des machines virtuelles Azure, si votre clé et la clé secrète n’existent pas dans le coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="f9e40-104">This article talks about using Azure VM Backup tooperform restore of encrypted Azure VMs, if your key and secret do not exist in hello key vault.</span></span> <span data-ttu-id="f9e40-105">Ces étapes peuvent également servir toomaintain une copie distincte de clé (clé de cryptage) et secret (clé de chiffrement BitLocker) pour hello restaurer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f9e40-105">These steps can also be used if you want toomaintain a separate copy of key (Key Encryption Key) and secret (BitLocker Encryption Key) for hello restored VM.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9e40-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f9e40-106">Prerequisites</span></span>
* <span data-ttu-id="f9e40-107">**Sauvegarder les machines virtuelles chiffrées** : les machines virtuelles Azure chiffrées ont été sauvegardées à l’aide d’Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="f9e40-107">**Backup encrypted VMs** - Encrypted Azure VMs have been backed up using Azure Backup.</span></span> <span data-ttu-id="f9e40-108">Consultez l’article de hello [gérer la sauvegarde et restauration de machines virtuelles de Azure à l’aide de PowerShell](backup-azure-vms-automation.md) pour plus d’informations sur le mode de chiffrement de machines virtuelles Azure toobackup.</span><span class="sxs-lookup"><span data-stu-id="f9e40-108">Refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md) for details about how toobackup encrypted Azure VMs.</span></span>
* <span data-ttu-id="f9e40-109">**Configurer Azure Key Vault** : Assurez-vous que le coffre de clés toowhich clés et toobe besoin de clés secrètes restauré est déjà présent.</span><span class="sxs-lookup"><span data-stu-id="f9e40-109">**Configure Azure Key Vault** – Ensure that key vault toowhich keys and secrets need toobe restored is already present.</span></span> <span data-ttu-id="f9e40-110">Consultez l’article de hello [prise en main d’Azure Key Vault](../key-vault/key-vault-get-started.md) pour plus d’informations sur la gestion de coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="f9e40-110">Refer hello article [Get Started with Azure Key Vault](../key-vault/key-vault-get-started.md) for details about key vault management.</span></span>
* <span data-ttu-id="f9e40-111">**Restauration du disque** : vérifiez que vous avez déclenché des travaux de restauration pour restaurer les disques d’une machine virtuelle chiffrée à l’aide des [étapes PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="f9e40-111">**Restore disk** - Ensure that you have triggered restore job for restoring disks for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm).</span></span> <span data-ttu-id="f9e40-112">Il s’agit, car ce travail génère un fichier JSON dans votre compte de stockage contenant les clés et les secrets pour hello chiffré toobe de machine virtuelle restaurée.</span><span class="sxs-lookup"><span data-stu-id="f9e40-112">This is because this job generates a JSON file in your storage account containing keys and secrets for hello encrypted VM toobe restored.</span></span>

## <a name="get-key-and-secret-from-azure-backup"></a><span data-ttu-id="f9e40-113">Obtenir la clé et le secret à partir d’Azure Backup</span><span class="sxs-lookup"><span data-stu-id="f9e40-113">Get key and secret from Azure Backup</span></span>

> [!NOTE]
> <span data-ttu-id="f9e40-114">Une fois que le disque a été restauré pour hello encrypted machine virtuelle, vérifiez que :</span><span class="sxs-lookup"><span data-stu-id="f9e40-114">Once disk has been restored for hello encrypted VM, ensure that:</span></span>
> 1. <span data-ttu-id="f9e40-115">$details est remplie avec les détails du travail de disque de restauration, comme indiqué dans [PowerShell les étapes dans la section de disques hello de restauration](backup-azure-vms-automation.md#restore-an-azure-vm)</span><span class="sxs-lookup"><span data-stu-id="f9e40-115">$details is populated with restore disk job details, as mentioned in [PowerShell steps in Restore hello Disks section](backup-azure-vms-automation.md#restore-an-azure-vm)</span></span>
> 2. <span data-ttu-id="f9e40-116">Machine virtuelle doit être créé à partir de disques restaurées uniquement **une fois la clé et la clé secrète tookey restaurée coffre**.</span><span class="sxs-lookup"><span data-stu-id="f9e40-116">VM should be created from restored disks only **after key and secret is restored tookey vault**.</span></span>
>
>

<span data-ttu-id="f9e40-117">Hello de requête restauré les propriétés du disque pour les détails de la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="f9e40-117">Query hello restored disk properties for hello job details.</span></span>

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

<span data-ttu-id="f9e40-118">Définir le contexte du stockage Azure hello et restaurez le fichier de configuration JSON contenant une clé et les détails de secret principal pour la machine virtuelle chiffré.</span><span class="sxs-lookup"><span data-stu-id="f9e40-118">Set hello Azure storage context and restore JSON configuration file containing key and secret details for encrypted VM.</span></span>

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a><span data-ttu-id="f9e40-119">Restaurer la clé</span><span class="sxs-lookup"><span data-stu-id="f9e40-119">Restore key</span></span>
<span data-ttu-id="f9e40-120">Une fois que le fichier JSON de hello est générée dans le chemin d’accès de destination hello mentionné ci-dessus, générer des fichiers de l’objet blob de clé à partir de hello JSON et flux de clé de hello tooput toorestore applet de commande de clés (KEK) dans le coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="f9e40-120">Once hello JSON file is generated in hello destination path mentioned above, generate key blob file from hello JSON and feed it toorestore key cmdlet tooput hello key (KEK) back in hello key vault.</span></span>

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a><span data-ttu-id="f9e40-121">Restaurer le secret</span><span class="sxs-lookup"><span data-stu-id="f9e40-121">Restore secret</span></span>
<span data-ttu-id="f9e40-122">Utilisez un fichier JSON hello généré au-dessus de valeur et le nom de clé secrète tooget et tooput d’applet de commande secret tooset secret hello (BEK) de flux dans le coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="f9e40-122">Use hello JSON file generated above tooget secret name and value and feed it tooset secret cmdlet tooput hello secret (BEK) back in hello key vault.</span></span> <span data-ttu-id="f9e40-123">**Utilisez ces applets de commande si votre machine virtuelle est chiffrée à l’aide de BEK et KEK.**</span><span class="sxs-lookup"><span data-stu-id="f9e40-123">**Use these cmdlets if your VM is encrypted using BEK and KEK.**</span></span>

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

<span data-ttu-id="f9e40-124">Si votre machine virtuelle est **chiffré à l’aide de BEK uniquement**tooput d’applet de commande secret toorestore secret hello (BEK) de flux dans le coffre de clés hello et générer de fichier blob secrète à partir de hello JSON.</span><span class="sxs-lookup"><span data-stu-id="f9e40-124">If your VM is **encrypted using BEK only**, generate secret blob file from hello JSON and feed it toorestore secret cmdlet tooput hello secret (BEK) back in hello key vault.</span></span>

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. <span data-ttu-id="f9e40-125">Valeur de $secretname peut être obtenue en faisant référence de sortie toohello de $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl et à l’aide du texte après secrets / par exemple, les URL de secret principal de sortie est https://keyvaultname.vault.azure.net/secrets/ Nom de B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 et secret est B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="f9e40-125">Value for $secretname can be obtained by referring toohello output of $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="f9e40-126">Valeur de balise de hello DiskEncryptionKeyFileName est identique au nom secret.</span><span class="sxs-lookup"><span data-stu-id="f9e40-126">Value of hello tag DiskEncryptionKeyFileName is same as secret name.</span></span>
>
>

## <a name="create-virtual-machine-from-restored-disk"></a><span data-ttu-id="f9e40-127">Créer une machine virtuelle à partir du disque restauré</span><span class="sxs-lookup"><span data-stu-id="f9e40-127">Create virtual machine from restored disk</span></span>
<span data-ttu-id="f9e40-128">Si vous avez sauvegardé VM chiffrée à l’aide de la sauvegarde de machine virtuelle Azure, hello applets de commande PowerShell ci-dessus aide que vous restaurez la clé et le coffre de clés secrètes toohello précédent.</span><span class="sxs-lookup"><span data-stu-id="f9e40-128">If you have backed up encrypted VM using Azure VM Backup, hello PowerShell cmdlets mentioned above help you restore key and secret back toohello key vault.</span></span> <span data-ttu-id="f9e40-129">Après leur restauration, consultez l’article de hello [gérer la sauvegarde et restauration de machines virtuelles de Azure à l’aide de PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate chiffré des machines virtuelles à partir de disque restaurée, la clé et secret.</span><span class="sxs-lookup"><span data-stu-id="f9e40-129">After restoring them, refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate encrypted VMs from restored disk, key, and secret.</span></span>

## <a name="legacy-approach"></a><span data-ttu-id="f9e40-130">Approche héritée</span><span class="sxs-lookup"><span data-stu-id="f9e40-130">Legacy approach</span></span>
<span data-ttu-id="f9e40-131">approche Hello mentionné ci-dessus fonctionne pour tous les points de récupération hello.</span><span class="sxs-lookup"><span data-stu-id="f9e40-131">hello approach mentioned above would work for all hello recovery points.</span></span> <span data-ttu-id="f9e40-132">Toutefois, hello une approche plus ancienne de l’obtention de la clé et des informations confidentielles à partir du point de récupération, est valide pour les points de récupération antérieurs à 11 juillet 2017 pour les machines virtuelles chiffrés à l’aide de BEK et KEK.</span><span class="sxs-lookup"><span data-stu-id="f9e40-132">However, hello older approach of getting key and secret information from recovery point, would be valid for recovery points older than July 11, 2017 for VMs encrypted using BEK and KEK.</span></span> <span data-ttu-id="f9e40-133">Une fois le travail de restauration du disque terminé pour la machine virtuelle chiffrée à l’aide des [étapes PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm), assurez-vous que $rp est alimenté avec une valeur valide.</span><span class="sxs-lookup"><span data-stu-id="f9e40-133">Once restore disk job is complete for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm), ensure that $rp is populated with a valid value.</span></span>

### <a name="restore-key"></a><span data-ttu-id="f9e40-134">Restaurer la clé</span><span class="sxs-lookup"><span data-stu-id="f9e40-134">Restore key</span></span>
<span data-ttu-id="f9e40-135">Utilisez hello suit les informations de clé (KEK) tooget applets de commande à partir du point de récupération et tooput d’applet de commande clé toorestore ensuite dans le coffre de clés hello de flux.</span><span class="sxs-lookup"><span data-stu-id="f9e40-135">Use hello following cmdlets tooget key (KEK) information from recovery point and feed it toorestore key cmdlet tooput it back in hello key vault.</span></span>

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a><span data-ttu-id="f9e40-136">Restaurer le secret</span><span class="sxs-lookup"><span data-stu-id="f9e40-136">Restore secret</span></span>
<span data-ttu-id="f9e40-137">Utilisez hello suit les informations de clé secrète (BEK) tooget applets de commande à partir du point de récupération et tooput d’applet de commande secret tooset ensuite dans le coffre de clés hello de flux.</span><span class="sxs-lookup"><span data-stu-id="f9e40-137">Use hello following cmdlets tooget secret (BEK) information from recovery point and feed it tooset secret cmdlet tooput it back in hello key vault.</span></span>

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. <span data-ttu-id="f9e40-138">Valeur de $secretname peut être obtenue en faisant référence de sortie toohello de $rp1. KeyAndSecretDetails.SecretUrl et à l’aide du texte après secrets / par exemple, les URL de secret principal de sortie est https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 et nom secret est B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="f9e40-138">Value for $secretname can be obtained by referring toohello output of $rp1.KeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="f9e40-139">Valeur de balise de hello DiskEncryptionKeyFileName est identique au nom secret.</span><span class="sxs-lookup"><span data-stu-id="f9e40-139">Value of hello tag DiskEncryptionKeyFileName is same as secret name.</span></span>
> 3. <span data-ttu-id="f9e40-140">Valeur de DiskEncryptionKeyEncryptionKeyURL peut être obtenue à partir du coffre de clés après la restauration des clés de hello et à l’aide de [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) applet de commande</span><span class="sxs-lookup"><span data-stu-id="f9e40-140">Value for DiskEncryptionKeyEncryptionKeyURL can be obtained from key vault after restoring hello keys back and using [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="f9e40-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f9e40-141">Next steps</span></span>
<span data-ttu-id="f9e40-142">Après la restauration de clé et coffre de secret principal tookey précédent, consultez l’article de hello [gérer la sauvegarde et restauration de machines virtuelles de Azure à l’aide de PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate chiffré des machines virtuelles à partir de disque restaurée, clé et une clé secrète.</span><span class="sxs-lookup"><span data-stu-id="f9e40-142">After restoring key and secret back tookey vault, refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate encrypted VMs from restored disk, key and secret.</span></span>
