---
title: "Résolution des problèmes de déploiement de la machine virtuelle Windows dans Azure | Microsoft Docs"
description: "Résolution des problèmes de déploiement de la machine virtuelle Windows dans le modèle de déploiement d’Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: genlin
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
ms.openlocfilehash: 6800c137097c2803f28dec7365f6d3f2a173b411
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-deploying-windows-virtual-machine-issues-in-azure"></a><span data-ttu-id="b6893-103">Résolution des problèmes de déploiement de la machine virtuelle Windows dans Azure</span><span class="sxs-lookup"><span data-stu-id="b6893-103">Troubleshoot deploying Windows virtual machine issues in Azure</span></span>

<span data-ttu-id="b6893-104">Pour résoudre les problèmes de déploiement de la machine virtuelle (VM) dans Azure, passez en revue les [principaux problèmes](#top-issues) pour voir les erreurs courantes et les solutions.</span><span class="sxs-lookup"><span data-stu-id="b6893-104">To troubleshoot virtual machine (VM) deployment issues in Azure, review the [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="b6893-105">Si vous avez besoin d’une aide supplémentaire à quelque étape que ce soit dans cet article, vous pouvez contacter les experts Azure sur les [forums MSDN Azure et Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="b6893-105">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="b6893-106">Vous pouvez également signaler un incident au support Azure.</span><span class="sxs-lookup"><span data-stu-id="b6893-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="b6893-107">Accédez au [site du support Azure](https://azure.microsoft.com/support/options/) , puis cliquez sur **Obtenir un support**.</span><span class="sxs-lookup"><span data-stu-id="b6893-107">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="b6893-108">Problèmes principaux</span><span class="sxs-lookup"><span data-stu-id="b6893-108">Top issues</span></span>
[!INCLUDE [virtual-machines-windows-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

## <a name="the-cluster-cannot-support-the-requested-vm-size"></a><span data-ttu-id="b6893-109">Le cluster ne peut pas prendre en charge la taille de machine virtuelle demandée</span><span class="sxs-lookup"><span data-stu-id="b6893-109">The cluster cannot support the requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="b6893-110">Relancez la requête en utilisant une taille inférieure pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b6893-110">Retry the request using a smaller VM size.</span></span>
- <span data-ttu-id="b6893-111">Si la taille de la machine virtuelle requise ne peut pas être modifiée :</span><span class="sxs-lookup"><span data-stu-id="b6893-111">If the size of the requested VM cannot be changed:</span></span>
    - <span data-ttu-id="b6893-112">Arrêtez toutes les machines virtuelles dans le groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="b6893-112">Stop all the VMs in the availability set.</span></span> <span data-ttu-id="b6893-113">Cliquez sur **Groupes de ressources** > votre groupe de ressources > **Ressources** > votre groupe à haute disponibilité > **Machines virtuelles** > votre machine virtuelle > **Arrêter**.</span><span class="sxs-lookup"><span data-stu-id="b6893-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="b6893-114">Une fois que toutes les machines virtuelles sont arrêtées, créez une machine virtuelle à la taille souhaitée.</span><span class="sxs-lookup"><span data-stu-id="b6893-114">After all the VMs stop, create the VM in the desired size.</span></span>
    - <span data-ttu-id="b6893-115">Démarrez la nouvelle machine virtuelle en premier, puis sélectionnez chacune des machines virtuelles arrêtées et cliquez sur Démarrer.</span><span class="sxs-lookup"><span data-stu-id="b6893-115">Start the new VM first, and then select each of the stopped VMs and click Start.</span></span>


## <a name="the-cluster-does-not-have-free-resources"></a><span data-ttu-id="b6893-116">Le cluster n’a pas de ressources libres</span><span class="sxs-lookup"><span data-stu-id="b6893-116">The cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="b6893-117">Relancez la requête ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="b6893-117">Retry the request later.</span></span>
- <span data-ttu-id="b6893-118">Si la nouvelle machine virtuelle peut faire partie d’un autre groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="b6893-118">If the new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="b6893-119">Créez une machine virtuelle dans un autre groupe à haute disponibilité (dans la même région).</span><span class="sxs-lookup"><span data-stu-id="b6893-119">Create a VM in a different availability set (in the same region).</span></span>
    - <span data-ttu-id="b6893-120">Ajoutez la nouvelle machine virtuelle au même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="b6893-120">Add the new VM to the same virtual network.</span></span>

## <a name="how-can-i-use-and-deploy-a-windows-client-image-into-azure"></a><span data-ttu-id="b6893-121">Comment utiliser et déployer des images de client Windows dans Azure ?</span><span class="sxs-lookup"><span data-stu-id="b6893-121">How can I use and deploy a windows client image into Azure?</span></span>

<span data-ttu-id="b6893-122">Vous pouvez utiliser Windows 7, Windows 8 ou Windows 10 dans Azure pour des scénarios de développement /de test à condition de disposer d'un abonnement Visual Studio (anciennement MSDN) approprié.</span><span class="sxs-lookup"><span data-stu-id="b6893-122">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios if you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> <span data-ttu-id="b6893-123">Cet [article](client-images.md) décrit les conditions d’éligibilité pour les clients Windows en cours d’exécution dans Azure et l’utilisation des images de galerie Azure.</span><span class="sxs-lookup"><span data-stu-id="b6893-123">This [article](client-images.md) outlines the eligibility requirements for running Windows client in Azure and uses of the Azure Gallery images.</span></span>

## <a name="how-can-i-deploy-a-virtual-machine-using-the-hybrid-use-benefit-hub"></a><span data-ttu-id="b6893-124">Comment déployer une machine virtuelle à l’aide du Hybrid Use Benefit (HUB) ?</span><span class="sxs-lookup"><span data-stu-id="b6893-124">How can I deploy a virtual machine using the Hybrid Use Benefit (HUB)?</span></span>

<span data-ttu-id="b6893-125">Il existe de nombreuses manières de déployer des machines virtuelles Windows avec Azure Hybrid Use Benefit.</span><span class="sxs-lookup"><span data-stu-id="b6893-125">There are a couple of different ways to deploy Windows virtual machines with the Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="b6893-126">Un abonnement avec un contrat Entreprise :</span><span class="sxs-lookup"><span data-stu-id="b6893-126">For an Enterprise Agreement subscription:</span></span>

<span data-ttu-id="b6893-127">•   Déployez des machines virtuelles à partir d’images de la Place de marché spécifiques qui sont préconfigurées avec Azure Hybrid Use Benefit.</span><span class="sxs-lookup"><span data-stu-id="b6893-127">•   Deploy VMs from specific Marketplace images that are pre-configured with Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="b6893-128">Contrat Entreprise :</span><span class="sxs-lookup"><span data-stu-id="b6893-128">For Enterprise agreement:</span></span>

<span data-ttu-id="b6893-129">•  Téléchargez une machine virtuelle personnalisée et effectuez le déploiement à l’aide d’un modèle Resource Manager ou d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b6893-129">•   Upload a custom VM and deploy using a Resource Manager template or Azure PowerShell.</span></span>

<span data-ttu-id="b6893-130">Pour plus d’informations, consultez les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="b6893-130">For more information, see the following resources:</span></span>

 - [<span data-ttu-id="b6893-131">Présentation d’Azure Hybrid Use Benefit </span><span class="sxs-lookup"><span data-stu-id="b6893-131">Azure Hybrid Use Benefit overview </span></span>](https://azure.microsoft.com/pricing/hybrid-use-benefit/)

 - [<span data-ttu-id="b6893-132">FAQ téléchargeable</span><span class="sxs-lookup"><span data-stu-id="b6893-132">Downloadable FAQ</span></span>](http://download.microsoft.com/download/4/2/1/4211AC94-D607-4A45-B472-4B30EDF437DE/Windows_Server_Azure_Hybrid_Use_FAQ_EN_US.pdf)

 - <span data-ttu-id="b6893-133">[Azure Hybrid Use Benefit pour Windows Server et client Windows](hybrid-use-benefit-licensing.md).</span><span class="sxs-lookup"><span data-stu-id="b6893-133">[Azure Hybrid Use Benefit for Windows Server and Windows Client](hybrid-use-benefit-licensing.md).</span></span>

 - [<span data-ttu-id="b6893-134">Utilisation de Hybrid Use Benefit dans Azure</span><span class="sxs-lookup"><span data-stu-id="b6893-134">How can I use the Hybrid Use Benefit in Azure</span></span>](https://blogs.msdn.microsoft.com/azureedu/2016/04/13/how-can-i-use-the-hybrid-use-benefit-in-azure)

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="b6893-135">Comment activer mon crédit mensuel pour Visual Studio Enterprise (BizSpark) ?</span><span class="sxs-lookup"><span data-stu-id="b6893-135">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="b6893-136">Pour activer votre crédit mensuel, consultez cet [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="b6893-136">To activate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="how-to-add-enterprise-devtest-to-my-enterprise-agreement-ea-to-get-access-to-window-client-images"></a><span data-ttu-id="b6893-137">Comment ajouter Enterprise Dev/Test à mon Contrat Entreprise (EA) pour accéder aux images de client Windows ?</span><span class="sxs-lookup"><span data-stu-id="b6893-137">How to add Enterprise Dev/Test to my Enterprise Agreement (EA) to get access to Window client images?</span></span>

<span data-ttu-id="b6893-138">La possibilité de créer des abonnements basés sur l’offre Enterprise Dev/Test est limitée aux propriétaires de comptes qui y ont été autorisés par un administrateur d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="b6893-138">The ability to create subscriptions based on the Enterprise Dev/Test offer is restricted to Account Owners who have been given permission to do so by an Enterprise Administrator.</span></span> <span data-ttu-id="b6893-139">Le propriétaire de compte crée les abonnements par le biais du portail des comptes Azure. Il doit ensuite ajouter les abonnés Visual Studio actifs en tant que coadministrateurs.</span><span class="sxs-lookup"><span data-stu-id="b6893-139">The Account Owner creates subscriptions via the Azure Account Portal, and then should add active Visual Studio subscribers as co-administrators.</span></span> <span data-ttu-id="b6893-140">Ils pourront alors gérer et utiliser les ressources nécessaires au développement et au test.</span><span class="sxs-lookup"><span data-stu-id="b6893-140">So that they can manage and use the resources needed for development and testing.</span></span> <span data-ttu-id="b6893-141">Pour plus d’informations, consultez [Enterprise Dev/Test](https://azure.microsoft.com/offers/ms-azr-0148p/).</span><span class="sxs-lookup"><span data-stu-id="b6893-141">For more information, see [Enterprise Dev/Test](https://azure.microsoft.com/offers/ms-azr-0148p/).</span></span>

## <a name="my-drivers-are-missing-for-my-windows-n-series-vm"></a><span data-ttu-id="b6893-142">Il manque des pilotes sur ma machine virtuelle Windows Série N</span><span class="sxs-lookup"><span data-stu-id="b6893-142">My drivers are missing for my Windows N-Series VM</span></span>

<span data-ttu-id="b6893-143">Les pilotes pour les machines virtuelles Windows se trouvent [ici](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="b6893-143">Drivers for Windows-based VMs are located [here](n-series-driver-setup.md).</span></span>

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="b6893-144">Impossible de trouver une instance GPU dans ma machine virtuelle Série N</span><span class="sxs-lookup"><span data-stu-id="b6893-144">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="b6893-145">Pour tirer parti des fonctionnalités GPU des machines virtuelles série N Azure exécutant Windows Server 2016 ou Windows Server 2012 R2, vous devez installer des pilotes graphiques NVIDIA sur chaque machine virtuelle après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="b6893-145">To take advantage of the GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="b6893-146">Des informations de configuration du pilote sont disponibles pour [les machines virtuelles Windows](n-series-driver-setup.md) et [les machines virtuelles Linux](../linux/n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="b6893-146">Driver setup information is available for [Windows VMs](n-series-driver-setup.md) and [Linux VMs](../linux/n-series-driver-setup.md).</span></span>

## <a name="are-client-images-supported-for-n-series"></a><span data-ttu-id="b6893-147">Est-ce que les Séries N prennent en charge les images de client ?</span><span class="sxs-lookup"><span data-stu-id="b6893-147">Are client images supported for N-Series?</span></span>

<span data-ttu-id="b6893-148">À l’heure actuelle, Azure ne prend en charge que les machines virtuelles Séries N exécutant Windows Server et les systèmes d’exploitation Linux.</span><span class="sxs-lookup"><span data-stu-id="b6893-148">Currently, Azure only supports N-Series on VMs running Windows Server and Linux operating systems.</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="b6893-149">Les machines virtuelles Séries N sont-elles disponibles dans ma région ?</span><span class="sxs-lookup"><span data-stu-id="b6893-149">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="b6893-150">Vous pouvez vérifier la disponibilité à l’aide de la [Table des produits disponibles par région](https://azure.microsoft.com/regions/services) ainsi que les tarifications [ici](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="b6893-150">You can check the availability from the [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="what-client-images-can-i-use-and-deploy-in-azure-and-how-to-i-get-them"></a><span data-ttu-id="b6893-151">Quelles sont les images de client que je peux utiliser et déployer dans Azure, et comment les obtenir ?</span><span class="sxs-lookup"><span data-stu-id="b6893-151">What client images can I use and deploy in Azure, and how to I get them?</span></span>

<span data-ttu-id="b6893-152">Vous pouvez utiliser Windows 7, Windows 8 ou Windows 10 dans Azure pour des scénarios de développement / de test à condition de disposer d'un abonnement Visual Studio (anciennement MSDN) approprié.</span><span class="sxs-lookup"><span data-stu-id="b6893-152">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios provided you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> 

- <span data-ttu-id="b6893-153">Les images Windows 10 sont disponibles dans la galerie Azure sous [eligible dev/test offers](client-images.md#eligible-offers).</span><span class="sxs-lookup"><span data-stu-id="b6893-153">Windows 10 images are available from the Azure Gallery within [eligible dev/test offers](client-images.md#eligible-offers).</span></span> 
- <span data-ttu-id="b6893-154">Les abonnés Visual Studio dans n’importe quel type d’offre peuvent également [préparer et créer correctement](prepare-for-upload-vhd-image.md) une image 64 bits de Windows 7, Windows 8 ou Windows 10, puis la [charger dans Azure](upload-generalized-managed.md).</span><span class="sxs-lookup"><span data-stu-id="b6893-154">Visual Studio subscribers within any type of offer can also [adequately prepare and create](prepare-for-upload-vhd-image.md) a 64-bit Windows 7, Windows 8, or Windows 10 image and then [upload to Azure](upload-generalized-managed.md).</span></span> <span data-ttu-id="b6893-155">L’utilisation reste limitée au développement/test par les abonnés Visual Studio actifs.</span><span class="sxs-lookup"><span data-stu-id="b6893-155">The use remains limited to dev/test by active Visual Studio subscribers.</span></span>

<span data-ttu-id="b6893-156">Cet [article](client-images.md) décrit les conditions d’éligibilité pour les clients Windows en cours d’exécution dans Azure et l’utilisation des images de galerie Azure.</span><span class="sxs-lookup"><span data-stu-id="b6893-156">This [article](client-images.md) outlines the eligibility requirements for running Windows client in Azure and use of the Azure Gallery images.</span></span>

## <a name="i-am-not-able-to-see-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="b6893-157">Impossible de voir les différentes familles de taille de machines virtuelles quand je redimensionne ma machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b6893-157">I am not able to see VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="b6893-158">Lorsqu’un ordinateur virtuel est en cours d’exécution, il est déployé sur un serveur physique.</span><span class="sxs-lookup"><span data-stu-id="b6893-158">When a VM is running, it is deployed to a physical server.</span></span> <span data-ttu-id="b6893-159">Les serveurs physiques dans les régions Azure sont regroupés dans des clusters de matériel physique commun.</span><span class="sxs-lookup"><span data-stu-id="b6893-159">The physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="b6893-160">La méthode pour redimensionner une machine virtuelle qui doit être transférée vers différents clusters de matériel physique peut varier en fonction du modèle de déploiement utilisé pour déployer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b6893-160">Resizing a VM that requires the VM to be moved to different hardware clusters is different depending on which deployment model was used to deploy the VM.</span></span>

- <span data-ttu-id="b6893-161">Si les machines virtuelles sont déployées à partir d’un modèle de déploiement classique, le déploiement du service cloud doit être supprimé et redéployé afin de changer la taille de la machine virtuelle pour une autre famille de taille.</span><span class="sxs-lookup"><span data-stu-id="b6893-161">VMs deployed in Classic deployment model, the cloud service deployment must be removed and redeployed to change the VMs to a size in another size family.</span></span>

- <span data-ttu-id="b6893-162">Si les machines virtuelles sont déployées à partir du modèle de déploiement Resource Manager, vous devez arrêter toutes les machines virtuelles dans le groupe à haute disponibilité avant de changer la taille d’une machine dans le groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="b6893-162">VMs deployed in Resource Manager deployment model, you must stop all VMs in the availability set before changing the size of any VM in the availability set.</span></span>

## <a name="the-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="b6893-163">La taille de machine virtuelle répertoriée n’est pas prise en charge lors du déploiement dans le groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="b6893-163">The listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="b6893-164">Choisissez une taille prise en charge par le cluster du groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="b6893-164">Choose a size that is supported on the availability set's cluster.</span></span> <span data-ttu-id="b6893-165">Lors de la création d’un groupe à haute disponibilité, il est recommandé de choisir la plus grande taille de machine virtuelle dont vous pensez avoir besoin. Ce sera votre premier déploiement dans le groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="b6893-165">It is recommended when creating an availability set to choose the largest VM size you think you need, and have that be your first deployment to the Availability set.</span></span>

## <a name="can-i-add-an-existing-classic-vm-to-an-availability-set"></a><span data-ttu-id="b6893-166">Est-il possible d’ajouter une machine virtuelle classique à un groupe à haute disponibilité ?</span><span class="sxs-lookup"><span data-stu-id="b6893-166">Can I add an existing Classic VM to an availability set?</span></span>

<span data-ttu-id="b6893-167">Oui.</span><span class="sxs-lookup"><span data-stu-id="b6893-167">Yes.</span></span> <span data-ttu-id="b6893-168">Vous pouvez ajouter une machine virtuelle classique existante à un nouveau groupe ou à un groupe à haute disponibilité déjà existant.</span><span class="sxs-lookup"><span data-stu-id="b6893-168">You can add an existing classic VM to a new or existing Availability Set.</span></span> <span data-ttu-id="b6893-169">Pour plus d’informations, consultez [Ajouter une machine virtuelle existante à un groupe à haute disponibilité](classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="b6893-169">For more information see [Add an existing virtual machine to an availability set](classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="b6893-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b6893-170">Next steps</span></span>
<span data-ttu-id="b6893-171">Si vous avez besoin d’une aide supplémentaire à quelque étape que ce soit dans cet article, vous pouvez contacter les experts Azure sur les [forums MSDN Azure et Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="b6893-171">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="b6893-172">Vous pouvez également signaler un incident au support Azure.</span><span class="sxs-lookup"><span data-stu-id="b6893-172">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="b6893-173">Accédez au [site du support Azure](https://azure.microsoft.com/support/options/) , puis cliquez sur **Obtenir un support**.</span><span class="sxs-lookup"><span data-stu-id="b6893-173">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
