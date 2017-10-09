---
title: aaaAzure exemple de Script CLI - chiffrer un VM Linux | Documents Microsoft
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
ms.openlocfilehash: 1e455da4a8ea6d75b6d0d74b338d2e4d84973413
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="50759-103">Chiffrer une machine virtuelle Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="50759-103">Encrypt a Linux virtual machine in Azure</span></span>

<span data-ttu-id="50759-104">Ce script crée une solution Key Vault sécurisée, des clés de chiffrement, un principal de service Azure Active Directory et une machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="50759-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Linux virtual machine (VM).</span></span> <span data-ttu-id="50759-105">Hello machine virtuelle est ensuite chiffrée à l’aide de la clé de chiffrement hello coffre de clés et les informations d’identification du principal de service.</span><span class="sxs-lookup"><span data-stu-id="50759-105">hello VM is then encrypted using hello encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="50759-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="50759-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_vm.sh "Encrypt VM disks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="50759-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="50759-107">Clean up deployment</span></span> 

<span data-ttu-id="50759-108">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="50759-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="50759-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="50759-109">Script explanation</span></span>

<span data-ttu-id="50759-110">Ce script utilise hello suivant toocreate de commandes d’un ordinateur virtuel ressource groupe, le coffre de clés Azure, service principal, et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="50759-110">This script uses hello following commands toocreate a resource group, Azure Key Vault, service principal, virtual machine, and all related resources.</span></span> <span data-ttu-id="50759-111">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="50759-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="50759-112">Commande</span><span class="sxs-lookup"><span data-stu-id="50759-112">Command</span></span> | <span data-ttu-id="50759-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="50759-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="50759-114">az group create</span><span class="sxs-lookup"><span data-stu-id="50759-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="50759-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="50759-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="50759-116">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="50759-116">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="50759-117">Crée une coffre de clés Azure toostore sécuriser les données telles que des clés de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="50759-117">Creates an Azure Key Vault toostore secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="50759-118">az keyvault key create</span><span class="sxs-lookup"><span data-stu-id="50759-118">az keyvault key create</span></span>](https://docs.microsoft.com/cli/azure/keyvault/key#create) | <span data-ttu-id="50759-119">Crée une clé de chiffrement dans Key Vault.</span><span class="sxs-lookup"><span data-stu-id="50759-119">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="50759-120">az ad sp create-for-rbac</span><span class="sxs-lookup"><span data-stu-id="50759-120">az ad sp create-for-rbac</span></span>](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | <span data-ttu-id="50759-121">Crée un service Azure Active Directory toosecurely principal authentifier et contrôler les clés d’accès tooencryption.</span><span class="sxs-lookup"><span data-stu-id="50759-121">Creates an Azure Active Directory service principal toosecurely authenticate and control access tooencryption keys.</span></span> |
| [<span data-ttu-id="50759-122">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="50759-122">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="50759-123">Définit des autorisations sur hello coffre de clés toogrant hello service principal tooencryption clés d’accès.</span><span class="sxs-lookup"><span data-stu-id="50759-123">Sets permissions on hello Key Vault toogrant hello service principal access tooencryption keys.</span></span> |
| [<span data-ttu-id="50759-124">az vm create</span><span class="sxs-lookup"><span data-stu-id="50759-124">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="50759-125">Crée la machine virtuelle de hello et connecte une carte réseau de toohello, du réseau virtuel, sous-réseau et groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="50759-125">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="50759-126">Cette commande spécifie également toobe d’image de machine virtuelle hello utilisé et les informations d’identification administratives.</span><span class="sxs-lookup"><span data-stu-id="50759-126">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="50759-127">az vm encryption enable</span><span class="sxs-lookup"><span data-stu-id="50759-127">az vm encryption enable</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | <span data-ttu-id="50759-128">Active le chiffrement sur une machine virtuelle à l’aide des informations d’identification de hello service principal et la clé de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="50759-128">Enables encryption on a VM using hello service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="50759-129">az vm encryption show</span><span class="sxs-lookup"><span data-stu-id="50759-129">az vm encryption show</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#show) | <span data-ttu-id="50759-130">Montre l’état hello Hello processus de chiffrement de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="50759-130">Shows hello status of hello VM encryption process.</span></span> |
| [<span data-ttu-id="50759-131">az group delete</span><span class="sxs-lookup"><span data-stu-id="50759-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="50759-132">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="50759-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="50759-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="50759-133">Next steps</span></span>

<span data-ttu-id="50759-134">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="50759-134">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="50759-135">Exemples de script CLI supplémentaires de l’ordinateur virtuel se trouvent dans hello [documentation de la machine virtuelle de Azure Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="50759-135">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
