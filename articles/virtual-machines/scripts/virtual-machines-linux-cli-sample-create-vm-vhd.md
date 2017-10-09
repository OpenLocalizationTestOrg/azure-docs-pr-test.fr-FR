---
title: "aaaAzure exemple de Script CLI - créer une machine virtuelle avec un disque dur virtuel | Documents Microsoft"
description: "Exemple de script Azure CLI - Créez une machine virtuelle avec un disque dur virtuel (VHD)."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/09/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: ce39092697a51e4e8a8e59ba8eb919955f616458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a><span data-ttu-id="77079-103">Créer une machine virtuelle avec un disque dur virtuel (VHD)</span><span class="sxs-lookup"><span data-stu-id="77079-103">Create a VM with a virtual hard disk</span></span>

<span data-ttu-id="77079-104">Cet exemple crée une machine virtuelle à l’aide d’un disque dur virtuel (VHD).</span><span class="sxs-lookup"><span data-stu-id="77079-104">This example creates a virtual machine using a VHD.</span></span>
<span data-ttu-id="77079-105">Il crée un groupe de ressources, un compte de stockage et un conteneur, puis il crée une machine virtuelle en téléchargeant le conteneur de toohello de disque dur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="77079-105">It creates a resource group, a storage account, and a container, then it creates a VM by uploading hello VHD toohello container.</span></span>
<span data-ttu-id="77079-106">Il remplace hello ssh public de clé avec votre clé publique afin que vous ayez accès toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="77079-106">It replaces hello ssh public key with your public key so that you have access toohello VM.</span></span>

<span data-ttu-id="77079-107">Vous devez disposer d’un VHD amorçable.</span><span class="sxs-lookup"><span data-stu-id="77079-107">You'll need a bootable VHD.</span></span>
<span data-ttu-id="77079-108">Vous pouvez télécharger hello VHD que nous avons utilisés à partir de https://azclisamples.blob.core.windows.net/vhds/sample.vhd, ou utiliser votre propre disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="77079-108">You can download hello VHD that we used from https://azclisamples.blob.core.windows.net/vhds/sample.vhd, or use your own VHD.</span></span> <span data-ttu-id="77079-109">script de Hello recherche `~/sample.vhd`.</span><span class="sxs-lookup"><span data-stu-id="77079-109">hello script looks for `~/sample.vhd`.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="77079-110">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="77079-110">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]

## <a name="clean-up-deployment"></a><span data-ttu-id="77079-111">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="77079-111">Clean up deployment</span></span> 

<span data-ttu-id="77079-112">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="77079-112">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a><span data-ttu-id="77079-113">Explication du script</span><span class="sxs-lookup"><span data-stu-id="77079-113">Script explanation</span></span>

<span data-ttu-id="77079-114">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, machine virtuelle, haute disponibilité, équilibrage de charge et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="77079-114">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="77079-115">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="77079-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="77079-116">Commande</span><span class="sxs-lookup"><span data-stu-id="77079-116">Command</span></span> | <span data-ttu-id="77079-117">Remarques</span><span class="sxs-lookup"><span data-stu-id="77079-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="77079-118">az group create</span><span class="sxs-lookup"><span data-stu-id="77079-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="77079-119">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="77079-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="77079-120">az storage account list</span><span class="sxs-lookup"><span data-stu-id="77079-120">az storage account list</span></span>](https://docs.microsoft.com/cli/azure/storage/account#list) | <span data-ttu-id="77079-121">Répertorie les comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="77079-121">Lists storage accounts</span></span> |
| [<span data-ttu-id="77079-122">az storage account check-name</span><span class="sxs-lookup"><span data-stu-id="77079-122">az storage account check-name</span></span>](https://docs.microsoft.com/cli/azure/storage/account#check-name) | <span data-ttu-id="77079-123">Vérifie qu’un nom de compte de stockage est valide et qu’il n’existe pas déjà</span><span class="sxs-lookup"><span data-stu-id="77079-123">Checks that a storage account name is valid and that it doesn't already exist</span></span> |
| [<span data-ttu-id="77079-124">az storage account keys list</span><span class="sxs-lookup"><span data-stu-id="77079-124">az storage account keys list</span></span>](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | <span data-ttu-id="77079-125">Répertorie les clés pour les comptes de stockage hello</span><span class="sxs-lookup"><span data-stu-id="77079-125">Lists keys for hello storage accounts</span></span> |
| [<span data-ttu-id="77079-126">az storage blob exists</span><span class="sxs-lookup"><span data-stu-id="77079-126">az storage blob exists</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#exists) | <span data-ttu-id="77079-127">Vérifie l’existence d’un objet blob de hello</span><span class="sxs-lookup"><span data-stu-id="77079-127">Checks whether hello blob exists</span></span> |
| [<span data-ttu-id="77079-128">az storage container create</span><span class="sxs-lookup"><span data-stu-id="77079-128">az storage container create</span></span>](https://docs.microsoft.com/cli/azure/storage/container#create) | <span data-ttu-id="77079-129">Crée un conteneur dans un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="77079-129">Creates a container in a storage account.</span></span> |
| [<span data-ttu-id="77079-130">az storage blob upload</span><span class="sxs-lookup"><span data-stu-id="77079-130">az storage blob upload</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#upload) | <span data-ttu-id="77079-131">Crée un objet blob dans le conteneur de hello par téléchargement hello de disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="77079-131">Creates a blob in hello container by uploading hello VHD.</span></span> |
| [<span data-ttu-id="77079-132">az vm list</span><span class="sxs-lookup"><span data-stu-id="77079-132">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="77079-133">Utilisé avec `--query` vérifier si le nom d’ordinateur virtuel hello est en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="77079-133">Used with `--query` check whether hello VM name is in use.</span></span> | 
| [<span data-ttu-id="77079-134">az vm create</span><span class="sxs-lookup"><span data-stu-id="77079-134">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="77079-135">Crée des machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="77079-135">Creates hello virtual machines.</span></span> |
| [<span data-ttu-id="77079-136">az vm access set-linux-user</span><span class="sxs-lookup"><span data-stu-id="77079-136">az vm access set-linux-user</span></span>](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | <span data-ttu-id="77079-137">Réinitialise hello SSH toogive clé hello actuel utilisateur accès toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="77079-137">Resets hello SSH key toogive hello current user access toohello VM.</span></span> |
| [<span data-ttu-id="77079-138">az vm list-ip-addresses</span><span class="sxs-lookup"><span data-stu-id="77079-138">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="77079-139">Obtient l’adresse IP de hello Hello machine virtuelle qui a été créé.</span><span class="sxs-lookup"><span data-stu-id="77079-139">Gets hello IP address of hello VM that was created.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="77079-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="77079-140">Next steps</span></span>

<span data-ttu-id="77079-141">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="77079-141">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="77079-142">Exemples de script CLI supplémentaires de l’ordinateur virtuel se trouvent dans hello [documentation de la machine virtuelle de Azure Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="77079-142">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
