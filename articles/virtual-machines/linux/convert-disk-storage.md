---
title: "le stockage de disques géré d’aaaConvert Azure à partir de toopremium standard et vice versa | Documents Microsoft"
description: "Comment tooconvert Azure le stockage de disques géré à partir de toopremium standard et vice versa, à l’aide de CLI d’Azure."
services: virtual-machines-linux
documentationcenter: 
author: ramankum
manager: kavithag
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ramankum
ms.openlocfilehash: 261d77202f7fd381085c4e25211a5d0026f43b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="fa92c-103">Convertir Azure le stockage des disques géré à partir de toopremium standard et vice versa</span><span class="sxs-lookup"><span data-stu-id="fa92c-103">Convert Azure managed disks storage from standard toopremium, and vice versa</span></span>

<span data-ttu-id="fa92c-104">Managed Disks propose deux options de stockage : [Premium](../../storage/storage-premium-storage.md) (SSD) et [Standard](../../storage/storage-standard-storage.md) (HDD).</span><span class="sxs-lookup"><span data-stu-id="fa92c-104">Managed disks offers two storage options: [Premium](../../storage/storage-premium-storage.md) (SSD-based) and [Standard](../../storage/storage-standard-storage.md) (HDD-based).</span></span> <span data-ttu-id="fa92c-105">Il vous permet de basculer tooeasily d’options hello deux avec un temps mort minimal selon vos besoins de performances.</span><span class="sxs-lookup"><span data-stu-id="fa92c-105">It allows you tooeasily switch between hello two options with minimal downtime based on your performance needs.</span></span> <span data-ttu-id="fa92c-106">Cette fonctionnalité n’est pas disponible pour les disques non gérés.</span><span class="sxs-lookup"><span data-stu-id="fa92c-106">This capability is not available for unmanaged disks.</span></span> <span data-ttu-id="fa92c-107">Toutefois, vous pouvez facilement [convertir les disques toomanaged](convert-unmanaged-to-managed-disks.md) commutateur tooeasily entre les options hello deux.</span><span class="sxs-lookup"><span data-stu-id="fa92c-107">But you can easily [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) tooeasily switch between hello two options.</span></span>

<span data-ttu-id="fa92c-108">Cet article explique comment tooconvert des disques gérés par à partir de toopremium standard et vice versa à l’aide de CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="fa92c-108">This article shows you how tooconvert managed disks from standard toopremium, and vice versa by using Azure CLI.</span></span> <span data-ttu-id="fa92c-109">Si vous avez besoin de tooinstall ou mettre à niveau, consultez [installer Azure CLI 2.0](/cli/azure/install-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="fa92c-109">If you need tooinstall or upgrade it, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="fa92c-110">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="fa92c-110">Before you begin</span></span>

* <span data-ttu-id="fa92c-111">conversion de Hello nécessite un redémarrage de machine virtuelle de hello, par conséquent, planifier la migration de votre stockage de disques hello pendant une fenêtre de maintenance existant.</span><span class="sxs-lookup"><span data-stu-id="fa92c-111">hello conversion requires a restart of hello VM, so schedule hello migration of your disks storage during a pre-existing maintenance window.</span></span> 
* <span data-ttu-id="fa92c-112">Si vous utilisez des disques non managés, tout d’abord [convertir les disques toomanaged](convert-unmanaged-to-managed-disks.md) toouse tooswitch de cet article entre les options de stockage hello deux.</span><span class="sxs-lookup"><span data-stu-id="fa92c-112">If you are using unmanaged disks, first [convert toomanaged disks](convert-unmanaged-to-managed-disks.md) toouse this article tooswitch between hello two storage options.</span></span> 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="fa92c-113">Convertir toutes les hello gérés disques d’une machine virtuelle à partir de toopremium standard et vice versa</span><span class="sxs-lookup"><span data-stu-id="fa92c-113">Convert all hello managed disks of a VM from standard toopremium, and vice versa</span></span>

<span data-ttu-id="fa92c-114">Bonjour l’exemple suivant, nous montrons comment tooswitch tous hello disques d’une machine virtuelle à partir du stockage de toopremium standard.</span><span class="sxs-lookup"><span data-stu-id="fa92c-114">In hello following example, we show how tooswitch all hello disks of a VM from standard toopremium storage.</span></span> <span data-ttu-id="fa92c-115">des disques gérés par toouse premium, votre machine virtuelle doit utiliser un [taille de machine virtuelle](sizes.md) qui prend en charge le stockage premium.</span><span class="sxs-lookup"><span data-stu-id="fa92c-115">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="fa92c-116">Cet exemple bascule également taille tooa qui prend en charge le stockage premium.</span><span class="sxs-lookup"><span data-stu-id="fa92c-116">This example also switches tooa size that supports premium storage.</span></span>

 ```azurecli

#resource group that contains hello virtual machine
rgName='yourResourceGroup'

#Name of hello virtual machine
vmName='yourVM'

#Premium capable size 
#Required only if converting from standard toopremium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Deallocate hello VM before changing hello size of hello VM
az vm deallocate --name $vmName --resource-group $rgName

#Change hello VM size tooa size that supports premium storage 
#Skip this step if converting storage from premium toostandard
az vm resize --resource-group $rgName --name $vmName --size $size

#Update hello sku of all hello data disks 
az vm show -n $vmName -g $rgName --query storageProfile.dataDisks[*].managedDisk -o tsv \
 | awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

#Update hello sku of hello OS disk
az vm show -n $vmName -g $rgName --query storageProfile.osDisk.managedDisk -o tsv \
| awk -v sku=$sku '{system("az disk update --sku "sku" --ids "$1)}'

az vm start --name $vmName --resource-group $rgName

```
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a><span data-ttu-id="fa92c-117">Convertir un disque géré à partir de toopremium standard et vice versa</span><span class="sxs-lookup"><span data-stu-id="fa92c-117">Convert a managed disk from standard toopremium, and vice versa</span></span>

<span data-ttu-id="fa92c-118">Pour votre charge de travail de développement et de test, vous voudrez mélange toohave de disques standard et premium tooreduce votre coût.</span><span class="sxs-lookup"><span data-stu-id="fa92c-118">For your dev/test workload, you may want toohave mixture of standard and premium disks tooreduce your cost.</span></span> <span data-ttu-id="fa92c-119">Vous pouvez l’effectuer en mettant à niveau toopremium stockage, seuls les disques hello qui nécessitent de meilleures performances.</span><span class="sxs-lookup"><span data-stu-id="fa92c-119">You can accomplish it by upgrading toopremium storage, only hello disks that require better performance.</span></span> <span data-ttu-id="fa92c-120">Bonjour l’exemple suivant, nous montrons comment tooswitch un seul disque d’un ordinateur virtuel à partir du stockage de toopremium standard et vice versa.</span><span class="sxs-lookup"><span data-stu-id="fa92c-120">In hello following example, we show how tooswitch a single disk of a VM from standard toopremium storage, and vice versa.</span></span> <span data-ttu-id="fa92c-121">des disques gérés par toouse premium, votre machine virtuelle doit utiliser un [taille de machine virtuelle](sizes.md) qui prend en charge le stockage premium.</span><span class="sxs-lookup"><span data-stu-id="fa92c-121">toouse premium managed disks, your VM must use a [VM size](sizes.md) that supports premium storage.</span></span> <span data-ttu-id="fa92c-122">Cet exemple bascule également taille tooa qui prend en charge le stockage premium.</span><span class="sxs-lookup"><span data-stu-id="fa92c-122">This example also switches tooa size that supports premium storage.</span></span>

 ```azurecli

#resource group that contains hello managed disk
rgName='yourResourceGroup'

#Name of your managed disk
diskName='yourManagedDiskName'

#Premium capable size 
#Required only if converting from standard toopremium
size='Standard_DS2_v2'

#Choose between Standard_LRS and Premium_LRS based on your scenario
sku='Premium_LRS'

#Get hello parent VM Id 
vmId=$(az disk show --name $diskName --resource-group $rgName --query managedBy --output tsv)

#Deallocate hello VM before changing hello size of hello VM
az vm deallocate --ids $vmId 

#Change hello VM size tooa size that supports premium storage 
#Skip this step if converting storage from premium toostandard
az vm resize --ids $vmId --size $size

# Update hello sku
az disk update --sku $sku --name $diskName --resource-group $rgName 

az vm start --ids $vmId 
```

## <a name="next-steps"></a><span data-ttu-id="fa92c-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fa92c-123">Next steps</span></span>

<span data-ttu-id="fa92c-124">Créez une copie en lecture seule d’une machine virtuelle en utilisant des [captures instantanées](snapshot-copy-managed-disk.md).</span><span class="sxs-lookup"><span data-stu-id="fa92c-124">Take a read-only copy of a VM by using [snapshots](snapshot-copy-managed-disk.md).</span></span>

