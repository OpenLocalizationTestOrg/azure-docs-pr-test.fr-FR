---
title: "Problèmes de redémarrage ou de redimensionnement de machines virtuelles | Microsoft Docs"
description: "Résoudre les problèmes de déploiement classiques liés au redémarrage ou au redimensionnement d’une machine virtuelle Linux existante dans Azure"
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 73f2672c-602e-4766-8948-2b180115d299
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: required
ms.date: 01/10/2017
ms.devlang: na
ms.author: delhan
ms.openlocfilehash: c6d4ed45133dc3f4b1f3d17fb5a87d3bf77aa3f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-linux-virtual-machine-in-azure"></a><span data-ttu-id="4cfb1-103">Résoudre les problèmes de déploiement classiques liés au redémarrage ou au redimensionnement d’une machine virtuelle Linux existante dans Azure</span><span class="sxs-lookup"><span data-stu-id="4cfb1-103">Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4cfb1-104">Classique</span><span class="sxs-lookup"><span data-stu-id="4cfb1-104">Classic</span></span>](restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="4cfb1-105">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="4cfb1-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<span data-ttu-id="4cfb1-106">Lorsque vous essayez de démarrer une machine virtuelle Azure arrêtée ou de redimensionner une machine virtuelle Azure existante, l’erreur la plus fréquemment rencontrée est un échec d’allocation.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-106">When you try to start a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, the common error you encounter is an allocation failure.</span></span> <span data-ttu-id="4cfb1-107">Cette erreur se produit lorsque le cluster ou la région n’ont pas de ressources disponibles ou ne prennent pas en charge la taille de machine virtuelle demandée.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-107">This error results when the cluster or region either does not have resources available or cannot support the requested VM size.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="4cfb1-108">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4cfb1-108">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4cfb1-109">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-109">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="4cfb1-110">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="4cfb1-111">Pour la version de Resource Manager, suivi [ce lien](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4cfb1-111">For the Resource Manager version, see [here](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="4cfb1-112">Collecter des journaux d’audit</span><span class="sxs-lookup"><span data-stu-id="4cfb1-112">Collect audit logs</span></span>
<span data-ttu-id="4cfb1-113">Pour résoudre les problèmes, commencez par collecter les journaux d’audit afin d’identifier l’erreur associée au problème.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-113">To start troubleshooting, collect the audit logs to identify the error associated with the issue.</span></span>

<span data-ttu-id="4cfb1-114">Dans le portail Azure, cliquez sur **Parcourir** > **Machines virtuelles** > *votre machine virtuelle Linux* > **Paramètres** > **Journaux d’audit**.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-114">In the Azure portal, click **Browse** > **Virtual machines** > *your Linux virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="4cfb1-115">Problème : erreur lors du démarrage d’une machine virtuelle arrêtée</span><span class="sxs-lookup"><span data-stu-id="4cfb1-115">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="4cfb1-116">Vous essayez de démarrer une machine virtuelle arrêtée, mais obtenez un échec d’allocation.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-116">You try to start a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="4cfb1-117">Cause :</span><span class="sxs-lookup"><span data-stu-id="4cfb1-117">Cause</span></span>
<span data-ttu-id="4cfb1-118">La demande de démarrage de la machine virtuelle arrêtée doit être exécutée sur le cluster d’origine qui héberge le service cloud.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-118">The request to start the stopped VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="4cfb1-119">Toutefois, le cluster n’a pas d’espace libre pour répondre à la demande.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-119">However, the cluster does not have free space available to fulfill the request.</span></span>

### <a name="resolution"></a><span data-ttu-id="4cfb1-120">Résolution :</span><span class="sxs-lookup"><span data-stu-id="4cfb1-120">Resolution</span></span>
* <span data-ttu-id="4cfb1-121">Créez un service cloud et associez-le à une région ou à un réseau virtuel basé sur une région, mais non à un groupe d’affinités.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-121">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="4cfb1-122">Supprimez la machine virtuelle arrêtée.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-122">Delete the stopped VM.</span></span>
* <span data-ttu-id="4cfb1-123">Recréez la machine virtuelle dans le nouveau service cloud à l’aide des disques.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-123">Recreate the VM in the new cloud service by using the disks.</span></span>
* <span data-ttu-id="4cfb1-124">Démarrez la machine virtuelle recréée.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-124">Start the re-created VM.</span></span>

<span data-ttu-id="4cfb1-125">Si vous obtenez une erreur lorsque vous tentez de créer un service cloud, vous pouvez soit réessayer ultérieurement, soit modifier la région du service cloud.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-125">If you get an error when trying to create a new cloud service, either retry at a later time or change the region for the cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4cfb1-126">Le nouveau service cloud aura un nouveau nom et une nouvelle adresse IP virtuelle. Vous devrez donc modifier ces valeurs pour toutes les dépendances qui utilisent ces informations pour le service cloud existant.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-126">The new cloud service will have a new name and VIP, so you will need to change that information for all the dependencies that use that information for the existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="4cfb1-127">Problème : erreur lors du redimensionnement d’une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="4cfb1-127">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="4cfb1-128">Vous essayez de redimensionner une machine virtuelle existante, mais obtenez un échec d’allocation.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-128">You try to resize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="4cfb1-129">Cause :</span><span class="sxs-lookup"><span data-stu-id="4cfb1-129">Cause</span></span>
<span data-ttu-id="4cfb1-130">La demande de redimensionnement de la machine virtuelle doit être exécutée sur le cluster d’origine qui héberge le service cloud.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-130">The request to resize the VM has to be attempted at the original cluster that hosts the cloud service.</span></span> <span data-ttu-id="4cfb1-131">Toutefois, le cluster ne prend pas en charge la taille de machine virtuelle demandée.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-131">However, the cluster does not support the requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="4cfb1-132">Résolution :</span><span class="sxs-lookup"><span data-stu-id="4cfb1-132">Resolution</span></span>
<span data-ttu-id="4cfb1-133">Réduisez la taille de la machine virtuelle demandée, puis relancez la demande de redimensionnement.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-133">Reduce the requested VM size, and retry the resize request.</span></span>

* <span data-ttu-id="4cfb1-134">Cliquez sur **Parcourir tout** > **Machines virtuelles (classiques)** > *votre machine virtuelle* > **Paramètres** > **Taille**.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-134">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="4cfb1-135">Pour connaître la procédure détaillée, consultez [Redimensionner la machine virtuelle](https://msdn.microsoft.com/library/dn168976.aspx).</span><span class="sxs-lookup"><span data-stu-id="4cfb1-135">For detailed steps, see [Resize the virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="4cfb1-136">S’il est impossible de réduire la taille de la machine virtuelle, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4cfb1-136">If it is not possible to reduce the VM size, follow these steps:</span></span>

* <span data-ttu-id="4cfb1-137">Créez un service Cloud, en vous assurant qu’il n’est pas lié à un groupe d’affinités et pas associé à un réseau virtuel lié à un groupe d’affinités.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-137">Create a new cloud service, ensuring it is not linked to an affinity group and not associated with a virtual network that is linked to an affinity group.</span></span>
* <span data-ttu-id="4cfb1-138">Créez dans ce service une machine virtuelle plus volumineuse.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-138">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="4cfb1-139">Vous pouvez consolider toutes vos machines virtuelles dans le même service cloud.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-139">You can consolidate all your VMs in the same cloud service.</span></span> <span data-ttu-id="4cfb1-140">Si votre service cloud existant est associé à un réseau virtuel basé sur une région, vous pouvez connecter le nouveau service cloud au réseau virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-140">If your existing cloud service is associated with a region-based virtual network, you can connect the new cloud service to the existing virtual network.</span></span>

<span data-ttu-id="4cfb1-141">Si le service cloud existant n’est pas associé à un réseau virtuel basé sur une région, vous devez supprimer les machines virtuelles du service cloud existant, puis les recréer dans le nouveau service cloud à partir de leurs disques.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-141">If the existing cloud service is not associated with a region-based virtual network, then you have to delete the VMs in the existing cloud service, and recreate them in the new cloud service from their disks.</span></span> <span data-ttu-id="4cfb1-142">Toutefois, il est important de se rappeler que le nouveau service cloud aura un nouveau nom et une nouvelle adresse IP virtuelle. Vous devrez donc mettre à jour ces valeurs pour toutes les dépendances qui utilisent actuellement ces informations pour le service cloud existant.</span><span class="sxs-lookup"><span data-stu-id="4cfb1-142">However, it is important to remember that the new cloud service will have a new name and VIP, so you will need to update these for all the dependencies that currently use this information for the existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4cfb1-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4cfb1-143">Next steps</span></span>
<span data-ttu-id="4cfb1-144">Si vous rencontrez des problèmes lorsque vous créez une machine virtuelle Linux dans Azure, consultez [Résoudre les problèmes de déploiement liés à la création d’une machine virtuelle Linux dans Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4cfb1-144">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

