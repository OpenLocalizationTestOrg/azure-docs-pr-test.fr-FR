---
title: "Créer et modifier un circuit ExpressRoute avec PowerShell et le portail Azure Classic | Microsoft Docs"
description: "Cet article vous guide tout au long des étapes hello pour la création et configuration d’un circuit ExpressRoute. Cet article vous montre également comment toocheck état de hello, mettre à jour, ou le supprimer et annuler le déploiement de votre circuit."
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
ms.openlocfilehash: 9897c88776a2153ba22aa9ff328becb9f12b660b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a><span data-ttu-id="90ccc-104">Créer et modifier un circuit ExpressRoute à l’aide de PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="90ccc-104">Create and modify an ExpressRoute circuit using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="90ccc-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="90ccc-105">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="90ccc-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="90ccc-106">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="90ccc-107">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="90ccc-107">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="90ccc-108">Vidéo - portail Azure</span><span class="sxs-lookup"><span data-stu-id="90ccc-108">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="90ccc-109">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="90ccc-109">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="90ccc-110">Cet article vous guide hello étapes toocreate un circuit ExpressRoute d’Azure à l’aide du modèle de déploiement classique de hello et les applets de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="90ccc-110">This article walks you through hello steps toocreate an Azure ExpressRoute circuit by using PowerShell cmdlets and hello classic deployment model.</span></span> <span data-ttu-id="90ccc-111">Cet article vous montre également comment toocheck état de hello, mettre à jour, ou le supprimer et annuler le déploiement d’un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="90ccc-111">This article also shows you how toocheck hello status, update, or delete and deprovision an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


<span data-ttu-id="90ccc-112">**À propos des modèles de déploiement Azure**</span><span class="sxs-lookup"><span data-stu-id="90ccc-112">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a><span data-ttu-id="90ccc-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="90ccc-113">Before you begin</span></span>
### <a name="step-1-review-hello-prerequisites-and-workflow-articles"></a><span data-ttu-id="90ccc-114">Étape 1.</span><span class="sxs-lookup"><span data-stu-id="90ccc-114">Step 1.</span></span> <span data-ttu-id="90ccc-115">Passez en revue les conditions préalables de hello et les articles de flux de travail</span><span class="sxs-lookup"><span data-stu-id="90ccc-115">Review hello prerequisites and workflow articles</span></span>
<span data-ttu-id="90ccc-116">Assurez-vous que vous avez consulté hello [conditions préalables](expressroute-prerequisites.md) et [workflows](expressroute-workflows.md) avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="90ccc-116">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>  

### <a name="step-2-install-hello-latest-versions-of-hello-azure-service-management-sm-powershell-modules"></a><span data-ttu-id="90ccc-117">Étape 2.</span><span class="sxs-lookup"><span data-stu-id="90ccc-117">Step 2.</span></span> <span data-ttu-id="90ccc-118">Installer les versions les plus récentes des modules de gestion de Service Azure (SM) PowerShell hello hello</span><span class="sxs-lookup"><span data-stu-id="90ccc-118">Install hello latest versions of hello Azure Service Management (SM) PowerShell modules</span></span>
<span data-ttu-id="90ccc-119">Suivez les instructions de hello dans [prise en main des applets de commande Azure PowerShell](/powershell/azure/overview) pour obtenir des instructions sur la façon de tooconfigure votre ordinateur toouse hello Azure les modules PowerShell.</span><span class="sxs-lookup"><span data-stu-id="90ccc-119">Follow hello instructions in [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview) for step-by-step guidance on how tooconfigure your computer toouse hello Azure PowerShell modules.</span></span>

### <a name="step-3-log-in-tooyour-azure-account-and-select-a-subscription"></a><span data-ttu-id="90ccc-120">Étape 3.</span><span class="sxs-lookup"><span data-stu-id="90ccc-120">Step 3.</span></span> <span data-ttu-id="90ccc-121">Connectez-vous à tooyour compte Azure, puis sélectionnez un abonnement</span><span class="sxs-lookup"><span data-stu-id="90ccc-121">Log in tooyour Azure account and select a subscription</span></span>
1. <span data-ttu-id="90ccc-122">Ouvrez la console PowerShell avec des droits élevés et tooyour compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="90ccc-122">Open your PowerShell console with elevated rights and connect tooyour account.</span></span> <span data-ttu-id="90ccc-123">Utilisez hello suivant toohelp exemple que vous connectez :</span><span class="sxs-lookup"><span data-stu-id="90ccc-123">Use hello following example toohelp you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="90ccc-124">Vérifiez les abonnements hello pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="90ccc-124">Check hello subscriptions for hello account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="90ccc-125">Si vous avez plusieurs abonnements, sélectionnez l’abonnement hello que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="90ccc-125">If you have more than one subscription, select hello subscription that you want toouse.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="90ccc-126">Ensuite, utilisez hello suivant l’applet de commande tooadd tooPowerShell de votre abonnement Azure pour le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="90ccc-126">Next, use hello following cmdlet tooadd your Azure subscription tooPowerShell for hello classic deployment model.</span></span>

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="90ccc-127">Création et approvisionnement d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="90ccc-127">Create and provision an ExpressRoute circuit</span></span>
### <a name="step-1-import-hello-powershell-modules-for-expressroute"></a><span data-ttu-id="90ccc-128">Étape 1.</span><span class="sxs-lookup"><span data-stu-id="90ccc-128">Step 1.</span></span> <span data-ttu-id="90ccc-129">Importer les modules PowerShell hello pour ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="90ccc-129">Import hello PowerShell modules for ExpressRoute</span></span>
 <span data-ttu-id="90ccc-130">Si vous ne le n'avez pas déjà fait, vous devez importer les modules Azure et ExpressRoute hello dans la session de PowerShell hello dans toostart de commande à l’aide des applets de commande hello ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="90ccc-130">If you have not already done so, you must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="90ccc-131">Vous importez les modules hello hello emplacement qu’ils ont été installées tooon votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="90ccc-131">You import hello modules from hello location that they were installed tooon your local computer.</span></span> <span data-ttu-id="90ccc-132">En fonction de la méthode hello vous avez utilisé des modules de hello tooinstall, emplacement de hello peut être différent de celui hello suivant montre l’exemple.</span><span class="sxs-lookup"><span data-stu-id="90ccc-132">Depending on hello method you used tooinstall hello modules, hello location may be different than hello following example shows.</span></span> <span data-ttu-id="90ccc-133">Si nécessaire, modifier l’exemple de hello.</span><span class="sxs-lookup"><span data-stu-id="90ccc-133">Modify hello example if necessary.</span></span>  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="90ccc-134">Étape 2.</span><span class="sxs-lookup"><span data-stu-id="90ccc-134">Step 2.</span></span> <span data-ttu-id="90ccc-135">Obtenir la liste de hello de fournisseurs pris en charge, des emplacements et des bandes passantes</span><span class="sxs-lookup"><span data-stu-id="90ccc-135">Get hello list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="90ccc-136">Avant de créer un circuit ExpressRoute, vous devez liste hello de fournisseurs de connectivité pris en charge, des emplacements et des options de bande passante.</span><span class="sxs-lookup"><span data-stu-id="90ccc-136">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="90ccc-137">applet de commande PowerShell de Hello `Get-AzureDedicatedCircuitServiceProvider` retourne cette information, vous allez utiliser dans les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="90ccc-137">hello PowerShell cmdlet `Get-AzureDedicatedCircuitServiceProvider` returns this information, which you’ll use in later steps:</span></span>

    Get-AzureDedicatedCircuitServiceProvider

<span data-ttu-id="90ccc-138">Vérifiez toosee si votre fournisseur de connectivité y sont répertoriée.</span><span class="sxs-lookup"><span data-stu-id="90ccc-138">Check toosee if your connectivity provider is listed there.</span></span> <span data-ttu-id="90ccc-139">Prenez note des informations suivantes, car vous en aurez besoin ultérieurement lorsque vous créez un circuit de hello :</span><span class="sxs-lookup"><span data-stu-id="90ccc-139">Make a note of hello following information because you'll need it later when you create a circuit:</span></span>

* <span data-ttu-id="90ccc-140">Nom</span><span class="sxs-lookup"><span data-stu-id="90ccc-140">Name</span></span>
* <span data-ttu-id="90ccc-141">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="90ccc-141">PeeringLocations</span></span>
* <span data-ttu-id="90ccc-142">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="90ccc-142">BandwidthsOffered</span></span>

<span data-ttu-id="90ccc-143">Vous êtes maintenant prêt toocreate un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="90ccc-143">You're now ready toocreate an ExpressRoute circuit.</span></span>         

### <a name="step-3-create-an-expressroute-circuit"></a><span data-ttu-id="90ccc-144">Étape 3.</span><span class="sxs-lookup"><span data-stu-id="90ccc-144">Step 3.</span></span> <span data-ttu-id="90ccc-145">Création d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="90ccc-145">Create an ExpressRoute circuit</span></span>
<span data-ttu-id="90ccc-146">Bonjour à l’exemple suivant montre comment toocreate un ExpressRoute de 200 Mbits/s de circuit via Equinix dans Silicon Valley.</span><span class="sxs-lookup"><span data-stu-id="90ccc-146">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="90ccc-147">Si vous utilisez un autre fournisseur et des paramètres différents, utilisez ces informations quand vous créez votre requête.</span><span class="sxs-lookup"><span data-stu-id="90ccc-147">If you're using a different provider and different settings, substitute that information when you make your request.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="90ccc-148">Votre circuit ExpressRoute sera facturé dès hello, qu'une clé de service est émise.</span><span class="sxs-lookup"><span data-stu-id="90ccc-148">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="90ccc-149">Veillez à effectuer cette opération lorsque le fournisseur de connectivité hello est circuit de hello tooprovision prêt.</span><span class="sxs-lookup"><span data-stu-id="90ccc-149">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="90ccc-150">Hello Voici un exemple de demande pour une nouvelle clé de service :</span><span class="sxs-lookup"><span data-stu-id="90ccc-150">hello following is an example request for a new service key:</span></span>

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

<span data-ttu-id="90ccc-151">Ou, si vous voulez toocreate un circuit ExpressRoute avec un module complémentaire de hello premium, hello d’utiliser l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="90ccc-151">Or, if you want toocreate an ExpressRoute circuit with hello premium add-on, use hello following example.</span></span> <span data-ttu-id="90ccc-152">Consultez toohello [FAQ sur ExpressRoute](expressroute-faqs.md) pour plus d’informations sur le module complémentaire de hello premium.</span><span class="sxs-lookup"><span data-stu-id="90ccc-152">Refer toohello [ExpressRoute FAQ](expressroute-faqs.md) for more details about hello premium add-on.</span></span>

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


<span data-ttu-id="90ccc-153">réponse de Hello contiendra la clé du service hello.</span><span class="sxs-lookup"><span data-stu-id="90ccc-153">hello response will contain hello service key.</span></span> <span data-ttu-id="90ccc-154">Vous pouvez obtenir une description détaillée de tous les paramètres de hello en exécutant hello suivante :</span><span class="sxs-lookup"><span data-stu-id="90ccc-154">You can get detailed descriptions of all hello parameters by running hello following:</span></span>

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-hello-expressroute-circuits"></a><span data-ttu-id="90ccc-155">Étape 4.</span><span class="sxs-lookup"><span data-stu-id="90ccc-155">Step 4.</span></span> <span data-ttu-id="90ccc-156">Liste de tous les circuits ExpressRoute de hello</span><span class="sxs-lookup"><span data-stu-id="90ccc-156">List all hello ExpressRoute circuits</span></span>
<span data-ttu-id="90ccc-157">Vous pouvez exécuter hello `Get-AzureDedicatedCircuit` commande tooget une liste de tous les hello circuits ExpressRoute que vous avez créé :</span><span class="sxs-lookup"><span data-stu-id="90ccc-157">You can run hello `Get-AzureDedicatedCircuit` command tooget a list of all hello ExpressRoute circuits that you created:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="90ccc-158">réponse de Hello sera toohello quelque chose de similaire, l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="90ccc-158">hello response will be something similar toohello following example:</span></span>

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="90ccc-159">Vous pouvez récupérer ces informations à tout moment à l’aide de hello `Get-AzureDedicatedCircuit` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="90ccc-159">You can retrieve this information at any time by using hello `Get-AzureDedicatedCircuit` cmdlet.</span></span> <span data-ttu-id="90ccc-160">Exécuter hello à appel sans paramètre répertorie tous les circuits hello.</span><span class="sxs-lookup"><span data-stu-id="90ccc-160">Making hello call without any parameters lists all hello circuits.</span></span> <span data-ttu-id="90ccc-161">Votre clé de service s’afficheront dans hello *ServiceKey* champ.</span><span class="sxs-lookup"><span data-stu-id="90ccc-161">Your service key will be listed in hello *ServiceKey* field.</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="90ccc-162">Vous pouvez obtenir une description détaillée de tous les paramètres de hello en exécutant hello suivante :</span><span class="sxs-lookup"><span data-stu-id="90ccc-162">You can get detailed descriptions of all hello parameters by running hello following:</span></span>

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="90ccc-163">Étape 5.</span><span class="sxs-lookup"><span data-stu-id="90ccc-163">Step 5.</span></span> <span data-ttu-id="90ccc-164">Envoyer le fournisseur de connectivité hello service tooyour clé pour la configuration</span><span class="sxs-lookup"><span data-stu-id="90ccc-164">Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="90ccc-165">*ServiceProviderProvisioningState* fournit des informations sur l’état actuel de mise en service sur le côté du fournisseur de services hello hello.</span><span class="sxs-lookup"><span data-stu-id="90ccc-165">*ServiceProviderProvisioningState* provides information on hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="90ccc-166">*État* fournit l’état de hello sur hello côté de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="90ccc-166">*Status* provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="90ccc-167">Pour plus d’informations sur les États de configuration de circuit, consultez hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) l’article.</span><span class="sxs-lookup"><span data-stu-id="90ccc-167">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="90ccc-168">Lorsque vous créez un nouveau circuit ExpressRoute, circuit de hello sera Bonjour suivant l’état :</span><span class="sxs-lookup"><span data-stu-id="90ccc-168">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="90ccc-169">circuit de Hello passera toohello suivant l’état lorsque le fournisseur de connectivité hello est en cours de hello de l’activer pour vous :</span><span class="sxs-lookup"><span data-stu-id="90ccc-169">hello circuit will go toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="90ccc-170">Un circuit ExpressRoute doit être Bonjour suivant l’état pour vous toouse en mesure de toobe il :</span><span class="sxs-lookup"><span data-stu-id="90ccc-170">An ExpressRoute circuit must be in hello following state for you toobe able toouse it:</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="90ccc-171">Étape 6.</span><span class="sxs-lookup"><span data-stu-id="90ccc-171">Step 6.</span></span> <span data-ttu-id="90ccc-172">Vérifier régulièrement le statut de hello et état hello de clé du circuit hello</span><span class="sxs-lookup"><span data-stu-id="90ccc-172">Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="90ccc-173">Cela vous permet de savoir quand votre fournisseur a activé votre circuit.</span><span class="sxs-lookup"><span data-stu-id="90ccc-173">This lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="90ccc-174">Après la configuration de circuit de hello, *ServiceProviderProvisioningState* affichera en tant que *configuré* comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="90ccc-174">After hello circuit has been configured, *ServiceProviderProvisioningState* will display as *Provisioned* as shown in hello following example:</span></span>

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a><span data-ttu-id="90ccc-175">Étape 7.</span><span class="sxs-lookup"><span data-stu-id="90ccc-175">Step 7.</span></span> <span data-ttu-id="90ccc-176">Créer votre configuration de routage</span><span class="sxs-lookup"><span data-stu-id="90ccc-176">Create your routing configuration</span></span>
<span data-ttu-id="90ccc-177">Consultez toohello [circuit ExpressRoute de configuration de routage (créer et modifier des homologations de circuit)](expressroute-howto-routing-classic.md) article pour obtenir des instructions pas à pas.</span><span class="sxs-lookup"><span data-stu-id="90ccc-177">Refer toohello [ExpressRoute circuit routing configuration (create and modify circuit peerings)](expressroute-howto-routing-classic.md) article for step-by-step instructions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="90ccc-178">Ces instructions s’appliquent uniquement à toocircuits qui sont créés avec des fournisseurs de services qui offrent des services de couche 2 de connectivité.</span><span class="sxs-lookup"><span data-stu-id="90ccc-178">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="90ccc-179">Si vous utilisez un fournisseur de services proposant des services gérés de couche 3 (généralement un VPN IP, comme MPLS), votre fournisseur de connectivité configure et gère le routage pour vous.</span><span class="sxs-lookup"><span data-stu-id="90ccc-179">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="step-8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="90ccc-180">Étape 8 :</span><span class="sxs-lookup"><span data-stu-id="90ccc-180">Step 8.</span></span> <span data-ttu-id="90ccc-181">Lier un circuit ExpressRoute de tooan réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="90ccc-181">Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="90ccc-182">Ensuite, lier un circuit ExpressRoute de tooyour réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="90ccc-182">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="90ccc-183">Consultez trop[toovirtual réseaux des circuits ExpressRoute de liaison](expressroute-howto-linkvnet-classic.md) pour obtenir des instructions pas à pas.</span><span class="sxs-lookup"><span data-stu-id="90ccc-183">Refer too[Linking ExpressRoute circuits toovirtual networks](expressroute-howto-linkvnet-classic.md) for step-by-step instructions.</span></span> <span data-ttu-id="90ccc-184">Si vous avez besoin toocreate un réseau virtuel à l’aide du modèle de déploiement classique hello pour ExpressRoute, consultez [créer un réseau virtuel pour ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span><span class="sxs-lookup"><span data-stu-id="90ccc-184">If you need toocreate a virtual network using hello classic deployment model for ExpressRoute, see [Create a virtual network for ExpressRoute](expressroute-howto-vnet-portal-classic.md).</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="90ccc-185">État de hello lors de l’obtention d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="90ccc-185">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="90ccc-186">Vous pouvez récupérer ces informations à tout moment à l’aide de hello `Get-AzureCircuit` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="90ccc-186">You can retrieve this information at any time by using hello `Get-AzureCircuit` cmdlet.</span></span> <span data-ttu-id="90ccc-187">Exécuter hello à appel sans paramètre répertorie tous les circuits hello.</span><span class="sxs-lookup"><span data-stu-id="90ccc-187">Making hello call without any parameters lists all hello circuits.</span></span>

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

<span data-ttu-id="90ccc-188">Vous pouvez obtenir des informations sur un circuit ExpressRoute spécifique en passant la clé de service hello comme un appel de toohello de paramètre.</span><span class="sxs-lookup"><span data-stu-id="90ccc-188">You can get information on a specific ExpressRoute circuit by passing hello service key as a parameter toohello call.</span></span>

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


<span data-ttu-id="90ccc-189">Vous pouvez obtenir une description détaillée de tous les paramètres de hello en exécutant hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="90ccc-189">You can get detailed descriptions of all hello parameters by running hello following example:</span></span>

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="90ccc-190">Modification d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="90ccc-190">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="90ccc-191">Vous pouvez modifier certaines propriétés d'un circuit ExpressRoute sans affecter la connectivité.</span><span class="sxs-lookup"><span data-stu-id="90ccc-191">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="90ccc-192">Vous pouvez effectuer hello suivant sans interruption de service :</span><span class="sxs-lookup"><span data-stu-id="90ccc-192">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="90ccc-193">Activer ou désactiver le module complémentaire ExpressRoute Premium pour votre circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="90ccc-193">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="90ccc-194">La bande passante de hello augmentation de votre circuit ExpressRoute fourni la capacité est disponible sur le port hello.</span><span class="sxs-lookup"><span data-stu-id="90ccc-194">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="90ccc-195">Notez que la bande passante hello d’un circuit de rétrogradation n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="90ccc-195">Note that downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="90ccc-196">Modifier hello plan à partir de données de limitées tooUnlimited données de contrôle.</span><span class="sxs-lookup"><span data-stu-id="90ccc-196">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="90ccc-197">Notez ce plan de contrôle hello modification à partir de tooMetered données illimité que données ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="90ccc-197">Note that changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="90ccc-198">Vous pouvez activer et désactiver *Autoriser les opérations classiques*.</span><span class="sxs-lookup"><span data-stu-id="90ccc-198">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="90ccc-199">Consultez toohello [FAQ sur ExpressRoute](expressroute-faqs.md) pour plus d’informations sur les limites et limitations.</span><span class="sxs-lookup"><span data-stu-id="90ccc-199">Refer toohello [ExpressRoute FAQ](expressroute-faqs.md) for more information on limits and limitations.</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="90ccc-200">module complémentaire de tooenable hello ExpressRoute premium</span><span class="sxs-lookup"><span data-stu-id="90ccc-200">tooenable hello ExpressRoute premium add-on</span></span>
<span data-ttu-id="90ccc-201">Vous pouvez activer un module complémentaire de hello ExpressRoute premium pour votre circuit existant à l’aide de hello suivant l’applet de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="90ccc-201">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

<span data-ttu-id="90ccc-202">Votre circuit est désormais hello ExpressRoute premium module complémentaire fonctionnalités sont activées.</span><span class="sxs-lookup"><span data-stu-id="90ccc-202">Your circuit will now have hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="90ccc-203">Notez que nous allons commencer à vous de facturation pour la fonction d’un module complémentaire hello premium dès que la commande hello a été exécutée.</span><span class="sxs-lookup"><span data-stu-id="90ccc-203">Note that we will start billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="90ccc-204">module complémentaire de toodisable hello ExpressRoute premium</span><span class="sxs-lookup"><span data-stu-id="90ccc-204">toodisable hello ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="90ccc-205">Cette opération peut échouer si vous utilisez des ressources qui sont supérieures à ce qui est autorisé pour le circuit de standard hello.</span><span class="sxs-lookup"><span data-stu-id="90ccc-205">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

#### <a name="considerations"></a><span data-ttu-id="90ccc-206">Considérations</span><span class="sxs-lookup"><span data-stu-id="90ccc-206">Considerations</span></span>

* <span data-ttu-id="90ccc-207">Vous devez vous assurer que nombre hello de réseaux virtuels liés toohello circuit est inférieure à 10 avant à la rétrogradation à partir de premium toostandard.</span><span class="sxs-lookup"><span data-stu-id="90ccc-207">You must ensure that hello number of virtual networks linked toohello circuit is less than 10 before you downgrade from premium toostandard.</span></span> <span data-ttu-id="90ccc-208">Si vous ne le faites pas, votre demande de mise à jour échoue, et vous pourrez tarifs hello facturée.</span><span class="sxs-lookup"><span data-stu-id="90ccc-208">If you don't do this, your update request will fail, and you'll be billed hello premium rates.</span></span>
* <span data-ttu-id="90ccc-209">Vous devez dissocier tous les réseaux virtuels dans d'autres régions géopolitiques.</span><span class="sxs-lookup"><span data-stu-id="90ccc-209">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="90ccc-210">Si vous ne le faites pas, votre demande de mise à jour échoue, et vous pourrez tarifs hello facturée.</span><span class="sxs-lookup"><span data-stu-id="90ccc-210">If you don't do this, your update request will fail, and you'll be billed hello premium rates.</span></span>
* <span data-ttu-id="90ccc-211">Pour l’homologation privée, votre table de routage doit comporter moins de 4 000 routages.</span><span class="sxs-lookup"><span data-stu-id="90ccc-211">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="90ccc-212">Si la taille de la table de routage est supérieure à 4 000 itinéraires, session BGP hello supprimera et ne sera pas être réactivée jusqu'à ce que le nombre de hello de préfixes annoncés devient inférieur à 4 000.</span><span class="sxs-lookup"><span data-stu-id="90ccc-212">If your route table size is greater than 4,000 routes, hello BGP session will drop and won't be reenabled until hello number of advertised prefixes goes below 4,000.</span></span>

#### <a name="disable-hello-premium-add-on"></a><span data-ttu-id="90ccc-213">Désactiver le module complémentaire de hello premium</span><span class="sxs-lookup"><span data-stu-id="90ccc-213">Disable hello premium add-on</span></span>
<span data-ttu-id="90ccc-214">Vous pouvez désactiver le module complémentaire de premium hello ExpressRoute pour votre circuit existant à l’aide de hello suivant l’applet de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="90ccc-214">You can disable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell cmdlet:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="90ccc-215">bande passante du circuit ExpressRoute hello tooupdate</span><span class="sxs-lookup"><span data-stu-id="90ccc-215">tooupdate hello ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="90ccc-216">Vérifiez hello [FAQ sur ExpressRoute](expressroute-faqs.md) pour les options de bande passante pour le fournisseur de prise en charge.</span><span class="sxs-lookup"><span data-stu-id="90ccc-216">Check hello [ExpressRoute FAQ](expressroute-faqs.md) for supported bandwidth options for your provider.</span></span> <span data-ttu-id="90ccc-217">Vous pouvez choisir n’importe quelle taille est supérieure à la taille de hello de votre circuit existant tant que port physique de hello (sur lequel votre circuit est créé) permet.</span><span class="sxs-lookup"><span data-stu-id="90ccc-217">You can pick any size that is greater than hello size of your existing circuit as long as hello physical port (on which your circuit is created) allows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="90ccc-218">Vous avez peut-être circuit ExpressRoute de hello toorecreate si la capacité inadéquate est sur le port existant hello.</span><span class="sxs-lookup"><span data-stu-id="90ccc-218">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="90ccc-219">Vous ne peut pas mettre à niveau de circuit de hello si aucune capacité supplémentaire n’est disponible à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="90ccc-219">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="90ccc-220">Vous ne pouvez pas réduire la bande passante hello d’un circuit ExpressRoute sans interruption de service.</span><span class="sxs-lookup"><span data-stu-id="90ccc-220">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="90ccc-221">Rétrogradation de la bande passante vous oblige le circuit ExpressRoute de hello toodeprovision et puis reconfigurez un circuit ExpressRoute de nouveau.</span><span class="sxs-lookup"><span data-stu-id="90ccc-221">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> 

#### <a name="resize-a-circuit"></a><span data-ttu-id="90ccc-222">Redimensionner un circuit</span><span class="sxs-lookup"><span data-stu-id="90ccc-222">Resize a circuit</span></span>

<span data-ttu-id="90ccc-223">Après avoir déterminé la taille que vous avez besoin, vous pouvez utiliser votre circuit hello suivant tooresize de commande :</span><span class="sxs-lookup"><span data-stu-id="90ccc-223">After you decide what size you need, you can use hello following command tooresize your circuit:</span></span>

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="90ccc-224">Votre circuit sera ont dimensionnés côté de Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="90ccc-224">Your circuit will have been sized up on hello Microsoft side.</span></span> <span data-ttu-id="90ccc-225">Cette modification, vous devez contacter votre configurations tooupdate de fournisseur de connectivité sur leur toomatch côté.</span><span class="sxs-lookup"><span data-stu-id="90ccc-225">You must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="90ccc-226">Notez que nous allons commencer à vous de facturation pour hello mis à jour option de la bande passante à partir de ce point.</span><span class="sxs-lookup"><span data-stu-id="90ccc-226">Note that we will start billing you for hello updated bandwidth option from this point on.</span></span>

<span data-ttu-id="90ccc-227">Si vous voyez l’erreur suivante lors de l’augmentation de la bande passante du circuit hello de hello, il signifie qu’il ne reste aucun suffisamment de bande passante sur le port physique hello où votre circuit existant est créé.</span><span class="sxs-lookup"><span data-stu-id="90ccc-227">If you see hello following error when increasing hello circuit bandwidth, it means there is no sufficient bandwidth left on hello physical port where your existing circuit is created.</span></span> <span data-ttu-id="90ccc-228">Vous avez toodelete ce circuit et créez un nouveau circuit de taille hello que vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="90ccc-228">You have toodelete this circuit and create a new circuit of hello size you need.</span></span> 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available tooperform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="90ccc-229">Annulation de l’approvisionnement et suppression d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="90ccc-229">Deprovisioning and deleting an ExpressRoute circuit</span></span>

### <a name="considerations"></a><span data-ttu-id="90ccc-230">Considérations</span><span class="sxs-lookup"><span data-stu-id="90ccc-230">Considerations</span></span>

* <span data-ttu-id="90ccc-231">Vous devez supprimer le lien de tous les réseaux virtuels à partir de hello circuit ExpressRoute pour toosucceed de cette opération.</span><span class="sxs-lookup"><span data-stu-id="90ccc-231">You must unlink all virtual networks from hello ExpressRoute circuit for this operation toosucceed.</span></span> <span data-ttu-id="90ccc-232">Vérifiez toosee si vous avez des réseaux virtuels qui sont liés toohello circuit si cette opération échoue.</span><span class="sxs-lookup"><span data-stu-id="90ccc-232">Check toosee if you have any virtual networks that are linked toohello circuit if this operation fails.</span></span>
* <span data-ttu-id="90ccc-233">Si le fournisseur de service du circuit ExpressRoute hello état d’approvisionnement est **Provisioning** ou **configuré** vous devez collaborer avec votre circuit de hello toodeprovision service fournisseur de leur côté.</span><span class="sxs-lookup"><span data-stu-id="90ccc-233">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="90ccc-234">Nous allons continuer tooreserve ressources et vous facturer jusqu'à ce que le fournisseur de services hello termine de circuit de hello désaffectation et nous avertit.</span><span class="sxs-lookup"><span data-stu-id="90ccc-234">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="90ccc-235">Si le fournisseur de services hello a annulé le circuit de hello (fournisseur de services hello état d’approvisionnement est défini trop**non préparé**) vous pouvez ensuite supprimer le circuit de hello.</span><span class="sxs-lookup"><span data-stu-id="90ccc-235">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="90ccc-236">Cela arrêtera la facturation pour le circuit de hello.</span><span class="sxs-lookup"><span data-stu-id="90ccc-236">This will stop billing for hello circuit.</span></span>

#### <a name="delete-a-circuit"></a><span data-ttu-id="90ccc-237">Supprimer un circuit</span><span class="sxs-lookup"><span data-stu-id="90ccc-237">Delete a circuit</span></span>

<span data-ttu-id="90ccc-238">Vous pouvez supprimer votre circuit ExpressRoute en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="90ccc-238">You can delete your ExpressRoute circuit by running hello following command:</span></span>

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a><span data-ttu-id="90ccc-239">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="90ccc-239">Next steps</span></span>
<span data-ttu-id="90ccc-240">Après avoir créé votre circuit, assurez-vous que vous hello suivant :</span><span class="sxs-lookup"><span data-stu-id="90ccc-240">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="90ccc-241">Créer et modifier le routage le routage pour votre circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="90ccc-241">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-classic.md)
* [<span data-ttu-id="90ccc-242">Lier votre réseau virtuel de tooyour circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="90ccc-242">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

