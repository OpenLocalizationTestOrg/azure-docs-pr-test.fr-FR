---
title: disques aaaEncrypt sur un VM Linux avec hello Azure CLI 1.0 | Documents Microsoft
description: "Comment un VM Linux à l’aide de disques tooencrypt hello Azure CLI 1.0 et le modèle de déploiement du Gestionnaire de ressources hello"
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
ms.openlocfilehash: 68a0394d366c3c6941e2c6db0d4263123f951946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-disks-on-a-linux-vm-using-hello-azure-cli-10"></a><span data-ttu-id="15d64-103">Chiffrer les disques sur un VM Linux à l’aide de hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="15d64-103">Encrypt disks on a Linux VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="15d64-104">Pour renforcer la sécurité et la conformité de la machine virtuelle , les disques virtuels dans Azure peuvent être chiffrés au repos.</span><span class="sxs-lookup"><span data-stu-id="15d64-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted at rest.</span></span> <span data-ttu-id="15d64-105">Les disques sont chiffrés à l’aide de clés de chiffrement sécurisées dans un coffre de clés Azure.</span><span class="sxs-lookup"><span data-stu-id="15d64-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="15d64-106">Vous contrôlez ces clés de chiffrement et pouvez effectuer un audit de leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="15d64-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="15d64-107">Cet article décrit en détail comment tooencrypt des disques virtuels sur un VM Linux à l’aide de hello Azure CLI 1.0 et le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="15d64-107">This article details how tooencrypt virtual disks on a Linux VM using hello Azure CLI 1.0 and hello Resource Manager deployment model.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="15d64-108">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="15d64-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="15d64-109">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="15d64-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="15d64-110">[Azure CLI 1.0](#quick-commands) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)</span><span class="sxs-lookup"><span data-stu-id="15d64-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="15d64-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello</span><span class="sxs-lookup"><span data-stu-id="15d64-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="15d64-112">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="15d64-112">Quick commands</span></span>
<span data-ttu-id="15d64-113">Si vous avez besoin de tooquickly accomplir la tâche hello, hello suivant hello de détails section base commandes tooencrypt disques virtuels présents sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="15d64-113">If you need tooquickly accomplish hello task, hello following section details hello base commands tooencrypt virtual disks on your VM.</span></span> <span data-ttu-id="15d64-114">Plus d’informations et le contexte de chaque étape se trouve reste hello du document de hello, [Démarrer ici](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="15d64-114">More detailed information and context for each step can be found hello rest of hello document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="15d64-115">Vous devez hello [dernière Azure CLI 1.0](../../xplat-cli-install.md) installé et connecté à l’aide de mode de gestionnaire de ressources hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="15d64-115">You need hello [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="15d64-116">Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="15d64-116">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="15d64-117">Exemples de noms de paramètre : `myResourceGroup`, `myKeyVault` et `myVM`.</span><span class="sxs-lookup"><span data-stu-id="15d64-117">Example parameter names include `myResourceGroup`, `myKeyVault`, and `myVM`.</span></span>

<span data-ttu-id="15d64-118">D’abord activer le fournisseur de coffre de clés Azure hello dans votre abonnement Azure et créer un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="15d64-118">First, enable hello Azure Key Vault provider within your Azure subscription and create a resource group.</span></span> <span data-ttu-id="15d64-119">Hello exemple suivant crée un nom de groupe de ressources `myResourceGroup` Bonjour `WestUS` emplacement :</span><span class="sxs-lookup"><span data-stu-id="15d64-119">hello following example creates a resource group name `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="15d64-120">Créez un coffre de clés Azure.</span><span class="sxs-lookup"><span data-stu-id="15d64-120">Create an Azure Key Vault.</span></span> <span data-ttu-id="15d64-121">Hello exemple suivant crée un coffre de clés nommé `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="15d64-121">hello following example creates a Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="15d64-122">Créez une clé de chiffrement dans le coffre de clés et activez-la pour le chiffrement du disque.</span><span class="sxs-lookup"><span data-stu-id="15d64-122">Create a cryptographic key in your Key Vault and enable it for disk encryption.</span></span> <span data-ttu-id="15d64-123">Hello exemple suivant crée une clé nommée `myKey`:</span><span class="sxs-lookup"><span data-stu-id="15d64-123">hello following example creates a key named `myKey`:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

<span data-ttu-id="15d64-124">Créer un point de terminaison à l’aide d’Azure Active Directory pour la gestion de l’authentification de hello et l’échange de clés de chiffrement à partir du coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="15d64-124">Create an endpoint using Azure Active Directory for handling hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="15d64-125">Hello `--home-page` et `--identifier-uris` n’avez pas besoin d’adresse routable toobe.</span><span class="sxs-lookup"><span data-stu-id="15d64-125">hello `--home-page` and `--identifier-uris` do not need toobe actual routable address.</span></span> <span data-ttu-id="15d64-126">Hello plus haut niveau de sécurité, les clés secrètes client doivent être utilisés à la place des mots de passe.</span><span class="sxs-lookup"><span data-stu-id="15d64-126">For hello highest level of security, client secrets should be used instead of passwords.</span></span> <span data-ttu-id="15d64-127">Hello CLI d’Azure actuellement ne peut pas générer des clés secrètes client.</span><span class="sxs-lookup"><span data-stu-id="15d64-127">hello Azure CLI cannot currently generate client secrets.</span></span> <span data-ttu-id="15d64-128">Clés secrètes client ne peuvent pas être générés dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="15d64-128">Client secrets can only be generated in hello Azure portal.</span></span> <span data-ttu-id="15d64-129">Hello exemple suivant crée un point de terminaison Azure Active Directory nommé `myAADApp` et utilise un mot de passe de `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="15d64-129">hello following example creates an Azure Active Directory endpoint named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="15d64-130">Spécifiez votre propre mot de passe comme suit :</span><span class="sxs-lookup"><span data-stu-id="15d64-130">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="15d64-131">Hello de note `applicationId` indiqué dans la sortie de hello de hello précédant la commande.</span><span class="sxs-lookup"><span data-stu-id="15d64-131">Note hello `applicationId` shown in hello output from hello preceding command.</span></span> <span data-ttu-id="15d64-132">Cet ID d’application est utilisé dans hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="15d64-132">This application ID is used in hello following steps:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

<span data-ttu-id="15d64-133">Ajouter un tooan de disque de données existante de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="15d64-133">Add a data disk tooan existing VM.</span></span> <span data-ttu-id="15d64-134">Hello exemple suivant ajoute un tooa de disque de données machine virtuelle nommée `myVM`:</span><span class="sxs-lookup"><span data-stu-id="15d64-134">hello following example adds a data disk tooa VM named `myVM`:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="15d64-135">Passez en revue les détails de hello pour votre clé de coffre de clés et hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="15d64-135">Review hello details for your Key Vault and hello key you created.</span></span> <span data-ttu-id="15d64-136">Vous devez hello ID de clé de coffre, URI et clé de l’URL à l’étape finale de hello.</span><span class="sxs-lookup"><span data-stu-id="15d64-136">You need hello Key Vault ID, URI, and key URL in hello final step.</span></span> <span data-ttu-id="15d64-137">Hello exemple suivant passe en revue les détails de hello pour un coffre de clés nommé `myKeyVault` et la clé nommée `myKey`:</span><span class="sxs-lookup"><span data-stu-id="15d64-137">hello following example reviews hello details for a Key Vault named `myKeyVault` and key named `myKey`:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="15d64-138">Chiffrez vos disques comme suit, en entrant vos propres noms de paramètre :</span><span class="sxs-lookup"><span data-stu-id="15d64-138">Encrypt your disks as follows, entering your own parameter names throughout:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="15d64-139">Hello CLI d’Azure ne fournit pas des erreurs détaillées au cours du processus de chiffrement hello.</span><span class="sxs-lookup"><span data-stu-id="15d64-139">hello Azure CLI doesn't provide verbose errors during hello encryption process.</span></span> <span data-ttu-id="15d64-140">Pour obtenir plus d’informations de dépannage, consultez `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span><span class="sxs-lookup"><span data-stu-id="15d64-140">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span></span> <span data-ttu-id="15d64-141">En tant que hello précédant la commande a plusieurs variables et vous n’obtiendrez pas quantité indication as toowhy hello processus échoue, un exemple de commande complète se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="15d64-141">As hello preceding command has many variables and you may not get much indication as toowhy hello process fails, a complete command example would be as follows:</span></span>

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

<span data-ttu-id="15d64-142">Enfin, vérifiez le statut de chiffrement hello à nouveau les tooconfirm que vos disques virtuels ont désormais été chiffrés.</span><span class="sxs-lookup"><span data-stu-id="15d64-142">Finally, review hello encryption status again tooconfirm that your virtual disks have now been encrypted.</span></span> <span data-ttu-id="15d64-143">exemple Hello vérifie état hello d’un ordinateur virtuel nommé `myVM` Bonjour `myResourceGroup` groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="15d64-143">hello following example checks hello status of a VM named `myVM` in hello `myResourceGroup` resource group:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="15d64-144">Présentation du chiffrement de disque</span><span class="sxs-lookup"><span data-stu-id="15d64-144">Overview of disk encryption</span></span>
<span data-ttu-id="15d64-145">Les disques virtuels sur des machines virtuelles Linux sont chiffrés au repos à l’aide de la commande [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="15d64-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="15d64-146">Le chiffrement de disques virtuels dans Azure n’entraîne aucun frais.</span><span class="sxs-lookup"><span data-stu-id="15d64-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="15d64-147">Clés de chiffrement sont stockées dans le coffre de clés Azure à l’aide du logiciel de protection, ou vous pouvez importer ou générer vos clés dans des Modules de sécurité matériel (HSM) certifié tooFIPS normes de niveau 2 140-2.</span><span class="sxs-lookup"><span data-stu-id="15d64-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="15d64-148">Vous gardez le contrôle de ces clés de chiffrement et pouvez effectuer un audit de leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="15d64-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="15d64-149">Ces clés de chiffrement sont utilisé tooencrypt et déchiffrement tooyour de disques virtuels attachés machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="15d64-149">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="15d64-150">Un point de terminaison Azure Active Directory fournit un mécanisme sécurisé pour l’émission de ces clés de chiffrement lors de la mise sous tension et hors tension des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="15d64-150">An Azure Active Directory endpoint provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="15d64-151">processus de Hello de chiffrement d’une machine virtuelle est la suivante :</span><span class="sxs-lookup"><span data-stu-id="15d64-151">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="15d64-152">Créez une clé de chiffrement dans un coffre de clés Azure.</span><span class="sxs-lookup"><span data-stu-id="15d64-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="15d64-153">Configurer hello chiffrement clé toobe utilisable pour le chiffrement des disques.</span><span class="sxs-lookup"><span data-stu-id="15d64-153">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="15d64-154">clé de chiffrement hello tooread de hello Azure Key Vault, créez un point de terminaison à l’aide d’Azure Active Directory disposant des autorisations appropriées de hello.</span><span class="sxs-lookup"><span data-stu-id="15d64-154">tooread hello cryptographic key from hello Azure Key Vault, create an endpoint using Azure Active Directory with hello appropriate permissions.</span></span>
4. <span data-ttu-id="15d64-155">Émettre hello commande tooencrypt vos disques virtuels, en spécifiant le point de terminaison de hello Azure Active Directory et appropriée toobe de clés cryptographique utilisé.</span><span class="sxs-lookup"><span data-stu-id="15d64-155">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory endpoint and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="15d64-156">point de terminaison de Azure Active Directory Hello demande la clé de chiffrement requis hello dans Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="15d64-156">hello Azure Active Directory endpoint requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="15d64-157">les disques virtuels Hello sont chiffrées à l’aide de la clé de chiffrement hello fourni.</span><span class="sxs-lookup"><span data-stu-id="15d64-157">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="supporting-services-and-encryption-process"></a><span data-ttu-id="15d64-158">Services pris en charge et processus de chiffrement</span><span class="sxs-lookup"><span data-stu-id="15d64-158">Supporting services and encryption process</span></span>
<span data-ttu-id="15d64-159">Chiffrement de disque s’appuie sur hello suivant des composants supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="15d64-159">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="15d64-160">**Azure Key Vault** -utilisé toosafeguard les clés de chiffrement et les secrets utilisés pour le processus de chiffrement/déchiffrement de disque hello.</span><span class="sxs-lookup"><span data-stu-id="15d64-160">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span>
  * <span data-ttu-id="15d64-161">Le cas échéant, vous pouvez utiliser un coffre de clés Azure existant.</span><span class="sxs-lookup"><span data-stu-id="15d64-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="15d64-162">Vous n’avez pas de le toodedicate un disques tooencrypting de coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="15d64-162">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="15d64-163">les limites administratives tooseparate et la visibilité de clé, vous pouvez créer un coffre de clés dédié.</span><span class="sxs-lookup"><span data-stu-id="15d64-163">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="15d64-164">**Azure Active Directory** - handles hello échange sécurisé de clés de chiffrement requis et l’authentification pour demandé d’actions.</span><span class="sxs-lookup"><span data-stu-id="15d64-164">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="15d64-165">Vous pouvez généralement utiliser une instance Azure Active Directory existante pour héberger votre application.</span><span class="sxs-lookup"><span data-stu-id="15d64-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="15d64-166">application Hello est plus d’un point de terminaison pour hello coffre de clés et de Virtual Machine services toorequest et obtenir émis des clés de chiffrement appropriées hello.</span><span class="sxs-lookup"><span data-stu-id="15d64-166">hello application is more of an endpoint for hello Key Vault and Virtual Machine services toorequest and get issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="15d64-167">Vous ne développez pas de réelle application qui s’intègre à Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="15d64-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="15d64-168">Spécifications et limitations</span><span class="sxs-lookup"><span data-stu-id="15d64-168">Requirements and limitations</span></span>
<span data-ttu-id="15d64-169">Configuration requise et scénarios pris en charge pour le chiffrement de disque :</span><span class="sxs-lookup"><span data-stu-id="15d64-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="15d64-170">Hello suivant serveur Linux SKU - Ubuntu, CentOS, SUSE et SUSE Linux Enterprise Server (SLES) et Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="15d64-170">hello following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="15d64-171">Toutes les ressources (telles que le coffre de clés, le compte de stockage et machine virtuelle) doivent être Bonjour même région Azure et abonnement.</span><span class="sxs-lookup"><span data-stu-id="15d64-171">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="15d64-172">Machines virtuelles standard des séries A, D, DS, G et GS.</span><span class="sxs-lookup"><span data-stu-id="15d64-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="15d64-173">Chiffrement de disque n’est pas pris en charge dans hello les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="15d64-173">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="15d64-174">Machines virtuelles de niveau de base.</span><span class="sxs-lookup"><span data-stu-id="15d64-174">Basic tier VMs.</span></span>
* <span data-ttu-id="15d64-175">Machines virtuelles créées à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="15d64-175">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="15d64-176">Désactivation du chiffrement de disque du système d’exploitation sur les machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="15d64-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="15d64-177">Mise à jour des clés de chiffrement hello sur une VM Linux déjà chiffré.</span><span class="sxs-lookup"><span data-stu-id="15d64-177">Updating hello cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-hello-azure-key-vault-and-keys"></a><span data-ttu-id="15d64-178">Créer hello Azure Key Vault et des clés</span><span class="sxs-lookup"><span data-stu-id="15d64-178">Create hello Azure Key Vault and keys</span></span>
<span data-ttu-id="15d64-179">suite de hello toocomplete de ce guide, vous devez hello [dernière Azure CLI 1.0](../../xplat-cli-install.md) installé et connecté à l’aide de mode de gestionnaire de ressources hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="15d64-179">toocomplete hello remainder of this guide, you need hello [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="15d64-180">Dans l’ensemble des exemples de commandes hello, remplacer tous les paramètres de l’exemple avec votre propre nom, l’emplacement et valeurs de clés.</span><span class="sxs-lookup"><span data-stu-id="15d64-180">Throughout hello command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="15d64-181">Hello exemples suivants utilisent une convention de `myResourceGroup`, `myKeyVault`, `myAADApp`, etc..</span><span class="sxs-lookup"><span data-stu-id="15d64-181">hello following examples use a convention of `myResourceGroup`, `myKeyVault`, `myAADApp`, etc.</span></span>

<span data-ttu-id="15d64-182">première étape de Hello est toocreate un toostore Azure Key Vault vos clés de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="15d64-182">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="15d64-183">Coffre de clés Azure peuvent stocker des clés, des secrets, ou les mots de passe qui vous permettent de toosecurely leur implémentent dans vos applications et services.</span><span class="sxs-lookup"><span data-stu-id="15d64-183">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="15d64-184">Pour le chiffrement de disque virtuel, vous utilisez le coffre de clés toostore une clé de chiffrement qui est utilisé tooencrypt ou déchiffrer vos disques virtuels.</span><span class="sxs-lookup"><span data-stu-id="15d64-184">For virtual disk encryption, you use Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="15d64-185">Activer le fournisseur de coffre de clés Azure hello dans votre abonnement Azure, puis créer un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="15d64-185">Enable hello Azure Key Vault provider in your Azure subscription, then create a resource group.</span></span> <span data-ttu-id="15d64-186">Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` Bonjour `WestUS` emplacement :</span><span class="sxs-lookup"><span data-stu-id="15d64-186">hello following example creates a resource group named `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="15d64-187">Bonjour Azure Key Vault contenant hello clés de chiffrement et calcul associée ressources telles que le stockage et hello machine virtuelle proprement dite doivent résider dans hello même région.</span><span class="sxs-lookup"><span data-stu-id="15d64-187">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="15d64-188">Hello exemple suivant crée un coffre de clés Azure nommé `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="15d64-188">hello following example creates an Azure Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="15d64-189">Vous pouvez stocker des clés de chiffrement à l’aide d’une protection logicielle ou HSM (modèle de sécurité matériel).</span><span class="sxs-lookup"><span data-stu-id="15d64-189">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="15d64-190">L’utilisation d’une protection HSM nécessite un coffre de clés Premium.</span><span class="sxs-lookup"><span data-stu-id="15d64-190">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="15d64-191">Il est un toocreating coût supplémentaire un coffre de clés plutôt que le coffre de clés standard qui stocke les clés protégées par logiciel.</span><span class="sxs-lookup"><span data-stu-id="15d64-191">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="15d64-192">toocreate un coffre de clés, premium Bonjour précédant l’étape ajouter `--sku Premium` toohello commande.</span><span class="sxs-lookup"><span data-stu-id="15d64-192">toocreate a premium Key Vault, in hello preceding step add `--sku Premium` toohello command.</span></span> <span data-ttu-id="15d64-193">Hello exemple suivant utilise des clés de protection logicielle étant donné que nous avons créé un coffre de clés standard.</span><span class="sxs-lookup"><span data-stu-id="15d64-193">hello following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="15d64-194">Les modèles de protection, hello plateforme Azure doit toobe accordé accès toorequest les clés de chiffrement hello lorsque hello machine virtuelle démarre les disques virtuels toodecrypt hello.</span><span class="sxs-lookup"><span data-stu-id="15d64-194">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="15d64-195">Créez une clé de chiffrement dans votre coffre de clés, puis activez-la afin de l’utiliser pour le chiffrement de disque virtuel.</span><span class="sxs-lookup"><span data-stu-id="15d64-195">Create an encryption key within your Key Vault, then enable it for use with virtual disk encryption.</span></span> <span data-ttu-id="15d64-196">Hello exemple suivant crée une clé nommée `myKey` , puis l’active pour le chiffrement de disque :</span><span class="sxs-lookup"><span data-stu-id="15d64-196">hello following example creates a key named `myKey` and then enables it for disk encryption:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-hello-azure-active-directory-application"></a><span data-ttu-id="15d64-197">Créer l’application Azure Active Directory de hello</span><span class="sxs-lookup"><span data-stu-id="15d64-197">Create hello Azure Active Directory application</span></span>
<span data-ttu-id="15d64-198">Lorsque les disques virtuels sont chiffrées ou déchiffrées, vous utilisez une authentification de hello toohandle point de terminaison et l’échange de clés de chiffrement à partir du coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="15d64-198">When virtual disks are encrypted or decrypted, you use an endpoint toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="15d64-199">Ce point de terminaison, une application Azure Active Directory, permet de clés de chiffrement approprié hello pour le compte hello VM toorequest de plateforme Windows Azure hello.</span><span class="sxs-lookup"><span data-stu-id="15d64-199">This endpoint, an Azure Active Directory application, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="15d64-200">Une instance Azure Active Directory par défaut est disponible dans votre abonnement, bien que de nombreuses organisations utilisent des répertoires Azure Active Directory dédiés.</span><span class="sxs-lookup"><span data-stu-id="15d64-200">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="15d64-201">Comme vous ne créez pas une application Azure Active Directory complet, hello `--home-page` et `--identifier-uris` paramètres Bonjour exemple suivant n’est pas nécessaire d’adresse routable toobe.</span><span class="sxs-lookup"><span data-stu-id="15d64-201">As you are not creating a full Azure Active Directory application, hello `--home-page` and `--identifier-uris` parameters in hello following example do not need toobe actual routable address.</span></span> <span data-ttu-id="15d64-202">Hello exemple suivant spécifie également un mot de passe secret plutôt que des clés génération à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="15d64-202">hello following example also specifies a password-based secret rather than generating keys from within hello Azure portal.</span></span> <span data-ttu-id="15d64-203">En tant que cette fois-ci, génération de clés n’est pas possible de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="15d64-203">As this time, generating keys cannot be done from hello Azure CLI.</span></span>

<span data-ttu-id="15d64-204">Créez votre application Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="15d64-204">Create your Azure Active Directory application.</span></span> <span data-ttu-id="15d64-205">Hello exemple suivant crée une application nommée `myAADApp` et utilise un mot de passe de `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="15d64-205">hello following example creates an application named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="15d64-206">Spécifiez votre propre mot de passe comme suit :</span><span class="sxs-lookup"><span data-stu-id="15d64-206">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="15d64-207">Prenez note de hello `applicationId` qui est retourné dans la sortie de hello par hello précédant la commande.</span><span class="sxs-lookup"><span data-stu-id="15d64-207">Make a note of hello `applicationId` that is returned in hello output from hello preceding command.</span></span> <span data-ttu-id="15d64-208">Cet ID d’application est utilisé dans certains hello restant comme suit.</span><span class="sxs-lookup"><span data-stu-id="15d64-208">This application ID is used in some of hello remaining steps.</span></span> <span data-ttu-id="15d64-209">Ensuite, créez un nom principal de service (SPN) pour que l’application hello est accessible au sein de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="15d64-209">Next, create a service principal name (SPN) so that hello application is accessible within your environment.</span></span> <span data-ttu-id="15d64-210">toosuccessfully chiffrer ou déchiffrer des disques virtuels, les autorisations sur la clé de chiffrement hello stockées dans le coffre de clés doivent être tooread hello clés d’application Azure Active Directory ensemble toopermit hello.</span><span class="sxs-lookup"><span data-stu-id="15d64-210">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory application tooread hello keys.</span></span>

<span data-ttu-id="15d64-211">Créer hello SPN et définissez les autorisations appropriées de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="15d64-211">Create hello SPN and set hello appropriate permissions as follows:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a><span data-ttu-id="15d64-212">Ajouter un disque virtuel et vérifier l’état de chiffrement</span><span class="sxs-lookup"><span data-stu-id="15d64-212">Add a virtual disk and review encryption status</span></span>
<span data-ttu-id="15d64-213">tooactually chiffrer certains disques virtuels, permet d’ajouter un tooan de disque existant de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="15d64-213">tooactually encrypt some virtual disks, lets add a disk tooan existing VM.</span></span> <span data-ttu-id="15d64-214">Ajouter un tooan de disque de données de 5 Go existante de machine virtuelle comme suit :</span><span class="sxs-lookup"><span data-stu-id="15d64-214">Add a 5Gb data disk tooan existing VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="15d64-215">les disques virtuels Hello ne sont pas actuellement chiffrés.</span><span class="sxs-lookup"><span data-stu-id="15d64-215">hello virtual disks are not currently encrypted.</span></span> <span data-ttu-id="15d64-216">Passez en revue hello état actuel du chiffrement de votre machine virtuelle comme suit :</span><span class="sxs-lookup"><span data-stu-id="15d64-216">Review hello current encryption status of your VM as follows:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a><span data-ttu-id="15d64-217">Chiffrer des disques virtuels</span><span class="sxs-lookup"><span data-stu-id="15d64-217">Encrypt virtual disks</span></span>
<span data-ttu-id="15d64-218">toonow chiffrer les disques virtuels hello, vous réunissez tous les composants précédents hello :</span><span class="sxs-lookup"><span data-stu-id="15d64-218">toonow encrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="15d64-219">Spécifiez le mot de passe et l’application d’Azure Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="15d64-219">Specify hello Azure Active Directory application and password.</span></span>
2. <span data-ttu-id="15d64-220">Spécifier des métadonnées de hello toostore hello coffre de clés pour vos disques chiffrés.</span><span class="sxs-lookup"><span data-stu-id="15d64-220">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="15d64-221">Spécifiez toouse de clés de chiffrement hello pour chiffrement hello et le déchiffrement.</span><span class="sxs-lookup"><span data-stu-id="15d64-221">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="15d64-222">Spécifier si vous souhaitez disque hello du système d’exploitation de tooencrypt, des disques de données hello ou tous.</span><span class="sxs-lookup"><span data-stu-id="15d64-222">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="15d64-223">Permet de consulter les détails de hello pour votre clé Azure Key Vault et hello créé, que vous avez besoin hello ID de coffre de clé, un URI, puis l’URL de clés à l’étape finale de hello :</span><span class="sxs-lookup"><span data-stu-id="15d64-223">Lets review hello details for your Azure Key Vault and hello key you created, as you need hello Key Vault ID, URI, and then key URL in hello final step:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="15d64-224">Chiffrer vos disques virtuels à l’aide de la sortie de hello de hello `azure keyvault show` et `azure keyvault key show` commandes comme suit :</span><span class="sxs-lookup"><span data-stu-id="15d64-224">Encrypt your virtual disks using hello output from hello `azure keyvault show` and `azure keyvault key show` commands as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="15d64-225">Comme hello commande précédente a plusieurs variables, hello exemple suivant est commande complète hello pour référence :</span><span class="sxs-lookup"><span data-stu-id="15d64-225">As hello preceding command has many variables, hello following example is hello complete command for reference:</span></span>

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

<span data-ttu-id="15d64-226">Hello CLI d’Azure ne fournit pas des erreurs détaillées au cours du processus de chiffrement hello.</span><span class="sxs-lookup"><span data-stu-id="15d64-226">hello Azure CLI doesn't provide verbose errors during hello encryption process.</span></span> <span data-ttu-id="15d64-227">Pour plus d’informations, consultez `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` sur hello vous chiffrez de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="15d64-227">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` on hello VM you are encrypting.</span></span>

<span data-ttu-id="15d64-228">Enfin, vous permet de consulter l’état du chiffrement hello à nouveau les tooconfirm que vos disques virtuels ont désormais été chiffrés :</span><span class="sxs-lookup"><span data-stu-id="15d64-228">Finally, lets review hello encryption status again tooconfirm that your virtual disks have now been encrypted:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a><span data-ttu-id="15d64-229">Ajouter des disques de données supplémentaires</span><span class="sxs-lookup"><span data-stu-id="15d64-229">Add additional data disks</span></span>
<span data-ttu-id="15d64-230">Une fois que vous avez chiffré vos disques de données, vous pouvez ajouter ultérieurement des disques virtuels tooyour machine virtuelle et également de les chiffrer.</span><span class="sxs-lookup"><span data-stu-id="15d64-230">Once you have encrypted your data disks, you can later add additional virtual disks tooyour VM and also encrypt them.</span></span> <span data-ttu-id="15d64-231">Lorsque vous exécutez hello `azure vm enable-disk-encryption` commande, la version de la séquence hello incrément à l’aide de hello `--sequence-version` paramètre.</span><span class="sxs-lookup"><span data-stu-id="15d64-231">When you run hello `azure vm enable-disk-encryption` command, increment hello sequence version using hello `--sequence-version` parameter.</span></span> <span data-ttu-id="15d64-232">Ce paramètre de version de séquence vous permet de tooperform opérations répétées sur hello même machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="15d64-232">This sequence version parameter allows you tooperform repeated operations on hello same VM.</span></span>

<span data-ttu-id="15d64-233">Par exemple, vous permet d’ajouter un deuxième tooyour de disque virtuel VM, comme suit :</span><span class="sxs-lookup"><span data-stu-id="15d64-233">For example, lets add a second virtual disk tooyour VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="15d64-234">Réexécutez hello commande tooencrypt hello disques virtuels, cette fois Ajout hello `--sequence-version` paramètre et valeur hello incrémentation de notre première exécution comme suit :</span><span class="sxs-lookup"><span data-stu-id="15d64-234">Rerun hello command tooencrypt hello virtual disks, this time adding hello `--sequence-version` parameter, and incrementing hello value from our first run as follows:</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="15d64-235">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="15d64-235">Next steps</span></span>
* <span data-ttu-id="15d64-236">Pour plus d’informations sur la gestion du coffre de clés Azure, y compris la suppression des clés de chiffrement et des coffres, consultez [Gérer le coffre de clés à l’aide de l’interface de ligne de commande](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="15d64-236">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="15d64-237">Pour plus d’informations sur le chiffrement de disque, telles que la préparation d’une tooAzure tooupload machine virtuelle personnalisée chiffré, consultez [chiffrement de disque Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="15d64-237">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
