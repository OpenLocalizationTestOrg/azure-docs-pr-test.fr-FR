---
title: "disque aaaExpand du système d’exploitation Linux VM par hello Azure CLI 1.0 | Documents Microsoft"
description: "Découvrez comment tooexpand hello le système d’exploitation (OS) de disque virtuel sur un VM Linux à l’aide de hello Azure CLI 1.0 et le modèle de déploiement du Gestionnaire de ressources hello"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0db78c0b86b48b2c5358611e11bb0b7ad781a559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="expand-os-disk-on-a-linux-vm-using-hello-azure-cli-with-hello-azure-cli-10"></a><span data-ttu-id="a8beb-103">Développez le disque du système d’exploitation sur un VM Linux à l’aide de hello CLI d’Azure avec hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a8beb-103">Expand OS disk on a Linux VM using hello Azure CLI with hello Azure CLI 1.0</span></span>
<span data-ttu-id="a8beb-104">taille de disque dur virtuel par défaut Hello hello système d’exploitation (OS) est généralement 30 Go sur un ordinateur virtuel de Linux (VM) dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a8beb-104">hello default virtual hard disk size for hello operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="a8beb-105">Vous pouvez [ajouter des disques de données](add-disk.md) tooprovide d’espace de stockage supplémentaire, mais vous souhaiterez peut-être également disque hello du système d’exploitation de tooexpand.</span><span class="sxs-lookup"><span data-stu-id="a8beb-105">You can [add data disks](add-disk.md) tooprovide for additional storage space, but you may also wish tooexpand hello OS disk.</span></span> <span data-ttu-id="a8beb-106">Cet article décrit en détail comment tooexpand hello du système d’exploitation du disque pour un VM Linux à l’aide de disques non managés avec hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="a8beb-106">This article details how tooexpand hello OS disk for a Linux VM using unmanaged disks with hello Azure CLI 1.0.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="a8beb-107">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="a8beb-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="a8beb-108">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="a8beb-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="a8beb-109">[Azure CLI 1.0](#prerequisites) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)</span><span class="sxs-lookup"><span data-stu-id="a8beb-109">[Azure CLI 1.0](#prerequisites) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="a8beb-110">[Azure CLI 2.0](expand-disks.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello</span><span class="sxs-lookup"><span data-stu-id="a8beb-110">[Azure CLI 2.0](expand-disks.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8beb-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a8beb-111">Prerequisites</span></span>
<span data-ttu-id="a8beb-112">Vous devez hello [dernière Azure CLI 1.0](../../cli-install-nodejs.md) installé et enregistré dans tooan [compte Azure](https://azure.microsoft.com/pricing/free-trial/) en utilisant le mode Gestionnaire de ressources hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a8beb-112">You need hello [latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in tooan [Azure account](https://azure.microsoft.com/pricing/free-trial/) using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="a8beb-113">Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="a8beb-113">In hello following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="a8beb-114">Les noms de paramètre sont par exemple *myResourceGroup* et *myVM*.</span><span class="sxs-lookup"><span data-stu-id="a8beb-114">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

## <a name="expand-os-disk"></a><span data-ttu-id="a8beb-115">Développer le disque du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="a8beb-115">Expand OS disk</span></span>

1. <span data-ttu-id="a8beb-116">Opérations sur les disques durs virtuels ne peuvent pas être effectuées avec hello machine virtuelle en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="a8beb-116">Operations on virtual hard disks cannot be performed with hello VM running.</span></span> <span data-ttu-id="a8beb-117">Hello exemple suivant arrête et désalloue hello ordinateur virtuel nommé *myVM* dans le groupe de ressources hello nommé *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="a8beb-117">hello following example stops and deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="a8beb-118">`azure vm stop`ne libère pas de ressources de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="a8beb-118">`azure vm stop` does not release hello compute resources.</span></span> <span data-ttu-id="a8beb-119">toorelease des ressources de calcul, utilisez `azure vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="a8beb-119">toorelease compute resources, use `azure vm deallocate`.</span></span> <span data-ttu-id="a8beb-120">Hello machine virtuelle doit être libérée tooexpand hello un disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="a8beb-120">hello VM must be deallocated tooexpand hello virtual hard disk.</span></span>

2. <span data-ttu-id="a8beb-121">Mettre à jour de la taille de hello du disque du système d’exploitation hello non managée à l’aide de hello `azure vm set` commande.</span><span class="sxs-lookup"><span data-stu-id="a8beb-121">Update hello size of hello unmanaged OS disk using hello `azure vm set` command.</span></span> <span data-ttu-id="a8beb-122">Hello après les mises à jour de l’exemple hello ordinateur virtuel nommé *myVM* dans le groupe de ressources hello nommé *myResourceGroup* toobe *50* Go :</span><span class="sxs-lookup"><span data-stu-id="a8beb-122">hello following example updates hello VM named *myVM* in hello resource group named *myResourceGroup* toobe *50* GB:</span></span>

    ```azurecli
    azure vm set \
        --resource-group myResourceGroup \
        --name myVM \
        --new-os-disk-size 50
    ```

3. <span data-ttu-id="a8beb-123">Démarrez votre machine virtuelle comme suit :</span><span class="sxs-lookup"><span data-stu-id="a8beb-123">Start your VM as follows:</span></span>

    ```azurecli
    azure vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="a8beb-124">SSH tooyour machine virtuelle avec les informations d’identification appropriées hello.</span><span class="sxs-lookup"><span data-stu-id="a8beb-124">SSH tooyour VM with hello appropriate credentials.</span></span> <span data-ttu-id="a8beb-125">disque de hello du système d’exploitation tooverify a été redimensionné, utilisez `df -h`.</span><span class="sxs-lookup"><span data-stu-id="a8beb-125">tooverify hello OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="a8beb-126">Hello après la sortie de l’exemple montre la partition principale de hello (*/dev/sda1*) est maintenant de 50 Go :</span><span class="sxs-lookup"><span data-stu-id="a8beb-126">hello following example output shows hello primary partition (*/dev/sda1*) is now 50 GB:</span></span>

    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1.7G     0  1.7G   0% /dev
    tmpfs           344M  5.0M  340M   2% /run
    /dev/sda1        49G  1.3G   48G   3% /
    ```

## <a name="next-steps"></a><span data-ttu-id="a8beb-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a8beb-127">Next steps</span></span>
<span data-ttu-id="a8beb-128">Si vous avez besoin de stockage supplémentaire, vous également [ajouter des disques de données tooa Linux VM](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="a8beb-128">If you need additional storage, you also [add data disks tooa Linux VM](add-disk.md).</span></span> <span data-ttu-id="a8beb-129">Pour plus d’informations sur le chiffrement de disque, consultez [crypter les disques sur un VM Linux à l’aide de hello CLI d’Azure](encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="a8beb-129">For more information about disk encryption, see [Encrypt disks on a Linux VM using hello Azure CLI](encrypt-disks.md).</span></span>
