---
title: aaaHow tooresize un VM Linux avec hello Azure CLI 1.0 | Documents Microsoft
description: "Comment tooscale des ou mise à l’échelle vers le bas d’une machine virtuelle Linux, en modifiant hello taille de machine virtuelle."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2016
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 43dd955dc2f2dd9d1b2da07ecbfbf2459bcaa4d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-vm-with-azure-cli-10"></a><span data-ttu-id="f1197-103">Redimensionner une machine virtuelle Linux avec Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f1197-103">Resize a Linux VM with Azure CLI 1.0</span></span>

## <a name="overview"></a><span data-ttu-id="f1197-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f1197-104">Overview</span></span>

<span data-ttu-id="f1197-105">Une fois que vous configurez un ordinateur virtuel (VM), vous pouvez augmenter ou diminuer la hello machine virtuelle en modifiant hello [taille de machine virtuelle][vm-sizes].</span><span class="sxs-lookup"><span data-stu-id="f1197-105">After you provision a virtual machine (VM), you can scale hello VM up or down by changing hello [VM size][vm-sizes].</span></span> <span data-ttu-id="f1197-106">Dans certains cas, vous devez libérer hello VM tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="f1197-106">In some cases, you must deallocate hello VM first.</span></span> <span data-ttu-id="f1197-107">Cela peut se produire si la nouvelle taille de hello n’est pas disponible sur le cluster de matériel hello qui héberge hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f1197-107">This can happen if hello new size is not available on hello hardware cluster that is hosting hello VM.</span></span>

<span data-ttu-id="f1197-108">Cet article explique comment tooresize un VM Linux à l’aide de hello [CLI d’Azure][azure-cli].</span><span class="sxs-lookup"><span data-stu-id="f1197-108">This article shows how tooresize a Linux VM using hello [Azure CLI][azure-cli].</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="f1197-109">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="f1197-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="f1197-110">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="f1197-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="f1197-111">[Azure CLI 1.0](#resize-a-linux-vm) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)</span><span class="sxs-lookup"><span data-stu-id="f1197-111">[Azure CLI 1.0](#resize-a-linux-vm) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="f1197-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello</span><span class="sxs-lookup"><span data-stu-id="f1197-112">[Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="resize-a-linux-vm"></a><span data-ttu-id="f1197-113">Redimensionner une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="f1197-113">Resize a Linux VM</span></span>
<span data-ttu-id="f1197-114">tooresize une machine virtuelle, effectuez hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="f1197-114">tooresize a VM, perform hello following steps.</span></span>

1. <span data-ttu-id="f1197-115">Exécutez hello suivant commande CLI.</span><span class="sxs-lookup"><span data-stu-id="f1197-115">Run hello following CLI command.</span></span> <span data-ttu-id="f1197-116">Cette commande répertorie les tailles de machine virtuelle hello qui sont disponibles sur le cluster de matériel hello où hello ordinateur virtuel est hébergé.</span><span class="sxs-lookup"><span data-stu-id="f1197-116">This command lists hello VM sizes that are available on hello hardware cluster where hello VM is hosted.</span></span>
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. <span data-ttu-id="f1197-117">Si hello souhaité est indiquée, exécutez hello suivant commande tooresize hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f1197-117">If hello desired size is listed, run hello following command tooresize hello VM.</span></span>
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    <span data-ttu-id="f1197-118">Hello machine virtuelle va redémarrer pendant ce processus.</span><span class="sxs-lookup"><span data-stu-id="f1197-118">hello VM will restart during this process.</span></span> <span data-ttu-id="f1197-119">Après le redémarrage de hello, votre système d’exploitation existant et les disques de données seront remappés.</span><span class="sxs-lookup"><span data-stu-id="f1197-119">After hello restart, your existing OS and data disks will be remapped.</span></span> <span data-ttu-id="f1197-120">Quoi que ce soit sur le disque temporaire de hello seront perdu.</span><span class="sxs-lookup"><span data-stu-id="f1197-120">Anything on hello temporary disk will be lost.</span></span>
   
    <span data-ttu-id="f1197-121">Hello d’utilisation `--enable-boot-diagnostics` option active [diagnostics de démarrage][boot-diagnostics], toolog tout toostartup connexes d’erreurs.</span><span class="sxs-lookup"><span data-stu-id="f1197-121">Use hello `--enable-boot-diagnostics` option enables [boot diagnostics][boot-diagnostics], toolog any errors related toostartup.</span></span>
3. <span data-ttu-id="f1197-122">Dans le cas contraire, si hello souhaité de taille n’est pas répertoriée, exécutez hello suivant les commandes toodeallocate hello VM, redimensionner et redémarrez hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f1197-122">Otherwise, if hello desired size is not listed, run hello following commands toodeallocate hello VM, resize it, and then restart hello VM.</span></span>
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > <span data-ttu-id="f1197-123">Hello désallocation de machine virtuelle libère aussi toutes les adresses IP dynamiques affectées toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f1197-123">Deallocating hello VM also releases any dynamic IP addresses assigned toohello VM.</span></span> <span data-ttu-id="f1197-124">Hello du système d’exploitation et des disques de données ne sont pas affectées.</span><span class="sxs-lookup"><span data-stu-id="f1197-124">hello OS and data disks are not affected.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="f1197-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f1197-125">Next steps</span></span>
<span data-ttu-id="f1197-126">Pour une évolutivité supplémentaire, exécutez plusieurs instances de machine virtuelle et augmentez leur taille. Pour plus d’informations, consultez [Mise à l’échelle automatique des machines Linux dans un groupe de machines virtuelles à échelle identique][scale-set].</span><span class="sxs-lookup"><span data-stu-id="f1197-126">For additional scalability, run multiple VM instances and scale out. For more information, see [Automatically scale Linux machines in a Virtual Machine Scale Set][scale-set].</span></span> 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
