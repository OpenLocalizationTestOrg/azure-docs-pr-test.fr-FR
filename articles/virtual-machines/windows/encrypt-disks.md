---
title: disques aaaEncrypt sur un ordinateur virtuel Windows Azure | Documents Microsoft
description: "Comment tooencrypt des disques virtuels sur un ordinateur virtuel Windows pour amélioré la sécurité à l’aide d’Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/10/2017
ms.author: iainfou
ms.openlocfilehash: 77c42a67cb57a9dc5fe3159fce0be75e3a965be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-windows-vm"></a>Comment tooencrypt des disques virtuels sur une machine virtuelle Windows
Pour renforcer la sécurité et la conformité de la machine virtuelle, les disques virtuels dans Azure peuvent être chiffrés. Les disques sont chiffrés à l’aide de clés de chiffrement sécurisées dans un coffre de clés Azure. Vous contrôlez ces clés de chiffrement et pouvez effectuer un audit de leur utilisation. Cet article détails comment tooencrypt les disques virtuels sur un ordinateur virtuel de Windows à l’aide d’Azure PowerShell. Vous pouvez également [chiffrer un VM Linux à l’aide de hello Azure CLI 2.0](../linux/encrypt-disks.md).

## <a name="overview-of-disk-encryption"></a>Présentation du chiffrement de disque
Les disques virtuels sur des machines virtuelles Windows sont chiffrés au repos à l’aide de Bitlocker. Le chiffrement de disques virtuels dans Azure n’entraîne aucun frais. Clés de chiffrement sont stockées dans le coffre de clés Azure à l’aide du logiciel de protection, ou vous pouvez importer ou générer vos clés dans des Modules de sécurité matériel (HSM) certifié tooFIPS normes de niveau 2 140-2. Ces clés de chiffrement sont utilisé tooencrypt et déchiffrement tooyour de disques virtuels attachés machine virtuelle. Vous gardez le contrôle de ces clés de chiffrement et pouvez effectuer un audit de leur utilisation. Un principal de service Azure Active Directory fournit un mécanisme sécurisé pour l’émission de ces clés de chiffrement lors de la mise sous tension et hors tension des machines virtuelles.

processus de Hello de chiffrement d’une machine virtuelle est la suivante :

1. Créez une clé de chiffrement dans un coffre de clés Azure.
2. Configurer hello chiffrement clé toobe utilisable pour le chiffrement des disques.
3. clé de chiffrement hello tooread de hello Azure Key Vault, créez un service Azure Active Directory principal avec les autorisations appropriées hello.
4. Émettre hello commande tooencrypt vos disques virtuels, en spécifiant le principal du service Azure Active Directory hello et appropriée toobe de clés cryptographique utilisé.
5. demandes principales du service Azure Active Directory Hello hello clé de chiffrement requis à partir d’Azure Key Vault.
6. les disques virtuels Hello sont chiffrées à l’aide de la clé de chiffrement hello fourni.

## <a name="encryption-process"></a>Processus de chiffrement
Chiffrement de disque s’appuie sur hello suivant des composants supplémentaires :

* **Azure Key Vault** -utilisé toosafeguard les clés de chiffrement et les secrets utilisés pour le processus de chiffrement/déchiffrement de disque hello. 
  * Le cas échéant, vous pouvez utiliser un coffre de clés Azure existant. Vous n’avez pas de le toodedicate un disques tooencrypting de coffre de clés.
  * les limites administratives tooseparate et la visibilité de clé, vous pouvez créer un coffre de clés dédié.
* **Azure Active Directory** - handles hello échange sécurisé de clés de chiffrement requis et l’authentification pour demandé d’actions. 
  * Vous pouvez généralement utiliser une instance Azure Active Directory existante pour héberger votre application.
  * principal du service Hello fournit un mécanisme sécurisé de toorequest et être émis des clés de chiffrement appropriées hello. Vous ne développez pas de réelle application qui s’intègre à Azure Active Directory.

## <a name="requirements-and-limitations"></a>Spécifications et limitations
Configuration requise et scénarios pris en charge pour le chiffrement de disque :

* Activation du chiffrement sur les nouvelles machines virtuelles Windows à partir d’images Azure Marketplace ou d’une image de disque dur virtuel personnalisée.
* Activation du chiffrement sur les machines virtuelles Windows existantes dans Azure.
* Activation du chiffrement sur les machines virtuelles Windows configurées à l’aide d’espaces de stockage.
* Désactivation du chiffrement sur les systèmes d’exploitation et les lecteurs de données pour les machines virtuelles Windows.
* Toutes les ressources (telles que le coffre de clés, le compte de stockage et machine virtuelle) doivent être Bonjour même région Azure et abonnement.
* Machines virtuelles de niveau standard (A, D, DS, G, GS et GS, par exemple).

Chiffrement de disque n’est pas pris en charge dans hello les scénarios suivants :

* Machines virtuelles de niveau de base.
* Machines virtuelles créées à l’aide du modèle de déploiement classique hello.
* Mise à jour des clés de chiffrement hello sur une machine virtuelle déjà chiffrée.
* Intégration au service de gestion de clés local.

## <a name="create-azure-key-vault-and-keys"></a>Créer le coffre de clés Azure et les clés
Avant de commencer, assurez-vous que hello la dernière version de hello Azure PowerShell module a été installé. Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview). Dans l’ensemble des exemples de commandes hello, remplacer tous les paramètres de l’exemple avec votre propre nom, l’emplacement et valeurs de clés. Hello exemples suivants utilisent une convention de *myResourceGroup*, *myKeyVault*, *myVM*, etc..

première étape de Hello est toocreate un toostore Azure Key Vault vos clés de chiffrement. Coffre de clés Azure peuvent stocker des clés, des secrets, ou les mots de passe qui vous permettent de toosecurely leur implémentent dans vos applications et services. Pour le chiffrement de disque virtuel, vous créez un coffre de clés de toostore une clé de chiffrement qui est utilisé tooencrypt ou déchiffrer vos disques virtuels. 

Activer le fournisseur de coffre de clés Azure hello dans votre abonnement Azure avec [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), puis créer un groupe de ressources avec [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Hello exemple suivant crée un nom de groupe de ressources *myResourceGroup* Bonjour *États-Unis* emplacement :

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

Bonjour Azure Key Vault contenant hello clés de chiffrement et calcul associée ressources telles que le stockage et hello machine virtuelle proprement dite doivent résider dans hello même région. Créer un coffre de clés Azure avec [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) et activer hello coffre de clés pour une utilisation avec le chiffrement de disque. Spécifiez un nom de Key Vault unique pour *keyVaultName* comme suit :

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

Vous pouvez stocker des clés de chiffrement à l’aide d’une protection logicielle ou HSM (modèle de sécurité matériel). L’utilisation d’une protection HSM nécessite un coffre de clés Premium. Il est un toocreating coût supplémentaire un coffre de clés plutôt que le coffre de clés standard qui stocke les clés protégées par logiciel. toocreate un coffre de clés, premium Bonjour précédant l’étape Ajouter hello *- référence (SKU) « Premium »* paramètres. Hello exemple suivant utilise des clés de protection logicielle étant donné que nous avons créé un coffre de clés standard. 

Les modèles de protection, hello plateforme Azure doit toobe accordé accès toorequest les clés de chiffrement hello lorsque hello machine virtuelle démarre les disques virtuels toodecrypt hello. Créez une clé de chiffrement dans le coffre Key Vault avec [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey). Hello exemple suivant crée une clé nommée *myKey*:

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-hello-azure-active-directory-service-principal"></a>Créer hello principal du service Azure Active Directory
Lorsque les disques virtuels sont chiffrées ou déchiffrées, vous spécifiez une authentification hello toohandle des comptes et l’échange de clés de chiffrement à partir du coffre de clés. Ce compte, un principal du service Azure Active Directory, permet de clés de chiffrement approprié hello pour le compte hello VM toorequest de plateforme Windows Azure hello. Une instance Azure Active Directory par défaut est disponible dans votre abonnement, bien que de nombreuses organisations utilisent des répertoires Azure Active Directory dédiés.

Créez un principal du service dans Azure Active Directory avec [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal). toospecify un mot de passe sécurisé, suivez hello [des stratégies de mot de passe et les restrictions dans Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

toosuccessfully chiffrer ou déchiffrer des disques virtuels, les autorisations sur la clé de chiffrement hello stockées dans le coffre de clés doivent être principal tooread hello clés du service Azure Active Directory définies toopermit hello. Définissez des autorisations sur votre Key Vault avec [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) :

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a>Create virtual machine
tootest hello du processus de chiffrement, nous allons créer une machine virtuelle. Hello exemple suivant crée un ordinateur virtuel nommé *myVM* à l’aide un *Windows Server 2016 Datacenter* image :

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "mypublicdns$(Get-Random)"

$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$cred = Get-Credential

$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```


## <a name="encrypt-virtual-machine"></a>Chiffrement d’une machine virtuelle
disques virtuels de tooencrypt hello, vous réunissez tous les composants précédents hello :

1. Spécifiez hello principal du service Azure Active Directory et le mot de passe.
2. Spécifier des métadonnées de hello toostore hello coffre de clés pour vos disques chiffrés.
3. Spécifiez toouse de clés de chiffrement hello pour chiffrement hello et le déchiffrement.
4. Spécifier si vous souhaitez disque hello du système d’exploitation de tooencrypt, des disques de données hello ou tous.

Chiffrer votre machine virtuelle avec [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) à l’aide de la clé de coffre de clés Azure hello et les informations d’identification de principales Azure Active Directory service. Hello exemple suivant récupère toutes les informations de clé hello puis chiffre hello ordinateur virtuel nommé *myVM*:

```powershell
$keyVault = Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $rgName;
$diskEncryptionKeyVaultUrl = $keyVault.VaultUri;
$keyVaultResourceId = $keyVault.ResourceId;
$keyEncryptionKeyUrl = (Get-AzureKeyVaultKey -VaultName $keyVaultName -Name myKey).Key.kid;

Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $rgName `
    -VMName $vmName `
    -AadClientID $app.ApplicationId `
    -AadClientSecret $securePassword `
    -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl `
    -DiskEncryptionKeyVaultId $keyVaultResourceId `
    -KeyEncryptionKeyUrl $keyEncryptionKeyUrl `
    -KeyEncryptionKeyVaultId $keyVaultResourceId
```

Accepter toocontinue d’invite de commandes hello avec le chiffrement de machine virtuelle hello. Hello machine virtuelle redémarre pendant le processus de hello. Une fois que se termine le processus de chiffrement hello et hello machine virtuelle a redémarré, examinez l’état du chiffrement hello avec [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

Hello la sortie est similaire toohello l’exemple suivant :

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur la gestion d’Azure Key Vault, consultez [Configuration de Key Vault pour des machines virtuelles](key-vault-setup.md).
* Pour plus d’informations sur le chiffrement de disque, telles que la préparation d’une tooAzure tooupload machine virtuelle personnalisée chiffré, consultez [chiffrement de disque Azure](../../security/azure-security-disk-encryption.md).
