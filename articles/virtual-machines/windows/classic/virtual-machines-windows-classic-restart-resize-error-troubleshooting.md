---
title: "Problèmes de redémarrage ou de redimensionnement de machines virtuelles | Microsoft Docs"
description: "Résoudre les problèmes de déploiement Classic liés au redémarrage ou au redimensionnement d’une machine virtuelle Windows existante dans Azure"
services: virtual-machines-windows
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: aa854fff-c057-4b8e-ad77-e4dbc39648cc
ms.service: virtual-machines-windows
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: required
ms.date: 06/13/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: 7fe0636366c60d4679cfc69bd96cd532695b080e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-windows-virtual-machine-in-azure"></a><span data-ttu-id="65784-103">Résoudre les problèmes de déploiement Classic liés au redémarrage ou au redimensionnement d’une machine virtuelle Windows existante dans Azure</span><span class="sxs-lookup"><span data-stu-id="65784-103">Troubleshoot classic deployment issues with restarting or resizing an existing Windows Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="65784-104">Classique</span><span class="sxs-lookup"><span data-stu-id="65784-104">Classic</span></span>](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="65784-105">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="65784-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
> 
> 

<span data-ttu-id="65784-106">Lorsque vous essayez de démarrer une machine virtuelle Azure arrêtée ou de redimensionner une machine virtuelle Azure existante, l’erreur la plus fréquemment rencontrée est un échec d’allocation.</span><span class="sxs-lookup"><span data-stu-id="65784-106">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span></span> <span data-ttu-id="65784-107">Cette erreur se produit lorsque le cluster ou la région n’ont pas de ressources disponibles ou ne prennent pas en charge la taille de machine virtuelle demandée.</span><span class="sxs-lookup"><span data-stu-id="65784-107">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65784-108">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="65784-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="65784-109">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="65784-109">This article covers using the classic deployment model.</span></span> <span data-ttu-id="65784-110">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="65784-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> 
> 

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="65784-111">Collecter des journaux d’audit</span><span class="sxs-lookup"><span data-stu-id="65784-111">Collect audit logs</span></span>
<span data-ttu-id="65784-112">Pour résoudre les problèmes, commencez par collecter les journaux d’audit afin d’identifier l’erreur associée au problème.</span><span class="sxs-lookup"><span data-stu-id="65784-112">To start troubleshooting, collect the audit logs to identify the error associated with the issue.</span></span>

<span data-ttu-id="65784-113">Dans le portail Azure, cliquez sur **Parcourir** > **Machines virtuelles** > *votre machine virtuelle Windows* > **Paramètres** > **Journaux d’audit**.</span><span class="sxs-lookup"><span data-stu-id="65784-113">In the Azure portal, click **Browse** > **Virtual machines** > *your Windows virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="65784-114">Problème : erreur lors du démarrage d’une machine virtuelle arrêtée</span><span class="sxs-lookup"><span data-stu-id="65784-114">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="65784-115">Vous essayez de démarrer une machine virtuelle arrêtée, mais obtenez un échec d’allocation.</span><span class="sxs-lookup"><span data-stu-id="65784-115">You try to start a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="65784-116">Cause :</span><span class="sxs-lookup"><span data-stu-id="65784-116">Cause</span></span>
<span data-ttu-id="65784-117">La demande de démarrage de la machine virtuelle arrêtée doit être exécutée sur le cluster d’origine qui héberge le service cloud.</span><span class="sxs-lookup"><span data-stu-id="65784-117">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="65784-118">Toutefois, le cluster n’a pas d’espace libre pour répondre à la demande.</span><span class="sxs-lookup"><span data-stu-id="65784-118">However, the cluster does not have free space available to fulfill the request.</span></span>

### <a name="resolution"></a><span data-ttu-id="65784-119">Résolution :</span><span class="sxs-lookup"><span data-stu-id="65784-119">Resolution</span></span>
* <span data-ttu-id="65784-120">Créez un service cloud et associez-le à une région ou à un réseau virtuel basé sur une région, mais non à un groupe d’affinités.</span><span class="sxs-lookup"><span data-stu-id="65784-120">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="65784-121">Supprimez la machine virtuelle arrêtée.</span><span class="sxs-lookup"><span data-stu-id="65784-121">Delete the stopped VM.</span></span>
* <span data-ttu-id="65784-122">Recréez la machine virtuelle dans le nouveau service cloud à l’aide des disques.</span><span class="sxs-lookup"><span data-stu-id="65784-122">Recreate the VM in the new cloud service by using the disks.</span></span>
* <span data-ttu-id="65784-123">Démarrez la machine virtuelle recréée.</span><span class="sxs-lookup"><span data-stu-id="65784-123">Start the re-created VM.</span></span>

<span data-ttu-id="65784-124">Si vous obtenez une erreur lorsque vous tentez de créer un service cloud, vous pouvez soit réessayer ultérieurement, soit modifier la région du service cloud.</span><span class="sxs-lookup"><span data-stu-id="65784-124">If you get an error when trying to create a new cloud service, either retry later or change the region for the cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="65784-125">Le nouveau service cloud aura un nouveau nom et une nouvelle adresse IP virtuelle. Vous devrez donc modifier ces valeurs pour toutes les dépendances qui utilisent ces informations pour le service cloud existant.</span><span class="sxs-lookup"><span data-stu-id="65784-125">The new cloud service will have a new name and VIP, so you will need to change that information for all the dependencies that use that information for the existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="65784-126">Problème : erreur lors du redimensionnement d’une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="65784-126">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="65784-127">Vous essayez de redimensionner une machine virtuelle existante, mais obtenez un échec d’allocation.</span><span class="sxs-lookup"><span data-stu-id="65784-127">You try to resize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="65784-128">Cause :</span><span class="sxs-lookup"><span data-stu-id="65784-128">Cause</span></span>
<span data-ttu-id="65784-129">La demande de redimensionnement de la machine virtuelle doit être exécutée sur le cluster d’origine qui héberge le service cloud.</span><span class="sxs-lookup"><span data-stu-id="65784-129">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="65784-130">Toutefois, le cluster ne prend pas en charge la taille de machine virtuelle demandée.</span><span class="sxs-lookup"><span data-stu-id="65784-130">However, the cluster does not support the requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="65784-131">Résolution :</span><span class="sxs-lookup"><span data-stu-id="65784-131">Resolution</span></span>
<span data-ttu-id="65784-132">Réduisez la taille de la machine virtuelle demandée, puis relancez la demande de redimensionnement.</span><span class="sxs-lookup"><span data-stu-id="65784-132">Reduce the requested VM size, and retry the resize request.</span></span>

* <span data-ttu-id="65784-133">Cliquez sur **Parcourir tout** > **Machines virtuelles (classiques)** > *votre machine virtuelle* > **Paramètres** > **Taille**.</span><span class="sxs-lookup"><span data-stu-id="65784-133">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="65784-134">Pour connaître la procédure détaillée, consultez [Redimensionner la machine virtuelle](https://msdn.microsoft.com/library/dn168976.aspx).</span><span class="sxs-lookup"><span data-stu-id="65784-134">For detailed steps, see [Resize the virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="65784-135">S’il est impossible de réduire la taille de la machine virtuelle, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="65784-135">If it is not possible to reduce the VM size, follow these steps:</span></span>

* <span data-ttu-id="65784-136">Créez un service Cloud, en vous assurant qu’il n’est pas lié à un groupe d’affinités et pas associé à un réseau virtuel lié à un groupe d’affinités.</span><span class="sxs-lookup"><span data-stu-id="65784-136">Create a new cloud service, ensuring it is not linked to an affinity group and not associated with a virtual network that is linked to an affinity group.</span></span>
* <span data-ttu-id="65784-137">Créez dans ce service une machine virtuelle plus volumineuse.</span><span class="sxs-lookup"><span data-stu-id="65784-137">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="65784-138">Vous pouvez consolider toutes vos machines virtuelles dans le même service cloud.</span><span class="sxs-lookup"><span data-stu-id="65784-138">You can consolidate all your VMs in the same cloud service.</span></span> <span data-ttu-id="65784-139">Si votre service cloud existant est associé à un réseau virtuel basé sur une région, vous pouvez connecter le nouveau service cloud au réseau virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="65784-139">If your existing cloud service is associated with a region-based virtual network, you can connect the new cloud service to the existing virtual network.</span></span>

<span data-ttu-id="65784-140">Si le service cloud existant n’est pas associé à un réseau virtuel basé sur une région, vous devez supprimer les machines virtuelles du service cloud existant, puis les recréer dans le nouveau service cloud à partir de leurs disques.</span><span class="sxs-lookup"><span data-stu-id="65784-140">If the existing cloud service is not associated with a region-based virtual network, then you have to delete the VMs in the existing cloud service, and recreate them in the new cloud service from their disks.</span></span> <span data-ttu-id="65784-141">Toutefois, il est important de se rappeler que le nouveau service cloud aura un nouveau nom et une nouvelle adresse IP virtuelle. Vous devrez donc mettre à jour ces valeurs pour toutes les dépendances qui utilisent actuellement ces informations pour le service cloud existant.</span><span class="sxs-lookup"><span data-stu-id="65784-141">However, it is important to remember that the new cloud service will have a new name and VIP, so you will need to update these for all the dependencies that currently use this information for the existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65784-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="65784-142">Next steps</span></span>
<span data-ttu-id="65784-143">Si vous rencontrez des problèmes lorsque vous créez une machine virtuelle Windows dans Azure, consultez [Résoudre les problèmes de déploiement liés à la création d’une machine virtuelle Windows dans Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="65784-143">If you encounter issues when you create a Windows VM in Azure, see [Troubleshoot deployment issues with creating a Windows virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

