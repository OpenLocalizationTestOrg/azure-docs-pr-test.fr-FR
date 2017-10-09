---
title: aaaCommon PowerShell des commandes pour les Machines virtuelles Azure | Documents Microsoft
description: "Tooget de commandes PowerShell courantes que vous avez démarré création et gestion de vos machines virtuelles Windows Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ba3839a2-f3d5-4e19-a5de-95bfb1c0e61e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 3de9bd4d20259ced2c0aa8ef7a3f7d9520a071d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="common-powershell-commands-for-creating-and-managing-azure-virtual-machines"></a>Commandes PowerShell courantes permettant de créer et de gérer des machines virtuelles Azure

Cet article traite des hello Qu'azure PowerShell des commandes que vous pouvez utiliser toocreate et gérer des ordinateurs virtuels dans votre abonnement Azure.  Pour en savoir plus sur les commutateurs et options de ligne de commande spécifiques, vous pouvez utiliser la **commande** *Get-Help*.

Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour plus d’informations sur l’installation hello dernière version de Azure PowerShell, en sélectionnant votre abonnement et l’ouverture de session tooyour compte.

Ces variables peuvent être utiles si plusieurs commandes hello en cours d’exécution dans cet article :

- $location - emplacement hello de machine virtuelle de hello. Vous pouvez utiliser [Get-AzureRmLocation](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermlocation) toofind un [région géographique](https://azure.microsoft.com/regions/) qui vous convient.
- $myResourceGroup - nom hello hello du groupe de ressources qui contient l’ordinateur virtuel de hello.
- $myVM - nom hello de machine virtuelle de hello.

## <a name="create-a-vm"></a>Créer une machine virtuelle

| Tâche | Commande |
| ---- | ------- |
| Créer une configuration de machine virtuelle |$vm = [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvmconfig) -VMName $myVM -VMSize "Standard_D1_v1"<BR></BR><BR></BR>configuration d’ordinateur virtuel Hello est les paramètres toodefine ou mise à jour utilisés pour hello machine virtuelle. configuration de Hello est initialisée avec le nom hello Hello machine virtuelle et ses [taille](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). |
| Ajouter des paramètres de configuration |$vm = [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) -VM $vm -Windows -ComputerName $myVM -Credential $cred -ProvisionVMAgent -EnableAutoUpdate<BR></BR><BR></BR>Les paramètres de système d’exploitation, y compris [informations d’identification](https://technet.microsoft.com/library/hh849815.aspx) sont ajoutés à des objets de configuration toohello que vous avez créé précédemment à l’aide de New-AzureRmVMConfig. |
| Ajouter une interface réseau |$vm = [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/Add-AzureRmVMNetworkInterface) -VM $vm -Id $nic.Id<BR></BR><BR></BR>Un ordinateur virtuel doit avoir un [interface réseau](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toocommunicate dans un réseau virtuel. Vous pouvez également utiliser [Get-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) tooretrieve un objet d’interface réseau existante. |
| Spécifier une image de plateforme |$vm = [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmsourceimage) -VM $vm -PublisherName "publisher_name" -Offer "publisher_offer" -Skus "product_sku" -Version "latest"<BR></BR><BR></BR>[Informations de l’image](cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) est ajouté l’objet de configuration toohello que vous avez créé précédemment à l’aide de New-AzureRmVMConfig. objet Hello retourné à partir de cette commande est utilisée uniquement lorsque vous définissez hello du système d’exploitation disque toouse une image de plateforme. |
| Définissez toouse de disque du système d’exploitation à une image de plateforme |$vm = [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmosdisk) -VM $vm -Name "myOSDisk" -VhdUri "http://mystore1.blob.core.windows.net/vhds/myOSDisk.vhd" -CreateOption FromImage<BR></BR><BR></BR>nom de Hello du disque du système d’exploitation hello et son emplacement dans [stockage](../../storage/common/storage-powershell-guide-full.md) est ajouté l’objet de configuration toohello que vous avez créé précédemment. |
| Définissez toouse de disque du système d’exploitation une image généralisée |$vm = Set-AzureRmVMOSDisk -VM $vm -Name "myOSDisk" -SourceImageUri "https://mystore1.blob.core.windows.net/system/Microsoft.Compute/Images/myimages/myprefix-osDisk.{guid}.vhd" -VhdUri "https://mystore1.blob.core.windows.net/vhds/disk_name.vhd" -CreateOption FromImage -Windows<BR></BR><BR></BR>nom de Hello du disque du système d’exploitation hello, l’emplacement de hello de l’image source de hello et emplacement du disque hello dans [stockage](../../storage/common/storage-powershell-guide-full.md) est ajouté l’objet de configuration toohello. |
| Définissez toouse de disque du système d’exploitation une image spécialisée |$vm = Set-AzureRmVMOSDisk -VM $vm -Name "myOSDisk" -VhdUri "http://mystore1.blob.core.windows.net/vhds/" -CreateOption Attach -Windows |
| Créer une machine virtuelle |[New-AzureRmVM]() -ResourceGroupName $myResourceGroup -Location $location -VM $vm<BR></BR><BR></BR>Toutes les ressources sont créées dans un [groupe de ressources](../../azure-resource-manager/powershell-azure-resource-manager.md). Avant d’exécuter cette commande, exécutez les commandes New-AzureRmVMConfig, Set-AzureRmVMOperatingSystem, Set-AzureRmVMSourceImage, Add-AzureRmVMNetworkInterface et Set-AzureRmVMOSDisk. |

## <a name="get-information-about-vms"></a>Obtenir des informations sur les machines virtuelles

| Task | Commande |
| ---- | ------- |
| Répertorier les machines virtuelles au sein d’un abonnement |[Get-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvm) |
| Répertorier les machines virtuelles au sein d’un groupe de ressources |Get-AzureRmVM -ResourceGroupName $myResourceGroup<BR></BR><BR></BR>tooget une liste de ressources de groupes dans votre abonnement, utilisez [Get-AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermresourcegroup). |
| Obtenir des informations sur une machine virtuelle |Get-AzureRmVM -ResourceGroupName $myResourceGroup -Name $myVM |

## <a name="manage-vms"></a>Gérer les machines virtuelles
| Task | Commande |
| --- | --- |
| Démarrer une machine virtuelle |[Start-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/start-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| Arrêter une machine virtuelle |[Stop-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/stop-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| Redémarrer une machine virtuelle en cours d’exécution |[Restart-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/restart-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| Supprimer une machine virtuelle |[Remove-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| Généraliser une machine virtuelle |[Set-AzureRmVm](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM -Generalized<BR></BR><BR></BR>Exécutez cette commande avant la commande Save-AzureRmVMImage. |
| Capturer une machine virtuelle |[Save-AzureRmVMImage](https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvmimage) -ResourceGroupName $myResourceGroup -VMName $myVM -DestinationContainerName "myImageContainer" -VHDNamePrefix "myImagePrefix" -Path "C:\filepath\filename.json"<BR></BR><BR></BR>Un ordinateur virtuel doit être [préparé, arrêter et généralisé](prepare-for-upload-vhd-image.md) toobe utilisé toocreate une image. Avant d’exécuter cette commande, exécutez la commande Set-AzureRmVm. |
| Mettre à jour une machine virtuelle |[Update-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/update-azurermvm) -ResourceGroupName $myResourceGroup -VM $vm<BR></BR><BR></BR>Obtenir hello configuration de machine virtuelle en cours à l’aide de Get-AzureRmVM, modifier les paramètres de configuration sur l’objet d’ordinateur virtuel hello, puis exécutez la commande. |
| Ajouter un tooa de disque de données machine virtuelle |[Add-AzureRmVMDataDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmdatadisk) -VM $vm -Name "myDataDisk" -VhdUri "https://mystore1.blob.core.windows.net/vhds/myDataDisk.vhd" -LUN # -Caching ReadWrite -DiskSizeinGB # -CreateOption Empty<BR></BR><BR></BR>Utilisez l’objet ordinateur virtuel de Get-AzureRmVM tooget hello. Spécifiez le numéro de LUN hello et taille hello du disque de hello. Exécuter la mise à jour-AzureRmVM tooapply hello configuration modifications toohello machine virtuelle. disque Hello que vous ajoutez n’est pas initialisé. |
| Supprimer un disque de données à partir d'une machine virtuelle |[Remove-AzureRmVMDataDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvmdatadisk) -VM $vm -Name "myDataDisk"<BR></BR><BR></BR>Utilisez l’objet ordinateur virtuel de Get-AzureRmVM tooget hello. Exécuter la mise à jour-AzureRmVM tooapply hello configuration modifications toohello machine virtuelle. |
| Ajouter une extension de tooa machine virtuelle |[Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) -ResourceGroupName $myResourceGroup -Location $location -VMName $myVM -Name "extensionName" -Publisher "publisherName" -Type "extensionType" -TypeHandlerVersion "#.#" -Settings $Settings -ProtectedSettings $ProtectedSettings<BR></BR><BR></BR>Exécutez cette commande avec hello approprié [les informations de configuration](template-description.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#extensions) pour extension hello que vous souhaitez tooinstall. |
| Supprimer une extension de machine virtuelle |[Remove-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvmextension) -ResourceGroupName $myResourceGroup -Name "extensionName" -VMName $myVM |

## <a name="next-steps"></a>Étapes suivantes
* Consultez les étapes de base hello pour la création d’une machine virtuelle dans [créer une machine virtuelle de Windows à l’aide du Gestionnaire de ressources et PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

