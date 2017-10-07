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
# <a name="how-tooencrypt-virtual-disks-on-a-windows-vm"></a><span data-ttu-id="9691c-103">Comment tooencrypt des disques virtuels sur une machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="9691c-103">How tooencrypt virtual disks on a Windows VM</span></span>
<span data-ttu-id="9691c-104">Pour renforcer la sécurité et la conformité de la machine virtuelle, les disques virtuels dans Azure peuvent être chiffrés.</span><span class="sxs-lookup"><span data-stu-id="9691c-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="9691c-105">Les disques sont chiffrés à l’aide de clés de chiffrement sécurisées dans un coffre de clés Azure.</span><span class="sxs-lookup"><span data-stu-id="9691c-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="9691c-106">Vous contrôlez ces clés de chiffrement et pouvez effectuer un audit de leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="9691c-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="9691c-107">Cet article détails comment tooencrypt les disques virtuels sur un ordinateur virtuel de Windows à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9691c-107">This article details how tooencrypt virtual disks on a Windows VM using Azure PowerShell.</span></span> <span data-ttu-id="9691c-108">Vous pouvez également [chiffrer un VM Linux à l’aide de hello Azure CLI 2.0](../linux/encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="9691c-108">You can also [encrypt a Linux VM using hello Azure CLI 2.0](../linux/encrypt-disks.md).</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="9691c-109">Présentation du chiffrement de disque</span><span class="sxs-lookup"><span data-stu-id="9691c-109">Overview of disk encryption</span></span>
<span data-ttu-id="9691c-110">Les disques virtuels sur des machines virtuelles Windows sont chiffrés au repos à l’aide de Bitlocker.</span><span class="sxs-lookup"><span data-stu-id="9691c-110">Virtual disks on Windows VMs are encrypted at rest using Bitlocker.</span></span> <span data-ttu-id="9691c-111">Le chiffrement de disques virtuels dans Azure n’entraîne aucun frais.</span><span class="sxs-lookup"><span data-stu-id="9691c-111">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="9691c-112">Clés de chiffrement sont stockées dans le coffre de clés Azure à l’aide du logiciel de protection, ou vous pouvez importer ou générer vos clés dans des Modules de sécurité matériel (HSM) certifié tooFIPS normes de niveau 2 140-2.</span><span class="sxs-lookup"><span data-stu-id="9691c-112">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="9691c-113">Ces clés de chiffrement sont utilisé tooencrypt et déchiffrement tooyour de disques virtuels attachés machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9691c-113">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="9691c-114">Vous gardez le contrôle de ces clés de chiffrement et pouvez effectuer un audit de leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="9691c-114">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="9691c-115">Un principal de service Azure Active Directory fournit un mécanisme sécurisé pour l’émission de ces clés de chiffrement lors de la mise sous tension et hors tension des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="9691c-115">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="9691c-116">processus de Hello de chiffrement d’une machine virtuelle est la suivante :</span><span class="sxs-lookup"><span data-stu-id="9691c-116">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="9691c-117">Créez une clé de chiffrement dans un coffre de clés Azure.</span><span class="sxs-lookup"><span data-stu-id="9691c-117">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="9691c-118">Configurer hello chiffrement clé toobe utilisable pour le chiffrement des disques.</span><span class="sxs-lookup"><span data-stu-id="9691c-118">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="9691c-119">clé de chiffrement hello tooread de hello Azure Key Vault, créez un service Azure Active Directory principal avec les autorisations appropriées hello.</span><span class="sxs-lookup"><span data-stu-id="9691c-119">tooread hello cryptographic key from hello Azure Key Vault, create an Azure Active Directory service principal with hello appropriate permissions.</span></span>
4. <span data-ttu-id="9691c-120">Émettre hello commande tooencrypt vos disques virtuels, en spécifiant le principal du service Azure Active Directory hello et appropriée toobe de clés cryptographique utilisé.</span><span class="sxs-lookup"><span data-stu-id="9691c-120">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory service principal and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="9691c-121">demandes principales du service Azure Active Directory Hello hello clé de chiffrement requis à partir d’Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="9691c-121">hello Azure Active Directory service principal requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="9691c-122">les disques virtuels Hello sont chiffrées à l’aide de la clé de chiffrement hello fourni.</span><span class="sxs-lookup"><span data-stu-id="9691c-122">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="9691c-123">Processus de chiffrement</span><span class="sxs-lookup"><span data-stu-id="9691c-123">Encryption process</span></span>
<span data-ttu-id="9691c-124">Chiffrement de disque s’appuie sur hello suivant des composants supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="9691c-124">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="9691c-125">**Azure Key Vault** -utilisé toosafeguard les clés de chiffrement et les secrets utilisés pour le processus de chiffrement/déchiffrement de disque hello.</span><span class="sxs-lookup"><span data-stu-id="9691c-125">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span> 
  * <span data-ttu-id="9691c-126">Le cas échéant, vous pouvez utiliser un coffre de clés Azure existant.</span><span class="sxs-lookup"><span data-stu-id="9691c-126">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="9691c-127">Vous n’avez pas de le toodedicate un disques tooencrypting de coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="9691c-127">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="9691c-128">les limites administratives tooseparate et la visibilité de clé, vous pouvez créer un coffre de clés dédié.</span><span class="sxs-lookup"><span data-stu-id="9691c-128">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="9691c-129">**Azure Active Directory** - handles hello échange sécurisé de clés de chiffrement requis et l’authentification pour demandé d’actions.</span><span class="sxs-lookup"><span data-stu-id="9691c-129">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span> 
  * <span data-ttu-id="9691c-130">Vous pouvez généralement utiliser une instance Azure Active Directory existante pour héberger votre application.</span><span class="sxs-lookup"><span data-stu-id="9691c-130">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="9691c-131">principal du service Hello fournit un mécanisme sécurisé de toorequest et être émis des clés de chiffrement appropriées hello.</span><span class="sxs-lookup"><span data-stu-id="9691c-131">hello service principal provides a secure mechanism toorequest and be issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="9691c-132">Vous ne développez pas de réelle application qui s’intègre à Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9691c-132">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="9691c-133">Spécifications et limitations</span><span class="sxs-lookup"><span data-stu-id="9691c-133">Requirements and limitations</span></span>
<span data-ttu-id="9691c-134">Configuration requise et scénarios pris en charge pour le chiffrement de disque :</span><span class="sxs-lookup"><span data-stu-id="9691c-134">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="9691c-135">Activation du chiffrement sur les nouvelles machines virtuelles Windows à partir d’images Azure Marketplace ou d’une image de disque dur virtuel personnalisée.</span><span class="sxs-lookup"><span data-stu-id="9691c-135">Enabling encryption on new Windows VMs from Azure Marketplace images or custom VHD image.</span></span>
* <span data-ttu-id="9691c-136">Activation du chiffrement sur les machines virtuelles Windows existantes dans Azure.</span><span class="sxs-lookup"><span data-stu-id="9691c-136">Enabling encryption on existing Windows VMs in Azure.</span></span>
* <span data-ttu-id="9691c-137">Activation du chiffrement sur les machines virtuelles Windows configurées à l’aide d’espaces de stockage.</span><span class="sxs-lookup"><span data-stu-id="9691c-137">Enabling encryption on Windows VMs that are configured using Storage Spaces.</span></span>
* <span data-ttu-id="9691c-138">Désactivation du chiffrement sur les systèmes d’exploitation et les lecteurs de données pour les machines virtuelles Windows.</span><span class="sxs-lookup"><span data-stu-id="9691c-138">Disabling encryption on OS and data drives for Windows VMs.</span></span>
* <span data-ttu-id="9691c-139">Toutes les ressources (telles que le coffre de clés, le compte de stockage et machine virtuelle) doivent être Bonjour même région Azure et abonnement.</span><span class="sxs-lookup"><span data-stu-id="9691c-139">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="9691c-140">Machines virtuelles de niveau standard (A, D, DS, G, GS et GS, par exemple).</span><span class="sxs-lookup"><span data-stu-id="9691c-140">Standard tier VMs, such as A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="9691c-141">Chiffrement de disque n’est pas pris en charge dans hello les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="9691c-141">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="9691c-142">Machines virtuelles de niveau de base.</span><span class="sxs-lookup"><span data-stu-id="9691c-142">Basic tier VMs.</span></span>
* <span data-ttu-id="9691c-143">Machines virtuelles créées à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="9691c-143">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="9691c-144">Mise à jour des clés de chiffrement hello sur une machine virtuelle déjà chiffrée.</span><span class="sxs-lookup"><span data-stu-id="9691c-144">Updating hello cryptographic keys on an already encrypted VM.</span></span>
* <span data-ttu-id="9691c-145">Intégration au service de gestion de clés local.</span><span class="sxs-lookup"><span data-stu-id="9691c-145">Integration with on-prem Key Management Service.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="9691c-146">Créer le coffre de clés Azure et les clés</span><span class="sxs-lookup"><span data-stu-id="9691c-146">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="9691c-147">Avant de commencer, assurez-vous que hello la dernière version de hello Azure PowerShell module a été installé.</span><span class="sxs-lookup"><span data-stu-id="9691c-147">Before you start, make sure that hello latest version of hello Azure PowerShell module has been installed.</span></span> <span data-ttu-id="9691c-148">Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9691c-148">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="9691c-149">Dans l’ensemble des exemples de commandes hello, remplacer tous les paramètres de l’exemple avec votre propre nom, l’emplacement et valeurs de clés.</span><span class="sxs-lookup"><span data-stu-id="9691c-149">Throughout hello command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="9691c-150">Hello exemples suivants utilisent une convention de *myResourceGroup*, *myKeyVault*, *myVM*, etc..</span><span class="sxs-lookup"><span data-stu-id="9691c-150">hello following examples use a convention of *myResourceGroup*, *myKeyVault*, *myVM*, etc.</span></span>

<span data-ttu-id="9691c-151">première étape de Hello est toocreate un toostore Azure Key Vault vos clés de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="9691c-151">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="9691c-152">Coffre de clés Azure peuvent stocker des clés, des secrets, ou les mots de passe qui vous permettent de toosecurely leur implémentent dans vos applications et services.</span><span class="sxs-lookup"><span data-stu-id="9691c-152">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="9691c-153">Pour le chiffrement de disque virtuel, vous créez un coffre de clés de toostore une clé de chiffrement qui est utilisé tooencrypt ou déchiffrer vos disques virtuels.</span><span class="sxs-lookup"><span data-stu-id="9691c-153">For virtual disk encryption, you create a Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span> 

<span data-ttu-id="9691c-154">Activer le fournisseur de coffre de clés Azure hello dans votre abonnement Azure avec [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), puis créer un groupe de ressources avec [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="9691c-154">Enable hello Azure Key Vault provider within your Azure subscription with [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), then create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="9691c-155">Hello exemple suivant crée un nom de groupe de ressources *myResourceGroup* Bonjour *États-Unis* emplacement :</span><span class="sxs-lookup"><span data-stu-id="9691c-155">hello following example creates a resource group name *myResourceGroup* in hello *East US* location:</span></span>

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

<span data-ttu-id="9691c-156">Bonjour Azure Key Vault contenant hello clés de chiffrement et calcul associée ressources telles que le stockage et hello machine virtuelle proprement dite doivent résider dans hello même région.</span><span class="sxs-lookup"><span data-stu-id="9691c-156">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="9691c-157">Créer un coffre de clés Azure avec [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) et activer hello coffre de clés pour une utilisation avec le chiffrement de disque.</span><span class="sxs-lookup"><span data-stu-id="9691c-157">Create an Azure Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="9691c-158">Spécifiez un nom de Key Vault unique pour *keyVaultName* comme suit :</span><span class="sxs-lookup"><span data-stu-id="9691c-158">Specify a unique Key Vault name for *keyVaultName* as follows:</span></span>

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

<span data-ttu-id="9691c-159">Vous pouvez stocker des clés de chiffrement à l’aide d’une protection logicielle ou HSM (modèle de sécurité matériel).</span><span class="sxs-lookup"><span data-stu-id="9691c-159">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="9691c-160">L’utilisation d’une protection HSM nécessite un coffre de clés Premium.</span><span class="sxs-lookup"><span data-stu-id="9691c-160">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="9691c-161">Il est un toocreating coût supplémentaire un coffre de clés plutôt que le coffre de clés standard qui stocke les clés protégées par logiciel.</span><span class="sxs-lookup"><span data-stu-id="9691c-161">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="9691c-162">toocreate un coffre de clés, premium Bonjour précédant l’étape Ajouter hello *- référence (SKU) « Premium »* paramètres.</span><span class="sxs-lookup"><span data-stu-id="9691c-162">toocreate a premium Key Vault, in hello preceding step add hello *-Sku "Premium"* parameters.</span></span> <span data-ttu-id="9691c-163">Hello exemple suivant utilise des clés de protection logicielle étant donné que nous avons créé un coffre de clés standard.</span><span class="sxs-lookup"><span data-stu-id="9691c-163">hello following example uses software-protected keys since we created a standard Key Vault.</span></span> 

<span data-ttu-id="9691c-164">Les modèles de protection, hello plateforme Azure doit toobe accordé accès toorequest les clés de chiffrement hello lorsque hello machine virtuelle démarre les disques virtuels toodecrypt hello.</span><span class="sxs-lookup"><span data-stu-id="9691c-164">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="9691c-165">Créez une clé de chiffrement dans le coffre Key Vault avec [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span><span class="sxs-lookup"><span data-stu-id="9691c-165">Create a cryptographic key in your Key Vault with [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey).</span></span> <span data-ttu-id="9691c-166">Hello exemple suivant crée une clé nommée *myKey*:</span><span class="sxs-lookup"><span data-stu-id="9691c-166">hello following example creates a key named *myKey*:</span></span>

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-hello-azure-active-directory-service-principal"></a><span data-ttu-id="9691c-167">Créer hello principal du service Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9691c-167">Create hello Azure Active Directory service principal</span></span>
<span data-ttu-id="9691c-168">Lorsque les disques virtuels sont chiffrées ou déchiffrées, vous spécifiez une authentification hello toohandle des comptes et l’échange de clés de chiffrement à partir du coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="9691c-168">When virtual disks are encrypted or decrypted, you specify an account toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="9691c-169">Ce compte, un principal du service Azure Active Directory, permet de clés de chiffrement approprié hello pour le compte hello VM toorequest de plateforme Windows Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9691c-169">This account, an Azure Active Directory service principal, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="9691c-170">Une instance Azure Active Directory par défaut est disponible dans votre abonnement, bien que de nombreuses organisations utilisent des répertoires Azure Active Directory dédiés.</span><span class="sxs-lookup"><span data-stu-id="9691c-170">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="9691c-171">Créez un principal du service dans Azure Active Directory avec [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span><span class="sxs-lookup"><span data-stu-id="9691c-171">Create a service principal in Azure Active Directory with [New-AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal).</span></span> <span data-ttu-id="9691c-172">toospecify un mot de passe sécurisé, suivez hello [des stratégies de mot de passe et les restrictions dans Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):</span><span class="sxs-lookup"><span data-stu-id="9691c-172">toospecify a secure password, follow hello [Password policies and restrictions in Azure Active Directory](../../active-directory/active-directory-passwords-policy.md):</span></span>

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

<span data-ttu-id="9691c-173">toosuccessfully chiffrer ou déchiffrer des disques virtuels, les autorisations sur la clé de chiffrement hello stockées dans le coffre de clés doivent être principal tooread hello clés du service Azure Active Directory définies toopermit hello.</span><span class="sxs-lookup"><span data-stu-id="9691c-173">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory service principal tooread hello keys.</span></span> <span data-ttu-id="9691c-174">Définissez des autorisations sur votre Key Vault avec [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) :</span><span class="sxs-lookup"><span data-stu-id="9691c-174">Set permissions on your Key Vault with [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a><span data-ttu-id="9691c-175">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="9691c-175">Create virtual machine</span></span>
<span data-ttu-id="9691c-176">tootest hello du processus de chiffrement, nous allons créer une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9691c-176">tootest hello encryption process, let's create a VM.</span></span> <span data-ttu-id="9691c-177">Hello exemple suivant crée un ordinateur virtuel nommé *myVM* à l’aide un *Windows Server 2016 Datacenter* image :</span><span class="sxs-lookup"><span data-stu-id="9691c-177">hello following example creates a VM named *myVM* using a *Windows Server 2016 Datacenter* image:</span></span>

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


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="9691c-178">Chiffrement d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="9691c-178">Encrypt virtual machine</span></span>
<span data-ttu-id="9691c-179">disques virtuels de tooencrypt hello, vous réunissez tous les composants précédents hello :</span><span class="sxs-lookup"><span data-stu-id="9691c-179">tooencrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="9691c-180">Spécifiez hello principal du service Azure Active Directory et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="9691c-180">Specify hello Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="9691c-181">Spécifier des métadonnées de hello toostore hello coffre de clés pour vos disques chiffrés.</span><span class="sxs-lookup"><span data-stu-id="9691c-181">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="9691c-182">Spécifiez toouse de clés de chiffrement hello pour chiffrement hello et le déchiffrement.</span><span class="sxs-lookup"><span data-stu-id="9691c-182">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="9691c-183">Spécifier si vous souhaitez disque hello du système d’exploitation de tooencrypt, des disques de données hello ou tous.</span><span class="sxs-lookup"><span data-stu-id="9691c-183">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="9691c-184">Chiffrer votre machine virtuelle avec [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) à l’aide de la clé de coffre de clés Azure hello et les informations d’identification de principales Azure Active Directory service.</span><span class="sxs-lookup"><span data-stu-id="9691c-184">Encrypt your VM with [Set-AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) using hello Azure Key Vault key and Azure Active Directory service principal credentials.</span></span> <span data-ttu-id="9691c-185">Hello exemple suivant récupère toutes les informations de clé hello puis chiffre hello ordinateur virtuel nommé *myVM*:</span><span class="sxs-lookup"><span data-stu-id="9691c-185">hello following example retrieves all hello key information then encrypts hello VM named *myVM*:</span></span>

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

<span data-ttu-id="9691c-186">Accepter toocontinue d’invite de commandes hello avec le chiffrement de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="9691c-186">Accept hello prompt toocontinue with hello VM encryption.</span></span> <span data-ttu-id="9691c-187">Hello machine virtuelle redémarre pendant le processus de hello.</span><span class="sxs-lookup"><span data-stu-id="9691c-187">hello VM restarts during hello process.</span></span> <span data-ttu-id="9691c-188">Une fois que se termine le processus de chiffrement hello et hello machine virtuelle a redémarré, examinez l’état du chiffrement hello avec [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span><span class="sxs-lookup"><span data-stu-id="9691c-188">Once hello encryption process completes and hello VM has rebooted, review hello encryption status with [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):</span></span>

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

<span data-ttu-id="9691c-189">Hello la sortie est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="9691c-189">hello output is similar toohello following example:</span></span>

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a><span data-ttu-id="9691c-190">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9691c-190">Next steps</span></span>
* <span data-ttu-id="9691c-191">Pour plus d’informations sur la gestion d’Azure Key Vault, consultez [Configuration de Key Vault pour des machines virtuelles](key-vault-setup.md).</span><span class="sxs-lookup"><span data-stu-id="9691c-191">For more information about managing Azure Key Vault, see [Set up Key Vault for virtual machines](key-vault-setup.md).</span></span>
* <span data-ttu-id="9691c-192">Pour plus d’informations sur le chiffrement de disque, telles que la préparation d’une tooAzure tooupload machine virtuelle personnalisée chiffré, consultez [chiffrement de disque Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="9691c-192">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
