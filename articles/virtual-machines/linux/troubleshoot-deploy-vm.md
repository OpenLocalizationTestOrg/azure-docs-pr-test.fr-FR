---
title: "aaaTroubleshoot déploiement des problèmes d’ordinateur virtuel Linux dans Azure | Documents Microsoft"
description: "Résolution des problèmes de déploiement de la machine virtuelle Linux dans le modèle de déploiement d’Azure Resource Manager."
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
ms.date: 06/22/2017
ms.author: genli
ms.openlocfilehash: d1092ca3d9d51af7510b19c8c9a79e6dda588697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a><span data-ttu-id="faeb8-103">Résolution des problèmes de déploiement de la machine virtuelle Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="faeb8-103">Troubleshoot deploying Linux virtual machine issues in Azure</span></span>

<span data-ttu-id="faeb8-104">problèmes de déploiement d’ordinateur virtuel (VM) tootroubleshoot dans Azure, passez en revue les hello [problèmes principaux](#top-issues) des défaillances et des solutions courantes.</span><span class="sxs-lookup"><span data-stu-id="faeb8-104">tootroubleshoot virtual machine (VM) deployment issues in Azure, review hello [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="faeb8-105">Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez contacter hello experts Azure sur [hello forums MSDN Azure et le débordement de pile](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="faeb8-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="faeb8-106">Vous pouvez également signaler un incident au support Azure.</span><span class="sxs-lookup"><span data-stu-id="faeb8-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="faeb8-107">Accédez toohello [site de support technique Azure](https://azure.microsoft.com/support/options/) et sélectionnez **obtenir prend en charge**.</span><span class="sxs-lookup"><span data-stu-id="faeb8-107">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="faeb8-108">Problèmes principaux</span><span class="sxs-lookup"><span data-stu-id="faeb8-108">Top issues</span></span>
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a><span data-ttu-id="faeb8-109">cluster de Hello ne peut pas prendre en charge hello demandé la taille de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="faeb8-109">hello cluster cannot support hello requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="faeb8-110">Réessayez la demande hello à l’aide d’une plus petite taille de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="faeb8-110">Retry hello request using a smaller VM size.</span></span>
- <span data-ttu-id="faeb8-111">Si hello taille Hello demandé de que machine virtuelle ne peut pas être modifié :</span><span class="sxs-lookup"><span data-stu-id="faeb8-111">If hello size of hello requested VM cannot be changed:</span></span>
    - <span data-ttu-id="faeb8-112">Arrêtez tous les ordinateurs virtuels de hello dans hello à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="faeb8-112">Stop all hello VMs in hello availability set.</span></span> <span data-ttu-id="faeb8-113">Cliquez sur **Groupes de ressources** > votre groupe de ressources > **Ressources** > votre groupe à haute disponibilité > **Machines virtuelles** > votre machine virtuelle > **Arrêter**.</span><span class="sxs-lookup"><span data-stu-id="faeb8-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="faeb8-114">Une fois toutes les hello arrêt des machines virtuelles, créez des hello machine virtuelle de taille de hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="faeb8-114">After all hello VMs stop, create hello VM in hello desired size.</span></span>
    - <span data-ttu-id="faeb8-115">Démarrer hello nouvelle machine virtuelle tout d’abord, puis sélectionnez chacun des hello s’est arrêté de machines virtuelles, puis cliquez sur Démarrer.</span><span class="sxs-lookup"><span data-stu-id="faeb8-115">Start hello new VM first, and then select each of hello stopped VMs and click Start.</span></span>


## <a name="hello-cluster-does-not-have-free-resources"></a><span data-ttu-id="faeb8-116">cluster de Hello n’a pas de libérer des ressources</span><span class="sxs-lookup"><span data-stu-id="faeb8-116">hello cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="faeb8-117">Réessayez la demande de hello plus tard.</span><span class="sxs-lookup"><span data-stu-id="faeb8-117">Retry hello request later.</span></span>
- <span data-ttu-id="faeb8-118">Si hello nouvelle machine virtuelle peut être définie partie d’une haute disponibilité distincts</span><span class="sxs-lookup"><span data-stu-id="faeb8-118">If hello new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="faeb8-119">Créer une machine virtuelle dans un ensemble différent de disponibilité (Bonjour même région).</span><span class="sxs-lookup"><span data-stu-id="faeb8-119">Create a VM in a different availability set (in hello same region).</span></span>
    - <span data-ttu-id="faeb8-120">Ajouter hello nouvelle machine virtuelle toohello même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="faeb8-120">Add hello new VM toohello same virtual network.</span></span>

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="faeb8-121">Comment activer mon crédit mensuel pour Visual Studio Enterprise (BizSpark) ?</span><span class="sxs-lookup"><span data-stu-id="faeb8-121">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="faeb8-122">tooactivate votre mensuel de crédit, consultez ce [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="faeb8-122">tooactivate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="why-can-i-not-install-hello-gpu-driver-for-an-ubuntu-nv-vm"></a><span data-ttu-id="faeb8-123">Pourquoi ne puis-je pas installer pilote GPU hello pour une machine virtuelle NV de Ubuntu ?</span><span class="sxs-lookup"><span data-stu-id="faeb8-123">Why can I not install hello GPU driver for an Ubuntu NV VM?</span></span>

<span data-ttu-id="faeb8-124">Actuellement, la prise en charge de GPU Linux est uniquement disponible sur les machines virtuelles NC Azure exécutant Ubuntu Server 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="faeb8-124">Currently, Linux GPU support is only available on Azure NC VMs running Ubuntu Server 16.04 LTS.</span></span> <span data-ttu-id="faeb8-125">Pour plus d’informations, consultez [Configuration des pilotes GPU NVIDIA pour les machines virtuelles séries N exécutant Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="faeb8-125">For more information, see [Set up GPU drivers for N-series VMs running Linux](n-series-driver-setup.md).</span></span>

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a><span data-ttu-id="faeb8-126">Il manque des pilotes sur ma machine virtuelle Linux série N</span><span class="sxs-lookup"><span data-stu-id="faeb8-126">My drivers are missing for my Linux N-Series VM</span></span>

<span data-ttu-id="faeb8-127">Les pilotes pour les machines virtuelles Linux se trouvent [ici](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="faeb8-127">Drivers for Linux-based VMs are located [here](n-series-driver-setup.md).</span></span> 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="faeb8-128">Impossible de trouver une instance GPU dans ma machine virtuelle Série N</span><span class="sxs-lookup"><span data-stu-id="faeb8-128">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="faeb8-129">avantage tootake hello GPU des fonctionnalités de machines virtuelles N-series Azure exécutant Windows Server 2016 ou Windows Server 2012 R2, vous devez installer les pilotes de graphiques NVIDIA sur chaque machine virtuelle après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="faeb8-129">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="faeb8-130">Des informations de configuration du pilote sont disponibles pour [les machines virtuelles Windows](../windows/n-series-driver-setup.md) et [les machines virtuelles Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="faeb8-130">Driver setup information is available for [Windows VMs](../windows/n-series-driver-setup.md) and [Linux VMs](n-series-driver-setup.md).</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="faeb8-131">Les machines virtuelles Séries N sont-elles disponibles dans ma région ?</span><span class="sxs-lookup"><span data-stu-id="faeb8-131">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="faeb8-132">Vous pouvez vérifier la disponibilité de hello de hello [produits disponibles par la table region](https://azure.microsoft.com/regions/services)et la tarification [ici](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="faeb8-132">You can check hello availability from hello [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="faeb8-133">Je ne suis pas famille de taille de machine virtuelle en mesure de toosee que je veux lors du redimensionnement de ma machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="faeb8-133">I am not able toosee VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="faeb8-134">Lorsqu’un ordinateur virtuel est en cours d’exécution, il est déployé tooa des serveurs physiques.</span><span class="sxs-lookup"><span data-stu-id="faeb8-134">When a VM is running, it is deployed tooa physical server.</span></span> <span data-ttu-id="faeb8-135">Hello des serveurs physiques dans des régions Azure sont regroupés dans des clusters de matériel physique commun.</span><span class="sxs-lookup"><span data-stu-id="faeb8-135">hello physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="faeb8-136">Redimensionnement d’une machine virtuelle qui nécessite des clusters matériels de hello VM toobe déplacé toodifferent diffère selon le modèle de déploiement a été utilisé toodeploy hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="faeb8-136">Resizing a VM that requires hello VM toobe moved toodifferent hardware clusters is different depending on which deployment model was used toodeploy hello VM.</span></span>

- <span data-ttu-id="faeb8-137">Machines virtuelles déployées dans le modèle de déploiement classique, déploiement de service cloud hello doivent être supprimés et redéploiement taille de tooa toochange hello machines virtuelles dans une autre famille de taille.</span><span class="sxs-lookup"><span data-stu-id="faeb8-137">VMs deployed in Classic deployment model, hello cloud service deployment must be removed and redeployed toochange hello VMs tooa size in another size family.</span></span>

- <span data-ttu-id="faeb8-138">Machines virtuelles déployées dans le modèle de déploiement de gestionnaire de ressources, vous devez arrêter toutes les machines virtuelles hello groupe à haute disponibilité avant de modifier la taille de hello de n’importe quel ordinateur virtuel à haute disponibilité hello.</span><span class="sxs-lookup"><span data-stu-id="faeb8-138">VMs deployed in Resource Manager deployment model, you must stop all VMs in hello availability set before changing hello size of any VM in hello availability set.</span></span>

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="faeb8-139">Hello répertorié taille de machine virtuelle n'est pas pris en charge lors du déploiement de haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="faeb8-139">hello listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="faeb8-140">Choisissez une taille qui est pris en charge sur le cluster de l’ensemble de disponibilité hello.</span><span class="sxs-lookup"><span data-stu-id="faeb8-140">Choose a size that is supported on hello availability set's cluster.</span></span> <span data-ttu-id="faeb8-141">Il est recommandé lorsque vous créez qu'un ensemble de disponibilité toochoose hello plus grande taille de machine virtuelle vous pensez que vous avez besoin et que vous avez être votre première toohello de déploiement à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="faeb8-141">It is recommended when creating an availability set toochoose hello largest VM size you think you need, and have that be your first deployment toohello Availability set.</span></span>

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a><span data-ttu-id="faeb8-142">Quelles distributions/versions de Linux sont prises en charges par Azure ?</span><span class="sxs-lookup"><span data-stu-id="faeb8-142">What Linux distributions/versions are supported on Azure?</span></span>

<span data-ttu-id="faeb8-143">Vous trouverez la liste hello à Linux sur [Azure-Endorsed Distributions](endorsed-distros.md).</span><span class="sxs-lookup"><span data-stu-id="faeb8-143">You can find hello list at Linux on [Azure-Endorsed Distributions](endorsed-distros.md).</span></span>

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a><span data-ttu-id="faeb8-144">Puis-je ajouter un ensemble de disponibilité tooan classique de machine virtuelle existant ?</span><span class="sxs-lookup"><span data-stu-id="faeb8-144">Can I add an existing Classic VM tooan availability set?</span></span>

<span data-ttu-id="faeb8-145">Oui.</span><span class="sxs-lookup"><span data-stu-id="faeb8-145">Yes.</span></span> <span data-ttu-id="faeb8-146">Vous pouvez ajouter un tooa d’ordinateur virtuel classique existante nouvelle ou existante à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="faeb8-146">You can add an existing classic VM tooa new or existing Availability Set.</span></span> <span data-ttu-id="faeb8-147">Pour plus d’informations, consultez [ajouter un ensemble de disponibilité tooan machine virtuelle existante](../windows/classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="faeb8-147">For more information see [Add an existing virtual machine tooan availability set](../windows/classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="faeb8-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="faeb8-148">Next steps</span></span>
<span data-ttu-id="faeb8-149">Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez contacter hello experts Azure sur [hello forums MSDN Azure et le débordement de pile](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="faeb8-149">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="faeb8-150">Vous pouvez également signaler un incident au support Azure.</span><span class="sxs-lookup"><span data-stu-id="faeb8-150">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="faeb8-151">Accédez toohello [site de support technique Azure](https://azure.microsoft.com/support/options/) et sélectionnez **obtenir prend en charge**.</span><span class="sxs-lookup"><span data-stu-id="faeb8-151">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
