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
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a>Restaurer la clé et le secret du Key Vault pour les machines virtuelles chiffrées à l’aide d’Azure Backup
Cet article traite d’à l’aide de restauration tooperform de sauvegarde de machine virtuelle Azure de chiffrée des machines virtuelles Azure, si votre clé et la clé secrète n’existent pas dans le coffre de clés hello. Ces étapes peuvent également servir toomaintain une copie distincte de clé (clé de cryptage) et secret (clé de chiffrement BitLocker) pour hello restaurer la machine virtuelle.

## <a name="prerequisites"></a>Composants requis
* **Sauvegarder les machines virtuelles chiffrées** : les machines virtuelles Azure chiffrées ont été sauvegardées à l’aide d’Azure Backup. Consultez l’article de hello [gérer la sauvegarde et restauration de machines virtuelles de Azure à l’aide de PowerShell](backup-azure-vms-automation.md) pour plus d’informations sur le mode de chiffrement de machines virtuelles Azure toobackup.
* **Configurer Azure Key Vault** : Assurez-vous que le coffre de clés toowhich clés et toobe besoin de clés secrètes restauré est déjà présent. Consultez l’article de hello [prise en main d’Azure Key Vault](../key-vault/key-vault-get-started.md) pour plus d’informations sur la gestion de coffre de clés.
* **Restauration du disque** : vérifiez que vous avez déclenché des travaux de restauration pour restaurer les disques d’une machine virtuelle chiffrée à l’aide des [étapes PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm). Il s’agit, car ce travail génère un fichier JSON dans votre compte de stockage contenant les clés et les secrets pour hello chiffré toobe de machine virtuelle restaurée.

## <a name="get-key-and-secret-from-azure-backup"></a>Obtenir la clé et le secret à partir d’Azure Backup

> [!NOTE]
> Une fois que le disque a été restauré pour hello encrypted machine virtuelle, vérifiez que :
> 1. $details est remplie avec les détails du travail de disque de restauration, comme indiqué dans [PowerShell les étapes dans la section de disques hello de restauration](backup-azure-vms-automation.md#restore-an-azure-vm)
> 2. Machine virtuelle doit être créé à partir de disques restaurées uniquement **une fois la clé et la clé secrète tookey restaurée coffre**.
>
>

Hello de requête restauré les propriétés du disque pour les détails de la tâche hello.

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

Définir le contexte du stockage Azure hello et restaurez le fichier de configuration JSON contenant une clé et les détails de secret principal pour la machine virtuelle chiffré.

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a>Restaurer la clé
Une fois que le fichier JSON de hello est générée dans le chemin d’accès de destination hello mentionné ci-dessus, générer des fichiers de l’objet blob de clé à partir de hello JSON et flux de clé de hello tooput toorestore applet de commande de clés (KEK) dans le coffre de clés hello.

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a>Restaurer le secret
Utilisez un fichier JSON hello généré au-dessus de valeur et le nom de clé secrète tooget et tooput d’applet de commande secret tooset secret hello (BEK) de flux dans le coffre de clés hello. **Utilisez ces applets de commande si votre machine virtuelle est chiffrée à l’aide de BEK et KEK.**

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

Si votre machine virtuelle est **chiffré à l’aide de BEK uniquement**tooput d’applet de commande secret toorestore secret hello (BEK) de flux dans le coffre de clés hello et générer de fichier blob secrète à partir de hello JSON.

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. Valeur de $secretname peut être obtenue en faisant référence de sortie toohello de $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl et à l’aide du texte après secrets / par exemple, les URL de secret principal de sortie est https://keyvaultname.vault.azure.net/secrets/ Nom de B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 et secret est B3284AAA-DAAA-4AAA-B393-60CAA848AAAA
> 2. Valeur de balise de hello DiskEncryptionKeyFileName est identique au nom secret.
>
>

## <a name="create-virtual-machine-from-restored-disk"></a>Créer une machine virtuelle à partir du disque restauré
Si vous avez sauvegardé VM chiffrée à l’aide de la sauvegarde de machine virtuelle Azure, hello applets de commande PowerShell ci-dessus aide que vous restaurez la clé et le coffre de clés secrètes toohello précédent. Après leur restauration, consultez l’article de hello [gérer la sauvegarde et restauration de machines virtuelles de Azure à l’aide de PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate chiffré des machines virtuelles à partir de disque restaurée, la clé et secret.

## <a name="legacy-approach"></a>Approche héritée
approche Hello mentionné ci-dessus fonctionne pour tous les points de récupération hello. Toutefois, hello une approche plus ancienne de l’obtention de la clé et des informations confidentielles à partir du point de récupération, est valide pour les points de récupération antérieurs à 11 juillet 2017 pour les machines virtuelles chiffrés à l’aide de BEK et KEK. Une fois le travail de restauration du disque terminé pour la machine virtuelle chiffrée à l’aide des [étapes PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm), assurez-vous que $rp est alimenté avec une valeur valide.

### <a name="restore-key"></a>Restaurer la clé
Utilisez hello suit les informations de clé (KEK) tooget applets de commande à partir du point de récupération et tooput d’applet de commande clé toorestore ensuite dans le coffre de clés hello de flux.

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a>Restaurer le secret
Utilisez hello suit les informations de clé secrète (BEK) tooget applets de commande à partir du point de récupération et tooput d’applet de commande secret tooset ensuite dans le coffre de clés hello de flux.

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. Valeur de $secretname peut être obtenue en faisant référence de sortie toohello de $rp1. KeyAndSecretDetails.SecretUrl et à l’aide du texte après secrets / par exemple, les URL de secret principal de sortie est https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 et nom secret est B3284AAA-DAAA-4AAA-B393-60CAA848AAAA
> 2. Valeur de balise de hello DiskEncryptionKeyFileName est identique au nom secret.
> 3. Valeur de DiskEncryptionKeyEncryptionKeyURL peut être obtenue à partir du coffre de clés après la restauration des clés de hello et à l’aide de [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) applet de commande
>
>

## <a name="next-steps"></a>Étapes suivantes
Après la restauration de clé et coffre de secret principal tookey précédent, consultez l’article de hello [gérer la sauvegarde et restauration de machines virtuelles de Azure à l’aide de PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate chiffré des machines virtuelles à partir de disque restaurée, clé et une clé secrète.
