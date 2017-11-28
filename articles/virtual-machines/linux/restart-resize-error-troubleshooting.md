---
title: "aaaVM redémarrage ou redimensionnement de problèmes dans Azure | Documents Microsoft"
description: "Résoudre les problèmes de déploiement Resource Manager liés au redémarrage ou au redimensionnement d’une machine virtuelle Linux existante dans Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: Deland-Han
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 51f1610c-0290-464a-97d4-c2e485c7ae7f
ms.service: virtual-machines-linux
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.workload: required
ms.date: 01/10/2017
ms.author: delhan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d9ff76b64b6646b04565eb93110759c4ebc858e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-restarting-or-resizing-an-existing-linux-vm-in-azure"></a><span data-ttu-id="e7dd5-103">Résoudre les problèmes de déploiement liés au redémarrage ou au redimensionnement d’une machine virtuelle Linux existante dans Azure</span><span class="sxs-lookup"><span data-stu-id="e7dd5-103">Troubleshoot deployment issues with restarting or resizing an existing Linux VM in Azure</span></span>
<span data-ttu-id="e7dd5-104">Lorsque vous essayez de toostart une Machine virtuelle de Azure (VM) arrêté ou redimensionnez une machine virtuelle Azure existante, les erreurs courantes hello que vous rencontrez sont un échec d’allocation.</span><span class="sxs-lookup"><span data-stu-id="e7dd5-104">When you try toostart a stopped Azure Virtual Machine (VM), or resize an existing Azure VM, hello common error you encounter is an allocation failure.</span></span> <span data-ttu-id="e7dd5-105">Cette erreur se produit lorsque le cluster de hello ou la région n’a pas de ressources disponibles ou ne peut pas prise en charge hello demandée taille de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e7dd5-105">This error results when hello cluster or region either does not have resources available or cannot support hello requested VM size.</span></span>

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]

## <a name="collect-activity-logs"></a><span data-ttu-id="e7dd5-106">Collecte des journaux d’activité</span><span class="sxs-lookup"><span data-stu-id="e7dd5-106">Collect activity logs</span></span>
<span data-ttu-id="e7dd5-107">toostart résolution des problèmes, activité hello collecter consigne l’erreur de hello de tooidentify associé au problème de hello.</span><span class="sxs-lookup"><span data-stu-id="e7dd5-107">toostart troubleshooting, collect hello activity logs tooidentify hello error associated with hello issue.</span></span> <span data-ttu-id="e7dd5-108">Hello suivant liens contiennent des informations détaillées sur les processus hello :</span><span class="sxs-lookup"><span data-stu-id="e7dd5-108">hello following links contain detailed information on hello process:</span></span>

[<span data-ttu-id="e7dd5-109">Voir les opérations de déploiement</span><span class="sxs-lookup"><span data-stu-id="e7dd5-109">View deployment operations</span></span>](../../azure-resource-manager/resource-manager-deployment-operations.md)

[<span data-ttu-id="e7dd5-110">Afficher l’activité des journaux toomanage Azure ressources</span><span class="sxs-lookup"><span data-stu-id="e7dd5-110">View activity logs toomanage Azure resources</span></span>](../../resource-group-audit.md)

## <a name="issue-error-when-starting-a-stopped-vm"></a><span data-ttu-id="e7dd5-111">Problème : erreur lors du démarrage d’une machine virtuelle arrêtée</span><span class="sxs-lookup"><span data-stu-id="e7dd5-111">Issue: Error when starting a stopped VM</span></span>
<span data-ttu-id="e7dd5-112">Vous essayez de toostart une machine virtuelle arrêtée mais obtenez un échec d’allocation.</span><span class="sxs-lookup"><span data-stu-id="e7dd5-112">You try toostart a stopped VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="e7dd5-113">Cause :</span><span class="sxs-lookup"><span data-stu-id="e7dd5-113">Cause</span></span>
<span data-ttu-id="e7dd5-114">demande Hello toostart hello arrêté la machine virtuelle a toobe émise au cluster d’origine hello qui héberge le service de cloud computing hello.</span><span class="sxs-lookup"><span data-stu-id="e7dd5-114">hello request toostart hello stopped VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="e7dd5-115">Toutefois, les clusters hello n’ont pas de demande de hello toofulfill disponible d’espace libre.</span><span class="sxs-lookup"><span data-stu-id="e7dd5-115">However, hello cluster does not have free space available toofulfill hello request.</span></span>

### <a name="resolution"></a><span data-ttu-id="e7dd5-116">Résolution :</span><span class="sxs-lookup"><span data-stu-id="e7dd5-116">Resolution</span></span>
* <span data-ttu-id="e7dd5-117">Arrêter hello toutes les machines virtuelles dans la disponibilité de hello définir, puis redémarrer chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e7dd5-117">Stop all hello VMs in hello availability set, and then restart each VM.</span></span>
  
  1. <span data-ttu-id="e7dd5-118">Cliquez sur **Groupes de ressources** > *votre groupe de ressources* > **Ressources** > *votre groupe à haute disponibilité* > **Machines virtuelles** > *votre machine virtuelle* > **Arrêter**.</span><span class="sxs-lookup"><span data-stu-id="e7dd5-118">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="e7dd5-119">Une fois toutes les hello arrêt des machines virtuelles, chacune des machines virtuelles de hello arrêté puis cliquez sur Démarrer.</span><span class="sxs-lookup"><span data-stu-id="e7dd5-119">After all hello VMs stop, select each of hello stopped VMs and click Start.</span></span>
* <span data-ttu-id="e7dd5-120">Relancez la demande de redémarrage de hello ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="e7dd5-120">Retry hello restart request at a later time.</span></span>

## <a name="issue-error-when-resizing-an-existing-vm"></a><span data-ttu-id="e7dd5-121">Problème : erreur lors du redimensionnement d’une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="e7dd5-121">Issue: Error when resizing an existing VM</span></span>
<span data-ttu-id="e7dd5-122">Vous essayez tooresize une machine virtuelle existante mais un échec d’allocation.</span><span class="sxs-lookup"><span data-stu-id="e7dd5-122">You try tooresize an existing VM but get an allocation failure.</span></span>

### <a name="cause"></a><span data-ttu-id="e7dd5-123">Cause :</span><span class="sxs-lookup"><span data-stu-id="e7dd5-123">Cause</span></span>
<span data-ttu-id="e7dd5-124">demande Hello tooresize hello machine virtuelle a toobe tentée au cluster d’origine de hello ce service de cloud hello hôtes.</span><span class="sxs-lookup"><span data-stu-id="e7dd5-124">hello request tooresize hello VM has toobe attempted at hello original cluster that hosts hello cloud service.</span></span> <span data-ttu-id="e7dd5-125">Toutefois, les clusters hello ne prend pas en charge hello demandé la taille de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e7dd5-125">However, hello cluster does not support hello requested VM size.</span></span>

### <a name="resolution"></a><span data-ttu-id="e7dd5-126">Résolution :</span><span class="sxs-lookup"><span data-stu-id="e7dd5-126">Resolution</span></span>
* <span data-ttu-id="e7dd5-127">Réessayez la demande hello à l’aide d’une plus petite taille de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e7dd5-127">Retry hello request using a smaller VM size.</span></span>
* <span data-ttu-id="e7dd5-128">Si hello taille Hello demandé de que machine virtuelle ne peut pas être modifié :</span><span class="sxs-lookup"><span data-stu-id="e7dd5-128">If hello size of hello requested VM cannot be changed：</span></span>
  
  1. <span data-ttu-id="e7dd5-129">Arrêtez tous les ordinateurs virtuels de hello dans hello à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="e7dd5-129">Stop all hello VMs in hello availability set.</span></span>
     
     * <span data-ttu-id="e7dd5-130">Cliquez sur **Groupes de ressources** > *votre groupe de ressources* > **Ressources** > *votre groupe à haute disponibilité* > **Machines virtuelles** > *votre machine virtuelle* > **Arrêter**.</span><span class="sxs-lookup"><span data-stu-id="e7dd5-130">Click **Resource groups** > *your resource group* > **Resources** > *your availability set* > **Virtual Machines** > *your virtual machine* > **Stop**.</span></span>
  2. <span data-ttu-id="e7dd5-131">Une fois toutes les hello arrêt des machines virtuelles, redimensionner hello souhaité VM tooa plus grande taille.</span><span class="sxs-lookup"><span data-stu-id="e7dd5-131">After all hello VMs stop, resize hello desired VM tooa larger size.</span></span>
  3. <span data-ttu-id="e7dd5-132">Sélectionnez hello redimensionné la machine virtuelle et cliquez sur **Démarrer**, puis démarrez chaque hello a cessé de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="e7dd5-132">Select hello resized VM and click **Start**, and then start each of hello stopped VMs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7dd5-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e7dd5-133">Next steps</span></span>
<span data-ttu-id="e7dd5-134">Si vous rencontrez des problèmes lorsque vous créez une machine virtuelle Linux dans Azure, consultez [Résoudre les problèmes de déploiement liés à la création d’une machine virtuelle Linux dans Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e7dd5-134">If you encounter issues when you create a new Linux VM in Azure, see [Troubleshoot deployment issues with creating a new Linux virtual machine in Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

