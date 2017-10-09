---
title: "aaaVM le redémarrage ou redimensionnement | Documents Microsoft"
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
ms.openlocfilehash: fb1dc88bb1b83043c434590118bc8810ad402872
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-classic-deployment-issues-with-restarting-or-resizing-an-existing-linux-virtual-machine-in-azure"></a><span data-ttu-id="71dbf-103">Résoudre les problèmes de déploiement classiques liés au redémarrage ou au redimensionnement d’une machine virtuelle Linux existante dans Azure</span><span class="sxs-lookup"><span data-stu-id="71dbf-103">Troubleshoot classic deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="71dbf-104">Classique</span><span class="sxs-lookup"><span data-stu-id="71dbf-104">Classic</span></span>](restart-resize-error-troubleshooting.md)
> * [<span data-ttu-id="71dbf-105">Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="71dbf-105">Resource Manager</span></span>](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<span data-ttu-id="71dbf-106">Lorsque vous essayez de toostart une Machine virtuelle de Azure (VM) arrêté ou redimensionnez une machine virtuelle Azure existante, les erreurs courantes hello que vous rencontrez sont un échec d’allocation.</span><span class="sxs-lookup"><span data-stu-id="71dbf-106">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="71dbf-107">Cette erreur se produit lorsque le cluster de hello ou la région n’a pas de ressources disponibles ou ne peut pas prise en charge hello demandée taille de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="71dbf-107">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="71dbf-108">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="71dbf-108">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="71dbf-109">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="71dbf-109">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="71dbf-110">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="71dbf-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="71dbf-111">Pour la version du Gestionnaire de ressources hello, consultez [ici](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="71dbf-111">For hello Resource Manager version, see [here](../restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="collect-audit-logs"></a><span data-ttu-id="71dbf-112">Collecter des journaux d’audit</span><span class="sxs-lookup"><span data-stu-id="71dbf-112">Collect audit logs</span></span>
<span data-ttu-id="71dbf-113">toostart résolution des problèmes, d’audit de collecter hello consigne l’erreur de hello de tooidentify associé au problème de hello.</span><span class="sxs-lookup"><span data-stu-id="71dbf-113">toostart troubleshooting, collect hello audit logs tooidentify hello error associated with hello issue.</span></span>

<span data-ttu-id="71dbf-114">Bonjour portail Azure, cliquez sur **Parcourir** > **virtuels** > *votre machine virtuelle de Linux*  >   **Paramètres** > **journaux d’Audit**.</span><span class="sxs-lookup"><span data-stu-id="71dbf-114">In hello Azure portal, click **Browse** > **Virtual machines** > *your Linux virtual machine* > **Settings** > **Audit logs**.</span></span>

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="71dbf-115">Problème : erreur lors du démarrage d’une machine virtuelle arrêtée</span><span class="sxs-lookup"><span data-stu-id="71dbf-115">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="71dbf-116">Vous essayez de toostart une machine virtuelle arrêtée mais obtenez un échec d’allocation.</span><span class="sxs-lookup"><span data-stu-id="71dbf-116">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="71dbf-117">Cause :</span><span class="sxs-lookup"><span data-stu-id="71dbf-117">Cause</span></span>
<span data-ttu-id="71dbf-118">demande Hello toostart hello arrêté la machine virtuelle a toobe émise au cluster d’origine hello qui héberge le service de cloud computing hello.</span><span class="sxs-lookup"><span data-stu-id="71dbf-118">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="71dbf-119">Toutefois, les clusters hello n’ont pas de demande de hello toofulfill disponible d’espace libre.</span><span class="sxs-lookup"><span data-stu-id="71dbf-119">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="71dbf-120">Résolution :</span><span class="sxs-lookup"><span data-stu-id="71dbf-120">Resolution</span></span>
* <span data-ttu-id="71dbf-121">Créez un service cloud et associez-le à une région ou à un réseau virtuel basé sur une région, mais non à un groupe d’affinités.</span><span class="sxs-lookup"><span data-stu-id="71dbf-121">Create a new cloud service and associate it with either a region or a region-based virtual network, but not an affinity group.</span></span>
* <span data-ttu-id="71dbf-122">Supprimer hello arrêté la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="71dbf-122">Delete hello stopped VM.</span></span>
* <span data-ttu-id="71dbf-123">Recréez hello machine virtuelle dans le nouveau service de cloud hello en utilisant des disques hello.</span><span class="sxs-lookup"><span data-stu-id="71dbf-123">Recreate hello VM in hello new cloud service by using hello disks.</span></span>
* <span data-ttu-id="71dbf-124">Démarrer hello recréé la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="71dbf-124">Start hello re-created VM.</span></span>

<span data-ttu-id="71dbf-125">Si vous obtenez une erreur lors de la tentative de toocreate un nouveau service cloud, réessayez ultérieurement, ou modifier la région de hello pour le service cloud hello.</span><span class="sxs-lookup"><span data-stu-id="71dbf-125">If you get an error when trying toocreate a new cloud service, either retry at a later time or change hello region for hello cloud service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="71dbf-126">nouveau service de cloud Hello aura un nouveau nom et l’adresse IP virtuelle, vous devez toochange ces informations pour toutes les dépendances de hello qui utilisent ces informations pour le service cloud existant hello.</span><span class="sxs-lookup"><span data-stu-id="71dbf-126">hello new cloud service will have a new name and VIP, so you will need toochange that information for all hello dependencies that use that information for hello existing cloud service.</span></span>
> 
> 

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="71dbf-127">Problème : erreur lors du redimensionnement d’une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="71dbf-127">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="71dbf-128">Vous essayez tooresize une machine virtuelle existante mais un échec d’allocation.</span><span class="sxs-lookup"><span data-stu-id="71dbf-128">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="71dbf-129">Cause :</span><span class="sxs-lookup"><span data-stu-id="71dbf-129">Cause</span></span>
<span data-ttu-id="71dbf-130">demande Hello tooresize hello machine virtuelle a toobe tentée au cluster d’origine de hello ce service de cloud hello hôtes.</span><span class="sxs-lookup"><span data-stu-id="71dbf-130">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="71dbf-131">Toutefois, les clusters hello ne prend pas en charge hello demandé la taille de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="71dbf-131">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="71dbf-132">Résolution :</span><span class="sxs-lookup"><span data-stu-id="71dbf-132">Resolution</span></span>
<span data-ttu-id="71dbf-133">Réduire hello demandé la taille de machine virtuelle et réessayer hello redimensionner la demande.</span><span class="sxs-lookup"><span data-stu-id="71dbf-133">Reduce hello requested VM size, and retry hello resize request.</span></span>

* <span data-ttu-id="71dbf-134">Cliquez sur **Parcourir tout** > **Machines virtuelles (classiques)** > *votre machine virtuelle* > **Paramètres** > **Taille**.</span><span class="sxs-lookup"><span data-stu-id="71dbf-134">Click **Browse all** > **Virtual machines (classic)** > *your virtual machine* > **Settings** > **Size**.</span></span> <span data-ttu-id="71dbf-135">Pour des instructions détaillées, consultez [redimensionnement de la machine virtuelle de hello](https://msdn.microsoft.com/library/dn168976.aspx).</span><span class="sxs-lookup"><span data-stu-id="71dbf-135">For detailed steps, see [Resize hello virtual machine](https://msdn.microsoft.com/library/dn168976.aspx).</span></span>

<span data-ttu-id="71dbf-136">Si elle n’est pas possible de tooreduce hello taille de machine virtuelle, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="71dbf-136">If it is not possible tooreduce hello VM size, follow these steps:</span></span>

* <span data-ttu-id="71dbf-137">Créer un nouveau service cloud, en veillant à ce qu’il n’est pas lié tooan affinité du groupe et non associé à un réseau virtuel qui est le groupe d’affinités de tooan lié.</span><span class="sxs-lookup"><span data-stu-id="71dbf-137">Create a new cloud service, ensuring it is not linked tooan affinity group and not associated with a virtual network that is linked tooan affinity group.</span></span>
* <span data-ttu-id="71dbf-138">Créez dans ce service une machine virtuelle plus volumineuse.</span><span class="sxs-lookup"><span data-stu-id="71dbf-138">Create a new, larger-sized VM in it.</span></span>

<span data-ttu-id="71dbf-139">Vous pouvez consolider toutes vos machines virtuelles Bonjour même service cloud.</span><span class="sxs-lookup"><span data-stu-id="71dbf-139">You can consolidate all your VMs in hello same cloud service.</span></span> <span data-ttu-id="71dbf-140">Si votre service cloud existant est associé à un réseau virtuel en fonction de la région, vous pouvez vous connecter hello nouveau cloud service toohello réseau virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="71dbf-140">If your existing cloud service is associated with a region-based virtual network, you can connect hello new cloud service toohello existing virtual network.</span></span>

<span data-ttu-id="71dbf-141">Si le service cloud existant hello n’est pas associé à un réseau virtuel en fonction de la région, puis vous avez toodelete hello machines virtuelles dans le service cloud existant hello et les recréez dans le nouveau service de cloud hello à partir de leurs disques.</span><span class="sxs-lookup"><span data-stu-id="71dbf-141">If hello existing cloud service is not associated with a region-based virtual network, then you have toodelete hello VMs in hello existing cloud service, and recreate them in hello new cloud service from their disks.</span></span> <span data-ttu-id="71dbf-142">Toutefois, il est important tooremember nouveau service de cloud hello qu’un nouveau nom et l’adresse IP virtuelle, vous devez tooupdate ces valeurs pour toutes les dépendances de hello qui utilisent ces informations pour le service cloud existant hello.</span><span class="sxs-lookup"><span data-stu-id="71dbf-142">However, it is important tooremember that hello new cloud service will have a new name and VIP, so you will need tooupdate these for all hello dependencies that currently use this information for hello existing cloud service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71dbf-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="71dbf-143">Next steps</span></span>
<span data-ttu-id="71dbf-144">Si vous rencontrez des problèmes lorsque vous créez une machine virtuelle Linux dans Azure, consultez [Résoudre les problèmes de déploiement liés à la création d’une machine virtuelle Linux dans Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="71dbf-144">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](../troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

