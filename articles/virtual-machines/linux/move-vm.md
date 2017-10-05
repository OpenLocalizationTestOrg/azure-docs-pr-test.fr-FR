---
title: "Déplacer une machine virtuelle Linux dans Azure | Microsoft Docs"
description: "Déplacez une machine virtuelle Linux vers un autre abonnement ou groupe de ressources Azure dans le modèle de déploiement Resource Manager."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d635f0a5-4458-4b95-a5f8-eed4f41eb4d4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 4695a9c934f97f2b2d448c4990e7ad5533e38e9f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="move-a-linux-vm-to-another-subscription-or-resource-group"></a><span data-ttu-id="baa48-103">Déplacer une machine virtuelle Linux vers un autre abonnement ou groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="baa48-103">Move a Linux VM to another subscription or resource group</span></span>
<span data-ttu-id="baa48-104">Cet article vous guide tout au long du déplacement d’une machine virtuelle Linux entre des groupes de ressources ou des abonnements.</span><span class="sxs-lookup"><span data-stu-id="baa48-104">This article walks you through how to move a Linux VM between resource groups or subscriptions.</span></span> <span data-ttu-id="baa48-105">Le déplacement d’une machine virtuelle entre abonnements peut être pratique si vous avez créé une machine virtuelle dans un abonnement personnel, et que vous souhaitez à présent la déplacer vers l’abonnement de votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="baa48-105">Moving a VM between subscriptions can be handy if you created a VM in a personal subscription and now want to move it to your company's subscription.</span></span>

> [!IMPORTANT]
><span data-ttu-id="baa48-106">Vous ne pouvez pas déplacer des disques managés pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="baa48-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="baa48-107">De nouveaux ID de ressource sont créés dans le cadre du déplacement.</span><span class="sxs-lookup"><span data-stu-id="baa48-107">New resource IDs are created as part of the move.</span></span> <span data-ttu-id="baa48-108">Une fois que la machine virtuelle a été déplacée, vous devez mettre à jour vos outils et vos scripts pour utiliser les nouveaux ID de ressource.</span><span class="sxs-lookup"><span data-stu-id="baa48-108">Once the VM has been moved, you need to update your tools and scripts to use the new resource IDs.</span></span> 
> 
> 

## <a name="use-the-azure-cli-to-move-a-vm"></a><span data-ttu-id="baa48-109">Utiliser l’interface CLI Azure pour déplacer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="baa48-109">Use the Azure CLI to move a VM</span></span>
<span data-ttu-id="baa48-110">Pour déplacer avec succès une machine virtuelle, vous devez déplacer la machine virtuelle et toutes les ressources qui l’accompagnent.</span><span class="sxs-lookup"><span data-stu-id="baa48-110">To successfully move a VM, you need to move the VM and all its supporting resources.</span></span> <span data-ttu-id="baa48-111">Utilisez la commande **azure group show** pour répertorier toutes les ressources d’un groupe de ressources et leurs ID.</span><span class="sxs-lookup"><span data-stu-id="baa48-111">Use the **azure group show** command to list all the resources in a resource group and their IDs.</span></span> <span data-ttu-id="baa48-112">Cela permet de diriger la sortie de cette commande dans un fichier. Vous pouvez ainsi copier et coller les ID dans des commandes ultérieures.</span><span class="sxs-lookup"><span data-stu-id="baa48-112">It helps to pipe the output of this command to a file so you can copy and paste the IDs into later commands.</span></span>

    azure group show <resourceGroupName>

<span data-ttu-id="baa48-113">Pour déplacer une machine virtuelle et ses ressources vers un autre groupe de ressources, exécutez la commande CLI **azure resource move** .</span><span class="sxs-lookup"><span data-stu-id="baa48-113">To move a VM and its resources to another resource group, use the **azure resource move** CLI command.</span></span> <span data-ttu-id="baa48-114">L’exemple suivant montre comment déplacer une machine virtuelle et les ressources courantes nécessaires.</span><span class="sxs-lookup"><span data-stu-id="baa48-114">The following example shows how to move a VM and the most common resources it requires.</span></span> <span data-ttu-id="baa48-115">Nous utilisons le paramètre **-i** et transmettons une liste séparée par des virgules (sans espaces) d’ID de ressources à déplacer.</span><span class="sxs-lookup"><span data-stu-id="baa48-115">We use the **-i** parameter and pass in a comma-separated list (without spaces) of IDs for the resources to move.</span></span>

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

<span data-ttu-id="baa48-116">Si vous souhaitez déplacer la machine virtuelle et ses ressources vers un autre abonnement, ajoutez le paramètre **--destination-subscriptionId &#60;destinationSubscriptionID&#62;** pour spécifier l’abonnement de destination.</span><span class="sxs-lookup"><span data-stu-id="baa48-116">If you want to move the VM and its resources to a different subscription, add the **--destination-subscriptionId &#60;destinationSubscriptionID&#62;** parameter to specify the destination subscription.</span></span>

<span data-ttu-id="baa48-117">Si vous travaillez sur l’invite de commandes d’un ordinateur Windows, vous devez ajouter un **$** devant les noms de variables lorsque vous les déclarez.</span><span class="sxs-lookup"><span data-stu-id="baa48-117">If you are working from the Command Prompt on a Windows computer, you need to add a **$** in front of the variable names when you declare them.</span></span> <span data-ttu-id="baa48-118">Cela n’est pas nécessaire sous Linux.</span><span class="sxs-lookup"><span data-stu-id="baa48-118">This isn't needed in Linux.</span></span>

<span data-ttu-id="baa48-119">Vous devez confirmer que vous souhaitez déplacer la ressource spécifiée.</span><span class="sxs-lookup"><span data-stu-id="baa48-119">You are asked to confirm that you want to move the specified resource.</span></span> <span data-ttu-id="baa48-120">Tapez **Y** pour confirmer que vous souhaitez déplacer les ressources.</span><span class="sxs-lookup"><span data-stu-id="baa48-120">Type **Y** to confirm that you want to move the resources.</span></span>

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="baa48-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="baa48-121">Next steps</span></span>
<span data-ttu-id="baa48-122">Vous pouvez déplacer de nombreux types de ressources différents entre les groupes de ressources et les abonnements.</span><span class="sxs-lookup"><span data-stu-id="baa48-122">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="baa48-123">Pour plus d’informations, consultez la page [Déplacement de ressources vers un nouveau groupe de ressources ou un abonnement](../../resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="baa48-123">For more information, see [Move resources to new resource group or subscription](../../resource-group-move-resources.md).</span></span>    

