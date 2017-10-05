---
title: "Chiffrer les disques sur une machine virtuelle Linux avec Azure CLI 1.0 | Microsoft Docs"
description: "Comment chiffrer des disques sur une machine virtuelle Linux avec Azure CLI 1.0 et le modèle de déploiement Resource Manager"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/06/2017
ms.author: iainfou
ms.openlocfilehash: b436f2d43c41000f4385889edb3fa3983d4a8c66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="encrypt-disks-on-a-linux-vm-using-the-azure-cli-10"></a><span data-ttu-id="5f8f2-103">Chiffrer des disques sur une machine virtuelle Linux avec Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5f8f2-103">Encrypt disks on a Linux VM using the Azure CLI 1.0</span></span>
<span data-ttu-id="5f8f2-104">Pour renforcer la sécurité et la conformité de la machine virtuelle , les disques virtuels dans Azure peuvent être chiffrés au repos.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted at rest.</span></span> <span data-ttu-id="5f8f2-105">Les disques sont chiffrés à l’aide de clés de chiffrement sécurisées dans un coffre de clés Azure.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="5f8f2-106">Vous contrôlez ces clés de chiffrement et pouvez effectuer un audit de leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="5f8f2-107">Cet article explique comment chiffrer des disques virtuels sur une machine virtuelle Linux avec Azure CLI 1.0 et le modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-107">This article details how to encrypt virtual disks on a Linux VM using the Azure CLI 1.0 and the Resource Manager deployment model.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="5f8f2-108">Versions de l’interface de ligne de commande permettant d’effectuer la tâche</span><span class="sxs-lookup"><span data-stu-id="5f8f2-108">CLI versions to complete the task</span></span>
<span data-ttu-id="5f8f2-109">Vous pouvez exécuter la tâche en utilisant l’une des versions suivantes de l’interface de ligne de commande (CLI) :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-109">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="5f8f2-110">[Azure CLI 1.0](#quick-commands) : notre interface de ligne de commande pour les modèles de déploiement Classique et Resource Manager (cet article)</span><span class="sxs-lookup"><span data-stu-id="5f8f2-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="5f8f2-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) : notre interface Azure CLI nouvelle génération pour le modèle de déploiement Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5f8f2-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="5f8f2-112">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="5f8f2-112">Quick commands</span></span>
<span data-ttu-id="5f8f2-113">Si vous avez besoin d’accomplir rapidement cette tâche, la section suivante décrit les commandes de base pour chiffrer des disques virtuels sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-113">If you need to quickly accomplish the task, the following section details the base commands to encrypt virtual disks on your VM.</span></span> <span data-ttu-id="5f8f2-114">Pour obtenir plus d’informations et davantage de contexte pour chaque étape, lisez la suite de ce document, [à partir de cette section](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="5f8f2-114">More detailed information and context for each step can be found the rest of the document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="5f8f2-115">La [dernière version d’Azure CLI 1.0](../../xplat-cli-install.md) doit être installée et connectée ainsi, selon le mode Resource Manager :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-115">You need the [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="5f8f2-116">Dans les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-116">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="5f8f2-117">Exemples de noms de paramètre : `myResourceGroup`, `myKeyVault` et `myVM`.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-117">Example parameter names include `myResourceGroup`, `myKeyVault`, and `myVM`.</span></span>

<span data-ttu-id="5f8f2-118">Tout d’abord, activez le fournisseur Azure Key Vault au sein de votre abonnement Azure puis créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-118">First, enable the Azure Key Vault provider within your Azure subscription and create a resource group.</span></span> <span data-ttu-id="5f8f2-119">L’exemple suivant crée un groupe de ressources nommé `myResourceGroup` à l’emplacement `WestUS` :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-119">The following example creates a resource group name `myResourceGroup` in the `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="5f8f2-120">Créez un coffre de clés Azure.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-120">Create an Azure Key Vault.</span></span> <span data-ttu-id="5f8f2-121">L’exemple qui suit permet de créer un coffre de clés nommé `myKeyVault` :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-121">The following example creates a Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="5f8f2-122">Créez une clé de chiffrement dans le coffre de clés et activez-la pour le chiffrement du disque.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-122">Create a cryptographic key in your Key Vault and enable it for disk encryption.</span></span> <span data-ttu-id="5f8f2-123">L’exemple qui suit permet de créer une clé nommée `myKey` :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-123">The following example creates a key named `myKey`:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

<span data-ttu-id="5f8f2-124">Créez un point de terminaison à l’aide d’Azure Active Directory pour gérer l’authentification et l’échange de clés de chiffrement à partir du coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-124">Create an endpoint using Azure Active Directory for handling the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="5f8f2-125">Les valeurs `--home-page` et `--identifier-uris` peuvent ne pas représenter des adresses routables réelles.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-125">The `--home-page` and `--identifier-uris` do not need to be actual routable address.</span></span> <span data-ttu-id="5f8f2-126">Pour un niveau de sécurité maximal, vous devez utiliser des clés secrètes de client au lieu de mots de passe.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-126">For the highest level of security, client secrets should be used instead of passwords.</span></span> <span data-ttu-id="5f8f2-127">Actuellement, l’interface CLI Azure ne permet pas de générer des clés secrètes de client.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-127">The Azure CLI cannot currently generate client secrets.</span></span> <span data-ttu-id="5f8f2-128">Les clés secrètes de client peuvent uniquement être générées dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-128">Client secrets can only be generated in the Azure portal.</span></span> <span data-ttu-id="5f8f2-129">L’exemple suivant crée un point de terminaison Azure Active Directory nommé `myAADApp` et utilise un mot de passe `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-129">The following example creates an Azure Active Directory endpoint named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="5f8f2-130">Spécifiez votre propre mot de passe comme suit :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-130">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="5f8f2-131">Notez la valeur `applicationId` indiquée dans la sortie de la commande précédente.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-131">Note the `applicationId` shown in the output from the preceding command.</span></span> <span data-ttu-id="5f8f2-132">Cet ID d’application est utilisé dans les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-132">This application ID is used in the following steps:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

<span data-ttu-id="5f8f2-133">Ajoutez un disque de données à une machine Virtuelle existante.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-133">Add a data disk to an existing VM.</span></span> <span data-ttu-id="5f8f2-134">L’exemple suivant ajoute un disque de données à une machine virtuelle nommée `myVM`:</span><span class="sxs-lookup"><span data-stu-id="5f8f2-134">The following example adds a data disk to a VM named `myVM`:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="5f8f2-135">Examinez les détails de votre coffre de clés et la clé que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-135">Review the details for your Key Vault and the key you created.</span></span> <span data-ttu-id="5f8f2-136">Vous avez besoin de l’ID du coffre de clés, de l’URI et de l’URL de la clé à la dernière étape.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-136">You need the Key Vault ID, URI, and key URL in the final step.</span></span> <span data-ttu-id="5f8f2-137">L’exemple suivant passe détaille un coffre de clés nommé `myKeyVault` et une clé nommée `myKey` :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-137">The following example reviews the details for a Key Vault named `myKeyVault` and key named `myKey`:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="5f8f2-138">Chiffrez vos disques comme suit, en entrant vos propres noms de paramètre :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-138">Encrypt your disks as follows, entering your own parameter names throughout:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="5f8f2-139">L’interface CLI Azure ne fournit pas le détail des erreurs au cours du processus de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-139">The Azure CLI doesn't provide verbose errors during the encryption process.</span></span> <span data-ttu-id="5f8f2-140">Pour obtenir plus d’informations de dépannage, consultez `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-140">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span></span> <span data-ttu-id="5f8f2-141">Comme la commande précédente comporte plusieurs variables et que vous risquez de ne pas pouvoir identifier avec précision l’origine de l’échec du processus, voici un exemple de commande complet :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-141">As the preceding command has many variables and you may not get much indication as to why the process fails, a complete command example would be as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

<span data-ttu-id="5f8f2-142">Pour terminer, réexaminez l’état de chiffrement pour confirmer que vos disques virtuels ont bien été chiffrés.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-142">Finally, review the encryption status again to confirm that your virtual disks have now been encrypted.</span></span> <span data-ttu-id="5f8f2-143">L’exemple suivant vérifie l’état d’une machine virtuelle nommée `myVM` dans le groupe de ressources `myResourceGroup` :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-143">The following example checks the status of a VM named `myVM` in the `myResourceGroup` resource group:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="5f8f2-144">Présentation du chiffrement de disque</span><span class="sxs-lookup"><span data-stu-id="5f8f2-144">Overview of disk encryption</span></span>
<span data-ttu-id="5f8f2-145">Les disques virtuels sur des machines virtuelles Linux sont chiffrés au repos à l’aide de la commande [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="5f8f2-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="5f8f2-146">Le chiffrement de disques virtuels dans Azure n’entraîne aucun frais.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="5f8f2-147">Les clés de chiffrement sont stockées dans le coffre de clés Azure à l’aide d’une protection logicielle, mais vous pouvez importer ou générer vos clés dans des modules de sécurité matériels (HSM) certifiés conformes aux normes FIPS 140-2 de niveau 2.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified to FIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="5f8f2-148">Vous gardez le contrôle de ces clés de chiffrement et pouvez effectuer un audit de leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="5f8f2-149">Ces clés de chiffrement servent à chiffrer et à déchiffrer les disques virtuels connectés à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-149">These cryptographic keys are used to encrypt and decrypt virtual disks attached to your VM.</span></span> <span data-ttu-id="5f8f2-150">Un point de terminaison Azure Active Directory fournit un mécanisme sécurisé pour l’émission de ces clés de chiffrement lors de la mise sous tension et hors tension des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-150">An Azure Active Directory endpoint provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="5f8f2-151">Le processus de chiffrement d’une machine virtuelle est le suivant :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-151">The process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="5f8f2-152">Créez une clé de chiffrement dans un coffre de clés Azure.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="5f8f2-153">Configurez la clé de chiffrement afin de la rendre utilisable pour le chiffrement des disques.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-153">Configure the cryptographic key to be usable for encrypting disks.</span></span>
3. <span data-ttu-id="5f8f2-154">Pour lire la clé de chiffrement à partir du coffre de clés Azure, créez un point de terminaison à l’aide d’Azure Active Directory avec les autorisations appropriées.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-154">To read the cryptographic key from the Azure Key Vault, create an endpoint using Azure Active Directory with the appropriate permissions.</span></span>
4. <span data-ttu-id="5f8f2-155">Exécutez la commande pour chiffrer vos disques virtuels, en spécifiant le point de terminaison Azure Active Directory et la clé de chiffrement appropriée à utiliser.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-155">Issue the command to encrypt your virtual disks, specifying the Azure Active Directory endpoint and appropriate cryptographic key to be used.</span></span>
5. <span data-ttu-id="5f8f2-156">Le point de terminaison Azure Active Directory demande la clé de chiffrement requise au coffre de clés Azure.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-156">The Azure Active Directory endpoint requests the required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="5f8f2-157">Les disques virtuels sont chiffrés à l’aide de la clé de chiffrement fournie.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-157">The virtual disks are encrypted using the provided cryptographic key.</span></span>

## <a name="supporting-services-and-encryption-process"></a><span data-ttu-id="5f8f2-158">Services pris en charge et processus de chiffrement</span><span class="sxs-lookup"><span data-stu-id="5f8f2-158">Supporting services and encryption process</span></span>
<span data-ttu-id="5f8f2-159">Le chiffrement de disque s’appuie sur les composants supplémentaires suivants :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-159">Disk encryption relies on the following additional components:</span></span>

* <span data-ttu-id="5f8f2-160">**Coffre de clés Azure** - permet de sauvegarder les clés de chiffrement et les clés secrètes utilisées pour le processus de chiffrement/déchiffrement de disque.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-160">**Azure Key Vault** - used to safeguard cryptographic keys and secrets used for the disk encryption/decryption process.</span></span>
  * <span data-ttu-id="5f8f2-161">Le cas échéant, vous pouvez utiliser un coffre de clés Azure existant.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="5f8f2-162">Vous n’êtes pas obligé de dédier un coffre de clés au chiffrement des disques.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-162">You do not have to dedicate a Key Vault to encrypting disks.</span></span>
  * <span data-ttu-id="5f8f2-163">Pour séparer les limites administratives et la visibilité de la clé, vous pouvez créer un coffre de clés dédié.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-163">To separate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="5f8f2-164">**Azure Active Directory** - gère l’échange sécurisé des clés de chiffrement requises et l’authentification des actions demandées.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-164">**Azure Active Directory** - handles the secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="5f8f2-165">Vous pouvez généralement utiliser une instance Azure Active Directory existante pour héberger votre application.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="5f8f2-166">L’application est plus un point de terminaison permettant aux services de coffre de clés et de machine virtuelle de demander et d’obtenir les clés de chiffrement appropriées.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-166">The application is more of an endpoint for the Key Vault and Virtual Machine services to request and get issued the appropriate cryptographic keys.</span></span> <span data-ttu-id="5f8f2-167">Vous ne développez pas de réelle application qui s’intègre à Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="5f8f2-168">Spécifications et limitations</span><span class="sxs-lookup"><span data-stu-id="5f8f2-168">Requirements and limitations</span></span>
<span data-ttu-id="5f8f2-169">Configuration requise et scénarios pris en charge pour le chiffrement de disque :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="5f8f2-170">Les versions serveur Linux suivantes : Ubuntu, CentOS, SUSE, SUSE Linux Enterprise Server (SLES) et Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-170">The following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="5f8f2-171">Toutes les ressources (par exemple, le coffre de clés, le compte de stockage, la machine virtuelle, etc.) doivent appartenir à la même région et au même abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-171">All resources (such as Key Vault, Storage account, and VM) must be in the same Azure region and subscription.</span></span>
* <span data-ttu-id="5f8f2-172">Machines virtuelles standard des séries A, D, DS, G et GS.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="5f8f2-173">Le chiffrement de disque n’est actuellement pas pris en charge dans les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-173">Disk encryption is not currently supported in the following scenarios:</span></span>

* <span data-ttu-id="5f8f2-174">Machines virtuelles de niveau de base.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-174">Basic tier VMs.</span></span>
* <span data-ttu-id="5f8f2-175">Machines virtuelles créées à l’aide du modèle de déploiement Classic.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-175">VMs created using the Classic deployment model.</span></span>
* <span data-ttu-id="5f8f2-176">Désactivation du chiffrement de disque du système d’exploitation sur les machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="5f8f2-177">Mise à jour des clés de chiffrement sur une machine virtuelle Linux déjà chiffrée.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-177">Updating the cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-the-azure-key-vault-and-keys"></a><span data-ttu-id="5f8f2-178">Créer le coffre de clés Azure et les clés</span><span class="sxs-lookup"><span data-stu-id="5f8f2-178">Create the Azure Key Vault and keys</span></span>
<span data-ttu-id="5f8f2-179">Pour effectuer les étapes restantes de ce guide, la [dernière version d’Azure CLI 1.0](../../xplat-cli-install.md) doit être installée et connectée ainsi, selon le mode Resource Manager :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-179">To complete the remainder of this guide, you need the [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="5f8f2-180">Dans les exemples de commandes, remplacez tous les exemples de paramètres par vos propres noms, emplacement et valeurs de clés.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-180">Throughout the command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="5f8f2-181">Les exemples suivants utilisent une convention de type `myResourceGroup`, `myKeyVault`, `myAADApp`, etc.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-181">The following examples use a convention of `myResourceGroup`, `myKeyVault`, `myAADApp`, etc.</span></span>

<span data-ttu-id="5f8f2-182">La première étape consiste à créer un coffre de clés Azure pour y stocker les clés de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-182">The first step is to create an Azure Key Vault to store your cryptographic keys.</span></span> <span data-ttu-id="5f8f2-183">Un coffre de clés Azure peut stocker des clés, des clés secrètes ou des mots de passe vous permettant de les implémenter en toute sécurité dans vos applications et services.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-183">Azure Key Vault can store keys, secrets, or passwords that allow you to securely implement them in your applications and services.</span></span> <span data-ttu-id="5f8f2-184">Pour le chiffrement de disque virtuel, vous utilisez le coffre de clés afin de stocker une clé de chiffrement pour chiffrer ou déchiffrer vos disques virtuels.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-184">For virtual disk encryption, you use Key Vault to store a cryptographic key that is used to encrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="5f8f2-185">Activez le fournisseur Azure Key Vault au sein de votre abonnement Azure puis créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-185">Enable the Azure Key Vault provider in your Azure subscription, then create a resource group.</span></span> <span data-ttu-id="5f8f2-186">L’exemple suivant crée un groupe de ressources nommé `myResourceGroup` à l’emplacement `WestUS` :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-186">The following example creates a resource group named `myResourceGroup` in the `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="5f8f2-187">Le coffre de clés Azure contenant les clés de chiffrement et les ressources de calcul associées tels que le stockage et la machine virtuelle elle-même doit résider dans la même région.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-187">The Azure Key Vault containing the cryptographic keys and associated compute resources such as storage and the VM itself must reside in the same region.</span></span> <span data-ttu-id="5f8f2-188">L’exemple qui suit permet de créer un coffre de clés Azure nommé `myKeyVault` :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-188">The following example creates an Azure Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="5f8f2-189">Vous pouvez stocker des clés de chiffrement à l’aide d’une protection logicielle ou HSM (modèle de sécurité matériel).</span><span class="sxs-lookup"><span data-stu-id="5f8f2-189">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="5f8f2-190">L’utilisation d’une protection HSM nécessite un coffre de clés Premium.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-190">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="5f8f2-191">Contrairement à l’utilisation d’un coffre de clés standard qui stocke les clés protégées par logiciel, la création d’un coffre de clés Premium entraîne des frais.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-191">There is an additional cost to creating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="5f8f2-192">Pour créer un coffre de clés Premium, ajoutez `--sku Premium` à la commande de l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-192">To create a premium Key Vault, in the preceding step add `--sku Premium` to the command.</span></span> <span data-ttu-id="5f8f2-193">L’exemple suivant utilise des clés protégées par logiciel puisque nous avons créé un coffre de clés standard.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-193">The following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="5f8f2-194">Pour les deux modèles de protection, la plateforme Azure doit être autorisée à demander les clés de chiffrement lorsque la machine virtuelle démarre pour déchiffrer les disques virtuels.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-194">For both protection models, the Azure platform needs to be granted access to request the cryptographic keys when the VM boots to decrypt the virtual disks.</span></span> <span data-ttu-id="5f8f2-195">Créez une clé de chiffrement dans votre coffre de clés, puis activez-la afin de l’utiliser pour le chiffrement de disque virtuel.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-195">Create an encryption key within your Key Vault, then enable it for use with virtual disk encryption.</span></span> <span data-ttu-id="5f8f2-196">L’exemple suivant crée une clé nommée `myKey` puis l’active pour le chiffrement de disque :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-196">The following example creates a key named `myKey` and then enables it for disk encryption:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-the-azure-active-directory-application"></a><span data-ttu-id="5f8f2-197">Création de l’application Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5f8f2-197">Create the Azure Active Directory application</span></span>
<span data-ttu-id="5f8f2-198">Lorsque des disques virtuels sont chiffrés ou déchiffrés, vous utilisez un point de terminaison pour gérer l’authentification et l’échange de clés de chiffrement à partir du coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-198">When virtual disks are encrypted or decrypted, you use an endpoint to handle the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="5f8f2-199">Ce point de terminaison, une application Azure Active Directory, permet à la plateforme Azure de demander les clés de chiffrement appropriées pour le compte de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-199">This endpoint, an Azure Active Directory application, allows the Azure platform to request the appropriate cryptographic keys on behalf of the VM.</span></span> <span data-ttu-id="5f8f2-200">Une instance Azure Active Directory par défaut est disponible dans votre abonnement, bien que de nombreuses organisations utilisent des répertoires Azure Active Directory dédiés.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-200">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="5f8f2-201">Comme vous ne créez pas une application Azure Active Directory complète, les paramètres `--home-page` et `--identifier-uris` de l’exemple suivant n’ont pas besoin de représenter des adresses routables réelles.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-201">As you are not creating a full Azure Active Directory application, the `--home-page` and `--identifier-uris` parameters in the following example do not need to be actual routable address.</span></span> <span data-ttu-id="5f8f2-202">L’exemple suivant utilise également un mot de passe au lieu de générer des clés à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-202">The following example also specifies a password-based secret rather than generating keys from within the Azure portal.</span></span> <span data-ttu-id="5f8f2-203">Pour le moment, la génération de clés ne peut pas être effectuée à partir de l’interface CLI Azure.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-203">As this time, generating keys cannot be done from the Azure CLI.</span></span>

<span data-ttu-id="5f8f2-204">Créez votre application Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-204">Create your Azure Active Directory application.</span></span> <span data-ttu-id="5f8f2-205">L’exemple suivant crée une application nommée `myAADApp` et utilise un mot de passe `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-205">The following example creates an application named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="5f8f2-206">Spécifiez votre propre mot de passe comme suit :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-206">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="5f8f2-207">Notez la valeur `applicationId` retournée dans le résultat de la commande précédente.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-207">Make a note of the `applicationId` that is returned in the output from the preceding command.</span></span> <span data-ttu-id="5f8f2-208">Cet ID d’application est utilisé dans les étapes restantes.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-208">This application ID is used in some of the remaining steps.</span></span> <span data-ttu-id="5f8f2-209">Créez ensuite un nom de principal de service (SPN) afin que l’application soit accessible au sein de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-209">Next, create a service principal name (SPN) so that the application is accessible within your environment.</span></span> <span data-ttu-id="5f8f2-210">Pour chiffrer ou déchiffrer correctement des disques virtuels, des autorisations d’accès à la clé de chiffrement stockée dans le coffre de clés doivent être définies afin que l’application Azure Active Directory puisse lire les clés.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-210">To successfully encrypt or decrypt virtual disks, permissions on the cryptographic key stored in Key Vault must be set to permit the Azure Active Directory application to read the keys.</span></span>

<span data-ttu-id="5f8f2-211">Créez le SPN et définissez les autorisations appropriées comme suit :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-211">Create the SPN and set the appropriate permissions as follows:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a><span data-ttu-id="5f8f2-212">Ajouter un disque virtuel et vérifier l’état de chiffrement</span><span class="sxs-lookup"><span data-stu-id="5f8f2-212">Add a virtual disk and review encryption status</span></span>
<span data-ttu-id="5f8f2-213">Pour chiffrer réellement certains disques virtuels, ajoutons un disque à une machine virtuelle existante.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-213">To actually encrypt some virtual disks, lets add a disk to an existing VM.</span></span> <span data-ttu-id="5f8f2-214">Ajoutez un disque de données de 5 Go à une machine virtuelle existante comme suit :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-214">Add a 5Gb data disk to an existing VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="5f8f2-215">Actuellement, les disques virtuels ne sont pas chiffrés.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-215">The virtual disks are not currently encrypted.</span></span> <span data-ttu-id="5f8f2-216">Vérifiez l’état de chiffrement de votre machine virtuelle comme suit :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-216">Review the current encryption status of your VM as follows:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a><span data-ttu-id="5f8f2-217">Chiffrer des disques virtuels</span><span class="sxs-lookup"><span data-stu-id="5f8f2-217">Encrypt virtual disks</span></span>
<span data-ttu-id="5f8f2-218">Pour chiffrer maintenant les disques virtuels, vous allez réunir tous les composants précédents :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-218">To now encrypt the virtual disks, you bring together all the previous components:</span></span>

1. <span data-ttu-id="5f8f2-219">Spécifiez l’application et le mot de passe Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-219">Specify the Azure Active Directory application and password.</span></span>
2. <span data-ttu-id="5f8f2-220">Spécifiez le coffre de clés qui stockera les métadonnées de vos disques chiffrés.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-220">Specify the Key Vault to store the metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="5f8f2-221">Spécifiez les clés de chiffrement à utiliser pour le chiffrement et le déchiffrement réels.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-221">Specify the cryptographic keys to use for the actual encryption and decryption.</span></span>
4. <span data-ttu-id="5f8f2-222">Indiquez si vous souhaitez chiffrer le disque du système d’exploitation, les disques de données ou l’ensemble.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-222">Specify whether you want to encrypt the OS disk, the data disks, or all.</span></span>

<span data-ttu-id="5f8f2-223">Examinons en détail votre coffre de clés Azure et la clé que vous avez créée car vous aurez besoin de l’ID du coffre de clé, de l’URI et de l’URL de la clé à la dernière étape :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-223">Lets review the details for your Azure Key Vault and the key you created, as you need the Key Vault ID, URI, and then key URL in the final step:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="5f8f2-224">Chiffrez vos disques virtuels à l’aide du résultat des commandes `azure keyvault show` et `azure keyvault key show` comme suit :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-224">Encrypt your virtual disks using the output from the `azure keyvault show` and `azure keyvault key show` commands as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="5f8f2-225">La commande précédente comportant plusieurs variables, l’exemple suivant sert de commande de référence :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-225">As the preceding command has many variables, the following example is the complete command for reference:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

<span data-ttu-id="5f8f2-226">L’interface CLI Azure ne fournit pas le détail des erreurs au cours du processus de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-226">The Azure CLI doesn't provide verbose errors during the encryption process.</span></span> <span data-ttu-id="5f8f2-227">Pour plus d’informations de dépannage, consultez `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` sur la machine virtuelle que vous chiffrez.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-227">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` on the VM you are encrypting.</span></span>

<span data-ttu-id="5f8f2-228">Pour terminer, réexaminez l’état de chiffrement pour confirmer que vos disques virtuels ont bien été chiffrés :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-228">Finally, lets review the encryption status again to confirm that your virtual disks have now been encrypted:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a><span data-ttu-id="5f8f2-229">Ajouter des disques de données supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5f8f2-229">Add additional data disks</span></span>
<span data-ttu-id="5f8f2-230">Une fois que vous avez chiffré vos disques de données, vous pouvez ajouter ultérieurement d’autres disques virtuels à votre machine virtuelle et également les chiffrer.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-230">Once you have encrypted your data disks, you can later add additional virtual disks to your VM and also encrypt them.</span></span> <span data-ttu-id="5f8f2-231">Lorsque vous exécutez la commande `azure vm enable-disk-encryption`, incrémentez la version de la séquence à l’aide du paramètre `--sequence-version`.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-231">When you run the `azure vm enable-disk-encryption` command, increment the sequence version using the `--sequence-version` parameter.</span></span> <span data-ttu-id="5f8f2-232">Ce paramètre de version de séquence permet d’effectuer des opérations répétées sur la même machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5f8f2-232">This sequence version parameter allows you to perform repeated operations on the same VM.</span></span>

<span data-ttu-id="5f8f2-233">Par exemple, ajoutons un second disque virtuel à votre machine virtuelle comme suit :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-233">For example, lets add a second virtual disk to your VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="5f8f2-234">Réexécutez la commande pour chiffrer les disques virtuels, cette fois en ajoutant le paramètre `--sequence-version` et en incrémentant la valeur de notre première exécution comme suit :</span><span class="sxs-lookup"><span data-stu-id="5f8f2-234">Rerun the command to encrypt the virtual disks, this time adding the `--sequence-version` parameter, and incrementing the value from our first run as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
  --sequence-version 2
```


## <a name="next-steps"></a><span data-ttu-id="5f8f2-235">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5f8f2-235">Next steps</span></span>
* <span data-ttu-id="5f8f2-236">Pour plus d’informations sur la gestion du coffre de clés Azure, y compris la suppression des clés de chiffrement et des coffres, consultez [Gérer le coffre de clés à l’aide de l’interface de ligne de commande](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="5f8f2-236">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="5f8f2-237">Pour plus d’informations sur le chiffrement de disque, notamment la préparation d’une machine virtuelle personnalisée chiffrée à télécharger vers Azure, consultez [Chiffrement de disque Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="5f8f2-237">For more information about disk encryption, such as preparing an encrypted custom VM to upload to Azure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
