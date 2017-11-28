---
title: aaaHow tooresize un VM Linux avec hello Azure CLI 2.0 | Documents Microsoft
description: "Comment tooscale des ou mise à l’échelle vers le bas d’une machine virtuelle Linux, en modifiant hello taille de machine virtuelle."
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
ms.openlocfilehash: e8fba485b5bcc7824f546de5cf3df77624a28008
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a><span data-ttu-id="534b2-103">Redimensionner une machine virtuelle Linux avec CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="534b2-103">Resize a Linux virtual machine using CLI 2.0</span></span>

<span data-ttu-id="534b2-104">Une fois que vous configurez un ordinateur virtuel (VM), vous pouvez augmenter ou diminuer la hello machine virtuelle en modifiant hello [taille de machine virtuelle][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="534b2-104">After you provision a virtual machine (VM), you can scale hello VM up or down by changing hello [VM size][vm-sizes].</span></span> <span data-ttu-id="534b2-105">Dans certains cas, vous devez libérer hello VM tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="534b2-105">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="534b2-106">Vous devez toodeallocate hello machine virtuelle si vous le souhaitez hello taille n’est pas disponible sur le cluster de matériel hello qui héberge hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="534b2-106">You need toodeallocate hello VM if hello desired size is not available on hello hardware cluster that is hosting hello VM.</span></span> <span data-ttu-id="534b2-107">Cet article décrit en détail comment tooresize un VM Linux avec hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="534b2-107">This article details how tooresize a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="534b2-108">Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="534b2-108">You can also perform these steps with hello [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="resize-a-vm"></a><span data-ttu-id="534b2-109">Redimensionner une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="534b2-109">Resize a VM</span></span>
<span data-ttu-id="534b2-110">tooresize une machine virtuelle, vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="534b2-110">tooresize a VM, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

1. <span data-ttu-id="534b2-111">Afficher la liste hello des ordinateurs virtuels disponibles sur le cluster de matériel hello où hello machine virtuelle est hébergée avec des tailles de [az vm-vm-resize-options de la liste](/cli/azure/vm#list-vm-resize-options).</span><span class="sxs-lookup"><span data-stu-id="534b2-111">View hello list of available VM sizes on hello hardware cluster where hello VM is hosted with [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options).</span></span> <span data-ttu-id="534b2-112">Hello exemple suivant répertorie les tailles de machine virtuelle pour hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello `myResourceGroup` région :</span><span class="sxs-lookup"><span data-stu-id="534b2-112">hello following example lists VM sizes for hello VM named `myVM` in hello resource group `myResourceGroup` region:</span></span>
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. <span data-ttu-id="534b2-113">Si hello souhaité de taille de machine virtuelle est répertoriée, redimensionner hello machine virtuelle avec [az vm redimensionner](/cli/azure/vm#resize).</span><span class="sxs-lookup"><span data-stu-id="534b2-113">If hello desired VM size is listed, resize hello VM with [az vm resize](/cli/azure/vm#resize).</span></span> <span data-ttu-id="534b2-114">Hello suivant redimensionne de l’exemple hello ordinateur virtuel nommé `myVM` toohello `Standard_DS3_v2` taille :</span><span class="sxs-lookup"><span data-stu-id="534b2-114">hello following example resizes hello VM named `myVM` toohello `Standard_DS3_v2` size:</span></span>
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    <span data-ttu-id="534b2-115">Hello machine virtuelle redémarre pendant ce processus.</span><span class="sxs-lookup"><span data-stu-id="534b2-115">hello VM restarts during this process.</span></span> <span data-ttu-id="534b2-116">Après le redémarrage de hello, votre système d’exploitation existant et les disques de données sont remappés.</span><span class="sxs-lookup"><span data-stu-id="534b2-116">After hello restart, your existing OS and data disks are remapped.</span></span> <span data-ttu-id="534b2-117">Quoi que ce soit sur le disque temporaire de hello est perdu.</span><span class="sxs-lookup"><span data-stu-id="534b2-117">Anything on hello temporary disk is lost.</span></span>

3. <span data-ttu-id="534b2-118">Si hello souhaité de taille de machine virtuelle n’est pas répertorié, vous devez toofirst désallouer hello machine virtuelle avec [az vm désallouer](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="534b2-118">If hello desired VM size is not listed, you need toofirst deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="534b2-119">Ce processus autorise hello VM toothen être redimensionné tooany taille disponible qui prend en charge de la région de hello, puis démarré.</span><span class="sxs-lookup"><span data-stu-id="534b2-119">This process allows hello VM toothen be resized tooany size available that hello region supports and then started.</span></span> <span data-ttu-id="534b2-120">Hello suit désallouer, redimensionner et puis démarrez hello ordinateur virtuel nommé `myVM` dans le groupe de ressources hello nommé `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="534b2-120">hello following steps deallocate, resize, and then start hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="534b2-121">Hello désallocation de machine virtuelle libère aussi toutes les adresses IP dynamiques affectées toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="534b2-121">Deallocating hello VM also releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="534b2-122">Hello du système d’exploitation et des disques de données ne sont pas affectées.</span><span class="sxs-lookup"><span data-stu-id="534b2-122">hello OS and data disks are not affected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="534b2-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="534b2-123">Next steps</span></span>
<span data-ttu-id="534b2-124">Pour une évolutivité supplémentaire, exécutez plusieurs instances de machine virtuelle et augmentez leur taille. Pour plus d’informations, consultez [Mise à l’échelle automatique des machines Linux dans un groupe de machines virtuelles à échelle identique][scale-set].</span><span class="sxs-lookup"><span data-stu-id="534b2-124">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
