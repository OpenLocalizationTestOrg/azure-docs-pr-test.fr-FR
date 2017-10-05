---
title: "Résolution des problèmes de déploiement de la machine virtuelle Linux dans Azure | Microsoft Docs"
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
ms.openlocfilehash: 8bc9de90a49caf9155073caaa160585c6cc3728b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a><span data-ttu-id="48cd3-103">Résolution des problèmes de déploiement de la machine virtuelle Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="48cd3-103">Troubleshoot deploying Linux virtual machine issues in Azure</span></span>

<span data-ttu-id="48cd3-104">Pour résoudre les problèmes de déploiement de la machine virtuelle (VM) dans Azure, passez en revue les [problèmes principaux](#top-issues) pour voir les erreurs courantes et les solutions.</span><span class="sxs-lookup"><span data-stu-id="48cd3-104">To troubleshoot virtual machine (VM) deployment issues in Azure, review the [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="48cd3-105">Si vous avez besoin d’une aide supplémentaire à quelque étape que ce soit dans cet article, vous pouvez contacter les experts Azure sur les [forums MSDN Azure et Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="48cd3-105">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="48cd3-106">Vous pouvez également signaler un incident au support Azure.</span><span class="sxs-lookup"><span data-stu-id="48cd3-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="48cd3-107">Accédez au [site du support Azure](https://azure.microsoft.com/support/options/) , puis cliquez sur **Obtenir un support**.</span><span class="sxs-lookup"><span data-stu-id="48cd3-107">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="48cd3-108">Problèmes principaux</span><span class="sxs-lookup"><span data-stu-id="48cd3-108">Top issues</span></span>
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="the-cluster-cannot-support-the-requested-vm-size"></a><span data-ttu-id="48cd3-109">Le cluster ne peut pas prendre en charge la taille de machine virtuelle demandée</span><span class="sxs-lookup"><span data-stu-id="48cd3-109">The cluster cannot support the requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="48cd3-110">Relancez la requête en utilisant une taille inférieure pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="48cd3-110">Retry the request using a smaller VM size.</span></span>
- <span data-ttu-id="48cd3-111">Si la taille de la machine virtuelle requise ne peut pas être modifiée :</span><span class="sxs-lookup"><span data-stu-id="48cd3-111">If the size of the requested VM cannot be changed:</span></span>
    - <span data-ttu-id="48cd3-112">Arrêtez toutes les machines virtuelles dans le groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="48cd3-112">Stop all the VMs in the availability set.</span></span> <span data-ttu-id="48cd3-113">Cliquez sur **Groupes de ressources** > votre groupe de ressources > **Ressources** > votre groupe à haute disponibilité > **Machines virtuelles** > votre machine virtuelle > **Arrêter**.</span><span class="sxs-lookup"><span data-stu-id="48cd3-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="48cd3-114">Une fois que toutes les machines virtuelles sont arrêtées, créez une machine virtuelle à la taille souhaitée.</span><span class="sxs-lookup"><span data-stu-id="48cd3-114">After all the VMs stop, create the VM in the desired size.</span></span>
    - <span data-ttu-id="48cd3-115">Démarrez la nouvelle machine virtuelle en premier, puis sélectionnez chacune des machines virtuelles arrêtées et cliquez sur Démarrer.</span><span class="sxs-lookup"><span data-stu-id="48cd3-115">Start the new VM first, and then select each of the stopped VMs and click Start.</span></span>


## <a name="the-cluster-does-not-have-free-resources"></a><span data-ttu-id="48cd3-116">Le cluster n’a pas de ressources libres</span><span class="sxs-lookup"><span data-stu-id="48cd3-116">The cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="48cd3-117">Relancez la requête ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="48cd3-117">Retry the request later.</span></span>
- <span data-ttu-id="48cd3-118">Si la nouvelle machine virtuelle peut faire partie d’un autre groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="48cd3-118">If the new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="48cd3-119">Créez une machine virtuelle dans un autre groupe à haute disponibilité (dans la même région).</span><span class="sxs-lookup"><span data-stu-id="48cd3-119">Create a VM in a different availability set (in the same region).</span></span>
    - <span data-ttu-id="48cd3-120">Ajoutez la nouvelle machine virtuelle au même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="48cd3-120">Add the new VM to the same virtual network.</span></span>

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="48cd3-121">Comment activer mon crédit mensuel pour Visual Studio Enterprise (BizSpark) ?</span><span class="sxs-lookup"><span data-stu-id="48cd3-121">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="48cd3-122">Pour activer votre crédit mensuel, consultez cet [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="48cd3-122">To activate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="why-can-i-not-install-the-gpu-driver-for-an-ubuntu-nv-vm"></a><span data-ttu-id="48cd3-123">Pourquoi ne puis-je pas installer le pilote du GPU sur une machine virtuelle Ubuntu NV ?</span><span class="sxs-lookup"><span data-stu-id="48cd3-123">Why can I not install the GPU driver for an Ubuntu NV VM?</span></span>

<span data-ttu-id="48cd3-124">Actuellement, la prise en charge de GPU Linux est uniquement disponible sur les machines virtuelles NC Azure exécutant Ubuntu Server 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="48cd3-124">Currently, Linux GPU support is only available on Azure NC VMs running Ubuntu Server 16.04 LTS.</span></span> <span data-ttu-id="48cd3-125">Pour plus d’informations, consultez [Configuration des pilotes GPU NVIDIA pour les machines virtuelles séries N exécutant Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="48cd3-125">For more information, see [Set up GPU drivers for N-series VMs running Linux](n-series-driver-setup.md).</span></span>

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a><span data-ttu-id="48cd3-126">Il manque des pilotes sur ma machine virtuelle Linux série N</span><span class="sxs-lookup"><span data-stu-id="48cd3-126">My drivers are missing for my Linux N-Series VM</span></span>

<span data-ttu-id="48cd3-127">Les pilotes pour les machines virtuelles Linux se trouvent [ici](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="48cd3-127">Drivers for Linux-based VMs are located [here](n-series-driver-setup.md).</span></span> 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="48cd3-128">Impossible de trouver une instance GPU dans ma machine virtuelle série N</span><span class="sxs-lookup"><span data-stu-id="48cd3-128">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="48cd3-129">Pour tirer parti des fonctionnalités GPU des machines virtuelles série N Azure exécutant Windows Server 2016 ou Windows Server 2012 R2, vous devez installer des pilotes graphiques NVIDIA sur chaque machine virtuelle après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="48cd3-129">To take advantage of the GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="48cd3-130">Des informations de configuration du pilote sont disponibles pour [les machines virtuelles Windows](../windows/n-series-driver-setup.md) et [les machines virtuelles Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="48cd3-130">Driver setup information is available for [Windows VMs](../windows/n-series-driver-setup.md) and [Linux VMs](n-series-driver-setup.md).</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="48cd3-131">Les machines virtuelles Séries N sont-elles disponibles dans ma région ?</span><span class="sxs-lookup"><span data-stu-id="48cd3-131">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="48cd3-132">Vous pouvez vérifier la disponibilité à l’aide de la [Table des produits disponibles par région](https://azure.microsoft.com/regions/services) ainsi que les tarifications [ici](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="48cd3-132">You can check the availability from the [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="i-am-not-able-to-see-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="48cd3-133">Impossible de voir les différentes familles de taille de machines virtuelles quand je redimensionne ma machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="48cd3-133">I am not able to see VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="48cd3-134">Lorsqu’un ordinateur virtuel est en cours d’exécution, il est déployé sur un serveur physique.</span><span class="sxs-lookup"><span data-stu-id="48cd3-134">When a VM is running, it is deployed to a physical server.</span></span> <span data-ttu-id="48cd3-135">Les serveurs physiques dans les régions Azure sont regroupés dans des clusters de matériel physique commun.</span><span class="sxs-lookup"><span data-stu-id="48cd3-135">The physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="48cd3-136">La méthode pour redimensionner une machine virtuelle qui doit être transférée vers différents clusters de matériel physique peut varier en fonction du modèle de déploiement utilisé pour déployer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="48cd3-136">Resizing a VM that requires the VM to be moved to different hardware clusters is different depending on which deployment model was used to deploy the VM.</span></span>

- <span data-ttu-id="48cd3-137">Si les machines virtuelles sont déployées à partir d’un modèle de déploiement classique, le déploiement du service cloud doit être supprimé et redéployé afin de changer la taille de la machine virtuelle pour une autre famille de taille.</span><span class="sxs-lookup"><span data-stu-id="48cd3-137">VMs deployed in Classic deployment model, the cloud service deployment must be removed and redeployed to change the VMs to a size in another size family.</span></span>

- <span data-ttu-id="48cd3-138">Si les machines virtuelles sont déployées à partir du modèle de déploiement Resource Manager, vous devez arrêter toutes les machines virtuelles dans le groupe à haute disponibilité avant de changer la taille d’une machine dans le groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="48cd3-138">VMs deployed in Resource Manager deployment model, you must stop all VMs in the availability set before changing the size of any VM in the availability set.</span></span>

## <a name="the-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="48cd3-139">La taille de machine virtuelle répertoriée n’est pas prise en charge lors du déploiement dans le groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="48cd3-139">The listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="48cd3-140">Choisissez une taille prise en charge par le cluster du groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="48cd3-140">Choose a size that is supported on the availability set's cluster.</span></span> <span data-ttu-id="48cd3-141">Lors de la création d’un groupe à haute disponibilité, il est recommandé de choisir la plus grande taille de machine virtuelle dont vous pensez avoir besoin. Ce sera votre premier déploiement dans le groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="48cd3-141">It is recommended when creating an availability set to choose the largest VM size you think you need, and have that be your first deployment to the Availability set.</span></span>

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a><span data-ttu-id="48cd3-142">Quelles distributions/versions de Linux sont prises en charges par Azure ?</span><span class="sxs-lookup"><span data-stu-id="48cd3-142">What Linux distributions/versions are supported on Azure?</span></span>

<span data-ttu-id="48cd3-143">Vous pouvez trouver la liste sur Linux sur [Distributions prises en charge par Azure](endorsed-distros.md).</span><span class="sxs-lookup"><span data-stu-id="48cd3-143">You can find the list at Linux on [Azure-Endorsed Distributions](endorsed-distros.md).</span></span>

## <a name="can-i-add-an-existing-classic-vm-to-an-availability-set"></a><span data-ttu-id="48cd3-144">Est-il possible d’ajouter une machine virtuelle classique à un groupe à haute disponibilité ?</span><span class="sxs-lookup"><span data-stu-id="48cd3-144">Can I add an existing Classic VM to an availability set?</span></span>

<span data-ttu-id="48cd3-145">Oui.</span><span class="sxs-lookup"><span data-stu-id="48cd3-145">Yes.</span></span> <span data-ttu-id="48cd3-146">Vous pouvez ajouter une machine virtuelle classique existante à un nouveau groupe ou à un groupe à haute disponibilité déjà existant.</span><span class="sxs-lookup"><span data-stu-id="48cd3-146">You can add an existing classic VM to a new or existing Availability Set.</span></span> <span data-ttu-id="48cd3-147">Pour plus d’informations, consultez [Ajouter une machine virtuelle existante à un groupe à haute disponibilité](../windows/classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="48cd3-147">For more information see [Add an existing virtual machine to an availability set](../windows/classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="48cd3-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="48cd3-148">Next steps</span></span>
<span data-ttu-id="48cd3-149">Si vous avez besoin d’une aide supplémentaire à quelque étape que ce soit dans cet article, vous pouvez contacter les experts Azure sur les [forums MSDN Azure et Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="48cd3-149">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="48cd3-150">Vous pouvez également signaler un incident au support Azure.</span><span class="sxs-lookup"><span data-stu-id="48cd3-150">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="48cd3-151">Accédez au [site du support Azure](https://azure.microsoft.com/support/options/) , puis cliquez sur **Obtenir un support**.</span><span class="sxs-lookup"><span data-stu-id="48cd3-151">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
