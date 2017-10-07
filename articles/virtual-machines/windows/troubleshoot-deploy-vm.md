---
title: "aaaTroubleshoot déploiement des problèmes d’ordinateur virtuel Windows dans Azure | Documents Microsoft"
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
ms.openlocfilehash: 30de25827c050cc266761cfc14548bcc64237dac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-windows-virtual-machine-issues-in-azure"></a><span data-ttu-id="27bd1-103">Résolution des problèmes de déploiement de la machine virtuelle Windows dans Azure</span><span class="sxs-lookup"><span data-stu-id="27bd1-103">Troubleshoot deploying Windows virtual machine issues in Azure</span></span>

<span data-ttu-id="27bd1-104">problèmes de déploiement d’ordinateur virtuel (VM) tootroubleshoot dans Azure, passez en revue les hello [problèmes principaux](#top-issues) des défaillances et des solutions courantes.</span><span class="sxs-lookup"><span data-stu-id="27bd1-104">tootroubleshoot virtual machine (VM) deployment issues in Azure, review hello [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="27bd1-105">Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez contacter hello experts Azure sur [hello forums MSDN Azure et le débordement de pile](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="27bd1-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="27bd1-106">Vous pouvez également signaler un incident au support Azure.</span><span class="sxs-lookup"><span data-stu-id="27bd1-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="27bd1-107">Accédez toohello [site de support technique Azure](https://azure.microsoft.com/support/options/) et sélectionnez **obtenir prend en charge**.</span><span class="sxs-lookup"><span data-stu-id="27bd1-107">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="27bd1-108">Problèmes principaux</span><span class="sxs-lookup"><span data-stu-id="27bd1-108">Top issues</span></span>
[!INCLUDE [virtual-machines-windows-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a><span data-ttu-id="27bd1-109">cluster de Hello ne peut pas prendre en charge hello demandé la taille de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="27bd1-109">hello cluster cannot support hello requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="27bd1-110">Réessayez la demande hello à l’aide d’une plus petite taille de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="27bd1-110">Retry hello request using a smaller VM size.</span></span>
- <span data-ttu-id="27bd1-111">Si hello taille Hello demandé de que machine virtuelle ne peut pas être modifié :</span><span class="sxs-lookup"><span data-stu-id="27bd1-111">If hello size of hello requested VM cannot be changed:</span></span>
    - <span data-ttu-id="27bd1-112">Arrêtez tous les ordinateurs virtuels de hello dans hello à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="27bd1-112">Stop all hello VMs in hello availability set.</span></span> <span data-ttu-id="27bd1-113">Cliquez sur **Groupes de ressources** > votre groupe de ressources > **Ressources** > votre groupe à haute disponibilité > **Machines virtuelles** > votre machine virtuelle > **Arrêter**.</span><span class="sxs-lookup"><span data-stu-id="27bd1-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="27bd1-114">Une fois toutes les hello arrêt des machines virtuelles, créez des hello machine virtuelle de taille de hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="27bd1-114">After all hello VMs stop, create hello VM in hello desired size.</span></span>
    - <span data-ttu-id="27bd1-115">Démarrer hello nouvelle machine virtuelle tout d’abord, puis sélectionnez chacun des hello s’est arrêté de machines virtuelles, puis cliquez sur Démarrer.</span><span class="sxs-lookup"><span data-stu-id="27bd1-115">Start hello new VM first, and then select each of hello stopped VMs and click Start.</span></span>


## <a name="hello-cluster-does-not-have-free-resources"></a><span data-ttu-id="27bd1-116">cluster de Hello n’a pas de libérer des ressources</span><span class="sxs-lookup"><span data-stu-id="27bd1-116">hello cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="27bd1-117">Réessayez la demande de hello plus tard.</span><span class="sxs-lookup"><span data-stu-id="27bd1-117">Retry hello request later.</span></span>
- <span data-ttu-id="27bd1-118">Si hello nouvelle machine virtuelle peut être définie partie d’une haute disponibilité distincts</span><span class="sxs-lookup"><span data-stu-id="27bd1-118">If hello new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="27bd1-119">Créer une machine virtuelle dans un ensemble différent de disponibilité (Bonjour même région).</span><span class="sxs-lookup"><span data-stu-id="27bd1-119">Create a VM in a different availability set (in hello same region).</span></span>
    - <span data-ttu-id="27bd1-120">Ajouter hello nouvelle machine virtuelle toohello même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="27bd1-120">Add hello new VM toohello same virtual network.</span></span>

## <a name="how-can-i-use-and-deploy-a-windows-client-image-into-azure"></a><span data-ttu-id="27bd1-121">Comment utiliser et déployer des images de client Windows dans Azure ?</span><span class="sxs-lookup"><span data-stu-id="27bd1-121">How can I use and deploy a windows client image into Azure?</span></span>

<span data-ttu-id="27bd1-122">Vous pouvez utiliser Windows 7, Windows 8 ou Windows 10 dans Azure pour des scénarios de développement /de test à condition de disposer d'un abonnement Visual Studio (anciennement MSDN) approprié.</span><span class="sxs-lookup"><span data-stu-id="27bd1-122">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios if you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> <span data-ttu-id="27bd1-123">Cela [article](client-images.md) contours hello conditions préalables pour l’exécution de client Windows dans Azure et les utilisations de hello images de la galerie Azure.</span><span class="sxs-lookup"><span data-stu-id="27bd1-123">This [article](client-images.md) outlines hello eligibility requirements for running Windows client in Azure and uses of hello Azure Gallery images.</span></span>

## <a name="how-can-i-deploy-a-virtual-machine-using-hello-hybrid-use-benefit-hub"></a><span data-ttu-id="27bd1-124">Comment puis-je déployer un ordinateur virtuel à l’aide de hello avantage d’utiliser hybride (HUB) ?</span><span class="sxs-lookup"><span data-stu-id="27bd1-124">How can I deploy a virtual machine using hello Hybrid Use Benefit (HUB)?</span></span>

<span data-ttu-id="27bd1-125">Il existe deux façons différentes toodeploy des machines virtuelles Windows avec hello avantage d’utiliser Azure hybride.</span><span class="sxs-lookup"><span data-stu-id="27bd1-125">There are a couple of different ways toodeploy Windows virtual machines with hello Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="27bd1-126">Un abonnement avec un contrat Entreprise :</span><span class="sxs-lookup"><span data-stu-id="27bd1-126">For an Enterprise Agreement subscription:</span></span>

<span data-ttu-id="27bd1-127">•   Déployez des machines virtuelles à partir d’images de la Place de marché spécifiques qui sont préconfigurées avec Azure Hybrid Use Benefit.</span><span class="sxs-lookup"><span data-stu-id="27bd1-127">•   Deploy VMs from specific Marketplace images that are pre-configured with Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="27bd1-128">Contrat Entreprise :</span><span class="sxs-lookup"><span data-stu-id="27bd1-128">For Enterprise agreement:</span></span>

<span data-ttu-id="27bd1-129">•  Téléchargez une machine virtuelle personnalisée et effectuez le déploiement à l’aide d’un modèle Resource Manager ou d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27bd1-129">•   Upload a custom VM and deploy using a Resource Manager template or Azure PowerShell.</span></span>

<span data-ttu-id="27bd1-130">Pour plus d’informations, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="27bd1-130">For more information, see hello following resources:</span></span>

 - [<span data-ttu-id="27bd1-131">Présentation d’Azure Hybrid Use Benefit </span><span class="sxs-lookup"><span data-stu-id="27bd1-131">Azure Hybrid Use Benefit overview </span></span>](https://azure.microsoft.com/pricing/hybrid-use-benefit/)

 - [<span data-ttu-id="27bd1-132">FAQ téléchargeable</span><span class="sxs-lookup"><span data-stu-id="27bd1-132">Downloadable FAQ</span></span>](http://download.microsoft.com/download/4/2/1/4211AC94-D607-4A45-B472-4B30EDF437DE/Windows_Server_Azure_Hybrid_Use_FAQ_EN_US.pdf)

 - <span data-ttu-id="27bd1-133">[Azure Hybrid Use Benefit pour Windows Server et client Windows](hybrid-use-benefit-licensing.md).</span><span class="sxs-lookup"><span data-stu-id="27bd1-133">[Azure Hybrid Use Benefit for Windows Server and Windows Client](hybrid-use-benefit-licensing.md).</span></span>

 - [<span data-ttu-id="27bd1-134">Comment puis-je utiliser hello avantage d’utiliser hybrides dans Azure</span><span class="sxs-lookup"><span data-stu-id="27bd1-134">How can I use hello Hybrid Use Benefit in Azure</span></span>](https://blogs.msdn.microsoft.com/azureedu/2016/04/13/how-can-i-use-the-hybrid-use-benefit-in-azure)

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="27bd1-135">Comment activer mon crédit mensuel pour Visual Studio Enterprise (BizSpark) ?</span><span class="sxs-lookup"><span data-stu-id="27bd1-135">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="27bd1-136">tooactivate votre mensuel de crédit, consultez ce [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="27bd1-136">tooactivate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="how-tooadd-enterprise-devtest-toomy-enterprise-agreement-ea-tooget-access-toowindow-client-images"></a><span data-ttu-id="27bd1-137">Comment tooadd entreprise Développement/Test toomy accord entreprise (EA) tooget aux images de client tooWindow ?</span><span class="sxs-lookup"><span data-stu-id="27bd1-137">How tooadd Enterprise Dev/Test toomy Enterprise Agreement (EA) tooget access tooWindow client images?</span></span>

<span data-ttu-id="27bd1-138">les abonnements de toocreate de capacité Hello en fonction hello entreprise Développement/Test offrent est propriétaires tooAccount restreints qui ont reçu l’autorisation toodo c’est le cas par un administrateur d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="27bd1-138">hello ability toocreate subscriptions based on hello Enterprise Dev/Test offer is restricted tooAccount Owners who have been given permission toodo so by an Enterprise Administrator.</span></span> <span data-ttu-id="27bd1-139">Hello propriétaire du compte crée des abonnements via hello portail du compte Azure et doit ensuite ajouter des abonnés actifs de Visual Studio en tant que coadministrateurs.</span><span class="sxs-lookup"><span data-stu-id="27bd1-139">hello Account Owner creates subscriptions via hello Azure Account Portal, and then should add active Visual Studio subscribers as co-administrators.</span></span> <span data-ttu-id="27bd1-140">Afin qu’ils puissent gérer et utiliser les ressources hello nécessaires pour le développement et de test.</span><span class="sxs-lookup"><span data-stu-id="27bd1-140">So that they can manage and use hello resources needed for development and testing.</span></span> <span data-ttu-id="27bd1-141">Pour plus d’informations, consultez [Enterprise Dev/Test](https://azure.microsoft.com/offers/ms-azr-0148p/).</span><span class="sxs-lookup"><span data-stu-id="27bd1-141">For more information, see [Enterprise Dev/Test](https://azure.microsoft.com/offers/ms-azr-0148p/).</span></span>

## <a name="my-drivers-are-missing-for-my-windows-n-series-vm"></a><span data-ttu-id="27bd1-142">Il manque des pilotes sur ma machine virtuelle Windows Série N</span><span class="sxs-lookup"><span data-stu-id="27bd1-142">My drivers are missing for my Windows N-Series VM</span></span>

<span data-ttu-id="27bd1-143">Les pilotes pour les machines virtuelles Windows se trouvent [ici](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="27bd1-143">Drivers for Windows-based VMs are located [here](n-series-driver-setup.md).</span></span>

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="27bd1-144">Impossible de trouver une instance GPU dans ma machine virtuelle Série N</span><span class="sxs-lookup"><span data-stu-id="27bd1-144">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="27bd1-145">avantage tootake hello GPU des fonctionnalités de machines virtuelles N-series Azure exécutant Windows Server 2016 ou Windows Server 2012 R2, vous devez installer les pilotes de graphiques NVIDIA sur chaque machine virtuelle après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="27bd1-145">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="27bd1-146">Des informations de configuration du pilote sont disponibles pour [les machines virtuelles Windows](n-series-driver-setup.md) et [les machines virtuelles Linux](../linux/n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="27bd1-146">Driver setup information is available for [Windows VMs](n-series-driver-setup.md) and [Linux VMs](../linux/n-series-driver-setup.md).</span></span>

## <a name="are-client-images-supported-for-n-series"></a><span data-ttu-id="27bd1-147">Est-ce que les Séries N prennent en charge les images de client ?</span><span class="sxs-lookup"><span data-stu-id="27bd1-147">Are client images supported for N-Series?</span></span>

<span data-ttu-id="27bd1-148">À l’heure actuelle, Azure ne prend en charge que les machines virtuelles Séries N exécutant Windows Server et les systèmes d’exploitation Linux.</span><span class="sxs-lookup"><span data-stu-id="27bd1-148">Currently, Azure only supports N-Series on VMs running Windows Server and Linux operating systems.</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="27bd1-149">Les machines virtuelles Séries N sont-elles disponibles dans ma région ?</span><span class="sxs-lookup"><span data-stu-id="27bd1-149">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="27bd1-150">Vous pouvez vérifier la disponibilité de hello de hello [produits disponibles par la table region](https://azure.microsoft.com/regions/services)et la tarification [ici](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="27bd1-150">You can check hello availability from hello [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="what-client-images-can-i-use-and-deploy-in-azure-and-how-tooi-get-them"></a><span data-ttu-id="27bd1-151">Les images des clients puis-je utiliser et déployer dans Azure, et comment tooI les obtenir ?</span><span class="sxs-lookup"><span data-stu-id="27bd1-151">What client images can I use and deploy in Azure, and how tooI get them?</span></span>

<span data-ttu-id="27bd1-152">Vous pouvez utiliser Windows 7, Windows 8 ou Windows 10 dans Azure pour des scénarios de développement / de test à condition de disposer d'un abonnement Visual Studio (anciennement MSDN) approprié.</span><span class="sxs-lookup"><span data-stu-id="27bd1-152">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios provided you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> 

- <span data-ttu-id="27bd1-153">Les images de Windows 10 sont disponibles à partir de la galerie d’Azure hello dans [offre de développement/test éligible](client-images.md#eligible-offers).</span><span class="sxs-lookup"><span data-stu-id="27bd1-153">Windows 10 images are available from hello Azure Gallery within [eligible dev/test offers](client-images.md#eligible-offers).</span></span> 
- <span data-ttu-id="27bd1-154">Les abonnés Visual Studio dans n’importe quel type d’offre peuvent également [correctement préparer et créer](prepare-for-upload-vhd-image.md) une image 64 bits de Windows 7, Windows 8 ou Windows 10, puis [télécharger tooAzure](upload-generalized-managed.md).</span><span class="sxs-lookup"><span data-stu-id="27bd1-154">Visual Studio subscribers within any type of offer can also [adequately prepare and create](prepare-for-upload-vhd-image.md) a 64-bit Windows 7, Windows 8, or Windows 10 image and then [upload tooAzure](upload-generalized-managed.md).</span></span> <span data-ttu-id="27bd1-155">utilisation de Hello reste toodev/test limité par les abonnés actifs de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="27bd1-155">hello use remains limited toodev/test by active Visual Studio subscribers.</span></span>

<span data-ttu-id="27bd1-156">Cela [article](client-images.md) contours hello conditions préalables pour l’exécution de client Windows dans Azure et l’utilisation de hello images de la galerie Azure.</span><span class="sxs-lookup"><span data-stu-id="27bd1-156">This [article](client-images.md) outlines hello eligibility requirements for running Windows client in Azure and use of hello Azure Gallery images.</span></span>

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="27bd1-157">Je ne suis pas famille de taille de machine virtuelle en mesure de toosee que je veux lors du redimensionnement de ma machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="27bd1-157">I am not able toosee VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="27bd1-158">Lorsqu’un ordinateur virtuel est en cours d’exécution, il est déployé tooa des serveurs physiques.</span><span class="sxs-lookup"><span data-stu-id="27bd1-158">When a VM is running, it is deployed tooa physical server.</span></span> <span data-ttu-id="27bd1-159">Hello des serveurs physiques dans des régions Azure sont regroupés dans des clusters de matériel physique commun.</span><span class="sxs-lookup"><span data-stu-id="27bd1-159">hello physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="27bd1-160">Redimensionnement d’une machine virtuelle qui nécessite des clusters matériels de hello VM toobe déplacé toodifferent diffère selon le modèle de déploiement a été utilisé toodeploy hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="27bd1-160">Resizing a VM that requires hello VM toobe moved toodifferent hardware clusters is different depending on which deployment model was used toodeploy hello VM.</span></span>

- <span data-ttu-id="27bd1-161">Machines virtuelles déployées dans le modèle de déploiement classique, déploiement de service cloud hello doivent être supprimés et redéploiement taille de tooa toochange hello machines virtuelles dans une autre famille de taille.</span><span class="sxs-lookup"><span data-stu-id="27bd1-161">VMs deployed in Classic deployment model, hello cloud service deployment must be removed and redeployed toochange hello VMs tooa size in another size family.</span></span>

- <span data-ttu-id="27bd1-162">Machines virtuelles déployées dans le modèle de déploiement de gestionnaire de ressources, vous devez arrêter toutes les machines virtuelles hello groupe à haute disponibilité avant de modifier la taille de hello de n’importe quel ordinateur virtuel à haute disponibilité hello.</span><span class="sxs-lookup"><span data-stu-id="27bd1-162">VMs deployed in Resource Manager deployment model, you must stop all VMs in hello availability set before changing hello size of any VM in hello availability set.</span></span>

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="27bd1-163">Hello répertorié taille de machine virtuelle n'est pas pris en charge lors du déploiement de haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="27bd1-163">hello listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="27bd1-164">Choisissez une taille qui est pris en charge sur le cluster de l’ensemble de disponibilité hello.</span><span class="sxs-lookup"><span data-stu-id="27bd1-164">Choose a size that is supported on hello availability set's cluster.</span></span> <span data-ttu-id="27bd1-165">Il est recommandé lorsque vous créez qu'un ensemble de disponibilité toochoose hello plus grande taille de machine virtuelle vous pensez que vous avez besoin et que vous avez être votre première toohello de déploiement à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="27bd1-165">It is recommended when creating an availability set toochoose hello largest VM size you think you need, and have that be your first deployment toohello Availability set.</span></span>

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a><span data-ttu-id="27bd1-166">Puis-je ajouter un ensemble de disponibilité tooan classique de machine virtuelle existant ?</span><span class="sxs-lookup"><span data-stu-id="27bd1-166">Can I add an existing Classic VM tooan availability set?</span></span>

<span data-ttu-id="27bd1-167">Oui.</span><span class="sxs-lookup"><span data-stu-id="27bd1-167">Yes.</span></span> <span data-ttu-id="27bd1-168">Vous pouvez ajouter un tooa d’ordinateur virtuel classique existante nouvelle ou existante à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="27bd1-168">You can add an existing classic VM tooa new or existing Availability Set.</span></span> <span data-ttu-id="27bd1-169">Pour plus d’informations, consultez [ajouter un ensemble de disponibilité tooan machine virtuelle existante](classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="27bd1-169">For more information see [Add an existing virtual machine tooan availability set](classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="27bd1-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="27bd1-170">Next steps</span></span>
<span data-ttu-id="27bd1-171">Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez contacter hello experts Azure sur [hello forums MSDN Azure et le débordement de pile](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="27bd1-171">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="27bd1-172">Vous pouvez également signaler un incident au support Azure.</span><span class="sxs-lookup"><span data-stu-id="27bd1-172">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="27bd1-173">Accédez toohello [site de support technique Azure](https://azure.microsoft.com/support/options/) et sélectionnez **obtenir prend en charge**.</span><span class="sxs-lookup"><span data-stu-id="27bd1-173">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
