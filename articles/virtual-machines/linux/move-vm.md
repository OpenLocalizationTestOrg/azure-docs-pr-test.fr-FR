---
title: aaaMove un VM Linux dans Azure | Documents Microsoft
description: "Déplacer un Linux VM tooanother abonnement Azure ou un groupe de ressources dans le modèle de déploiement du Gestionnaire de ressources hello."
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
ms.openlocfilehash: 938d04234059111912f03e72d14dabd338bc0678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-linux-vm-tooanother-subscription-or-resource-group"></a><span data-ttu-id="d894a-103">Déplacer un groupe d’abonnement ou une ressource de tooanother Linux VM</span><span class="sxs-lookup"><span data-stu-id="d894a-103">Move a Linux VM tooanother subscription or resource group</span></span>
<span data-ttu-id="d894a-104">Cet article vous guide toomove un VM Linux entre les groupes de ressources ou des abonnements.</span><span class="sxs-lookup"><span data-stu-id="d894a-104">This article walks you through how toomove a Linux VM between resource groups or subscriptions.</span></span> <span data-ttu-id="d894a-105">Déplacer un ordinateur virtuel entre des abonnements peut être pratique si vous avez créé une machine virtuelle dans un abonnement personnel, vous souhaitez toomove il abonnement tooyour société.</span><span class="sxs-lookup"><span data-stu-id="d894a-105">Moving a VM between subscriptions can be handy if you created a VM in a personal subscription and now want toomove it tooyour company's subscription.</span></span>

> [!IMPORTANT]
><span data-ttu-id="d894a-106">Vous ne pouvez pas déplacer des disques managés pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="d894a-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="d894a-107">Nouveaux ID de ressource sont créés dans le cadre de déplacement de hello.</span><span class="sxs-lookup"><span data-stu-id="d894a-107">New resource IDs are created as part of hello move.</span></span> <span data-ttu-id="d894a-108">Une fois que hello machine virtuelle a été déplacé, vous devez tooupdate vos outils et scripts toouse hello nouveaux ID de ressource.</span><span class="sxs-lookup"><span data-stu-id="d894a-108">Once hello VM has been moved, you need tooupdate your tools and scripts toouse hello new resource IDs.</span></span> 
> 
> 

## <a name="use-hello-azure-cli-toomove-a-vm"></a><span data-ttu-id="d894a-109">Utilisez hello CLI d’Azure toomove une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="d894a-109">Use hello Azure CLI toomove a VM</span></span>
<span data-ttu-id="d894a-110">toosuccessfully déplacer un ordinateur virtuel, vous devez toomove hello VM et toutes ses ressources de prise en charge.</span><span class="sxs-lookup"><span data-stu-id="d894a-110">toosuccessfully move a VM, you need toomove hello VM and all its supporting resources.</span></span> <span data-ttu-id="d894a-111">Hello d’utilisation **afficher de groupe azure** commande toolist toutes les ressources hello dans un groupe de ressources et leurs ID.</span><span class="sxs-lookup"><span data-stu-id="d894a-111">Use hello **azure group show** command toolist all hello resources in a resource group and their IDs.</span></span> <span data-ttu-id="d894a-112">Il permet de sortie de hello toopipe cet tooa du fichier de commandes afin de pouvoir copier et coller hello ID des commandes ultérieures.</span><span class="sxs-lookup"><span data-stu-id="d894a-112">It helps toopipe hello output of this command tooa file so you can copy and paste hello IDs into later commands.</span></span>

    azure group show <resourceGroupName>

<span data-ttu-id="d894a-113">toomove une machine virtuelle et son groupe de ressources tooanother ressources, utilisez hello **du déplacement des Ressources azure** commande CLI.</span><span class="sxs-lookup"><span data-stu-id="d894a-113">toomove a VM and its resources tooanother resource group, use hello **azure resource move** CLI command.</span></span> <span data-ttu-id="d894a-114">Bonjour à l’exemple suivant montre comment toomove une machine virtuelle et ressources courants de hello il requiert.</span><span class="sxs-lookup"><span data-stu-id="d894a-114">hello following example shows how toomove a VM and hello most common resources it requires.</span></span> <span data-ttu-id="d894a-115">Nous utilisons hello **-i** paramètre et passez une liste séparée par des virgules (sans espaces) d’ID pour hello ressources toomove.</span><span class="sxs-lookup"><span data-stu-id="d894a-115">We use hello **-i** parameter and pass in a comma-separated list (without spaces) of IDs for hello resources toomove.</span></span>

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

<span data-ttu-id="d894a-116">Si vous souhaitez toomove hello de machine virtuelle et son abonnement aux ressources de différentes tooa, ajouter hello **--destination-subscriptionId &#60; destinationSubscriptionID &#62;** abonnement de destination paramètre toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="d894a-116">If you want toomove hello VM and its resources tooa different subscription, add hello **--destination-subscriptionId &#60;destinationSubscriptionID&#62;** parameter toospecify hello destination subscription.</span></span>

<span data-ttu-id="d894a-117">Si vous travaillez à partir de l’invite de commandes de hello sur un ordinateur Windows, vous devez tooadd une  **$**  devant les noms de variable hello lorsque vous les déclarez.</span><span class="sxs-lookup"><span data-stu-id="d894a-117">If you are working from hello Command Prompt on a Windows computer, you need tooadd a **$** in front of hello variable names when you declare them.</span></span> <span data-ttu-id="d894a-118">Cela n’est pas nécessaire sous Linux.</span><span class="sxs-lookup"><span data-stu-id="d894a-118">This isn't needed in Linux.</span></span>

<span data-ttu-id="d894a-119">Vous êtes invité tooconfirm que vous souhaitez toomove hello de la ressource spécifiée.</span><span class="sxs-lookup"><span data-stu-id="d894a-119">You are asked tooconfirm that you want toomove hello specified resource.</span></span> <span data-ttu-id="d894a-120">Type **Y** tooconfirm que vous souhaitez que les ressources de hello toomove.</span><span class="sxs-lookup"><span data-stu-id="d894a-120">Type **Y** tooconfirm that you want toomove hello resources.</span></span>

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="d894a-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d894a-121">Next steps</span></span>
<span data-ttu-id="d894a-122">Vous pouvez déplacer de nombreux types de ressources différents entre les groupes de ressources et les abonnements.</span><span class="sxs-lookup"><span data-stu-id="d894a-122">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="d894a-123">Pour plus d’informations, consultez [déplacer le groupe de ressources toonew ressources ou d’un abonnement](../../resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="d894a-123">For more information, see [Move resources toonew resource group or subscription](../../resource-group-move-resources.md).</span></span>    

