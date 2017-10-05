---
title: "Comment redimensionner une machine virtuelle Linux avec Azure CLI 2.0 | Microsoft Docs"
description: "Comment augmenter ou diminuer les capacités d’une machine virtuelle Linux, en en modifiant la taille."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: e163f878-b919-45c5-9f5a-75a64f3b14a0
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2017
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23fc9f7f34732079682857d4ee685fe811751698
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a><span data-ttu-id="0720a-103">Redimensionner une machine virtuelle Linux avec CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0720a-103">Resize a Linux virtual machine using CLI 2.0</span></span>

<span data-ttu-id="0720a-104">Après avoir approvisionné une machine virtuelle, vous pouvez le mettre à l’échelle en en modifiant la [taille][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="0720a-104">After you provision a virtual machine (VM), you can scale the VM up or down by changing the [VM size][vm-sizes].</span></span> <span data-ttu-id="0720a-105">Dans certains cas, vous devez commencer par libérer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0720a-105">In some cases, you must deallocate the VM first.</span></span> <span data-ttu-id="0720a-106">C’est le cas notamment lorsque la taille souhaitée n’est pas disponible sur le cluster matériel qui héberge la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0720a-106">You need to deallocate the VM if the desired size is not available on the hardware cluster that is hosting the VM.</span></span> <span data-ttu-id="0720a-107">Cet article explique comment redimensionner une machine virtuelle Linux avec Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="0720a-107">This article details how to resize a Linux VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="0720a-108">Vous pouvez également effectuer ces étapes à l’aide [d’Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0720a-108">You can also perform these steps with the [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="resize-a-vm"></a><span data-ttu-id="0720a-109">Redimensionner une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="0720a-109">Resize a VM</span></span>
<span data-ttu-id="0720a-110">Pour redimensionner une machine virtuelle, vous devez disposer de la dernière version [d’Azure CLI 2.0](/cli/azure/install-az-cli2) et vous connecter à un compte Azure avec la commande [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="0720a-110">To resize a VM, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

1. <span data-ttu-id="0720a-111">Affichez la liste des tailles de machine virtuelle disponibles dans le cluster matériel qui héberge la machine virtuelle à l’aide de la commande [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span><span class="sxs-lookup"><span data-stu-id="0720a-111">View the list of available VM sizes on the hardware cluster where the VM is hosted with [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span></span> <span data-ttu-id="0720a-112">L’exemple suivant répertorie les tailles de machine virtuelle pour la machine virtuelle nommée `myVM` dans la région du groupe de ressources `myResourceGroup` :</span><span class="sxs-lookup"><span data-stu-id="0720a-112">The following example lists VM sizes for the VM named `myVM` in the resource group `myResourceGroup` region:</span></span>
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. <span data-ttu-id="0720a-113">Si la taille de machine virtuelle souhaitée est répertoriée, redimensionnez la machine virtuelle avec la commande [az vm resize](/cli/azure/vm#resize).</span><span class="sxs-lookup"><span data-stu-id="0720a-113">If the desired VM size is listed, resize the VM with [az vm resize](/cli/azure/vm#resize).</span></span> <span data-ttu-id="0720a-114">L’exemple suivant redimensionne la machine virtuelle nommée `myVM` à la taille `Standard_DS3_v2` :</span><span class="sxs-lookup"><span data-stu-id="0720a-114">The following example resizes the VM named `myVM` to the `Standard_DS3_v2` size:</span></span>
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    <span data-ttu-id="0720a-115">La machine virtuelle redémarre pendant le processus.</span><span class="sxs-lookup"><span data-stu-id="0720a-115">The VM restarts during this process.</span></span> <span data-ttu-id="0720a-116">Après le redémarrage, votre système d’exploitation existant et les disques de données sont remappés.</span><span class="sxs-lookup"><span data-stu-id="0720a-116">After the restart, your existing OS and data disks are remapped.</span></span> <span data-ttu-id="0720a-117">Tout le contenu du disque temporaire est perdu.</span><span class="sxs-lookup"><span data-stu-id="0720a-117">Anything on the temporary disk is lost.</span></span>

3. <span data-ttu-id="0720a-118">Si la taille de machine virtuelle souhaitée n’est pas répertoriée, vous devez d’abord libérer la machine virtuelle avec la commande [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="0720a-118">If the desired VM size is not listed, you need to first deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="0720a-119">Ce processus permet de redimensionner ensuite la machine virtuelle à n’importe quelle taille disponible dans la région, puis de la redémarrer.</span><span class="sxs-lookup"><span data-stu-id="0720a-119">This process allows the VM to then be resized to any size available that the region supports and then started.</span></span> <span data-ttu-id="0720a-120">Les étapes suivantes consistent à libérer, redimensionner, puis démarrer la machine virtuelle nommée `myVM` dans le groupe de ressources nommé `myResourceGroup` :</span><span class="sxs-lookup"><span data-stu-id="0720a-120">The following steps deallocate, resize, and then start the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="0720a-121">Le fait de libérer la machine virtuelle libère également toutes les adresses IP dynamiques affectées à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0720a-121">Deallocating the VM also releases any dynamic IP addresses assigned to the VM.</span></span> <span data-ttu-id="0720a-122">Les disques de données et du système d’exploitation ne sont pas affectés.</span><span class="sxs-lookup"><span data-stu-id="0720a-122">The OS and data disks are not affected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0720a-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0720a-123">Next steps</span></span>
<span data-ttu-id="0720a-124">Pour une évolutivité supplémentaire, exécutez plusieurs instances de machine virtuelle et augmentez leur taille.</span><span class="sxs-lookup"><span data-stu-id="0720a-124">For additional scalability, run multiple VM instances and scale out.</span></span> <span data-ttu-id="0720a-125">Pour plus d’informations, consultez [Mise à l’échelle automatique des machines Linux dans un groupe de machines virtuelles à échelle identique][scale-set].</span><span class="sxs-lookup"><span data-stu-id="0720a-125">For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
