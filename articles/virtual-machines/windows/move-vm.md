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
# <a name="move-a-windows-vm-tooanother-azure-subscription-or-resource-group"></a><span data-ttu-id="c658e-103">Déplacer un ordinateur virtuel Windows tooanother abonnement Azure ou un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="c658e-103">Move a Windows VM tooanother Azure subscription or resource group</span></span>
<span data-ttu-id="c658e-104">Cet article vous guide toomove une machine virtuelle de Windows entre les groupes de ressources ou des abonnements.</span><span class="sxs-lookup"><span data-stu-id="c658e-104">This article walks you through how toomove a Windows VM between resource groups or subscriptions.</span></span> <span data-ttu-id="c658e-105">Déplacement entre des abonnements peut être pratique si vous avez créé à l’origine d’une machine virtuelle dans un abonnement personnel, vous souhaitez toomove il toocontinue d’abonnement de la société tooyour votre travail.</span><span class="sxs-lookup"><span data-stu-id="c658e-105">Moving between subscriptions can be handy if you originally created a VM in a personal subscription and now want toomove it tooyour company's subscription toocontinue your work.</span></span>

> [!IMPORTANT]
><span data-ttu-id="c658e-106">Vous ne pouvez pas déplacer des disques managés pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="c658e-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="c658e-107">Nouveaux ID de ressource sont créés dans le cadre de déplacement de hello.</span><span class="sxs-lookup"><span data-stu-id="c658e-107">New resource IDs are created as part of hello move.</span></span> <span data-ttu-id="c658e-108">Une fois que hello machine virtuelle a été déplacé, vous devez tooupdate vos outils et scripts toouse hello nouveaux ID de ressource.</span><span class="sxs-lookup"><span data-stu-id="c658e-108">Once hello VM has been moved, you need tooupdate your tools and scripts toouse hello new resource IDs.</span></span> 
> 
> 

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="use-powershell-toomove-a-vm"></a><span data-ttu-id="c658e-109">Utilisez Powershell toomove une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="c658e-109">Use Powershell toomove a VM</span></span>
<span data-ttu-id="c658e-110">toomove un groupe de ressources tooanother machine virtuelle, vous devez toomake également déplacez toutes les ressources dépendantes hello.</span><span class="sxs-lookup"><span data-stu-id="c658e-110">toomove a virtual machine tooanother resource group, you need toomake sure that you also move all of hello dependent resources.</span></span> <span data-ttu-id="c658e-111">applet de commande Move-AzureRMResource de hello toouse, vous devez nom de la ressource hello et de type hello de ressource.</span><span class="sxs-lookup"><span data-stu-id="c658e-111">toouse hello Move-AzureRMResource cmdlet, you need hello resource name and hello type of resource.</span></span> <span data-ttu-id="c658e-112">Vous pouvez obtenir à la fois de l’applet de commande hello Find-AzureRMResource.</span><span class="sxs-lookup"><span data-stu-id="c658e-112">You can get both from hello Find-AzureRMResource cmdlet.</span></span>

    Find-AzureRMResource -ResourceGroupNameContains "<sourceResourceGroupName>"


<span data-ttu-id="c658e-113">toomove une machine virtuelle que nous devons toomove plusieurs ressources.</span><span class="sxs-lookup"><span data-stu-id="c658e-113">toomove a VM we need toomove multiple resources.</span></span> <span data-ttu-id="c658e-114">Nous pouvons simplement créer des variables distinctes pour chaque ressource, puis les répertorier.</span><span class="sxs-lookup"><span data-stu-id="c658e-114">We can just create separate variables for each resource and then list them.</span></span> <span data-ttu-id="c658e-115">Cet exemple inclut la plupart des ressources de base hello pour une machine virtuelle, mais vous pouvez ajouter d’autres en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="c658e-115">This example includes most of hello basic resources for a VM, but you can add more as needed.</span></span>

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

<span data-ttu-id="c658e-116">toomove hello abonnement aux ressources de toodifferent, inclure hello **- DestinationSubscriptionId** paramètre.</span><span class="sxs-lookup"><span data-stu-id="c658e-116">toomove hello resources toodifferent subscription, include hello **-DestinationSubscriptionId** parameter.</span></span> 

    Move-AzureRmResource -DestinationSubscriptionId "<destinationSubscriptionID>" -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId



<span data-ttu-id="c658e-117">Vous devez tooconfirm que vous souhaitez toomove hello les ressources spécifiées.</span><span class="sxs-lookup"><span data-stu-id="c658e-117">You will be asked tooconfirm that you want toomove hello specified resources.</span></span> <span data-ttu-id="c658e-118">Type **Y** tooconfirm que vous souhaitez que les ressources de hello toomove.</span><span class="sxs-lookup"><span data-stu-id="c658e-118">Type **Y** tooconfirm that you want toomove hello resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c658e-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c658e-119">Next steps</span></span>
<span data-ttu-id="c658e-120">Vous pouvez déplacer de nombreux types de ressources différents entre les groupes de ressources et les abonnements.</span><span class="sxs-lookup"><span data-stu-id="c658e-120">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="c658e-121">Pour plus d’informations, consultez [déplacer le groupe de ressources toonew ressources ou d’un abonnement](../../resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="c658e-121">For more information, see [Move resources toonew resource group or subscription](../../resource-group-move-resources.md).</span></span>    

