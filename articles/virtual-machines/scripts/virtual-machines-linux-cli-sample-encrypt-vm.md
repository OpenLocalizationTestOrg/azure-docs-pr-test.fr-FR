---
title: "Exemple de script Azure CLI - Chiffrement d’une machine virtuelle Linux | Microsoft Docs"
description: "Exemple de script Azure CLI - Chiffrement d’une machine virtuelle Linux"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 9388bce04e37d049301521f808cd8494c327e335
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="encrypt-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="c86af-103">Chiffrer une machine virtuelle Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="c86af-103">Encrypt a Linux virtual machine in Azure</span></span>

<span data-ttu-id="c86af-104">Ce script crée une solution Key Vault sécurisée, des clés de chiffrement, un principal de service Azure Active Directory et une machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="c86af-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Linux virtual machine (VM).</span></span> <span data-ttu-id="c86af-105">La machine virtuelle est ensuite chiffrée à l’aide de la clé de chiffrement de Key Vault et des informations d’identification du principal de service.</span><span class="sxs-lookup"><span data-stu-id="c86af-105">The VM is then encrypted using the encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c86af-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="c86af-106">Sample script</span></span>

<span data-ttu-id="c86af-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_vm.sh "Chiffrer des disques de machine virtuelle")]</span><span class="sxs-lookup"><span data-stu-id="c86af-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_vm.sh "Encrypt VM disks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="c86af-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="c86af-108">Clean up deployment</span></span> 

<span data-ttu-id="c86af-109">Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="c86af-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c86af-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="c86af-110">Script explanation</span></span>

<span data-ttu-id="c86af-111">Ce script utilise les commandes suivantes pour créer un groupe de ressources, une solution Key Vault, un principal de service, une machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="c86af-111">This script uses the following commands to create a resource group, Azure Key Vault, service principal, virtual machine, and all related resources.</span></span> <span data-ttu-id="c86af-112">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="c86af-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c86af-113">Commande</span><span class="sxs-lookup"><span data-stu-id="c86af-113">Command</span></span> | <span data-ttu-id="c86af-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="c86af-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c86af-115">az group create</span><span class="sxs-lookup"><span data-stu-id="c86af-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c86af-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="c86af-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c86af-117">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="c86af-117">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="c86af-118">Crée une solution Key Vault pour stocker des données sécurisées, telles que des clés de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="c86af-118">Creates an Azure Key Vault to store secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="c86af-119">az keyvault key create</span><span class="sxs-lookup"><span data-stu-id="c86af-119">az keyvault key create</span></span>](https://docs.microsoft.com/cli/azure/keyvault/key#create) | <span data-ttu-id="c86af-120">Crée une clé de chiffrement dans Key Vault.</span><span class="sxs-lookup"><span data-stu-id="c86af-120">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="c86af-121">az ad sp create-for-rbac</span><span class="sxs-lookup"><span data-stu-id="c86af-121">az ad sp create-for-rbac</span></span>](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | <span data-ttu-id="c86af-122">Crée un principal de service Azure Active Directory pour authentifier et contrôler l’accès aux clés de chiffrement en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="c86af-122">Creates an Azure Active Directory service principal to securely authenticate and control access to encryption keys.</span></span> |
| [<span data-ttu-id="c86af-123">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="c86af-123">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="c86af-124">Définit les autorisations sur Key Vault pour accorder au principal de service l’accès aux clés de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="c86af-124">Sets permissions on the Key Vault to grant the service principal access to encryption keys.</span></span> |
| [<span data-ttu-id="c86af-125">az vm create</span><span class="sxs-lookup"><span data-stu-id="c86af-125">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="c86af-126">Crée la machine virtuelle et l’associe à la carte réseau, au réseau virtuel, au sous-réseau et au groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="c86af-126">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="c86af-127">Cette commande spécifie également l’image de machine virtuelle à utiliser ainsi que les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="c86af-127">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="c86af-128">az vm encryption enable</span><span class="sxs-lookup"><span data-stu-id="c86af-128">az vm encryption enable</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | <span data-ttu-id="c86af-129">Active le chiffrement sur une machine virtuelle en utilisant les informations d’identification du principal de service et la clé de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="c86af-129">Enables encryption on a VM using the service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="c86af-130">az vm encryption show</span><span class="sxs-lookup"><span data-stu-id="c86af-130">az vm encryption show</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#show) | <span data-ttu-id="c86af-131">Affiche l’état du processus de chiffrement de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c86af-131">Shows the status of the VM encryption process.</span></span> |
| [<span data-ttu-id="c86af-132">az group delete</span><span class="sxs-lookup"><span data-stu-id="c86af-132">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="c86af-133">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="c86af-133">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c86af-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c86af-134">Next steps</span></span>

<span data-ttu-id="c86af-135">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c86af-135">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c86af-136">Vous trouverez des exemples supplémentaires de scripts CLI de machine virtuelle dans la [documentation relative aux machines virtuelles Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c86af-136">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
