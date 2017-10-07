---
title: "Créer et modifier un circuit ExpressRoute avec PowerShell et Azure Resource Manager | Microsoft Docs"
description: "Cet article décrit comment toocreate, configurer, vérifier, mettre à jour, supprimer et annuler le déploiement d’un circuit ExpressRoute."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f997182e-9b25-4a7a-b079-b004221dadcc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8d76c577a9cffdd393abac1b76cccc27d92e9e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="f1a48-103">Créer et modifier un circuit ExpressRoute à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1a48-103">Create and modify an ExpressRoute circuit using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f1a48-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="f1a48-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="f1a48-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1a48-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="f1a48-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="f1a48-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="f1a48-107">Vidéo - portail Azure</span><span class="sxs-lookup"><span data-stu-id="f1a48-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="f1a48-108">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="f1a48-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="f1a48-109">Cet article décrit comment toocreate un Azure ExpressRoute circuit en utilisant le modèle de déploiement Azure Resource Manager hello et les applets de commande de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1a48-109">This article describes how toocreate an Azure ExpressRoute circuit by using PowerShell cmdlets and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="f1a48-110">Cet article vous montre également l’état de hello toocheck du circuit de hello, mettre à jour, supprimer et ou annuler le déploiement.</span><span class="sxs-lookup"><span data-stu-id="f1a48-110">This article also shows you how toocheck hello status of hello circuit, update it, or delete and deprovision it.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f1a48-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="f1a48-111">Before you begin</span></span>
* <span data-ttu-id="f1a48-112">Installer la version la plus récente hello Hello applets de commande PowerShell de gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="f1a48-112">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="f1a48-113">Pour plus d’informations, voir [Présentation d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f1a48-113">For more information, see [Overview of Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="f1a48-114">Hello de révision [conditions préalables](expressroute-prerequisites.md) et [workflows](expressroute-workflows.md) avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="f1a48-114">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>


## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="f1a48-115">Création et approvisionnement d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f1a48-115">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a><span data-ttu-id="f1a48-116">1. Connectez-vous à tooyour compte Azure et sélectionnez votre abonnement</span><span class="sxs-lookup"><span data-stu-id="f1a48-116">1. Sign in tooyour Azure account and select your subscription</span></span>
<span data-ttu-id="f1a48-117">toobegin votre configuration, de connexion tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="f1a48-117">toobegin your configuration, sign in tooyour Azure account.</span></span> <span data-ttu-id="f1a48-118">Utilisez hello suivant toohelp exemples que vous connectez :</span><span class="sxs-lookup"><span data-stu-id="f1a48-118">Use hello following examples toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="f1a48-119">Vérifier les abonnements hello pour le compte de hello :</span><span class="sxs-lookup"><span data-stu-id="f1a48-119">Check hello subscriptions for hello account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="f1a48-120">Sélectionnez hello abonnement toocreate un ExpressRoute de circuit pour :</span><span class="sxs-lookup"><span data-stu-id="f1a48-120">Select hello subscription that you want toocreate an ExpressRoute circuit for:</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="f1a48-121">2. Obtenir la liste de hello de fournisseurs pris en charge, des emplacements et des bandes passantes</span><span class="sxs-lookup"><span data-stu-id="f1a48-121">2. Get hello list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="f1a48-122">Avant de créer un circuit ExpressRoute, vous devez liste hello de fournisseurs de connectivité pris en charge, des emplacements et des options de bande passante.</span><span class="sxs-lookup"><span data-stu-id="f1a48-122">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="f1a48-123">applet de commande PowerShell de Hello **Get-AzureRmExpressRouteServiceProvider** retourne cette information, vous allez utiliser dans les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f1a48-123">hello PowerShell cmdlet **Get-AzureRmExpressRouteServiceProvider** returns this information, which you’ll use in later steps:</span></span>

```powershell
Get-AzureRmExpressRouteServiceProvider
```

<span data-ttu-id="f1a48-124">Vérifiez toosee si votre fournisseur de connectivité y sont répertoriée.</span><span class="sxs-lookup"><span data-stu-id="f1a48-124">Check toosee if your connectivity provider is listed there.</span></span> <span data-ttu-id="f1a48-125">Prenez note de hello informations suivantes.</span><span class="sxs-lookup"><span data-stu-id="f1a48-125">Make a note of hello following information.</span></span> <span data-ttu-id="f1a48-126">Vous en aurez besoin ultérieurement lorsque vous créerez un circuit.</span><span class="sxs-lookup"><span data-stu-id="f1a48-126">You'll need it later when you create a circuit.</span></span>

* <span data-ttu-id="f1a48-127">Nom</span><span class="sxs-lookup"><span data-stu-id="f1a48-127">Name</span></span>
* <span data-ttu-id="f1a48-128">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="f1a48-128">PeeringLocations</span></span>
* <span data-ttu-id="f1a48-129">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="f1a48-129">BandwidthsOffered</span></span>

<span data-ttu-id="f1a48-130">Vous êtes maintenant prêt toocreate un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f1a48-130">You're now ready toocreate an ExpressRoute circuit.</span></span>   

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="f1a48-131">3. Création d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f1a48-131">3. Create an ExpressRoute circuit</span></span>
<span data-ttu-id="f1a48-132">Si vous n’avez pas déjà un groupe de ressources, vous devez en créer un avant de créer votre circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f1a48-132">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="f1a48-133">Vous pouvez le faire en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f1a48-133">You can do so by running hello following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


<span data-ttu-id="f1a48-134">Bonjour à l’exemple suivant montre comment toocreate un ExpressRoute de 200 Mbits/s de circuit via Equinix dans Silicon Valley.</span><span class="sxs-lookup"><span data-stu-id="f1a48-134">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="f1a48-135">Si vous utilisez un autre fournisseur et des paramètres différents, utilisez ces informations quand vous créez votre requête.</span><span class="sxs-lookup"><span data-stu-id="f1a48-135">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> <span data-ttu-id="f1a48-136">Hello Voici un exemple de demande pour une nouvelle clé de service :</span><span class="sxs-lookup"><span data-stu-id="f1a48-136">hello following is an example request for a new service key:</span></span>

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

<span data-ttu-id="f1a48-137">Assurez-vous que vous spécifiez un niveau de référence (SKU) correct hello et famille de référence (SKU) :</span><span class="sxs-lookup"><span data-stu-id="f1a48-137">Make sure that you specify hello correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="f1a48-138">Le niveau de référence détermine si ExpressRoute standard ou un module complémentaire ExpressRoute Premium est activé.</span><span class="sxs-lookup"><span data-stu-id="f1a48-138">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="f1a48-139">Vous pouvez spécifier *Standard* tooget hello référence (SKU) standard ou *Premium* pour le module complémentaire de hello premium.</span><span class="sxs-lookup"><span data-stu-id="f1a48-139">You can specify *Standard* tooget hello standard SKU or *Premium* for hello premium add-on.</span></span>
* <span data-ttu-id="f1a48-140">Famille de référence (SKU) détermine le type de facturation hello.</span><span class="sxs-lookup"><span data-stu-id="f1a48-140">SKU family determines hello billing type.</span></span> <span data-ttu-id="f1a48-141">Vous pouvez spécifier *Metereddata* pour définir un forfait de données limité et *Unlimiteddata* pour un forfait de données illimité.</span><span class="sxs-lookup"><span data-stu-id="f1a48-141">You can specify *Metereddata* for a metered data plan and *Unlimiteddata* for an unlimited data plan.</span></span> <span data-ttu-id="f1a48-142">Vous pouvez modifier le type de facturation hello de *Metereddata* trop*Unlimiteddata*, mais vous ne pouvez pas modifier le type hello de *Unlimiteddata* trop*Metereddata* .</span><span class="sxs-lookup"><span data-stu-id="f1a48-142">You can change hello billing type from *Metereddata* too*Unlimiteddata*, but you can't change hello type from *Unlimiteddata* too*Metereddata*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f1a48-143">Votre circuit ExpressRoute sera facturé dès hello, qu'une clé de service est émise.</span><span class="sxs-lookup"><span data-stu-id="f1a48-143">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="f1a48-144">Veillez à effectuer cette opération lorsque le fournisseur de connectivité hello est circuit de hello tooprovision prêt.</span><span class="sxs-lookup"><span data-stu-id="f1a48-144">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="f1a48-145">réponse de Hello contient la clé de service hello.</span><span class="sxs-lookup"><span data-stu-id="f1a48-145">hello response contains hello service key.</span></span> <span data-ttu-id="f1a48-146">Vous pouvez obtenir une description détaillée de tous les paramètres de hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f1a48-146">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="f1a48-147">4. Répertorier tous les circuits ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f1a48-147">4. List all ExpressRoute circuits</span></span>
<span data-ttu-id="f1a48-148">tooget une liste de tous les hello circuits ExpressRoute que vous avez créé, exécutez hello **Get-AzureRmExpressRouteCircuit** commande :</span><span class="sxs-lookup"><span data-stu-id="f1a48-148">tooget a list of all hello ExpressRoute circuits that you created, run hello **Get-AzureRmExpressRouteCircuit** command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

<span data-ttu-id="f1a48-149">réponse de Hello ressemblera toohello similaire, l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="f1a48-149">hello response will look similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                          }
    CircuitProvisioningState          : Enabled
    ServiceProviderProvisioningState  : NotProvisioned
    ServiceProviderNotes              :
    ServiceProviderProperties         : {
                                          "ServiceProviderName": "Equinix",
                                          "PeeringLocation": "Silicon Valley",
                                          "BandwidthInMbps": 200
                                        }
    ServiceKey                        : **************************************
    Peerings                          : []

<span data-ttu-id="f1a48-150">Vous pouvez récupérer ces informations à tout moment à l’aide de hello `Get-AzureRmExpressRouteCircuit` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="f1a48-150">You can retrieve this information at any time by using hello `Get-AzureRmExpressRouteCircuit` cmdlet.</span></span> <span data-ttu-id="f1a48-151">Rendre hello sans paramètre répertorie tous les circuits hello.</span><span class="sxs-lookup"><span data-stu-id="f1a48-151">Making hello call with no parameters lists all hello circuits.</span></span> <span data-ttu-id="f1a48-152">Votre clé de service s’afficheront dans hello *ServiceKey* champ :</span><span class="sxs-lookup"><span data-stu-id="f1a48-152">Your service key will be listed in hello *ServiceKey* field:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="f1a48-153">réponse de Hello ressemblera toohello similaire, l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="f1a48-153">hello response will look similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                          }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : NotProvisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


<span data-ttu-id="f1a48-154">Vous pouvez obtenir une description détaillée de tous les paramètres de hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f1a48-154">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="f1a48-155">5. Envoyer le fournisseur de connectivité hello service tooyour clé pour la configuration</span><span class="sxs-lookup"><span data-stu-id="f1a48-155">5. Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="f1a48-156">*ServiceProviderProvisioningState* fournit des informations sur l’état actuel de hello de configuration sur le côté du fournisseur de services hello.</span><span class="sxs-lookup"><span data-stu-id="f1a48-156">*ServiceProviderProvisioningState* provides information about hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="f1a48-157">État fournit les état hello sur hello côté de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f1a48-157">Status provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="f1a48-158">Pour plus d’informations sur les États de configuration de circuit, consultez hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) l’article.</span><span class="sxs-lookup"><span data-stu-id="f1a48-158">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="f1a48-159">Lorsque vous créez un nouveau circuit ExpressRoute, circuit de hello sera Bonjour suivant l’état :</span><span class="sxs-lookup"><span data-stu-id="f1a48-159">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



<span data-ttu-id="f1a48-160">circuit de Hello modifiera toohello suivant l’état lorsque le fournisseur de connectivité hello est en cours de hello de l’activer pour vous :</span><span class="sxs-lookup"><span data-stu-id="f1a48-160">hello circuit will change toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="f1a48-161">Pour vous toobe en mesure de toouse un circuit ExpressRoute, il doit être Bonjour suivant l’état :</span><span class="sxs-lookup"><span data-stu-id="f1a48-161">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="f1a48-162">6. Vérifier régulièrement le statut de hello et état hello de clé du circuit hello</span><span class="sxs-lookup"><span data-stu-id="f1a48-162">6. Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="f1a48-163">Vérification du statut de hello et état hello de clé du circuit hello vous permet de savoir quand votre fournisseur aura activé votre circuit.</span><span class="sxs-lookup"><span data-stu-id="f1a48-163">Checking hello status and hello state of hello circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="f1a48-164">Après la configuration de circuit de hello, *ServiceProviderProvisioningState* apparaît sous la forme *configuré*, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="f1a48-164">After hello circuit has been configured, *ServiceProviderProvisioningState* appears as *Provisioned*, as shown in hello following example:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="f1a48-165">réponse de Hello ressemblera toohello similaire, l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="f1a48-165">hello response will look similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                       }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                       }
    ServiceKey                       : **************************************
    Peerings                         : []

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="f1a48-166">7. Créer votre configuration de routage</span><span class="sxs-lookup"><span data-stu-id="f1a48-166">7. Create your routing configuration</span></span>
<span data-ttu-id="f1a48-167">Pour obtenir des instructions, consultez hello [circuit ExpressRoute de configuration de routage](expressroute-howto-routing-arm.md) toocreate de l’article et modifier des homologations de circuit.</span><span class="sxs-lookup"><span data-stu-id="f1a48-167">For step-by-step instructions, see hello [ExpressRoute circuit routing configuration](expressroute-howto-routing-arm.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f1a48-168">Ces instructions s’appliquent uniquement à toocircuits qui sont créés avec des fournisseurs de services qui offrent des services de couche 2 de connectivité.</span><span class="sxs-lookup"><span data-stu-id="f1a48-168">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="f1a48-169">Si vous utilisez un fournisseur de services proposant des services gérés de couche 3 (généralement un VPN IP, comme MPLS), votre fournisseur de connectivité configure et gère le routage pour vous.</span><span class="sxs-lookup"><span data-stu-id="f1a48-169">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="f1a48-170">8. Lier un circuit ExpressRoute de tooan réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="f1a48-170">8. Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="f1a48-171">Ensuite, lier un circuit ExpressRoute de tooyour réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f1a48-171">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="f1a48-172">Hello d’utilisation [liaison virtuel réseaux tooExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article lorsque vous travaillez avec un modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="f1a48-172">Use hello [Linking virtual networks tooExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with hello Resource Manager deployment model.</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="f1a48-173">État de hello lors de l’obtention d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f1a48-173">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="f1a48-174">Vous pouvez récupérer ces informations à tout moment à l’aide de hello **Get-AzureRmExpressRouteCircuit** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="f1a48-174">You can retrieve this information at any time by using hello **Get-AzureRmExpressRouteCircuit** cmdlet.</span></span> <span data-ttu-id="f1a48-175">Rendre hello sans paramètre répertorie tous les circuits hello.</span><span class="sxs-lookup"><span data-stu-id="f1a48-175">Making hello call with no parameters lists all hello circuits.</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="f1a48-176">réponse de Hello sera similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="f1a48-176">hello response will be similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                       }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                            "ServiceProviderName": "Equinix",
                                            "PeeringLocation": "Silicon Valley",
                                            "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


<span data-ttu-id="f1a48-177">Vous pouvez obtenir des informations sur un circuit ExpressRoute spécifique en passant le nom de groupe de ressources hello et nom du circuit comme un appel de toohello paramètre :</span><span class="sxs-lookup"><span data-stu-id="f1a48-177">You can get information on a specific ExpressRoute circuit by passing hello resource group name and circuit name as a parameter toohello call:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="f1a48-178">réponse de Hello ressemblera toohello similaire, l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="f1a48-178">hello response will look similar toohello following example:</span></span>

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                            "Tier": "Standard",
                                            "Family": "MeteredData"
                                          }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


<span data-ttu-id="f1a48-179">Vous pouvez obtenir une description détaillée de tous les paramètres de hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f1a48-179">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <span data-ttu-id="f1a48-180"><a name="modify"></a>Modification d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f1a48-180"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="f1a48-181">Vous pouvez modifier certaines propriétés d'un circuit ExpressRoute sans affecter la connectivité.</span><span class="sxs-lookup"><span data-stu-id="f1a48-181">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="f1a48-182">Vous pouvez effectuer hello suivant sans interruption de service :</span><span class="sxs-lookup"><span data-stu-id="f1a48-182">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="f1a48-183">Activer ou désactiver le module complémentaire ExpressRoute Premium pour votre circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f1a48-183">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="f1a48-184">La bande passante de hello augmentation de votre circuit ExpressRoute fourni la capacité est disponible sur le port hello.</span><span class="sxs-lookup"><span data-stu-id="f1a48-184">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="f1a48-185">Rétrogradation d’un circuit de bande passante hello n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="f1a48-185">Downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="f1a48-186">Modifier hello plan à partir de données de limitées tooUnlimited données de contrôle.</span><span class="sxs-lookup"><span data-stu-id="f1a48-186">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="f1a48-187">Modification de hello plan à partir de tooMetered données illimité que données ne sont pas prise en charge de contrôle.</span><span class="sxs-lookup"><span data-stu-id="f1a48-187">Changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="f1a48-188">Vous pouvez activer et désactiver *Autoriser les opérations classiques*.</span><span class="sxs-lookup"><span data-stu-id="f1a48-188">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="f1a48-189">Pour plus d’informations sur les limites et limitations, consultez toohello [FAQ sur ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="f1a48-189">For more information on limits and limitations, refer toohello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="f1a48-190">module complémentaire de tooenable hello ExpressRoute premium</span><span class="sxs-lookup"><span data-stu-id="f1a48-190">tooenable hello ExpressRoute premium add-on</span></span>
<span data-ttu-id="f1a48-191">Vous pouvez activer un module complémentaire de hello ExpressRoute premium pour votre circuit existant à l’aide de hello suivant extrait de code PowerShell :</span><span class="sxs-lookup"><span data-stu-id="f1a48-191">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

<span data-ttu-id="f1a48-192">circuit de Hello sera désormais hello ExpressRoute premium module complémentaire fonctionnalités sont activées.</span><span class="sxs-lookup"><span data-stu-id="f1a48-192">hello circuit will now have hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="f1a48-193">Nous allons commencer à vous de facturation pour la fonction d’un module complémentaire hello premium dès que la commande hello a été exécutée.</span><span class="sxs-lookup"><span data-stu-id="f1a48-193">We will begin billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="f1a48-194">module complémentaire de toodisable hello ExpressRoute premium</span><span class="sxs-lookup"><span data-stu-id="f1a48-194">toodisable hello ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f1a48-195">Cette opération peut échouer si vous utilisez des ressources qui sont supérieures à ce qui est autorisé pour le circuit de standard hello.</span><span class="sxs-lookup"><span data-stu-id="f1a48-195">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

<span data-ttu-id="f1a48-196">Notez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="f1a48-196">Note hello following:</span></span>

* <span data-ttu-id="f1a48-197">Rétrogradation à partir de premium toostandard, vous devez vous assurer que nombre hello des réseaux virtuels qui sont liées toohello circuit est inférieure à 10.</span><span class="sxs-lookup"><span data-stu-id="f1a48-197">Before you downgrade from premium toostandard, you must ensure that hello number of virtual networks that are linked toohello circuit is less than 10.</span></span> <span data-ttu-id="f1a48-198">Si vous ne le faites pas, votre demande de mise à jour échoue et nous appliquons les tarifs Premium.</span><span class="sxs-lookup"><span data-stu-id="f1a48-198">If you don't do this, your update request fails, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="f1a48-199">Vous devez dissocier tous les réseaux virtuels dans d'autres régions géopolitiques.</span><span class="sxs-lookup"><span data-stu-id="f1a48-199">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="f1a48-200">Si vous ne le faites pas, votre demande de mise à jour échoue et nous appliquons les tarifs Premium.</span><span class="sxs-lookup"><span data-stu-id="f1a48-200">If you don't do this, your update request will fail, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="f1a48-201">Pour l’homologation privée, votre table de routage doit comporter moins de 4 000 routages.</span><span class="sxs-lookup"><span data-stu-id="f1a48-201">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="f1a48-202">Si la taille de la table de routage est supérieure à 4 000 itinéraires, session BGP hello supprime et ne sera pas être réactivée jusqu'à ce que le nombre de hello de préfixes annoncés devient inférieur à 4 000.</span><span class="sxs-lookup"><span data-stu-id="f1a48-202">If your route table size is greater than 4,000 routes, hello BGP session drops and won't be reenabled until hello number of advertised prefixes goes below 4,000.</span></span>

<span data-ttu-id="f1a48-203">Vous pouvez désactiver complémentaire hello ExpressRoute pour le circuit existant de hello à l’aide de hello suivant l’applet de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="f1a48-203">You can disable hello ExpressRoute premium add-on for hello existing circuit by using hello following PowerShell cmdlet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="f1a48-204">bande passante du circuit ExpressRoute hello tooupdate</span><span class="sxs-lookup"><span data-stu-id="f1a48-204">tooupdate hello ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="f1a48-205">Pour les options de la bande passante prises en charge pour le fournisseur, vérifiez hello [FAQ sur ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="f1a48-205">For supported bandwidth options for your provider, check hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="f1a48-206">Vous pouvez choisir n’importe quelle taille supérieure à la taille de hello de votre circuit existant.</span><span class="sxs-lookup"><span data-stu-id="f1a48-206">You can pick any size greater than hello size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f1a48-207">Vous avez peut-être circuit ExpressRoute de hello toorecreate si la capacité inadéquate est sur le port existant hello.</span><span class="sxs-lookup"><span data-stu-id="f1a48-207">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="f1a48-208">Vous ne peut pas mettre à niveau de circuit de hello si aucune capacité supplémentaire n’est disponible à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="f1a48-208">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="f1a48-209">Vous ne pouvez pas réduire la bande passante hello d’un circuit ExpressRoute sans interruption de service.</span><span class="sxs-lookup"><span data-stu-id="f1a48-209">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="f1a48-210">Rétrogradation de la bande passante vous oblige le circuit ExpressRoute de hello toodeprovision et puis reconfigurez un circuit ExpressRoute de nouveau.</span><span class="sxs-lookup"><span data-stu-id="f1a48-210">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 

<span data-ttu-id="f1a48-211">Après avoir déterminé la taille que vous avez besoin, utilisez hello suivant commande tooresize votre circuit :</span><span class="sxs-lookup"><span data-stu-id="f1a48-211">After you decide what size you need, use hello following command tooresize your circuit:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


<span data-ttu-id="f1a48-212">A la taille votre circuit côté de Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="f1a48-212">Your circuit will be sized up on hello Microsoft side.</span></span> <span data-ttu-id="f1a48-213">Vous devez ensuite contacter vos configurations de tooupdate de fournisseur de connectivité sur leur toomatch côté cette modification.</span><span class="sxs-lookup"><span data-stu-id="f1a48-213">Then you must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="f1a48-214">Après avoir apporté cette notification, nous allons commencer à vous de facturation pour l’option de la bande passante hello mis à jour.</span><span class="sxs-lookup"><span data-stu-id="f1a48-214">After you make this notification, we will begin billing you for hello updated bandwidth option.</span></span>

### <a name="toomove-hello-sku-from-metered-toounlimited"></a><span data-ttu-id="f1a48-215">toomove hello référence (SKU) à partir de toounlimited limitée</span><span class="sxs-lookup"><span data-stu-id="f1a48-215">toomove hello SKU from metered toounlimited</span></span>
<span data-ttu-id="f1a48-216">Vous pouvez modifier hello référence (SKU) d’un circuit ExpressRoute à l’aide de hello suivant extrait de code PowerShell :</span><span class="sxs-lookup"><span data-stu-id="f1a48-216">You can change hello SKU of an ExpressRoute circuit by using hello following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a><span data-ttu-id="f1a48-217">classique de toohello toocontrol accès et les environnements de gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="f1a48-217">toocontrol access toohello classic and Resource Manager environments</span></span>
<span data-ttu-id="f1a48-218">Passez en revue les instructions hello dans [circuits ExpressRoute de déplacer à partir du modèle de déploiement du Gestionnaire de ressources hello classique toohello](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="f1a48-218">Review hello instructions in [Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="f1a48-219">Annulation de l’approvisionnement et suppression d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f1a48-219">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="f1a48-220">Notez hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="f1a48-220">Note hello following:</span></span>

* <span data-ttu-id="f1a48-221">Vous devez supprimer le lien de tous les réseaux virtuels à partir de hello circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f1a48-221">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="f1a48-222">Si cette opération échoue, vérifiez toosee si les réseaux virtuels sont liés toohello circuit.</span><span class="sxs-lookup"><span data-stu-id="f1a48-222">If this operation fails, check toosee if any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="f1a48-223">Si le fournisseur de service du circuit ExpressRoute hello état d’approvisionnement est **Provisioning** ou **configuré** vous devez collaborer avec votre circuit de hello toodeprovision service fournisseur de leur côté.</span><span class="sxs-lookup"><span data-stu-id="f1a48-223">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="f1a48-224">Nous allons continuer tooreserve ressources et vous facturer jusqu'à ce que le fournisseur de services hello termine de circuit de hello désaffectation et nous avertit.</span><span class="sxs-lookup"><span data-stu-id="f1a48-224">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="f1a48-225">Si le fournisseur de services hello a annulé le circuit de hello (fournisseur de services hello état d’approvisionnement est défini trop**non préparé**) vous pouvez ensuite supprimer le circuit de hello.</span><span class="sxs-lookup"><span data-stu-id="f1a48-225">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="f1a48-226">Cela arrêtera la facturation pour le circuit de hello</span><span class="sxs-lookup"><span data-stu-id="f1a48-226">This will stop billing for hello circuit</span></span>

<span data-ttu-id="f1a48-227">Vous pouvez supprimer votre circuit ExpressRoute en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f1a48-227">You can delete your ExpressRoute circuit by running hello following command:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a><span data-ttu-id="f1a48-228">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f1a48-228">Next steps</span></span>

<span data-ttu-id="f1a48-229">Après avoir créé votre circuit, assurez-vous que vous hello suivant :</span><span class="sxs-lookup"><span data-stu-id="f1a48-229">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="f1a48-230">Créer et modifier le routage le routage pour votre circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f1a48-230">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="f1a48-231">Lier votre réseau virtuel de tooyour circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f1a48-231">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
