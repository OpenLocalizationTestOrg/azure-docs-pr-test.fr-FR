---
title: disques aaaEncrypt sur un VM Linux dans Azure | Documents Microsoft
description: "Comment tooencrypt des disques virtuels sur un Linux VM pour à l’aide de la sécurité renforcée hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2a23b6fa-6941-4998-9804-8efe93b647b3
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: d6197742bc8562630e8395588c072093fc01d614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-linux-vm"></a><span data-ttu-id="c86fa-103">Comment tooencrypt des disques virtuels sur un VM Linux</span><span class="sxs-lookup"><span data-stu-id="c86fa-103">How tooencrypt virtual disks on a Linux VM</span></span>
<span data-ttu-id="c86fa-104">Pour renforcer la sécurité et la conformité de la machine virtuelle, les disques virtuels dans Azure peuvent être chiffrés.</span><span class="sxs-lookup"><span data-stu-id="c86fa-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="c86fa-105">Les disques sont chiffrés à l’aide de clés de chiffrement sécurisées dans un coffre de clés Azure.</span><span class="sxs-lookup"><span data-stu-id="c86fa-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="c86fa-106">Vous contrôlez ces clés de chiffrement et pouvez effectuer un audit de leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="c86fa-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="c86fa-107">Cet article décrit en détail comment tooencrypt des disques virtuels sur un VM Linux à l’aide de hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="c86fa-107">This article details how tooencrypt virtual disks on a Linux VM using hello Azure CLI 2.0.</span></span> <span data-ttu-id="c86fa-108">Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c86fa-108">You can also perform these steps with hello [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="c86fa-109">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="c86fa-109">Quick commands</span></span>
<span data-ttu-id="c86fa-110">Si vous avez besoin de tooquickly accomplir la tâche hello, hello suivant hello de détails section base commandes tooencrypt disques virtuels présents sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c86fa-110">If you need tooquickly accomplish hello task, hello following section details hello base commands tooencrypt virtual disks on your VM.</span></span> <span data-ttu-id="c86fa-111">Plus d’informations et le contexte de chaque étape se trouve reste hello du document de hello, [Démarrer ici](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="c86fa-111">More detailed information and context for each step can be found hello rest of hello document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="c86fa-112">Vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="c86fa-112">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="c86fa-113">Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="c86fa-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="c86fa-114">Les noms de paramètre sont par exemple *myResourceGroup*, *myKey* et *myVM*.</span><span class="sxs-lookup"><span data-stu-id="c86fa-114">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="c86fa-115">Tout d’abord, activer le fournisseur de coffre de clés Azure hello dans votre abonnement Azure avec [Registre du fournisseur az](/cli/azure/provider#register) et créer un groupe de ressources avec [az groupe créer](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="c86fa-115">First, enable hello Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="c86fa-116">Hello exemple suivant crée un nom de groupe de ressources *myResourceGroup* Bonjour *eastus* emplacement :</span><span class="sxs-lookup"><span data-stu-id="c86fa-116">hello following example creates a resource group name *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="c86fa-117">Créer un coffre de clés Azure avec [az keyvault créer](/cli/azure/keyvault#create) et activer hello coffre de clés pour une utilisation avec le chiffrement de disque.</span><span class="sxs-lookup"><span data-stu-id="c86fa-117">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="c86fa-118">Spécifiez un nom de Key Vault unique pour *keyvault_name* comme suit :</span><span class="sxs-lookup"><span data-stu-id="c86fa-118">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="c86fa-119">Créez une clé de chiffrement dans le coffre Key Vault avec [az keyvault key create](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="c86fa-119">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="c86fa-120">Hello exemple suivant crée une clé nommée *myKey*:</span><span class="sxs-lookup"><span data-stu-id="c86fa-120">hello following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

<span data-ttu-id="c86fa-121">Créez un principal de service à l’aide d’Azure Active Directory avec [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="c86fa-121">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="c86fa-122">handles de principal de service Hello hello authentification et l’échange de clés de chiffrement à partir du coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="c86fa-122">hello service principal handles hello authentication and exchange of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="c86fa-123">Bonjour à l’exemple suivant lit dans les valeurs hello principal du service hello Id et mot de passe utilisé dans les commandes ultérieures :</span><span class="sxs-lookup"><span data-stu-id="c86fa-123">hello following example reads in hello values for hello service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="c86fa-124">mot de passe Hello est de sortie uniquement lorsque vous créez hello principal du service.</span><span class="sxs-lookup"><span data-stu-id="c86fa-124">hello password is only output when you create hello service principal.</span></span> <span data-ttu-id="c86fa-125">Si vous le souhaitez, afficher et enregistrer hello mot de passe (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="c86fa-125">If desired, view and record hello password (`echo $sp_password`).</span></span> <span data-ttu-id="c86fa-126">Vous pouvez répertorier vos principaux de service avec [az ad sp list](/cli/azure/ad/sp#list) et afficher des informations supplémentaires sur un principal de service spécifique avec [az ad sp show](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="c86fa-126">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="c86fa-127">Définissez des autorisations sur votre Key Vault avec [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="c86fa-127">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="c86fa-128">Dans l’exemple suivant de hello, hello ID du principal de service est fournie par hello précédant la commande :</span><span class="sxs-lookup"><span data-stu-id="c86fa-128">In hello following example, hello service principal ID is supplied from hello preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

<span data-ttu-id="c86fa-129">Créez une machine virtuelle avec [az vm create](/cli/azure/vm#create) et attachez un disque de données de 5 Go.</span><span class="sxs-lookup"><span data-stu-id="c86fa-129">Create a VM with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="c86fa-130">Seules certaines images Marketplace prennent en charge le chiffrement de disque.</span><span class="sxs-lookup"><span data-stu-id="c86fa-130">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="c86fa-131">Hello exemple suivant crée un ordinateur virtuel nommé `myVM` à l’aide un **CentOS 7.2n** image :</span><span class="sxs-lookup"><span data-stu-id="c86fa-131">hello following example creates a VM named `myVM` using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="c86fa-132">SSH à l’aide de machine virtuelle tooyour hello `publicIpAddress` indiqué dans la sortie de hello Hello précédant la commande.</span><span class="sxs-lookup"><span data-stu-id="c86fa-132">SSH tooyour VM using hello `publicIpAddress` shown in hello output of hello preceding command.</span></span> <span data-ttu-id="c86fa-133">Créer une partition et le système de fichiers, puis monter le disque de données hello.</span><span class="sxs-lookup"><span data-stu-id="c86fa-133">Create a partition and filesystem, then mount hello data disk.</span></span> <span data-ttu-id="c86fa-134">Pour plus d’informations, consultez [connecter tooa nouveau disque Linux VM toomount hello](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="c86fa-134">For more information, see [Connect tooa Linux VM toomount hello new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="c86fa-135">Fermez votre session SSH.</span><span class="sxs-lookup"><span data-stu-id="c86fa-135">Close your SSH session.</span></span>

<span data-ttu-id="c86fa-136">Chiffrez votre machine virtuelle avec [az vm encryption enable](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="c86fa-136">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="c86fa-137">exemple Hello utilise hello `$sp_id` et `$sp_password` variables hello précédent `ad sp create-for-rbac` commande :</span><span class="sxs-lookup"><span data-stu-id="c86fa-137">hello following example uses hello `$sp_id` and `$sp_password` variables from hello preceding `ad sp create-for-rbac` command:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

<span data-ttu-id="c86fa-138">Il prend un certain temps pour toocomplete de processus de chiffrement de disque hello.</span><span class="sxs-lookup"><span data-stu-id="c86fa-138">It takes some time for hello disk encryption process toocomplete.</span></span> <span data-ttu-id="c86fa-139">Surveiller l’état de hello du processus hello avec [afficher de chiffrement de machine virtuelle az](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="c86fa-139">Monitor hello status of hello process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="c86fa-140">Hello état montre **EncryptionInProgress**.</span><span class="sxs-lookup"><span data-stu-id="c86fa-140">hello status shows **EncryptionInProgress**.</span></span> <span data-ttu-id="c86fa-141">Attendez que l’état de hello pour les rapports de disque du système d’exploitation de hello **VMRestartPending**, puis redémarrez votre machine virtuelle avec [redémarrage de machine virtuelle az](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="c86fa-141">Wait until hello status for hello OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="c86fa-142">processus de chiffrement de disque Hello est finalisé pendant le processus de démarrage hello, par conséquent, attendez quelques minutes avant de vérifier l’état de hello du chiffrement à l’aide de **afficher de chiffrement de machine virtuelle az**:</span><span class="sxs-lookup"><span data-stu-id="c86fa-142">hello disk encryption process is finalized during hello boot process, so wait a few minutes before checking hello status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="c86fa-143">rapport d’état de Hello doit maintenant disque de hello du système d’exploitation et de disque de données en tant que **Encrypted**.</span><span class="sxs-lookup"><span data-stu-id="c86fa-143">hello status should now report both hello OS disk and data disk as **Encrypted**.</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="c86fa-144">Présentation du chiffrement de disque</span><span class="sxs-lookup"><span data-stu-id="c86fa-144">Overview of disk encryption</span></span>
<span data-ttu-id="c86fa-145">Les disques virtuels sur des machines virtuelles Linux sont chiffrés au repos à l’aide de la commande [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="c86fa-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="c86fa-146">Le chiffrement de disques virtuels dans Azure n’entraîne aucun frais.</span><span class="sxs-lookup"><span data-stu-id="c86fa-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="c86fa-147">Clés de chiffrement sont stockées dans le coffre de clés Azure à l’aide du logiciel de protection, ou vous pouvez importer ou générer vos clés dans des Modules de sécurité matériel (HSM) certifié tooFIPS normes de niveau 2 140-2.</span><span class="sxs-lookup"><span data-stu-id="c86fa-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="c86fa-148">Vous gardez le contrôle de ces clés de chiffrement et pouvez effectuer un audit de leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="c86fa-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="c86fa-149">Ces clés de chiffrement sont utilisé tooencrypt et déchiffrement tooyour de disques virtuels attachés machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c86fa-149">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="c86fa-150">Un principal de service Azure Active Directory fournit un mécanisme sécurisé pour l’émission de ces clés de chiffrement lors de la mise sous tension et hors tension des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="c86fa-150">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="c86fa-151">processus de Hello de chiffrement d’une machine virtuelle est la suivante :</span><span class="sxs-lookup"><span data-stu-id="c86fa-151">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="c86fa-152">Créez une clé de chiffrement dans un coffre de clés Azure.</span><span class="sxs-lookup"><span data-stu-id="c86fa-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="c86fa-153">Configurer hello chiffrement clé toobe utilisable pour le chiffrement des disques.</span><span class="sxs-lookup"><span data-stu-id="c86fa-153">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="c86fa-154">clé de chiffrement hello tooread de hello Azure Key Vault, créez un service Azure Active Directory principal avec les autorisations appropriées hello.</span><span class="sxs-lookup"><span data-stu-id="c86fa-154">tooread hello cryptographic key from hello Azure Key Vault, create an Azure Active Directory service principal with hello appropriate permissions.</span></span>
4. <span data-ttu-id="c86fa-155">Émettre hello commande tooencrypt vos disques virtuels, en spécifiant le principal du service Azure Active Directory hello et appropriée toobe de clés cryptographique utilisé.</span><span class="sxs-lookup"><span data-stu-id="c86fa-155">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory service principal and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="c86fa-156">demandes principales du service Azure Active Directory Hello hello clé de chiffrement requis à partir d’Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c86fa-156">hello Azure Active Directory service principal requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="c86fa-157">les disques virtuels Hello sont chiffrées à l’aide de la clé de chiffrement hello fourni.</span><span class="sxs-lookup"><span data-stu-id="c86fa-157">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="c86fa-158">Processus de chiffrement</span><span class="sxs-lookup"><span data-stu-id="c86fa-158">Encryption process</span></span>
<span data-ttu-id="c86fa-159">Chiffrement de disque s’appuie sur hello suivant des composants supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="c86fa-159">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="c86fa-160">**Azure Key Vault** -utilisé toosafeguard les clés de chiffrement et les secrets utilisés pour le processus de chiffrement/déchiffrement de disque hello.</span><span class="sxs-lookup"><span data-stu-id="c86fa-160">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span>
  * <span data-ttu-id="c86fa-161">Le cas échéant, vous pouvez utiliser un coffre de clés Azure existant.</span><span class="sxs-lookup"><span data-stu-id="c86fa-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="c86fa-162">Vous n’avez pas de le toodedicate un disques tooencrypting de coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="c86fa-162">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="c86fa-163">les limites administratives tooseparate et la visibilité de clé, vous pouvez créer un coffre de clés dédié.</span><span class="sxs-lookup"><span data-stu-id="c86fa-163">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="c86fa-164">**Azure Active Directory** - handles hello échange sécurisé de clés de chiffrement requis et l’authentification pour demandé d’actions.</span><span class="sxs-lookup"><span data-stu-id="c86fa-164">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="c86fa-165">Vous pouvez généralement utiliser une instance Azure Active Directory existante pour héberger votre application.</span><span class="sxs-lookup"><span data-stu-id="c86fa-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="c86fa-166">principal du service Hello fournit un mécanisme sécurisé de toorequest et être émis des clés de chiffrement appropriées hello.</span><span class="sxs-lookup"><span data-stu-id="c86fa-166">hello service principal provides a secure mechanism toorequest and be issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="c86fa-167">Vous ne développez pas de réelle application qui s’intègre à Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c86fa-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="c86fa-168">Spécifications et limitations</span><span class="sxs-lookup"><span data-stu-id="c86fa-168">Requirements and limitations</span></span>
<span data-ttu-id="c86fa-169">Configuration requise et scénarios pris en charge pour le chiffrement de disque :</span><span class="sxs-lookup"><span data-stu-id="c86fa-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="c86fa-170">Hello suivant serveur Linux SKU - Ubuntu, CentOS, SUSE et SUSE Linux Enterprise Server (SLES) et Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="c86fa-170">hello following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="c86fa-171">Toutes les ressources (telles que le coffre de clés, le compte de stockage et machine virtuelle) doivent être Bonjour même région Azure et abonnement.</span><span class="sxs-lookup"><span data-stu-id="c86fa-171">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="c86fa-172">Machines virtuelles standard des séries A, D, DS, G et GS.</span><span class="sxs-lookup"><span data-stu-id="c86fa-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="c86fa-173">Chiffrement de disque n’est pas pris en charge dans hello les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="c86fa-173">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="c86fa-174">Machines virtuelles de niveau de base.</span><span class="sxs-lookup"><span data-stu-id="c86fa-174">Basic tier VMs.</span></span>
* <span data-ttu-id="c86fa-175">Machines virtuelles créées à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="c86fa-175">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="c86fa-176">Désactivation du chiffrement de disque du système d’exploitation sur les machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="c86fa-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="c86fa-177">Mise à jour des clés de chiffrement hello sur une VM Linux déjà chiffré.</span><span class="sxs-lookup"><span data-stu-id="c86fa-177">Updating hello cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="c86fa-178">Créer le coffre de clés Azure et les clés</span><span class="sxs-lookup"><span data-stu-id="c86fa-178">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="c86fa-179">Vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="c86fa-179">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="c86fa-180">Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="c86fa-180">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="c86fa-181">Les noms de paramètre sont par exemple *myResourceGroup*, *myKey* et *myVM*.</span><span class="sxs-lookup"><span data-stu-id="c86fa-181">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="c86fa-182">première étape de Hello est toocreate un toostore Azure Key Vault vos clés de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="c86fa-182">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="c86fa-183">Coffre de clés Azure peuvent stocker des clés, des secrets, ou les mots de passe qui vous permettent de toosecurely leur implémentent dans vos applications et services.</span><span class="sxs-lookup"><span data-stu-id="c86fa-183">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="c86fa-184">Pour le chiffrement de disque virtuel, vous utilisez le coffre de clés toostore une clé de chiffrement qui est utilisé tooencrypt ou déchiffrer vos disques virtuels.</span><span class="sxs-lookup"><span data-stu-id="c86fa-184">For virtual disk encryption, you use Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="c86fa-185">Activer le fournisseur de coffre de clés Azure hello dans votre abonnement Azure avec [Registre du fournisseur az](/cli/azure/provider#register) et créer un groupe de ressources avec [az groupe créer](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="c86fa-185">Enable hello Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="c86fa-186">Hello exemple suivant crée un nom de groupe de ressources *myResourceGroup* Bonjour `eastus` emplacement :</span><span class="sxs-lookup"><span data-stu-id="c86fa-186">hello following example creates a resource group name *myResourceGroup* in hello `eastus` location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="c86fa-187">Bonjour Azure Key Vault contenant hello clés de chiffrement et calcul associée ressources telles que le stockage et hello machine virtuelle proprement dite doivent résider dans hello même région.</span><span class="sxs-lookup"><span data-stu-id="c86fa-187">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="c86fa-188">Créer un coffre de clés Azure avec [az keyvault créer](/cli/azure/keyvault#create) et activer hello coffre de clés pour une utilisation avec le chiffrement de disque.</span><span class="sxs-lookup"><span data-stu-id="c86fa-188">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable hello Key Vault for use with disk encryption.</span></span> <span data-ttu-id="c86fa-189">Spécifiez un nom de Key Vault unique pour *keyvault_name* comme suit :</span><span class="sxs-lookup"><span data-stu-id="c86fa-189">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="c86fa-190">Vous pouvez stocker des clés de chiffrement à l’aide d’une protection logicielle ou HSM (modèle de sécurité matériel).</span><span class="sxs-lookup"><span data-stu-id="c86fa-190">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="c86fa-191">L’utilisation d’une protection HSM nécessite un coffre de clés Premium.</span><span class="sxs-lookup"><span data-stu-id="c86fa-191">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="c86fa-192">Il est un toocreating coût supplémentaire un coffre de clés plutôt que le coffre de clés standard qui stocke les clés protégées par logiciel.</span><span class="sxs-lookup"><span data-stu-id="c86fa-192">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="c86fa-193">toocreate un coffre de clés, premium Bonjour précédant l’étape ajouter `--sku Premium` toohello commande.</span><span class="sxs-lookup"><span data-stu-id="c86fa-193">toocreate a premium Key Vault, in hello preceding step add `--sku Premium` toohello command.</span></span> <span data-ttu-id="c86fa-194">Hello exemple suivant utilise des clés de protection logicielle étant donné que nous avons créé un coffre de clés standard.</span><span class="sxs-lookup"><span data-stu-id="c86fa-194">hello following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="c86fa-195">Les modèles de protection, hello plateforme Azure doit toobe accordé accès toorequest les clés de chiffrement hello lorsque hello machine virtuelle démarre les disques virtuels toodecrypt hello.</span><span class="sxs-lookup"><span data-stu-id="c86fa-195">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="c86fa-196">Créez une clé de chiffrement dans le coffre Key Vault avec [az keyvault key create](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="c86fa-196">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="c86fa-197">Hello exemple suivant crée une clé nommée *myKey*:</span><span class="sxs-lookup"><span data-stu-id="c86fa-197">hello following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-hello-azure-active-directory-service-principal"></a><span data-ttu-id="c86fa-198">Créer hello principal du service Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c86fa-198">Create hello Azure Active Directory service principal</span></span>
<span data-ttu-id="c86fa-199">Lorsque les disques virtuels sont chiffrées ou déchiffrées, vous spécifiez une authentification hello toohandle des comptes et l’échange de clés de chiffrement à partir du coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="c86fa-199">When virtual disks are encrypted or decrypted, you specify an account toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="c86fa-200">Ce compte, un principal du service Azure Active Directory, permet de clés de chiffrement approprié hello pour le compte hello VM toorequest de plateforme Windows Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c86fa-200">This account, an Azure Active Directory service principal, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="c86fa-201">Une instance Azure Active Directory par défaut est disponible dans votre abonnement, bien que de nombreuses organisations utilisent des répertoires Azure Active Directory dédiés.</span><span class="sxs-lookup"><span data-stu-id="c86fa-201">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="c86fa-202">Créez un principal de service à l’aide d’Azure Active Directory avec [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="c86fa-202">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="c86fa-203">Bonjour à l’exemple suivant lit dans les valeurs hello principal du service hello Id et mot de passe utilisé dans les commandes ultérieures :</span><span class="sxs-lookup"><span data-stu-id="c86fa-203">hello following example reads in hello values for hello service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="c86fa-204">mot de passe Hello s’affiche uniquement lorsque vous créez un service de hello principal.</span><span class="sxs-lookup"><span data-stu-id="c86fa-204">hello password is only displayed when you create hello service principal.</span></span> <span data-ttu-id="c86fa-205">Si vous le souhaitez, afficher et enregistrer hello mot de passe (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="c86fa-205">If desired, view and record hello password (`echo $sp_password`).</span></span> <span data-ttu-id="c86fa-206">Vous pouvez répertorier vos principaux de service avec [az ad sp list](/cli/azure/ad/sp#list) et afficher des informations supplémentaires sur un principal de service spécifique avec [az ad sp show](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="c86fa-206">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="c86fa-207">toosuccessfully chiffrer ou déchiffrer des disques virtuels, les autorisations sur la clé de chiffrement hello stockées dans le coffre de clés doivent être principal tooread hello clés du service Azure Active Directory définies toopermit hello.</span><span class="sxs-lookup"><span data-stu-id="c86fa-207">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory service principal tooread hello keys.</span></span> <span data-ttu-id="c86fa-208">Définissez des autorisations sur votre Key Vault avec [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="c86fa-208">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="c86fa-209">Dans l’exemple suivant de hello, hello ID du principal de service est fournie par hello précédant la commande :</span><span class="sxs-lookup"><span data-stu-id="c86fa-209">In hello following example, hello service principal ID is supplied from hello preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a><span data-ttu-id="c86fa-210">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="c86fa-210">Create virtual machine</span></span>
<span data-ttu-id="c86fa-211">tooactually chiffrer certains disques virtuels, vous permet de créer une machine virtuelle et ajoutez un disque de données.</span><span class="sxs-lookup"><span data-stu-id="c86fa-211">tooactually encrypt some virtual disks, lets create a VM and add a data disk.</span></span> <span data-ttu-id="c86fa-212">Créer un tooencrypt de machine virtuelle avec [az vm créer](/cli/azure/vm#create) et attacher un disque de données de 5 Go.</span><span class="sxs-lookup"><span data-stu-id="c86fa-212">Create a VM tooencrypt with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="c86fa-213">Seules certaines images Marketplace prennent en charge le chiffrement de disque.</span><span class="sxs-lookup"><span data-stu-id="c86fa-213">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="c86fa-214">Hello exemple suivant crée un ordinateur virtuel nommé *myVM* à l’aide un **CentOS 7.2n** image :</span><span class="sxs-lookup"><span data-stu-id="c86fa-214">hello following example creates a VM named *myVM* using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="c86fa-215">SSH à l’aide de machine virtuelle tooyour hello `publicIpAddress` indiqué dans la sortie de hello Hello précédant la commande.</span><span class="sxs-lookup"><span data-stu-id="c86fa-215">SSH tooyour VM using hello `publicIpAddress` shown in hello output of hello preceding command.</span></span> <span data-ttu-id="c86fa-216">Créer une partition et le système de fichiers, puis monter le disque de données hello.</span><span class="sxs-lookup"><span data-stu-id="c86fa-216">Create a partition and filesystem, then mount hello data disk.</span></span> <span data-ttu-id="c86fa-217">Pour plus d’informations, consultez [connecter tooa nouveau disque Linux VM toomount hello](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="c86fa-217">For more information, see [Connect tooa Linux VM toomount hello new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="c86fa-218">Fermez votre session SSH.</span><span class="sxs-lookup"><span data-stu-id="c86fa-218">Close your SSH session.</span></span>


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="c86fa-219">Chiffrement d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="c86fa-219">Encrypt virtual machine</span></span>
<span data-ttu-id="c86fa-220">disques virtuels de tooencrypt hello, vous réunissez tous les composants précédents hello :</span><span class="sxs-lookup"><span data-stu-id="c86fa-220">tooencrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="c86fa-221">Spécifiez hello principal du service Azure Active Directory et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="c86fa-221">Specify hello Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="c86fa-222">Spécifier des métadonnées de hello toostore hello coffre de clés pour vos disques chiffrés.</span><span class="sxs-lookup"><span data-stu-id="c86fa-222">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="c86fa-223">Spécifiez toouse de clés de chiffrement hello pour chiffrement hello et le déchiffrement.</span><span class="sxs-lookup"><span data-stu-id="c86fa-223">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="c86fa-224">Spécifier si vous souhaitez disque hello du système d’exploitation de tooencrypt, des disques de données hello ou tous.</span><span class="sxs-lookup"><span data-stu-id="c86fa-224">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="c86fa-225">Chiffrez votre machine virtuelle avec [az vm encryption enable](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="c86fa-225">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="c86fa-226">exemple Hello utilise hello `$sp_id` et `$sp_password` variables hello précédent `ad sp create-for-rbac` commande :</span><span class="sxs-lookup"><span data-stu-id="c86fa-226">hello following example uses hello `$sp_id` and `$sp_password` variables from hello preceding `ad sp create-for-rbac` command:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

<span data-ttu-id="c86fa-227">Il prend un certain temps pour toocomplete de processus de chiffrement de disque hello.</span><span class="sxs-lookup"><span data-stu-id="c86fa-227">It takes some time for hello disk encryption process toocomplete.</span></span> <span data-ttu-id="c86fa-228">Surveiller l’état de hello du processus hello avec [afficher de chiffrement de machine virtuelle az](/cli/azure/vm/encryption#show):</span><span class="sxs-lookup"><span data-stu-id="c86fa-228">Monitor hello status of hello process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="c86fa-229">Hello de sortie est tronquée exemple après la toohello similaire :</span><span class="sxs-lookup"><span data-stu-id="c86fa-229">hello output is similar toohello following truncated example:</span></span>

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

<span data-ttu-id="c86fa-230">Attendez que l’état de hello pour les rapports de disque du système d’exploitation de hello **VMRestartPending**, puis redémarrez votre machine virtuelle avec [redémarrage de machine virtuelle az](/cli/azure/vm#restart):</span><span class="sxs-lookup"><span data-stu-id="c86fa-230">Wait until hello status for hello OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="c86fa-231">processus de chiffrement de disque Hello est finalisé pendant le processus de démarrage hello, par conséquent, attendez quelques minutes avant de vérifier l’état de hello du chiffrement à l’aide de **afficher de chiffrement de machine virtuelle az**:</span><span class="sxs-lookup"><span data-stu-id="c86fa-231">hello disk encryption process is finalized during hello boot process, so wait a few minutes before checking hello status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="c86fa-232">rapport d’état de Hello doit maintenant disque de hello du système d’exploitation et de disque de données en tant que **Encrypted**.</span><span class="sxs-lookup"><span data-stu-id="c86fa-232">hello status should now report both hello OS disk and data disk as **Encrypted**.</span></span>


## <a name="add-additional-data-disks"></a><span data-ttu-id="c86fa-233">Ajouter des disques de données supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c86fa-233">Add additional data disks</span></span>
<span data-ttu-id="c86fa-234">Une fois que vous avez chiffré vos disques de données, vous pouvez ajouter ultérieurement des disques virtuels tooyour machine virtuelle et également de les chiffrer.</span><span class="sxs-lookup"><span data-stu-id="c86fa-234">Once you have encrypted your data disks, you can later add additional virtual disks tooyour VM and also encrypt them.</span></span> <span data-ttu-id="c86fa-235">Par exemple, vous permet d’ajouter un deuxième tooyour de disque virtuel VM, comme suit :</span><span class="sxs-lookup"><span data-stu-id="c86fa-235">For example, lets add a second virtual disk tooyour VM as follows:</span></span>

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

<span data-ttu-id="c86fa-236">Exécuter à nouveau les disques virtuels hello commande tooencrypt hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c86fa-236">Re-run hello command tooencrypt hello virtual disks as follows:</span></span>

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```


## <a name="next-steps"></a><span data-ttu-id="c86fa-237">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c86fa-237">Next steps</span></span>
* <span data-ttu-id="c86fa-238">Pour plus d’informations sur la gestion du coffre de clés Azure, y compris la suppression des clés de chiffrement et des coffres, consultez [Gérer le coffre de clés à l’aide de l’interface de ligne de commande](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="c86fa-238">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="c86fa-239">Pour plus d’informations sur le chiffrement de disque, telles que la préparation d’une tooAzure tooupload machine virtuelle personnalisée chiffré, consultez [chiffrement de disque Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="c86fa-239">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
