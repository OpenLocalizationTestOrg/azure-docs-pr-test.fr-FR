---
title: "aaaTroubleshoot Linux VM déploiement-RM | Documents Microsoft"
description: "Résoudre les problèmes de déploiement Resource Manager liés à la création d’une machine virtuelle Linux dans Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue, azure-resource-manager
ms.assetid: 906a9c89-6866-496b-b4a4-f07fb39f990c
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/09/2016
ms.author: cjiang
ms.openlocfilehash: 2dd7f1855bba75d86eb90f88e6d573cd42fd8d87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-resource-manager-deployment-issues-with-creating-a-new-linux-virtual-machine-in-azure"></a><span data-ttu-id="2fd95-103">Résoudre les problèmes de déploiement Resource Manager liés à la création d’une machine virtuelle Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="2fd95-103">Troubleshoot Resource Manager deployment issues with creating a new Linux virtual machine in Azure</span></span>
[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-opening](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-opening-include.md)]

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="top-issues"></a><span data-ttu-id="2fd95-104">Problèmes principaux</span><span class="sxs-lookup"><span data-stu-id="2fd95-104">Top issues</span></span>
[!INCLUDE [support-disclaimer](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

<span data-ttu-id="2fd95-105">Pour toute autre question ou problèmes concernant le déploiement de machine virtuelle, consultez [Troubleshoot deploying Linux virtual machine issues in Azure](troubleshoot-deploy-vm.md) (Résolution des problèmes de déploiement de la machine virtuelle Linux dans Azure).</span><span class="sxs-lookup"><span data-stu-id="2fd95-105">For other VM deployment issues and questions, see [Troubleshoot deploying Linux virtual machine issues in Azure](troubleshoot-deploy-vm.md).</span></span>
## <a name="collect-activity-logs"></a><span data-ttu-id="2fd95-106">Collecte des journaux d’activité</span><span class="sxs-lookup"><span data-stu-id="2fd95-106">Collect activity logs</span></span>
<span data-ttu-id="2fd95-107">toostart résolution des problèmes, activité hello collecter consigne l’erreur de hello de tooidentify associé au problème de hello.</span><span class="sxs-lookup"><span data-stu-id="2fd95-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="2fd95-108">Hello liens suivants contiennent des informations détaillées sur hello processus toofollow.</span><span class="sxs-lookup"><span data-stu-id="2fd95-108">hello following links contain detailed information on hello process toofollow.</span></span>

[<span data-ttu-id="2fd95-109">Voir les opérations de déploiement</span><span class="sxs-lookup"><span data-stu-id="2fd95-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="2fd95-110">Afficher l’activité des journaux toomanage Azure ressources</span><span class="sxs-lookup"><span data-stu-id="2fd95-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

[!INCLUDE [virtual-machines-troubleshoot-deployment-new-vm-issue1](../../../includes/virtual-machines-troubleshoot-deployment-new-vm-issue1-include.md)]

[!INCLUDE [virtual-machines-linux-troubleshoot-deployment-new-vm-table](../../../includes/virtual-machines-linux-troubleshoot-deployment-new-vm-table.md)]

<span data-ttu-id="2fd95-111">**Y:** si hello du système d’exploitation est Linux généralisé et il est téléchargé et/ou capturé avec hello généralisé définissant, n’aura pas toutes les erreurs.</span><span class="sxs-lookup"><span data-stu-id="2fd95-111">**Y:** If hello OS is Linux generalized, and it is uploaded and/or captured with hello generalized setting, then there won’t be any errors.</span></span> <span data-ttu-id="2fd95-112">De même, si hello du système d’exploitation est spécialisé de Linux, et il est téléchargé et/ou capturé avec hello spécialisée de paramètre, puis n’aura pas toutes les erreurs.</span><span class="sxs-lookup"><span data-stu-id="2fd95-112">Similarly, if hello OS is Linux specialized, and it is uploaded and/or captured with hello specialized setting, then there won’t be any errors.</span></span>

<span data-ttu-id="2fd95-113">**Erreurs de téléchargement :**</span><span class="sxs-lookup"><span data-stu-id="2fd95-113">**Upload Errors:**</span></span>

<span data-ttu-id="2fd95-114">**N<sup>1</sup>:** si hello du système d’exploitation est généralisé de Linux, et il est téléchargé en tant que spécialisé, vous obtiendrez une erreur de délai d’attente de configuration car hello machine virtuelle est bloqué au niveau de hello étape de configuration.</span><span class="sxs-lookup"><span data-stu-id="2fd95-114">**N<sup>1</sup>:** If hello OS is Linux generalized, and it is uploaded as specialized, you will get a provisioning timeout error because hello VM is stuck at hello provisioning stage.</span></span>

<span data-ttu-id="2fd95-115">**N<sup>2</sup>:** si hello du système d’exploitation est spécialisé de Linux, et il est téléchargé comme généralisé, vous obtiendrez une erreur d’échec de la configuration, car la nouvelle machine virtuelle hello s’exécute avec le nom de l’ordinateur d’origine hello, nom d’utilisateur et mot de passe.</span><span class="sxs-lookup"><span data-stu-id="2fd95-115">**N<sup>2</sup>:** If hello OS is Linux specialized, and it is uploaded as generalized, you will get a provisioning failure error because hello new VM is running with hello original computer name, username and password.</span></span>

<span data-ttu-id="2fd95-116">**Résolution :**</span><span class="sxs-lookup"><span data-stu-id="2fd95-116">**Resolution:**</span></span>

<span data-ttu-id="2fd95-117">téléchargement de ces deux erreurs, tooresolve hello du disque dur virtuel d’origine, disponible localement, avec hello même configuration que celle pour hello du système d’exploitation (généralisé/spécialisé).</span><span class="sxs-lookup"><span data-stu-id="2fd95-117">tooresolve both these errors, upload hello original VHD, available on-prem, with hello same setting as that for hello OS (generalized/specialized).</span></span> <span data-ttu-id="2fd95-118">tooupload comme généralisé, n’oubliez pas de toorun-tout d’abord annuler le déploiement.</span><span class="sxs-lookup"><span data-stu-id="2fd95-118">tooupload as generalized, remember toorun -deprovision first.</span></span>

<span data-ttu-id="2fd95-119">**Erreurs de capture :**</span><span class="sxs-lookup"><span data-stu-id="2fd95-119">**Capture Errors:**</span></span>

<span data-ttu-id="2fd95-120">**N<sup>3</sup>:** si hello du système d’exploitation est généralisé de Linux, et il est capturé en tant que spécialisé, vous obtiendrez une erreur de délai d’attente de configuration car hello original VM n’est pas utilisable car il est marqué comme généralisé.</span><span class="sxs-lookup"><span data-stu-id="2fd95-120">**N<sup>3</sup>:** If hello OS is Linux generalized, and it is captured as specialized, you will get a provisioning timeout error because hello original VM is not usable as it is marked as generalized.</span></span>

<span data-ttu-id="2fd95-121">**N<sup>4</sup>:** si hello du système d’exploitation est spécialisé de Linux, et elle est capturée comme généralisé, vous obtiendrez une erreur d’échec de la configuration, car la nouvelle machine virtuelle hello s’exécute avec le nom de l’ordinateur d’origine hello, nom d’utilisateur et mot de passe.</span><span class="sxs-lookup"><span data-stu-id="2fd95-121">**N<sup>4</sup>:** If hello OS is Linux specialized, and it is captured as generalized, you will get a provisioning failure error because hello new VM is running with hello original computer name, username and password.</span></span> <span data-ttu-id="2fd95-122">En outre, hello original VM n’est pas utilisable car il est marqué comme spécialisé.</span><span class="sxs-lookup"><span data-stu-id="2fd95-122">Also, hello original VM is not usable because it is marked as specialized.</span></span>

<span data-ttu-id="2fd95-123">**Résolution :**</span><span class="sxs-lookup"><span data-stu-id="2fd95-123">**Resolution:**</span></span>

<span data-ttu-id="2fd95-124">tooresolve les deux de ces erreurs, supprimez image actuelle de hello hello portail, et [acquérir à nouveau à partir de hello des disques durs virtuels en cours](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) avec hello même configuration que celle pour hello du système d’exploitation (généralisé/spécifique).</span><span class="sxs-lookup"><span data-stu-id="2fd95-124">tooresolve both these errors, delete hello current image from hello portal, and [recapture it from hello current VHDs](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) with hello same setting as that for hello OS (generalized/specialized).</span></span>

## <a name="issue-custom-gallery-marketplace-image-allocation-failure"></a><span data-ttu-id="2fd95-125">Problème : Image personnalisée / galerie / marketplace ; échec d’allocation</span><span class="sxs-lookup"><span data-stu-id="2fd95-125">Issue: Custom/ gallery/ marketplace image; allocation failure</span></span>
<span data-ttu-id="2fd95-126">Cette erreur se produit dans les situations lors de la nouvelle demande de machine virtuelle hello est cluster tooa épinglé qui ne peut pas de prendre en charge la taille de machine virtuelle hello demandé, ou n’a pas de demande de hello tooaccommodate d’espace libre.</span><span class="sxs-lookup"><span data-stu-id="2fd95-126">This error arises in situations when hello new VM request is pinned tooa cluster that either cannot support hello VM size being requested, or does not have available free space tooaccommodate hello request.</span></span>

<span data-ttu-id="2fd95-127">**Cause 1 :** prend en charge les clusters hello hello demandé la taille de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2fd95-127">**Cause 1:** hello cluster cannot support hello requested VM size.</span></span>

<span data-ttu-id="2fd95-128">**Résolution 1 :**</span><span class="sxs-lookup"><span data-stu-id="2fd95-128">**Resolution 1:**</span></span>

* <span data-ttu-id="2fd95-129">Réessayez la demande hello à l’aide d’une plus petite taille de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2fd95-129">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="2fd95-130">Si hello taille Hello demandé de que machine virtuelle ne peut pas être modifié :</span><span class="sxs-lookup"><span data-stu-id="2fd95-130">If hello size of hello requested VM cannot be changed:</span></span>
  * <span data-ttu-id="2fd95-131">Arrêtez tous les ordinateurs virtuels de hello dans hello à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="2fd95-131">Stop all hello VMs in hello availability set.</span></span>
    <span data-ttu-id="2fd95-132">Cliquez sur **Groupes de ressources** > *votre groupe de ressources* > **Ressources** > *votre groupe à haute disponibilité* > **Machines virtuelles** > *votre machine virtuelle* > **Arrêter**.</span><span class="sxs-lookup"><span data-stu-id="2fd95-132">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  * <span data-ttu-id="2fd95-133">Une fois que tous les hello arrêt des machines virtuelles, créer hello taille de machine virtuelle Bonjour souhaitée.</span><span class="sxs-lookup"><span data-stu-id="2fd95-133">After all hello VMs stop, create hello new VM in hello desired size.</span></span>
  * <span data-ttu-id="2fd95-134">Démarrer hello nouvelle machine virtuelle tout d’abord, puis sélectionnez chacun des hello a cessé de machines virtuelles et cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="2fd95-134">Start hello new VM first, and then select each of hello stopped VMs and click **Start**.</span></span>

<span data-ttu-id="2fd95-135">**Cause 2 :** cluster de hello n’a pas de libérer des ressources.</span><span class="sxs-lookup"><span data-stu-id="2fd95-135">**Cause 2:** hello cluster does not have free resources.</span></span>

<span data-ttu-id="2fd95-136">**Résolution 2 :**</span><span class="sxs-lookup"><span data-stu-id="2fd95-136">**Resolution 2:**</span></span>

* <span data-ttu-id="2fd95-137">Réessayez la demande de hello ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="2fd95-137">Retry hello request at a later time.</span></span>
* <span data-ttu-id="2fd95-138">Si hello nouvelle machine virtuelle peut être définie partie d’une haute disponibilité distincts</span><span class="sxs-lookup"><span data-stu-id="2fd95-138">If hello new VM can be part of a different availability set</span></span>
  * <span data-ttu-id="2fd95-139">Créer une machine virtuelle dans un ensemble différent de disponibilité (Bonjour même région).</span><span class="sxs-lookup"><span data-stu-id="2fd95-139">Create a new VM in a different availability set (in hello same region).</span></span>
  * <span data-ttu-id="2fd95-140">Ajouter hello nouvelle machine virtuelle toohello même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="2fd95-140">Add hello new VM toohello same virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2fd95-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2fd95-141">Next steps</span></span>
<span data-ttu-id="2fd95-142">Si vous rencontrez des problèmes lorsque vous démarrez une machine virtuelle Linux arrêtée ou que vous redimensionnez une machine virtuelle Linux existante dans Azure, consultez [Résoudre les problèmes de déploiement Resource Manager liés au redémarrage ou au redimensionnement d’une machine virtuelle Linux existante dans Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2fd95-142">If you encounter issues when you start a stopped Linux VM or resize an existing Linux VM in Azure, see [Troubleshoot Resource Manager deployment issues with restarting or resizing an existing Linux Virtual Machine in Azure](restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

