---
title: Chiffrer des disques sur une machine virtuelle Linux dans Azure | Microsoft Docs
description: "Guide de chiffrage de disques virtuels sur une machine virtuelle Linux pour renforcer la sécurité à l’aide d’Azure CLI 2.0"
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
ms.openlocfilehash: 172b4c8f5c098d776cb689543f5d8f163b8895b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-encrypt-virtual-disks-on-a-linux-vm"></a><span data-ttu-id="4fa1f-103">Guide de chiffrage de disques virtuels sur une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="4fa1f-103">How to encrypt virtual disks on a Linux VM</span></span>
<span data-ttu-id="4fa1f-104">Pour renforcer la sécurité et la conformité de la machine virtuelle, les disques virtuels dans Azure peuvent être chiffrés.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted.</span></span> <span data-ttu-id="4fa1f-105">Les disques sont chiffrés à l’aide de clés de chiffrement sécurisées dans un coffre de clés Azure.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="4fa1f-106">Vous contrôlez ces clés de chiffrement et pouvez effectuer un audit de leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="4fa1f-107">Cet article explique comment chiffrer des disques virtuels sur une machine virtuelle Linux à l’aide de l’interface Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-107">This article details how to encrypt virtual disks on a Linux VM using the Azure CLI 2.0.</span></span> <span data-ttu-id="4fa1f-108">Vous pouvez également effectuer ces étapes à l’aide [d’Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4fa1f-108">You can also perform these steps with the [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="4fa1f-109">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="4fa1f-109">Quick commands</span></span>
<span data-ttu-id="4fa1f-110">Si vous avez besoin d’accomplir rapidement cette tâche, la section suivante décrit les commandes de base pour chiffrer des disques virtuels sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-110">If you need to quickly accomplish the task, the following section details the base commands to encrypt virtual disks on your VM.</span></span> <span data-ttu-id="4fa1f-111">Pour obtenir plus d’informations et davantage de contexte pour chaque étape, lisez la suite de ce document, [à partir de cette section](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="4fa1f-111">More detailed information and context for each step can be found the rest of the document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="4fa1f-112">Vous devez disposer de la dernière version [d’Azure CLI 2.0](/cli/azure/install-az-cli2) et vous connecter à un compte Azure avec la commande [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="4fa1f-112">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="4fa1f-113">Dans les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-113">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="4fa1f-114">Les noms de paramètre sont par exemple *myResourceGroup*, *myKey* et *myVM*.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-114">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="4fa1f-115">Tout d’abord, activez le fournisseur Azure Key Vault au sein de votre abonnement Azure avec [az provider register](/cli/azure/provider#register) puis créez un groupe de ressources avec [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="4fa1f-115">First, enable the Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="4fa1f-116">L’exemple suivant crée un groupe de ressources nommé *myResourceGroup* à l’emplacement *eastus* :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-116">The following example creates a resource group name *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="4fa1f-117">Créez un coffre Azure Key Vault avec [az keyvault create](/cli/azure/keyvault#create) et activez Key Vault pour une utilisation avec le chiffrement de disque.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-117">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable the Key Vault for use with disk encryption.</span></span> <span data-ttu-id="4fa1f-118">Spécifiez un nom de Key Vault unique pour *keyvault_name* comme suit :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-118">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="4fa1f-119">Créez une clé de chiffrement dans le coffre Key Vault avec [az keyvault key create](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="4fa1f-119">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="4fa1f-120">L’exemple qui suit permet de créer une clé nommée *myKey* :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-120">The following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

<span data-ttu-id="4fa1f-121">Créez un principal de service à l’aide d’Azure Active Directory avec [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="4fa1f-121">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="4fa1f-122">L’entité de service gère l’authentification et l’échange de clés de chiffrement depuis le coffre Key Vault.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-122">The service principal handles the authentication and exchange of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="4fa1f-123">L’exemple suivant lit les valeurs pour l’ID et le mot de passe du principal de service à utiliser dans les commandes ultérieures :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-123">The following example reads in the values for the service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="4fa1f-124">Le mot de passe est émis uniquement lorsque vous créez le principal de service.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-124">The password is only output when you create the service principal.</span></span> <span data-ttu-id="4fa1f-125">Si vous le souhaitez, affichez et enregistrez le mot de passe (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="4fa1f-125">If desired, view and record the password (`echo $sp_password`).</span></span> <span data-ttu-id="4fa1f-126">Vous pouvez répertorier vos principaux de service avec [az ad sp list](/cli/azure/ad/sp#list) et afficher des informations supplémentaires sur un principal de service spécifique avec [az ad sp show](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="4fa1f-126">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="4fa1f-127">Définissez des autorisations sur votre Key Vault avec [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="4fa1f-127">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="4fa1f-128">Dans l’exemple suivant, l’ID du principal de service est fourni à partir de la commande précédente :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-128">In the following example, the service principal ID is supplied from the preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

<span data-ttu-id="4fa1f-129">Créez une machine virtuelle avec [az vm create](/cli/azure/vm#create) et attachez un disque de données de 5 Go.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-129">Create a VM with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="4fa1f-130">Seules certaines images Marketplace prennent en charge le chiffrement de disque.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-130">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="4fa1f-131">L’exemple qui suit permet de créer une machine virtuelle nommée `myVM` qui utilise une image **CentOS 7.2n** :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-131">The following example creates a VM named `myVM` using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="4fa1f-132">Connectez-vous avec SSH à votre machine virtuelle à l’aide de la valeur `publicIpAddress` indiquée dans la sortie de la commande précédente.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-132">SSH to your VM using the `publicIpAddress` shown in the output of the preceding command.</span></span> <span data-ttu-id="4fa1f-133">Créez une partition et un système de fichiers, puis montez le disque de données.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-133">Create a partition and filesystem, then mount the data disk.</span></span> <span data-ttu-id="4fa1f-134">Pour plus d’informations, consultez [Connexion à la machine virtuelle Linux pour monter le nouveau disque](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="4fa1f-134">For more information, see [Connect to a Linux VM to mount the new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="4fa1f-135">Fermez votre session SSH.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-135">Close your SSH session.</span></span>

<span data-ttu-id="4fa1f-136">Chiffrez votre machine virtuelle avec [az vm encryption enable](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="4fa1f-136">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="4fa1f-137">L’exemple suivant utilise les variables `$sp_id` et `$sp_password` à partir de la commande `ad sp create-for-rbac` précédente :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-137">The following example uses the `$sp_id` and `$sp_password` variables from the preceding `ad sp create-for-rbac` command:</span></span>

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

<span data-ttu-id="4fa1f-138">Il faut un certain temps pour que le processus de chiffrement de disque se termine.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-138">It takes some time for the disk encryption process to complete.</span></span> <span data-ttu-id="4fa1f-139">Surveillez l’état du processus avec [az vm encryption show](/cli/azure/vm/encryption#show) :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-139">Monitor the status of the process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="4fa1f-140">L’état indique **EncryptionInProgress**.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-140">The status shows **EncryptionInProgress**.</span></span> <span data-ttu-id="4fa1f-141">Attendez que l’état du disque du système d’exploitation signale **VMRestartPending**, puis redémarrez votre machine virtuelle avec [az vm restart](/cli/azure/vm#restart) :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-141">Wait until the status for the OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="4fa1f-142">Le processus de chiffrement de disque est finalisé pendant le processus de démarrage, aussi attendez quelques minutes avant de vérifier à nouveau l’état de chiffrement à l’aide de **az vm encryption show** :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-142">The disk encryption process is finalized during the boot process, so wait a few minutes before checking the status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="4fa1f-143">L’état doit maintenant signaler que le disque du système d’exploitation et le disque de données ont l’état **Chiffré**.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-143">The status should now report both the OS disk and data disk as **Encrypted**.</span></span>

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="4fa1f-144">Présentation du chiffrement de disque</span><span class="sxs-lookup"><span data-stu-id="4fa1f-144">Overview of disk encryption</span></span>
<span data-ttu-id="4fa1f-145">Les disques virtuels sur des machines virtuelles Linux sont chiffrés au repos à l’aide de la commande [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="4fa1f-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="4fa1f-146">Le chiffrement de disques virtuels dans Azure n’entraîne aucun frais.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="4fa1f-147">Les clés de chiffrement sont stockées dans le coffre de clés Azure à l’aide d’une protection logicielle, mais vous pouvez importer ou générer vos clés dans des modules de sécurité matériels (HSM) certifiés conformes aux normes FIPS 140-2 de niveau 2.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified to FIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="4fa1f-148">Vous gardez le contrôle de ces clés de chiffrement et pouvez effectuer un audit de leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="4fa1f-149">Ces clés de chiffrement servent à chiffrer et à déchiffrer les disques virtuels connectés à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-149">These cryptographic keys are used to encrypt and decrypt virtual disks attached to your VM.</span></span> <span data-ttu-id="4fa1f-150">Un principal de service Azure Active Directory fournit un mécanisme sécurisé pour l’émission de ces clés de chiffrement lors de la mise sous tension et hors tension des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-150">An Azure Active Directory service principal provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="4fa1f-151">Le processus de chiffrement d’une machine virtuelle est le suivant :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-151">The process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="4fa1f-152">Créez une clé de chiffrement dans un coffre de clés Azure.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="4fa1f-153">Configurez la clé de chiffrement afin de la rendre utilisable pour le chiffrement des disques.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-153">Configure the cryptographic key to be usable for encrypting disks.</span></span>
3. <span data-ttu-id="4fa1f-154">Pour lire la clé de chiffrement à partir du coffre de clés Azure, créez un principal de service Azure Active Directory avec les autorisations appropriées.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-154">To read the cryptographic key from the Azure Key Vault, create an Azure Active Directory service principal with the appropriate permissions.</span></span>
4. <span data-ttu-id="4fa1f-155">Exécutez la commande pour chiffrer vos disques virtuels, en spécifiant le principal de service Azure Active Directory et la clé de chiffrement appropriée à utiliser.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-155">Issue the command to encrypt your virtual disks, specifying the Azure Active Directory service principal and appropriate cryptographic key to be used.</span></span>
5. <span data-ttu-id="4fa1f-156">Le principal de service Azure Active Directory demande la clé de chiffrement requise au coffre de clés Azure.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-156">The Azure Active Directory service principal requests the required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="4fa1f-157">Les disques virtuels sont chiffrés à l’aide de la clé de chiffrement fournie.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-157">The virtual disks are encrypted using the provided cryptographic key.</span></span>

## <a name="encryption-process"></a><span data-ttu-id="4fa1f-158">Processus de chiffrement</span><span class="sxs-lookup"><span data-stu-id="4fa1f-158">Encryption process</span></span>
<span data-ttu-id="4fa1f-159">Le chiffrement de disque s’appuie sur les composants supplémentaires suivants :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-159">Disk encryption relies on the following additional components:</span></span>

* <span data-ttu-id="4fa1f-160">**Coffre de clés Azure** - permet de sauvegarder les clés de chiffrement et les clés secrètes utilisées pour le processus de chiffrement/déchiffrement de disque.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-160">**Azure Key Vault** - used to safeguard cryptographic keys and secrets used for the disk encryption/decryption process.</span></span>
  * <span data-ttu-id="4fa1f-161">Le cas échéant, vous pouvez utiliser un coffre de clés Azure existant.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="4fa1f-162">Vous n’êtes pas obligé de dédier un coffre de clés au chiffrement des disques.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-162">You do not have to dedicate a Key Vault to encrypting disks.</span></span>
  * <span data-ttu-id="4fa1f-163">Pour séparer les limites administratives et la visibilité de la clé, vous pouvez créer un coffre de clés dédié.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-163">To separate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="4fa1f-164">**Azure Active Directory** - gère l’échange sécurisé des clés de chiffrement requises et l’authentification des actions demandées.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-164">**Azure Active Directory** - handles the secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="4fa1f-165">Vous pouvez généralement utiliser une instance Azure Active Directory existante pour héberger votre application.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="4fa1f-166">Le principal du service fournit un mécanisme sécurisé pour demander et émettre les bonnes clés de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-166">The service principal provides a secure mechanism to request and be issued the appropriate cryptographic keys.</span></span> <span data-ttu-id="4fa1f-167">Vous ne développez pas de réelle application qui s’intègre à Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="4fa1f-168">Spécifications et limitations</span><span class="sxs-lookup"><span data-stu-id="4fa1f-168">Requirements and limitations</span></span>
<span data-ttu-id="4fa1f-169">Configuration requise et scénarios pris en charge pour le chiffrement de disque :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="4fa1f-170">Les versions serveur Linux suivantes : Ubuntu, CentOS, SUSE, SUSE Linux Enterprise Server (SLES) et Red Hat Enterprise Linux.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-170">The following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="4fa1f-171">Toutes les ressources (par exemple, le coffre de clés, le compte de stockage, la machine virtuelle, etc.) doivent appartenir à la même région et au même abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-171">All resources (such as Key Vault, Storage account, and VM) must be in the same Azure region and subscription.</span></span>
* <span data-ttu-id="4fa1f-172">Machines virtuelles standard des séries A, D, DS, G et GS.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="4fa1f-173">Le chiffrement de disque n’est actuellement pas pris en charge dans les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-173">Disk encryption is not currently supported in the following scenarios:</span></span>

* <span data-ttu-id="4fa1f-174">Machines virtuelles de niveau de base.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-174">Basic tier VMs.</span></span>
* <span data-ttu-id="4fa1f-175">Machines virtuelles créées à l’aide du modèle de déploiement Classic.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-175">VMs created using the Classic deployment model.</span></span>
* <span data-ttu-id="4fa1f-176">Désactivation du chiffrement de disque du système d’exploitation sur les machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="4fa1f-177">Mise à jour des clés de chiffrement sur une machine virtuelle Linux déjà chiffrée.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-177">Updating the cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-azure-key-vault-and-keys"></a><span data-ttu-id="4fa1f-178">Créer le coffre de clés Azure et les clés</span><span class="sxs-lookup"><span data-stu-id="4fa1f-178">Create Azure Key Vault and keys</span></span>
<span data-ttu-id="4fa1f-179">Vous devez disposer de la dernière version [d’Azure CLI 2.0](/cli/azure/install-az-cli2) et vous connecter à un compte Azure avec la commande [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="4fa1f-179">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="4fa1f-180">Dans les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-180">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="4fa1f-181">Les noms de paramètre sont par exemple *myResourceGroup*, *myKey* et *myVM*.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-181">Example parameter names include *myResourceGroup*, *myKey*, and *myVM*.</span></span>

<span data-ttu-id="4fa1f-182">La première étape consiste à créer un coffre de clés Azure pour y stocker les clés de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-182">The first step is to create an Azure Key Vault to store your cryptographic keys.</span></span> <span data-ttu-id="4fa1f-183">Un coffre de clés Azure peut stocker des clés, des clés secrètes ou des mots de passe vous permettant de les implémenter en toute sécurité dans vos applications et services.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-183">Azure Key Vault can store keys, secrets, or passwords that allow you to securely implement them in your applications and services.</span></span> <span data-ttu-id="4fa1f-184">Pour le chiffrement de disque virtuel, vous utilisez le coffre de clés afin de stocker une clé de chiffrement pour chiffrer ou déchiffrer vos disques virtuels.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-184">For virtual disk encryption, you use Key Vault to store a cryptographic key that is used to encrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="4fa1f-185">Activez le fournisseur Azure Key Vault au sein de votre abonnement Azure avec [az provider register](/cli/azure/provider#register) puis créez un groupe de ressources avec [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="4fa1f-185">Enable the Azure Key Vault provider within your Azure subscription with [az provider register](/cli/azure/provider#register) and create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="4fa1f-186">L’exemple suivant crée un groupe de ressources nommé *myResourceGroup* à l’emplacement `eastus` :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-186">The following example creates a resource group name *myResourceGroup* in the `eastus` location:</span></span>

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="4fa1f-187">Le coffre de clés Azure contenant les clés de chiffrement et les ressources de calcul associées tels que le stockage et la machine virtuelle elle-même doit résider dans la même région.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-187">The Azure Key Vault containing the cryptographic keys and associated compute resources such as storage and the VM itself must reside in the same region.</span></span> <span data-ttu-id="4fa1f-188">Créez un coffre Azure Key Vault avec [az keyvault create](/cli/azure/keyvault#create) et activez Key Vault pour une utilisation avec le chiffrement de disque.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-188">Create an Azure Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable the Key Vault for use with disk encryption.</span></span> <span data-ttu-id="4fa1f-189">Spécifiez un nom de Key Vault unique pour *keyvault_name* comme suit :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-189">Specify a unique Key Vault name for *keyvault_name* as follows:</span></span>

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

<span data-ttu-id="4fa1f-190">Vous pouvez stocker des clés de chiffrement à l’aide d’une protection logicielle ou HSM (modèle de sécurité matériel).</span><span class="sxs-lookup"><span data-stu-id="4fa1f-190">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="4fa1f-191">L’utilisation d’une protection HSM nécessite un coffre de clés Premium.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-191">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="4fa1f-192">Contrairement à l’utilisation d’un coffre de clés standard qui stocke les clés protégées par logiciel, la création d’un coffre de clés Premium entraîne des frais.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-192">There is an additional cost to creating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="4fa1f-193">Pour créer un coffre de clés Premium, ajoutez `--sku Premium` à la commande de l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-193">To create a premium Key Vault, in the preceding step add `--sku Premium` to the command.</span></span> <span data-ttu-id="4fa1f-194">L’exemple suivant utilise des clés protégées par logiciel puisque nous avons créé un coffre de clés standard.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-194">The following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="4fa1f-195">Pour les deux modèles de protection, la plateforme Azure doit être autorisée à demander les clés de chiffrement lorsque la machine virtuelle démarre pour déchiffrer les disques virtuels.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-195">For both protection models, the Azure platform needs to be granted access to request the cryptographic keys when the VM boots to decrypt the virtual disks.</span></span> <span data-ttu-id="4fa1f-196">Créez une clé de chiffrement dans le coffre Key Vault avec [az keyvault key create](/cli/azure/keyvault/key#create).</span><span class="sxs-lookup"><span data-stu-id="4fa1f-196">Create a cryptographic key in your Key Vault with [az keyvault key create](/cli/azure/keyvault/key#create).</span></span> <span data-ttu-id="4fa1f-197">L’exemple qui suit permet de créer une clé nommée *myKey* :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-197">The following example creates a key named *myKey*:</span></span>

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-the-azure-active-directory-service-principal"></a><span data-ttu-id="4fa1f-198">Création d’un principal de service Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4fa1f-198">Create the Azure Active Directory service principal</span></span>
<span data-ttu-id="4fa1f-199">Lorsque des disques virtuels sont chiffrés ou déchiffrés, vous spécifiez un compte pour gérer l’authentification et l’échange de clés de chiffrement à partir du coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-199">When virtual disks are encrypted or decrypted, you specify an account to handle the authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="4fa1f-200">Ce compte, un principal de service Azure Active Directory, permet à la plateforme Azure de demander les clés de chiffrement appropriées pour le compte de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-200">This account, an Azure Active Directory service principal, allows the Azure platform to request the appropriate cryptographic keys on behalf of the VM.</span></span> <span data-ttu-id="4fa1f-201">Une instance Azure Active Directory par défaut est disponible dans votre abonnement, bien que de nombreuses organisations utilisent des répertoires Azure Active Directory dédiés.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-201">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="4fa1f-202">Créez un principal de service à l’aide d’Azure Active Directory avec [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span><span class="sxs-lookup"><span data-stu-id="4fa1f-202">Create a service principal using Azure Active Directory with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac).</span></span> <span data-ttu-id="4fa1f-203">L’exemple suivant lit les valeurs pour l’ID et le mot de passe du principal de service à utiliser dans les commandes ultérieures :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-203">The following example reads in the values for the service principal Id and password for use in later commands:</span></span>

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

<span data-ttu-id="4fa1f-204">Le mot de passe s’affiche uniquement lorsque vous créez le principal de service.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-204">The password is only displayed when you create the service principal.</span></span> <span data-ttu-id="4fa1f-205">Si vous le souhaitez, affichez et enregistrez le mot de passe (`echo $sp_password`).</span><span class="sxs-lookup"><span data-stu-id="4fa1f-205">If desired, view and record the password (`echo $sp_password`).</span></span> <span data-ttu-id="4fa1f-206">Vous pouvez répertorier vos principaux de service avec [az ad sp list](/cli/azure/ad/sp#list) et afficher des informations supplémentaires sur un principal de service spécifique avec [az ad sp show](/cli/azure/ad/sp#show).</span><span class="sxs-lookup"><span data-stu-id="4fa1f-206">You can list your service principals with [az ad sp list](/cli/azure/ad/sp#list) and view additional information about a specific service principal with [az ad sp show](/cli/azure/ad/sp#show).</span></span>

<span data-ttu-id="4fa1f-207">Pour chiffrer ou déchiffrer correctement des disques virtuels, des autorisations d’accès à la clé de chiffrement stockée dans le coffre de clés doivent être définies afin que le principal de service Azure Active Directory puisse lire les clés.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-207">To successfully encrypt or decrypt virtual disks, permissions on the cryptographic key stored in Key Vault must be set to permit the Azure Active Directory service principal to read the keys.</span></span> <span data-ttu-id="4fa1f-208">Définissez des autorisations sur votre Key Vault avec [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span><span class="sxs-lookup"><span data-stu-id="4fa1f-208">Set permissions on your Key Vault with [az keyvault set-policy](/cli/azure/keyvault#set-policy).</span></span> <span data-ttu-id="4fa1f-209">Dans l’exemple suivant, l’ID du principal de service est fourni à partir de la commande précédente :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-209">In the following example, the service principal ID is supplied from the preceding command:</span></span>

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a><span data-ttu-id="4fa1f-210">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="4fa1f-210">Create virtual machine</span></span>
<span data-ttu-id="4fa1f-211">Pour chiffrer certains disques virtuels, créons une machine virtuelle et ajoutons un disque de données.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-211">To actually encrypt some virtual disks, lets create a VM and add a data disk.</span></span> <span data-ttu-id="4fa1f-212">Créez une machine virtuelle à chiffrer avec [az vm create](/cli/azure/vm#create) et attachez un disque de données de 5 Go.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-212">Create a VM to encrypt with [az vm create](/cli/azure/vm#create) and attach a 5Gb data disk.</span></span> <span data-ttu-id="4fa1f-213">Seules certaines images Marketplace prennent en charge le chiffrement de disque.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-213">Only certain marketplace images support disk encryption.</span></span> <span data-ttu-id="4fa1f-214">L’exemple qui suit permet de créer une machine virtuelle nommée *myVM* qui utilise une image **CentOS 7.2n** :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-214">The following example creates a VM named *myVM* using a **CentOS 7.2n** image:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

<span data-ttu-id="4fa1f-215">Connectez-vous avec SSH à votre machine virtuelle à l’aide de la valeur `publicIpAddress` indiquée dans la sortie de la commande précédente.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-215">SSH to your VM using the `publicIpAddress` shown in the output of the preceding command.</span></span> <span data-ttu-id="4fa1f-216">Créez une partition et un système de fichiers, puis montez le disque de données.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-216">Create a partition and filesystem, then mount the data disk.</span></span> <span data-ttu-id="4fa1f-217">Pour plus d’informations, consultez [Connexion à la machine virtuelle Linux pour monter le nouveau disque](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span><span class="sxs-lookup"><span data-stu-id="4fa1f-217">For more information, see [Connect to a Linux VM to mount the new disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk).</span></span> <span data-ttu-id="4fa1f-218">Fermez votre session SSH.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-218">Close your SSH session.</span></span>


## <a name="encrypt-virtual-machine"></a><span data-ttu-id="4fa1f-219">Chiffrement d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="4fa1f-219">Encrypt virtual machine</span></span>
<span data-ttu-id="4fa1f-220">Pour chiffrer les disques virtuels, vous allez réunir tous les composants précédents :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-220">To encrypt the virtual disks, you bring together all the previous components:</span></span>

1. <span data-ttu-id="4fa1f-221">Spécifiez le principal de service Azure Active Directory et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-221">Specify the Azure Active Directory service principal and password.</span></span>
2. <span data-ttu-id="4fa1f-222">Spécifiez le coffre de clés qui stockera les métadonnées de vos disques chiffrés.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-222">Specify the Key Vault to store the metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="4fa1f-223">Spécifiez les clés de chiffrement à utiliser pour le chiffrement et le déchiffrement réels.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-223">Specify the cryptographic keys to use for the actual encryption and decryption.</span></span>
4. <span data-ttu-id="4fa1f-224">Indiquez si vous souhaitez chiffrer le disque du système d’exploitation, les disques de données ou l’ensemble.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-224">Specify whether you want to encrypt the OS disk, the data disks, or all.</span></span>

<span data-ttu-id="4fa1f-225">Chiffrez votre machine virtuelle avec [az vm encryption enable](/cli/azure/vm/encryption#enable).</span><span class="sxs-lookup"><span data-stu-id="4fa1f-225">Encrypt your VM with [az vm encryption enable](/cli/azure/vm/encryption#enable).</span></span> <span data-ttu-id="4fa1f-226">L’exemple suivant utilise les variables `$sp_id` et `$sp_password` à partir de la commande `ad sp create-for-rbac` précédente :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-226">The following example uses the `$sp_id` and `$sp_password` variables from the preceding `ad sp create-for-rbac` command:</span></span>

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

<span data-ttu-id="4fa1f-227">Il faut un certain temps pour que le processus de chiffrement de disque se termine.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-227">It takes some time for the disk encryption process to complete.</span></span> <span data-ttu-id="4fa1f-228">Surveillez l’état du processus avec [az vm encryption show](/cli/azure/vm/encryption#show) :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-228">Monitor the status of the process with [az vm encryption show](/cli/azure/vm/encryption#show):</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="4fa1f-229">Le résultat ressemble à l’exemple tronqué suivant :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-229">The output is similar to the following truncated example:</span></span>

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

<span data-ttu-id="4fa1f-230">Attendez que l’état du disque du système d’exploitation signale **VMRestartPending**, puis redémarrez votre machine virtuelle avec [az vm restart](/cli/azure/vm#restart) :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-230">Wait until the status for the OS disk reports **VMRestartPending**, then restart your VM with [az vm restart](/cli/azure/vm#restart):</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="4fa1f-231">Le processus de chiffrement de disque est finalisé pendant le processus de démarrage, aussi attendez quelques minutes avant de vérifier à nouveau l’état de chiffrement à l’aide de **az vm encryption show** :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-231">The disk encryption process is finalized during the boot process, so wait a few minutes before checking the status of encryption again with **az vm encryption show**:</span></span>

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="4fa1f-232">L’état doit maintenant signaler que le disque du système d’exploitation et le disque de données ont l’état **Chiffré**.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-232">The status should now report both the OS disk and data disk as **Encrypted**.</span></span>


## <a name="add-additional-data-disks"></a><span data-ttu-id="4fa1f-233">Ajouter des disques de données supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4fa1f-233">Add additional data disks</span></span>
<span data-ttu-id="4fa1f-234">Une fois que vous avez chiffré vos disques de données, vous pouvez ajouter ultérieurement d’autres disques virtuels à votre machine virtuelle et également les chiffrer.</span><span class="sxs-lookup"><span data-stu-id="4fa1f-234">Once you have encrypted your data disks, you can later add additional virtual disks to your VM and also encrypt them.</span></span> <span data-ttu-id="4fa1f-235">Par exemple, ajoutons un second disque virtuel à votre machine virtuelle comme suit :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-235">For example, lets add a second virtual disk to your VM as follows:</span></span>

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

<span data-ttu-id="4fa1f-236">Réexécutez la commande pour chiffrer les disques virtuels de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="4fa1f-236">Re-run the command to encrypt the virtual disks as follows:</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="4fa1f-237">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4fa1f-237">Next steps</span></span>
* <span data-ttu-id="4fa1f-238">Pour plus d’informations sur la gestion du coffre de clés Azure, y compris la suppression des clés de chiffrement et des coffres, consultez [Gérer le coffre de clés à l’aide de l’interface de ligne de commande](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="4fa1f-238">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="4fa1f-239">Pour plus d’informations sur le chiffrement de disque, notamment la préparation d’une machine virtuelle personnalisée chiffrée à télécharger vers Azure, consultez [Chiffrement de disque Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="4fa1f-239">For more information about disk encryption, such as preparing an encrypted custom VM to upload to Azure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
