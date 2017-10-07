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
# <a name="convert-azure-managed-disks-storage-from-standard-toopremium-and-vice-versa"></a>Convertir Azure le stockage des disques géré à partir de toopremium standard et vice versa

Managed Disks propose deux options de stockage : [Premium](../../storage/storage-premium-storage.md) (SSD) et [Standard](../../storage/storage-standard-storage.md) (HDD). Il vous permet de basculer tooeasily d’options hello deux avec un temps mort minimal selon vos besoins de performances. Cette fonctionnalité n’est pas disponible pour les disques non gérés. Toutefois, vous pouvez facilement [convertir les disques toomanaged](convert-unmanaged-to-managed-disks.md) commutateur tooeasily entre les options hello deux.

Cet article explique comment tooconvert des disques gérés par à partir de toopremium standard et vice versa à l’aide de CLI d’Azure. Si vous avez besoin de tooinstall ou mettre à niveau, consultez [installer Azure CLI 2.0](/cli/azure/install-azure-cli.md). 

## <a name="before-you-begin"></a>Avant de commencer

* conversion de Hello nécessite un redémarrage de machine virtuelle de hello, par conséquent, planifier la migration de votre stockage de disques hello pendant une fenêtre de maintenance existant. 
* Si vous utilisez des disques non managés, tout d’abord [convertir les disques toomanaged](convert-unmanaged-to-managed-disks.md) toouse tooswitch de cet article entre les options de stockage hello deux. 


## <a name="convert-all-hello-managed-disks-of-a-vm-from-standard-toopremium-and-vice-versa"></a>Convertir toutes les hello gérés disques d’une machine virtuelle à partir de toopremium standard et vice versa

Bonjour l’exemple suivant, nous montrons comment tooswitch tous hello disques d’une machine virtuelle à partir du stockage de toopremium standard. des disques gérés par toouse premium, votre machine virtuelle doit utiliser un [taille de machine virtuelle](sizes.md) qui prend en charge le stockage premium. Cet exemple bascule également taille tooa qui prend en charge le stockage premium.

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
## <a name="convert-a-managed-disk-from-standard-toopremium-and-vice-versa"></a>Convertir un disque géré à partir de toopremium standard et vice versa

Pour votre charge de travail de développement et de test, vous voudrez mélange toohave de disques standard et premium tooreduce votre coût. Vous pouvez l’effectuer en mettant à niveau toopremium stockage, seuls les disques hello qui nécessitent de meilleures performances. Bonjour l’exemple suivant, nous montrons comment tooswitch un seul disque d’un ordinateur virtuel à partir du stockage de toopremium standard et vice versa. des disques gérés par toouse premium, votre machine virtuelle doit utiliser un [taille de machine virtuelle](sizes.md) qui prend en charge le stockage premium. Cet exemple bascule également taille tooa qui prend en charge le stockage premium.

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

## <a name="next-steps"></a>Étapes suivantes

Créez une copie en lecture seule d’une machine virtuelle en utilisant des [captures instantanées](snapshot-copy-managed-disk.md).

