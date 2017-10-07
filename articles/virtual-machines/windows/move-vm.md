---
title: "aaaMove une ressource d’ordinateur virtuel Windows dans Azure | Documents Microsoft"
description: "Déplacer une machine virtuelle Windows tooanother abonnement Azure ou un groupe de ressources dans le modèle de déploiement du Gestionnaire de ressources hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 859e78dce9acf1168780d4ee8e9f6dac0e3c11cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-tooanother-azure-subscription-or-resource-group"></a>Déplacer un ordinateur virtuel Windows tooanother abonnement Azure ou un groupe de ressources
Cet article vous guide toomove une machine virtuelle de Windows entre les groupes de ressources ou des abonnements. Déplacement entre des abonnements peut être pratique si vous avez créé à l’origine d’une machine virtuelle dans un abonnement personnel, vous souhaitez toomove il toocontinue d’abonnement de la société tooyour votre travail.

> [!IMPORTANT]
>Vous ne pouvez pas déplacer des disques managés pour l’instant. 
>
>Nouveaux ID de ressource sont créés dans le cadre de déplacement de hello. Une fois que hello machine virtuelle a été déplacé, vous devez tooupdate vos outils et scripts toouse hello nouveaux ID de ressource. 
> 
> 

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="use-powershell-toomove-a-vm"></a>Utilisez Powershell toomove une machine virtuelle
toomove un groupe de ressources tooanother machine virtuelle, vous devez toomake également déplacez toutes les ressources dépendantes hello. applet de commande Move-AzureRMResource de hello toouse, vous devez nom de la ressource hello et de type hello de ressource. Vous pouvez obtenir à la fois de l’applet de commande hello Find-AzureRMResource.

    Find-AzureRMResource -ResourceGroupNameContains "<sourceResourceGroupName>"


toomove une machine virtuelle que nous devons toomove plusieurs ressources. Nous pouvons simplement créer des variables distinctes pour chaque ressource, puis les répertorier. Cet exemple inclut la plupart des ressources de base hello pour une machine virtuelle, mais vous pouvez ajouter d’autres en fonction des besoins.

    $sourceRG = "<sourceResourceGroupName>"
    $destinationRG = "<destinationResourceGroupName>"

    $vm = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Compute/virtualMachines" -ResourceName "<vmName>"
    $storageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<storageAccountName>"
    $diagStorageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<diagnosticStorageAccountName>"
    $vNet = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/virtualNetworks" -ResourceName "<vNetName>"
    $nic = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkInterfaces" -ResourceName "<nicName>"
    $ip = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/publicIPAddresses" -ResourceName "<ipName>"
    $nsg = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkSecurityGroups" -ResourceName "<nsgName>"

    Move-AzureRmResource -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId

toomove hello abonnement aux ressources de toodifferent, inclure hello **- DestinationSubscriptionId** paramètre. 

    Move-AzureRmResource -DestinationSubscriptionId "<destinationSubscriptionID>" -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId



Vous devez tooconfirm que vous souhaitez toomove hello les ressources spécifiées. Type **Y** tooconfirm que vous souhaitez que les ressources de hello toomove.

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez déplacer de nombreux types de ressources différents entre les groupes de ressources et les abonnements. Pour plus d’informations, consultez [déplacer le groupe de ressources toonew ressources ou d’un abonnement](../../resource-group-move-resources.md).    

