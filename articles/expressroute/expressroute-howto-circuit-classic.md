---
title: "Créer et modifier un circuit ExpressRoute avec PowerShell et le portail Azure Classic | Microsoft Docs"
description: "Cet article vous guide tout au long des étapes de création et d’approvisionnement d'un circuit ExpressRoute. Cet article vous montre également comment vérifier l'état, mettre à jour ou supprimer et annuler l’approvisionnement de votre circuit."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0134d242-6459-4dec-a2f1-4657c3bc8b23
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 3b12bbb21ebf6a0160227c4a281c420cf192d6f7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="29b0a-104">Créer et modifier un circuit ExpressRoute à l’aide de PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="29b0a-104">Create and modify an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="29b0a-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="29b0a-105">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="29b0a-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="29b0a-106">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="29b0a-107">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="29b0a-107">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="29b0a-108">Vidéo - portail Azure</span><span class="sxs-lookup"><span data-stu-id="29b0a-108">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="29b0a-109">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="29b0a-109">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="29b0a-110">Cet article vous guide dans les étapes de création d’un circuit Azure ExpressRoute à l’aide d’applets de commande PowerShell et du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="29b0a-110">This article walks you through the steps to create an Azure ExpressRoute circuit by using PowerShell cmdlets and the classic deployment model.</span></span> <span data-ttu-id="29b0a-111">Cet article vous montre également comment vérifier l'état, mettre à jour ou supprimer et annuler l’approvisionnement d'un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="29b0a-111">This article also shows you how to check the status, update, or delete and deprovision an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


<span data-ttu-id="29b0a-112">**À propos des modèles de déploiement Azure**</span><span class="sxs-lookup"><span data-stu-id="29b0a-112">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a><span data-ttu-id="29b0a-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="29b0a-113">Before you begin</span></span>
### <a name="step-1-review-the-prerequisites-and-workflow-articles"></a><span data-ttu-id="29b0a-114">Étape 1.</span><span class="sxs-lookup"><span data-stu-id="29b0a-114">Step 1.</span></span> <span data-ttu-id="29b0a-115">Passez en revue les conditions préalables et les articles sur le flux de travail</span><span class="sxs-lookup"><span data-stu-id="29b0a-115">Review the prerequisites and workflow articles</span></span>
<span data-ttu-id="29b0a-116">Veillez à consulter les [conditions préalables](expressroute-prerequisites.md) et les [flux de travail](expressroute-workflows.md) avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="29b0a-116">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>  

### <a name="step-2-install-the-latest-versions-of-the-azure-service-management-sm-powershell-modules"></a><span data-ttu-id="29b0a-117">Étape 2.</span><span class="sxs-lookup"><span data-stu-id="29b0a-117">Step 2.</span></span> <span data-ttu-id="29b0a-118">Installez les dernières versions des modules PowerShell Azure Service Management (SM)</span><span class="sxs-lookup"><span data-stu-id="29b0a-118">Install the latest versions of the Azure Service Management (SM) PowerShell modules</span></span>
<span data-ttu-id="29b0a-119">Suivez les instructions de [Prise en main des applets de commande Azure PowerShell](/powershell/azure/overview) pour obtenir les procédures pas à pas de configuration de votre ordinateur pour l’utilisation des modules Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="29b0a-119">Follow the instructions in [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) for step-by-step guidance on how to configure your computer to use the Azure PowerShell modules.</span></span>

### <a name="step-3-log-in-to-your-azure-account-and-select-a-subscription"></a><span data-ttu-id="29b0a-120">Étape 3.</span><span class="sxs-lookup"><span data-stu-id="29b0a-120">Step 3.</span></span> <span data-ttu-id="29b0a-121">Connectez-vous à votre compte Azure et sélectionnez un abonnement</span><span class="sxs-lookup"><span data-stu-id="29b0a-121">Log in to your Azure account and select a subscription</span></span>
1. <span data-ttu-id="29b0a-122">Ouvrez la console PowerShell avec des droits élevés et connectez-vous à votre compte.</span><span class="sxs-lookup"><span data-stu-id="29b0a-122">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="29b0a-123">Utilisez l’exemple suivant pour faciliter votre connexion :</span><span class="sxs-lookup"><span data-stu-id="29b0a-123">Use the following example to help you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="29b0a-124">Vérifiez les abonnements associés au compte.</span><span class="sxs-lookup"><span data-stu-id="29b0a-124">Check the subscriptions for the account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="29b0a-125">Si vous avez plusieurs abonnements, sélectionnez celui que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="29b0a-125">If you have more than one subscription, select the subscription that you want to use.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="29b0a-126">Utilisez l’applet de commande suivante pour ajouter votre abonnement Azure à PowerShell pour le modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="29b0a-126">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span></span>

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="29b0a-127">Création et approvisionnement d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="29b0a-127">Create and provision an ExpressRoute circuit</span></span>
### <a name="step-1-import-the-powershell-modules-for-expressroute"></a><span data-ttu-id="29b0a-128">Étape 1.</span><span class="sxs-lookup"><span data-stu-id="29b0a-128">Step 1.</span></span> <span data-ttu-id="29b0a-129">Importer les modules PowerShell pour ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="29b0a-129">Import the PowerShell modules for ExpressRoute</span></span>
 <span data-ttu-id="29b0a-130">Si vous ne l’avez pas encore fait, vous devez importer les modules Azure et ExpressRoute dans la session PowerShell pour utiliser les applets de commande ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="29b0a-130">If you have not already done so, you must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="29b0a-131">Vous importez les modules à partir de l’emplacement où ils ont été installés sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="29b0a-131">You import the modules from the location that they were installed to on your local computer.</span></span> <span data-ttu-id="29b0a-132">Selon la méthode utilisée pour installer les modules, l’emplacement peut être différent de l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="29b0a-132">Depending on the method you used to install the modules, the location may be different than the following example shows.</span></span> <span data-ttu-id="29b0a-133">Modifiez l’exemple, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="29b0a-133">Modify the example if necessary.</span></span>  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-the-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="29b0a-134">Étape 2.</span><span class="sxs-lookup"><span data-stu-id="29b0a-134">Step 2.</span></span> <span data-ttu-id="29b0a-135">Récupérer la liste des fournisseurs, des emplacements et des bandes passantes pris en charge</span><span class="sxs-lookup"><span data-stu-id="29b0a-135">Get the list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="29b0a-136">Avant de créer un circuit ExpressRoute, vous avez besoin d’une liste des fournisseurs de services, des emplacements et des options de bande passante pris en charge.</span><span class="sxs-lookup"><span data-stu-id="29b0a-136">Before you create an ExpressRoute circuit, you need the list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="29b0a-137">L’applet de commande PowerShell `Get-AzureDedicatedCircuitServiceProvider` retourne ces informations que vous utilisez dans les étapes ultérieures :</span><span class="sxs-lookup"><span data-stu-id="29b0a-137">The PowerShell cmdlet `Get-AzureDedicatedCircuitServiceProvider` returns this information, which you’ll use in later steps:</span></span>

    Get-AzureDedicatedCircuitServiceProvider

<span data-ttu-id="29b0a-138">Vérifiez si votre fournisseur de connectivité y est référencé.</span><span class="sxs-lookup"><span data-stu-id="29b0a-138">Check to see if your connectivity provider is listed there.</span></span> <span data-ttu-id="29b0a-139">Prenez note des éléments suivants, car vous en avez besoin plus tard lors de la création d’un circuit :</span><span class="sxs-lookup"><span data-stu-id="29b0a-139">Make a note of the following information because you'll need it later when you create a circuit:</span></span>

* <span data-ttu-id="29b0a-140">Nom</span><span class="sxs-lookup"><span data-stu-id="29b0a-140">Name</span></span>
* <span data-ttu-id="29b0a-141">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="29b0a-141">PeeringLocations</span></span>
* <span data-ttu-id="29b0a-142">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="29b0a-142">BandwidthsOffered</span></span>

<span data-ttu-id="29b0a-143">Vous êtes maintenant prêt à créer un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="29b0a-143">You're now ready to create an ExpressRoute circuit.</span></span>         

### <a name="step-3-create-an-expressroute-circuit"></a><span data-ttu-id="29b0a-144">Étape 3.</span><span class="sxs-lookup"><span data-stu-id="29b0a-144">Step 3.</span></span> <span data-ttu-id="29b0a-145">Création d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="29b0a-145">Create an ExpressRoute circuit</span></span>
<span data-ttu-id="29b0a-146">L’exemple suivant montre comment créer un circuit ExpressRoute de 200 Mb/s par le biais d’Equinix dans la Silicon Valley.</span><span class="sxs-lookup"><span data-stu-id="29b0a-146">The following example shows how to create a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="29b0a-147">Si vous utilisez un autre fournisseur et des paramètres différents, utilisez ces informations quand vous créez votre requête.</span><span class="sxs-lookup"><span data-stu-id="29b0a-147">If you're using a different provider and different settings, substitute that information when you make your request.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="29b0a-148">Votre circuit ExpressRoute sera facturé à partir de l’émission d'une clé de service.</span><span class="sxs-lookup"><span data-stu-id="29b0a-148">Your ExpressRoute circuit will be billed from the moment a service key is issued.</span></span> <span data-ttu-id="29b0a-149">Effectuez cette opération seulement quand le fournisseur de connectivité prêt à approvisionner le circuit.</span><span class="sxs-lookup"><span data-stu-id="29b0a-149">Ensure that you perform this operation when the connectivity provider is ready to provision the circuit.</span></span>
> 
> 

<span data-ttu-id="29b0a-150">Voici un exemple de demande pour une nouvelle clé de service :</span><span class="sxs-lookup"><span data-stu-id="29b0a-150">The following is an example request for a new service key:</span></span>

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

<span data-ttu-id="29b0a-151">Si vous voulez créer un circuit ExpressRoute avec le module complémentaire Premium, utilisez l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="29b0a-151">Or, if you want to create an ExpressRoute circuit with the premium add-on, use the following example.</span></span> <span data-ttu-id="29b0a-152">Pour plus d’informations sur le module complémentaire Premium, consultez le [FAQ ExpressRoute](expressroute-faqs.md) .</span><span class="sxs-lookup"><span data-stu-id="29b0a-152">Refer to the [ExpressRoute FAQ](expressroute-faqs.md) for more details about the premium add-on.</span></span>

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


<span data-ttu-id="29b0a-153">La réponse contiendra la clé de service.</span><span class="sxs-lookup"><span data-stu-id="29b0a-153">The response will contain the service key.</span></span> <span data-ttu-id="29b0a-154">Vous pouvez obtenir une description détaillée de tous les paramètres en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="29b0a-154">You can get detailed descriptions of all the parameters by running the following:</span></span>

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-the-expressroute-circuits"></a><span data-ttu-id="29b0a-155">Étape 4.</span><span class="sxs-lookup"><span data-stu-id="29b0a-155">Step 4.</span></span> <span data-ttu-id="29b0a-156">Répertorier tous les circuits ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="29b0a-156">List all the ExpressRoute circuits</span></span>
<span data-ttu-id="29b0a-157">Vous pouvez exécuter la commande `Get-AzureDedicatedCircuit` pour obtenir la liste de tous les circuits ExpressRoute que vous avez créés :</span><span class="sxs-lookup"><span data-stu-id="29b0a-157">You can run the `Get-AzureDedicatedCircuit` command to get a list of all the ExpressRoute circuits that you created:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="29b0a-158">La réponse sera similaire à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="29b0a-158">The response will be something similar to the following example:</span></span>

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="29b0a-159">Vous pouvez récupérer ces informations à tout moment à l’aide de l’applet de commande `Get-AzureDedicatedCircuit` .</span><span class="sxs-lookup"><span data-stu-id="29b0a-159">You can retrieve this information at any time by using the `Get-AzureDedicatedCircuit` cmdlet.</span></span> <span data-ttu-id="29b0a-160">Un appel effectué sans aucun paramètre répertorie tous les circuits.</span><span class="sxs-lookup"><span data-stu-id="29b0a-160">Making the call without any parameters lists all the circuits.</span></span> <span data-ttu-id="29b0a-161">Votre clé de service apparaît dans le champ *ServiceKey* .</span><span class="sxs-lookup"><span data-stu-id="29b0a-161">Your service key will be listed in the *ServiceKey* field.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="29b0a-162">Vous pouvez obtenir une description détaillée de tous les paramètres en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="29b0a-162">You can get detailed descriptions of all the parameters by running the following:</span></span>

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="29b0a-163">Étape 5.</span><span class="sxs-lookup"><span data-stu-id="29b0a-163">Step 5.</span></span> <span data-ttu-id="29b0a-164">Envoyer la clé de service à votre fournisseur de connectivité pour l’approvisionnement</span><span class="sxs-lookup"><span data-stu-id="29b0a-164">Send the service key to your connectivity provider for provisioning</span></span>
<span data-ttu-id="29b0a-165">*ServiceProviderProvisioningState* fournit des informations sur l’état actuel de l’approvisionnement du côté du fournisseur de service.</span><span class="sxs-lookup"><span data-stu-id="29b0a-165">*ServiceProviderProvisioningState* provides information on the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="29b0a-166">*statut* indique l’état du côté Microsoft.</span><span class="sxs-lookup"><span data-stu-id="29b0a-166">*Status* provides the state on the Microsoft side.</span></span> <span data-ttu-id="29b0a-167">Pour plus d’informations sur les états d’approvisionnement des circuits, consultez l’article [Flux de travail](expressroute-workflows.md#expressroute-circuit-provisioning-states) .</span><span class="sxs-lookup"><span data-stu-id="29b0a-167">For more information about circuit provisioning states, see the [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="29b0a-168">Quand vous créez un circuit ExpressRoute, ce circuit affiche l’état suivant :</span><span class="sxs-lookup"><span data-stu-id="29b0a-168">When you create a new ExpressRoute circuit, the circuit will be in the following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="29b0a-169">Le circuit passe à l’état suivant quand le fournisseur de connectivité est sur le point de l’activer pour vous :</span><span class="sxs-lookup"><span data-stu-id="29b0a-169">The circuit will go to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="29b0a-170">Un circuit ExpressRoute doit être dans l’état suivant pour pouvoir être utilisé.</span><span class="sxs-lookup"><span data-stu-id="29b0a-170">An ExpressRoute circuit must be in the following state for you to be able to use it:</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="29b0a-171">Étape 6.</span><span class="sxs-lookup"><span data-stu-id="29b0a-171">Step 6.</span></span> <span data-ttu-id="29b0a-172">Vérifier régulièrement le statut et l’état de la clé du circuit</span><span class="sxs-lookup"><span data-stu-id="29b0a-172">Periodically check the status and the state of the circuit key</span></span>
<span data-ttu-id="29b0a-173">Cela vous permet de savoir quand votre fournisseur a activé votre circuit.</span><span class="sxs-lookup"><span data-stu-id="29b0a-173">This lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="29b0a-174">Une fois le circuit configuré, *ServiceProviderProvisioningState* apparaît *Approvisionné*, comme le montre l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="29b0a-174">After the circuit has been configured, *ServiceProviderProvisioningState* will display as *Provisioned* as shown in the following example:</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a><span data-ttu-id="29b0a-175">Étape 7.</span><span class="sxs-lookup"><span data-stu-id="29b0a-175">Step 7.</span></span> <span data-ttu-id="29b0a-176">Créer votre configuration de routage</span><span class="sxs-lookup"><span data-stu-id="29b0a-176">Create your routing configuration</span></span>
<span data-ttu-id="29b0a-177">Pour obtenir des instructions pas à pas, consultez l’article [Configuration du routage des circuits ExpressRoute (créer et modifier des homologations de circuit)](expressroute-howto-routing-classic.md) .</span><span class="sxs-lookup"><span data-stu-id="29b0a-177">Refer to the [ExpressRoute circuit routing configuration (create and modify circuit peerings)](expressroute-howto-routing-classic.md) article for step-by-step instructions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="29b0a-178">Ces instructions s’appliquent seulement aux circuits créés avec des fournisseurs de services proposant des services de connectivité de couche 2.</span><span class="sxs-lookup"><span data-stu-id="29b0a-178">These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="29b0a-179">Si vous utilisez un fournisseur de services proposant des services gérés de couche 3 (généralement un VPN IP, comme MPLS), votre fournisseur de connectivité configure et gère le routage pour vous.</span><span class="sxs-lookup"><span data-stu-id="29b0a-179">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="step-8-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="29b0a-180">Étape 8 :</span><span class="sxs-lookup"><span data-stu-id="29b0a-180">Step 8.</span></span> <span data-ttu-id="29b0a-181">Lier un réseau virtuel à un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="29b0a-181">Link a virtual network to an ExpressRoute circuit</span></span>
<span data-ttu-id="29b0a-182">Maintenant, vous devez lier un réseau virtuel à votre circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="29b0a-182">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="29b0a-183">Pour obtenir des instructions pas à pas, voir [Liaison de circuits ExpressRoute à des réseaux virtuels](expressroute-howto-linkvnet-classic.md) .</span><span class="sxs-lookup"><span data-stu-id="29b0a-183">Refer to [Linking ExpressRoute circuits to virtual networks](expressroute-howto-linkvnet-classic.md) for step-by-step instructions.</span></span> <span data-ttu-id="29b0a-184">Si vous avez besoin de créer un réseau virtuel à l’aide du modèle de déploiement classique pour ExpressRoute, consultez [Créer un réseau virtuel pour ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="29b0a-184">If you need to create a virtual network using the classic deployment model for ExpressRoute, see [Create a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

## <a name="getting-the-status-of-an-expressroute-circuit"></a><span data-ttu-id="29b0a-185">Récupération de l’état d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="29b0a-185">Getting the status of an ExpressRoute circuit</span></span>
<span data-ttu-id="29b0a-186">Vous pouvez récupérer ces informations à tout moment à l’aide de l’applet de commande `Get-AzureCircuit` .</span><span class="sxs-lookup"><span data-stu-id="29b0a-186">You can retrieve this information at any time by using the `Get-AzureCircuit` cmdlet.</span></span> <span data-ttu-id="29b0a-187">Un appel effectué sans aucun paramètre répertorie tous les circuits.</span><span class="sxs-lookup"><span data-stu-id="29b0a-187">Making the call without any parameters lists all the circuits.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

    Bandwidth                        : 1000
    CircuitName                      : MyAsiaCircuit
    Location                         : Singapore
    ServiceKey                       : #################################
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="29b0a-188">Vous pouvez obtenir des informations sur un circuit ExpressRoute spécifique en passant, en tant que paramètre, la clé de service à l’appel.</span><span class="sxs-lookup"><span data-stu-id="29b0a-188">You can get information on a specific ExpressRoute circuit by passing the service key as a parameter to the call.</span></span>

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


<span data-ttu-id="29b0a-189">Vous pouvez obtenir une description détaillée de tous les paramètres en exécutant l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="29b0a-189">You can get detailed descriptions of all the parameters by running the following example:</span></span>

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="29b0a-190">Modification d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="29b0a-190">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="29b0a-191">Vous pouvez modifier certaines propriétés d'un circuit ExpressRoute sans affecter la connectivité.</span><span class="sxs-lookup"><span data-stu-id="29b0a-191">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="29b0a-192">Vous pouvez effectuer les opérations suivantes sans entraîner d’interruption de service :</span><span class="sxs-lookup"><span data-stu-id="29b0a-192">You can do the following with no downtime:</span></span>

* <span data-ttu-id="29b0a-193">Activer ou désactiver le module complémentaire ExpressRoute Premium pour votre circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="29b0a-193">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="29b0a-194">Augmenter la bande passante de votre circuit ExpressRoute à condition que la capacité disponible sur le port le permette.</span><span class="sxs-lookup"><span data-stu-id="29b0a-194">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="29b0a-195">Notez que la rétrogradation de la bande passante d'un circuit n'est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="29b0a-195">Note that downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="29b0a-196">Modifiez le plan de mesure de Données limitées à Données illimitées.</span><span class="sxs-lookup"><span data-stu-id="29b0a-196">Change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="29b0a-197">Notez que la modification du plan de limitation de Données illimitées à Données limitées n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="29b0a-197">Note that changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="29b0a-198">Vous pouvez activer et désactiver *Autoriser les opérations classiques*.</span><span class="sxs-lookup"><span data-stu-id="29b0a-198">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="29b0a-199">Pour plus d’informations sur les limites et les limitations, reportez-vous au [FAQ ExpressRoute](expressroute-faqs.md) .</span><span class="sxs-lookup"><span data-stu-id="29b0a-199">Refer to the [ExpressRoute FAQ](expressroute-faqs.md) for more information on limits and limitations.</span></span>

### <a name="to-enable-the-expressroute-premium-add-on"></a><span data-ttu-id="29b0a-200">Pour activer le module complémentaire ExpressRoute Premium</span><span class="sxs-lookup"><span data-stu-id="29b0a-200">To enable the ExpressRoute premium add-on</span></span>
<span data-ttu-id="29b0a-201">Vous pouvez activer le module complémentaire ExpressRoute Premium pour votre circuit existant à l’aide de l’applet de commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="29b0a-201">You can enable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

<span data-ttu-id="29b0a-202">Les fonctionnalités du module complémentaire ExpressRoute premium seront activées sur votre circuit.</span><span class="sxs-lookup"><span data-stu-id="29b0a-202">Your circuit will now have the ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="29b0a-203">Notez que nous commencerons à vous facturer la fonctionnalité du module complémentaire premium dès que la commande aura été exécutée avec succès.</span><span class="sxs-lookup"><span data-stu-id="29b0a-203">Note that we will start billing you for the premium add-on capability as soon as the command has successfully run.</span></span>

### <a name="to-disable-the-expressroute-premium-add-on"></a><span data-ttu-id="29b0a-204">Pour désactiver le module complémentaire ExpressRoute Premium</span><span class="sxs-lookup"><span data-stu-id="29b0a-204">To disable the ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="29b0a-205">Cette opération peut échouer si vous utilisez des ressources supérieures à ce qui est autorisé pour le circuit standard.</span><span class="sxs-lookup"><span data-stu-id="29b0a-205">This operation can fail if you're using resources that are greater than what is permitted for the standard circuit.</span></span>
> 
> 

#### <a name="considerations"></a><span data-ttu-id="29b0a-206">Considérations</span><span class="sxs-lookup"><span data-stu-id="29b0a-206">Considerations</span></span>

* <span data-ttu-id="29b0a-207">Vous devez vous assurer que le nombre de réseaux virtuels liés au circuit est inférieur à 10 avant de rétrograder du niveau premium à standard.</span><span class="sxs-lookup"><span data-stu-id="29b0a-207">You must ensure that the number of virtual networks linked to the circuit is less than 10 before you downgrade from premium to standard.</span></span> <span data-ttu-id="29b0a-208">Si vous ne le faites pas, votre demande de mise à jour échoue et nous appliquons les tarifs Premium.</span><span class="sxs-lookup"><span data-stu-id="29b0a-208">If you don't do this, your update request will fail, and you'll be billed the premium rates.</span></span>
* <span data-ttu-id="29b0a-209">Vous devez dissocier tous les réseaux virtuels dans d'autres régions géopolitiques.</span><span class="sxs-lookup"><span data-stu-id="29b0a-209">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="29b0a-210">Si vous ne le faites pas, votre demande de mise à jour échoue et nous appliquons les tarifs Premium.</span><span class="sxs-lookup"><span data-stu-id="29b0a-210">If you don't do this, your update request will fail, and you'll be billed the premium rates.</span></span>
* <span data-ttu-id="29b0a-211">Pour l’homologation privée, votre table de routage doit comporter moins de 4 000 routages.</span><span class="sxs-lookup"><span data-stu-id="29b0a-211">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="29b0a-212">Si la table de routage comporte plus de 4 000 routages, la session BGP s’arrête et n’est pas réactivée tant que le nombre de préfixes publiés n’est pas inférieur à 4 000.</span><span class="sxs-lookup"><span data-stu-id="29b0a-212">If your route table size is greater than 4,000 routes, the BGP session will drop and won't be reenabled until the number of advertised prefixes goes below 4,000.</span></span>

#### <a name="disable-the-premium-add-on"></a><span data-ttu-id="29b0a-213">Désactiver le module complémentaire Premium</span><span class="sxs-lookup"><span data-stu-id="29b0a-213">Disable the premium add-on</span></span>
<span data-ttu-id="29b0a-214">Vous pouvez désactiver le module complémentaire ExpressRoute Premium pour votre circuit existant à l’aide de l’applet de commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="29b0a-214">You can disable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="to-update-the-expressroute-circuit-bandwidth"></a><span data-ttu-id="29b0a-215">Pour mettre à jour la bande passante d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="29b0a-215">To update the ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="29b0a-216">Pour connaître les options de bande passante prises en charge par votre fournisseur, consultez le [FAQ ExpressRoute](expressroute-faqs.md) .</span><span class="sxs-lookup"><span data-stu-id="29b0a-216">Check the [ExpressRoute FAQ](expressroute-faqs.md) for supported bandwidth options for your provider.</span></span> <span data-ttu-id="29b0a-217">Vous pouvez choisir toute taille supérieure à celle de votre circuit existant, pour autant que le port physique (sur lequel votre circuit est créé) le permette.</span><span class="sxs-lookup"><span data-stu-id="29b0a-217">You can pick any size that is greater than the size of your existing circuit as long as the physical port (on which your circuit is created) allows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="29b0a-218">Vous devrez peut-être recréer le circuit ExpressRoute si la capacité sur le port existant est inappropriée.</span><span class="sxs-lookup"><span data-stu-id="29b0a-218">You may have to recreate the ExpressRoute circuit if there is inadequate capacity on the existing port.</span></span> <span data-ttu-id="29b0a-219">Vous ne pouvez pas mettre le circuit à niveau si aucune capacité supplémentaire n’est disponible à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="29b0a-219">You cannot upgrade the circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="29b0a-220">Vous ne pouvez pas réduire la bande passante d’un circuit ExpressRoute sans interrompre le service.</span><span class="sxs-lookup"><span data-stu-id="29b0a-220">You cannot reduce the bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="29b0a-221">Le fait de passer à un niveau inférieur de bande passante vous oblige à annuler l’approvisionnement du circuit ExpressRoute, puis à réapprovisionner un nouveau circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="29b0a-221">Downgrading bandwidth requires you to deprovision the ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> 

#### <a name="resize-a-circuit"></a><span data-ttu-id="29b0a-222">Redimensionner un circuit</span><span class="sxs-lookup"><span data-stu-id="29b0a-222">Resize a circuit</span></span>

<span data-ttu-id="29b0a-223">Une fois que vous avez décidé de la taille dont vous avez besoin, vous pouvez utiliser la commande suivante pour redimensionner votre circuit :</span><span class="sxs-lookup"><span data-stu-id="29b0a-223">After you decide what size you need, you can use the following command to resize your circuit:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="29b0a-224">Votre circuit sera redimensionné du côté de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="29b0a-224">Your circuit will have been sized up on the Microsoft side.</span></span> <span data-ttu-id="29b0a-225">Vous devez contacter votre fournisseur de connectivité pour mettre à jour les configurations de son côté afin de refléter cette modification.</span><span class="sxs-lookup"><span data-stu-id="29b0a-225">You must contact your connectivity provider to update configurations on their side to match this change.</span></span> <span data-ttu-id="29b0a-226">Notez que nous allons commencer à vous facturer la bande bande passante mise à jour à partir de cet instant.</span><span class="sxs-lookup"><span data-stu-id="29b0a-226">Note that we will start billing you for the updated bandwidth option from this point on.</span></span>

<span data-ttu-id="29b0a-227">Si l’erreur suivante s’affiche lors de l’augmentation de la bande passante du circuit, cela signifie qu’il ne reste pas suffisamment de bande passante sur le port physique sur lequel votre circuit est créé.</span><span class="sxs-lookup"><span data-stu-id="29b0a-227">If you see the following error when increasing the circuit bandwidth, it means there is no sufficient bandwidth left on the physical port where your existing circuit is created.</span></span> <span data-ttu-id="29b0a-228">Vous devez supprimer ce circuit et en créer un nouveau de la taille nécessaire.</span><span class="sxs-lookup"><span data-stu-id="29b0a-228">You have to delete this circuit and create a new circuit of the size you need.</span></span> 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available to perform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="29b0a-229">Annulation de l’approvisionnement et suppression d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="29b0a-229">Deprovisioning and deleting an ExpressRoute circuit</span></span>

### <a name="considerations"></a><span data-ttu-id="29b0a-230">Considérations</span><span class="sxs-lookup"><span data-stu-id="29b0a-230">Considerations</span></span>

* <span data-ttu-id="29b0a-231">Vous devez annuler la liaison de tous les réseaux virtuels du circuit ExpressRoute pour que cette opération réussisse.</span><span class="sxs-lookup"><span data-stu-id="29b0a-231">You must unlink all virtual networks from the ExpressRoute circuit for this operation to succeed.</span></span> <span data-ttu-id="29b0a-232">Si cette opération échoue, vérifiez si des réseaux virtuels sont liés au circuit.</span><span class="sxs-lookup"><span data-stu-id="29b0a-232">Check to see if you have any virtual networks that are linked to the circuit if this operation fails.</span></span>
* <span data-ttu-id="29b0a-233">Si l’état d’approvisionnement du fournisseur de services du circuit ExpressRoute est **En cours d’approvisionnement** ou **Approvisionné**, vous devez vous mettre en relation avec votre fournisseur de services pour annuler l’approvisionnement du circuit de son côté.</span><span class="sxs-lookup"><span data-stu-id="29b0a-233">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="29b0a-234">Nous continuerons à réserver des ressources et à vous facturer jusqu’à ce que le fournisseur de services termine le désapprovisionnement du circuit et nous en avertisse.</span><span class="sxs-lookup"><span data-stu-id="29b0a-234">We will continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="29b0a-235">Si le fournisseur de services a annulé l’approvisionnement du circuit (l’état d’approvisionnement du fournisseur de services affiche la valeur **Non approvisionné**), vous pouvez supprimer le circuit.</span><span class="sxs-lookup"><span data-stu-id="29b0a-235">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**) you can then delete the circuit.</span></span> <span data-ttu-id="29b0a-236">Cette opération arrêtera la facturation du circuit.</span><span class="sxs-lookup"><span data-stu-id="29b0a-236">This will stop billing for the circuit.</span></span>

#### <a name="delete-a-circuit"></a><span data-ttu-id="29b0a-237">Supprimer un circuit</span><span class="sxs-lookup"><span data-stu-id="29b0a-237">Delete a circuit</span></span>

<span data-ttu-id="29b0a-238">Vous pouvez supprimer votre circuit ExpressRoute en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="29b0a-238">You can delete your ExpressRoute circuit by running the following command:</span></span>

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a><span data-ttu-id="29b0a-239">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="29b0a-239">Next steps</span></span>
<span data-ttu-id="29b0a-240">Après avoir créé votre circuit, effectuez les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="29b0a-240">After you create your circuit, make sure that you do the following:</span></span>

* [<span data-ttu-id="29b0a-241">Créer et modifier le routage le routage pour votre circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="29b0a-241">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-classic.md)
* [<span data-ttu-id="29b0a-242">Lier votre réseau virtuel à votre circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="29b0a-242">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

