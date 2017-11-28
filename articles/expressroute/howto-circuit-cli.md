---
title: "Créer et modifier un circuit Azure ExpressRoute : CLI | Microsoft Docs"
description: "Cet article décrit comment toocreate, configurer, vérifier, mettre à jour, supprimer et annuler le déploiement d’un circuit ExpressRoute à l’aide de CLI."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman;cherylmc
ms.openlocfilehash: 396e325658a59afadb209bb525cbb59ac775ae6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-cli"></a><span data-ttu-id="7c8f4-103">Créer et modifier un circuit ExpressRoute à l’aide de l’interface de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="7c8f4-103">Create and modify an ExpressRoute circuit using CLI</span></span>


<span data-ttu-id="7c8f4-104">Cet article décrit comment un circuit ExpressRoute d’Azure à l’aide de toocreate hello Interface de ligne de commande (CLI).</span><span class="sxs-lookup"><span data-stu-id="7c8f4-104">This article describes how toocreate an Azure ExpressRoute circuit by using hello Command Line Interface (CLI).</span></span> <span data-ttu-id="7c8f4-105">Cet article vous montre également comment toocheck état de hello, mettre à jour, ou supprimer et annuler le déploiement d’un circuit.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-105">This article also shows you how toocheck hello status, update, or delete and deprovision a circuit.</span></span> <span data-ttu-id="7c8f4-106">Si vous voulez toouse un toowork autre méthode avec des circuits ExpressRoute, vous pouvez sélectionner l’article de hello dans hello suivant liste :</span><span class="sxs-lookup"><span data-stu-id="7c8f4-106">If you want toouse a different method toowork with ExpressRoute circuits, you can select hello article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7c8f4-107">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="7c8f4-107">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="7c8f4-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c8f4-108">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="7c8f4-109">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="7c8f4-109">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="7c8f4-110">Vidéo - portail Azure</span><span class="sxs-lookup"><span data-stu-id="7c8f4-110">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="7c8f4-111">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="7c8f4-111">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
> 

## <a name="before-you-begin"></a><span data-ttu-id="7c8f4-112">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="7c8f4-112">Before you begin</span></span>

* <span data-ttu-id="7c8f4-113">Avant de commencer, installez hello dernière version des commandes CLI de hello (version 2.0 ou version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="7c8f4-113">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="7c8f4-114">Pour plus d’informations sur l’installation des commandes CLI de hello, consultez [installer Azure CLI 2.0](/cli/azure/install-azure-cli) et [prise en main Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7c8f4-114">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="7c8f4-115">Hello de révision [conditions préalables](expressroute-prerequisites.md) et [workflows](expressroute-workflows.md) avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-115">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="7c8f4-116">Création et approvisionnement d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7c8f4-116">Create and provision an ExpressRoute circuit</span></span>

### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a><span data-ttu-id="7c8f4-117">1. Connectez-vous à tooyour compte Azure et sélectionnez votre abonnement</span><span class="sxs-lookup"><span data-stu-id="7c8f4-117">1. Sign in tooyour Azure account and select your subscription</span></span>

<span data-ttu-id="7c8f4-118">toobegin votre configuration, de connexion tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-118">toobegin your configuration, sign in tooyour Azure account.</span></span> <span data-ttu-id="7c8f4-119">Utilisez hello suivant toohelp exemples que vous connectez :</span><span class="sxs-lookup"><span data-stu-id="7c8f4-119">Use hello following examples toohelp you connect:</span></span>

```azurecli
az login
```

<span data-ttu-id="7c8f4-120">Vérifiez les abonnements hello pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-120">Check hello subscriptions for hello account.</span></span>

```azurecli
az account list
```

<span data-ttu-id="7c8f4-121">Sélectionnez l’abonnement hello pour lequel vous souhaitez toocreate un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-121">Select hello subscription for which you want toocreate an ExpressRoute circuit.</span></span>

```azurecli
az account set --subscription "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="7c8f4-122">2. Obtenir la liste de hello de fournisseurs pris en charge, des emplacements et des bandes passantes</span><span class="sxs-lookup"><span data-stu-id="7c8f4-122">2. Get hello list of supported providers, locations, and bandwidths</span></span>

<span data-ttu-id="7c8f4-123">Avant de créer un circuit ExpressRoute, vous devez liste hello de fournisseurs de connectivité pris en charge, des emplacements et des options de bande passante.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-123">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span> <span data-ttu-id="7c8f4-124">Hello CLI commande 'az réseau-express route liste prestataires de service' renvoie ces informations, vous allez utiliser dans les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="7c8f4-124">hello CLI command 'az network express-route list-service-providers' returns this information, which you’ll use in later steps:</span></span>

```azurecli
az network express-route list-service-providers
```

<span data-ttu-id="7c8f4-125">réponse de Hello est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="7c8f4-125">hello response is similar toohello following example:</span></span>

```azurecli
[
  {
    "bandwidthsOffered": [
      {
        "offerName": "50Mbps",
        "valueInMbps": 50
      },
      {
        "offerName": "100Mbps",
        "valueInMbps": 100
      },
      {
        "offerName": "200Mbps",
        "valueInMbps": 200
      },
      {
        "offerName": "500Mbps",
        "valueInMbps": 500
      },
      {
        "offerName": "1Gbps",
        "valueInMbps": 1000
      },
      {
        "offerName": "2Gbps",
        "valueInMbps": 2000
      },
      {
        "offerName": "5Gbps",
        "valueInMbps": 5000
      },
      {
        "offerName": "10Gbps",
        "valueInMbps": 10000
      }
    ],
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/expressRouteServiceProviders/",
    "location": null,
    "name": "AARNet",
    "peeringLocations": [
      "Melbourne",
      "Sydney"
    ],
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "tags": null,
    "type": "Microsoft.Network/expressRouteServiceProviders"
  },
```

<span data-ttu-id="7c8f4-126">Vérifiez hello réponse toosee si votre fournisseur de connectivité n’est répertorié.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-126">Check hello response toosee if your connectivity provider is listed.</span></span> <span data-ttu-id="7c8f4-127">Prenez note de hello informations dont vous aurez besoin lorsque vous créez un circuit suivantes :</span><span class="sxs-lookup"><span data-stu-id="7c8f4-127">Make a note of hello following information, which you will need when you create a circuit:</span></span>

* <span data-ttu-id="7c8f4-128">Nom</span><span class="sxs-lookup"><span data-stu-id="7c8f4-128">Name</span></span>
* <span data-ttu-id="7c8f4-129">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="7c8f4-129">PeeringLocations</span></span>
* <span data-ttu-id="7c8f4-130">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="7c8f4-130">BandwidthsOffered</span></span>

<span data-ttu-id="7c8f4-131">Vous êtes maintenant prêt toocreate un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-131">You're now ready toocreate an ExpressRoute circuit.</span></span>

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="7c8f4-132">3. Création d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7c8f4-132">3. Create an ExpressRoute circuit</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c8f4-133">Votre circuit ExpressRoute est facturé à partir du moment hello qu'une clé de service est émise.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-133">Your ExpressRoute circuit is billed from hello moment a service key is issued.</span></span> <span data-ttu-id="7c8f4-134">Effectuer cette opération lorsque le fournisseur de connectivité hello est circuit de hello tooprovision prêt.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-134">Perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="7c8f4-135">Si vous n’avez pas déjà un groupe de ressources, vous devez en créer un avant de créer votre circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-135">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="7c8f4-136">Vous pouvez créer un groupe de ressources en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7c8f4-136">You can create a resource group by running hello following command:</span></span>

```azurecli
az group create -n ExpressRouteResourceGroup -l "West US"
```

<span data-ttu-id="7c8f4-137">Bonjour à l’exemple suivant montre comment toocreate un ExpressRoute de 200 Mbits/s de circuit via Equinix dans Silicon Valley.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-137">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="7c8f4-138">Si vous utilisez un autre fournisseur et des paramètres différents, utilisez ces informations quand vous créez votre requête.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-138">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> 

<span data-ttu-id="7c8f4-139">Assurez-vous que vous spécifiez un niveau de référence (SKU) correct hello et famille de référence (SKU) :</span><span class="sxs-lookup"><span data-stu-id="7c8f4-139">Make sure that you specify hello correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="7c8f4-140">Le niveau de référence détermine si ExpressRoute standard ou un module complémentaire ExpressRoute Premium est activé.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-140">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="7c8f4-141">Vous pouvez spécifier « Standard » hello tooget référence (SKU) standard ou 'Premium' pour le module complémentaire de hello premium.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-141">You can specify 'Standard' tooget hello standard SKU or 'Premium' for hello premium add-on.</span></span>
* <span data-ttu-id="7c8f4-142">Famille de référence (SKU) détermine le type de facturation hello.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-142">SKU family determines hello billing type.</span></span> <span data-ttu-id="7c8f4-143">Vous pouvez spécifier « Metereddata » pour définir un forfait de données limité et « Unlimiteddata » pour un forfait de données illimité.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-143">You can specify 'Metereddata' for a metered data plan and 'Unlimiteddata' for an unlimited data plan.</span></span> <span data-ttu-id="7c8f4-144">Vous pouvez modifier le type de facturation hello à partir de ' Metereddata 'too'Unlimiteddata', mais vous ne pouvez pas modifier hello type à partir de 'Unlimiteddata' too'Metereddata'.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-144">You can change hello billing type from 'Metereddata' too'Unlimiteddata', but you can't change hello type from 'Unlimiteddata' too'Metereddata'.</span></span>


<span data-ttu-id="7c8f4-145">Votre circuit ExpressRoute est facturé à partir du moment hello qu'une clé de service est émise.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-145">Your ExpressRoute circuit is billed from hello moment a service key is issued.</span></span> <span data-ttu-id="7c8f4-146">Bonjour à l’exemple suivant est une demande pour une nouvelle clé de service :</span><span class="sxs-lookup"><span data-stu-id="7c8f4-146">hello following example is a request for a new service key:</span></span>

```azurecli
az network express-route create --bandwidth 200 -n MyCircuit --peering-location "Silicon Valley" -g ExpressRouteResourceGroup --provider "Equinix" -l "West US" --sku-family MeteredData --sku-tier Standard
```

<span data-ttu-id="7c8f4-147">réponse de Hello contient la clé de service hello.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-147">hello response contains hello service key.</span></span>

### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="7c8f4-148">4. Répertorier tous les circuits ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7c8f4-148">4. List all ExpressRoute circuits</span></span>

<span data-ttu-id="7c8f4-149">tooget une liste de tous les circuits ExpressRoute hello que vous avez créé, exécutez la commande de « liste d’express route az réseau » de hello.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-149">tooget a list of all hello ExpressRoute circuits that you created, run hello 'az network express-route list' command.</span></span> <span data-ttu-id="7c8f4-150">Vous pouvez récupérer ces informations à tout moment à l’aide de cette commande.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-150">You can retrieve this information at any time by using this command.</span></span> <span data-ttu-id="7c8f4-151">toolist tous les circuits, appeler hello sans paramètres.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-151">toolist all circuits, make hello call with no parameters.</span></span>

```azurecli
az network express-route list
```

<span data-ttu-id="7c8f4-152">Votre clé de service est répertorié dans hello *ServiceKey* champ de réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-152">Your service key is listed in hello *ServiceKey* field of hello response.</span></span>

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

<span data-ttu-id="7c8f4-153">Vous pouvez obtenir une description détaillée de tous les paramètres de hello en exécutant la commande hello à l’aide de hello '-h' paramètre.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-153">You can get detailed descriptions of all hello parameters by running hello command using hello '-h' parameter.</span></span>

```azurecli
az network express-route list -h
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="7c8f4-154">5. Envoyer le fournisseur de connectivité hello service tooyour clé pour la configuration</span><span class="sxs-lookup"><span data-stu-id="7c8f4-154">5. Send hello service key tooyour connectivity provider for provisioning</span></span>

<span data-ttu-id="7c8f4-155">« ServiceProviderProvisioningState » fournit des informations sur l’état actuel de hello de configuration sur le côté du fournisseur de services hello.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-155">'ServiceProviderProvisioningState' provides information about hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="7c8f4-156">état des Hello fournit l’état de hello sur hello côté de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-156">hello status provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="7c8f4-157">Pour plus d’informations, consultez hello [article du flux de travail](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span><span class="sxs-lookup"><span data-stu-id="7c8f4-157">For more information, see hello [Workflows article](expressroute-workflows.md#expressroute-circuit-provisioning-states).</span></span>

<span data-ttu-id="7c8f4-158">Lorsque vous créez un nouveau circuit ExpressRoute, circuit de hello est Bonjour suivant l’état :</span><span class="sxs-lookup"><span data-stu-id="7c8f4-158">When you create a new ExpressRoute circuit, hello circuit is in hello following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "NotProvisioned"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="7c8f4-159">les modifications de circuit de Hello toohello suivant l’état lorsque le fournisseur de connectivité hello est en cours de hello de l’activer pour vous :</span><span class="sxs-lookup"><span data-stu-id="7c8f4-159">hello circuit changes toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioning"
"circuitProvisioningState": "Enabled"
```

<span data-ttu-id="7c8f4-160">Pour vous toobe en mesure de toouse un circuit ExpressRoute, il doit être Bonjour suivant l’état :</span><span class="sxs-lookup"><span data-stu-id="7c8f4-160">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

```azurecli
"serviceProviderProvisioningState": "Provisioned"
"circuitProvisioningState": "Enabled
```

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="7c8f4-161">6. Vérifier régulièrement le statut de hello et état hello de clé du circuit hello</span><span class="sxs-lookup"><span data-stu-id="7c8f4-161">6. Periodically check hello status and hello state of hello circuit key</span></span>

<span data-ttu-id="7c8f4-162">Vérification du statut de hello et état hello de clé du circuit hello vous permet de savoir quand votre fournisseur aura activé votre circuit.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-162">Checking hello status and hello state of hello circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="7c8f4-163">Après la configuration de circuit de hello, « ServiceProviderProvisioningState » s’affiche en tant que « Configuré », comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="7c8f4-163">After hello circuit has been configured, 'ServiceProviderProvisioningState' appears as 'Provisioned', as shown in hello following example:</span></span>

```azurecli
az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
```

<span data-ttu-id="7c8f4-164">réponse de Hello est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="7c8f4-164">hello response is similar toohello following example:</span></span>

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="7c8f4-165">7. Créer votre configuration de routage</span><span class="sxs-lookup"><span data-stu-id="7c8f4-165">7. Create your routing configuration</span></span>

<span data-ttu-id="7c8f4-166">Pour obtenir des instructions, consultez hello [circuit ExpressRoute de configuration de routage](howto-routing-cli.md) toocreate de l’article et modifier des homologations de circuit.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-166">For step-by-step instructions, see hello [ExpressRoute circuit routing configuration](howto-routing-cli.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c8f4-167">Ces instructions s’appliquent uniquement à toocircuits qui sont créés avec des fournisseurs de services qui offrent des services de couche 2 de connectivité.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-167">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="7c8f4-168">Si vous utilisez un fournisseur de services proposant des services gérés de couche 3 (généralement un VPN IP, comme MPLS), votre fournisseur de connectivité configure et gère le routage pour vous.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-168">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider configures and manages routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="7c8f4-169">8. Lier un circuit ExpressRoute de tooan réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="7c8f4-169">8. Link a virtual network tooan ExpressRoute circuit</span></span>

<span data-ttu-id="7c8f4-170">Ensuite, lier un circuit ExpressRoute de tooyour réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-170">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="7c8f4-171">Hello d’utilisation [liaison virtuel réseaux tooExpressRoute circuits](howto-linkvnet-cli.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-171">Use hello [Linking virtual networks tooExpressRoute circuits](howto-linkvnet-cli.md) article.</span></span>

## <span data-ttu-id="7c8f4-172"><a name="modify"></a>Modification d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7c8f4-172"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>

<span data-ttu-id="7c8f4-173">Vous pouvez modifier certaines propriétés d'un circuit ExpressRoute sans affecter la connectivité.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-173">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span> <span data-ttu-id="7c8f4-174">Vous pouvez apporter hello modifications sans interruption de service suivantes :</span><span class="sxs-lookup"><span data-stu-id="7c8f4-174">You can make hello following changes with no downtime:</span></span>

* <span data-ttu-id="7c8f4-175">Vous pouvez activer ou désactiver le module complémentaire ExpressRoute Premium pour votre circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-175">You can enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="7c8f4-176">Vous pouvez augmenter la bande passante hello de votre circuit ExpressRoute autant de capacité est disponible sur le port hello.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-176">You can increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="7c8f4-177">Toutefois, la bande passante hello d’un circuit de rétrogradation n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-177">However, downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="7c8f4-178">Vous pouvez modifier le plan de contrôle hello à partir de données de limitées tooUnlimited données.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-178">You can change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="7c8f4-179">Toutefois, la modification hello plan à partir de tooMetered données illimité que données ne sont pas prise en charge de contrôle.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-179">However, changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="7c8f4-180">Vous pouvez activer et désactiver *Autoriser les opérations classiques*.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-180">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="7c8f4-181">Pour plus d’informations sur les limites et limitations, consultez hello [FAQ sur ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="7c8f4-181">For more information on limits and limitations, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="7c8f4-182">module complémentaire de tooenable hello ExpressRoute premium</span><span class="sxs-lookup"><span data-stu-id="7c8f4-182">tooenable hello ExpressRoute premium add-on</span></span>

<span data-ttu-id="7c8f4-183">Vous pouvez activer un module complémentaire de hello ExpressRoute premium pour votre circuit existant à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7c8f4-183">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following command:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Premium
```

<span data-ttu-id="7c8f4-184">circuit de Hello dispose désormais des fonctionnalités d’un module complémentaire hello ExpressRoute premium activées.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-184">hello circuit now has hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="7c8f4-185">Commencer à vous de facturation pour la fonction d’un module complémentaire hello premium dès que la commande hello a été exécutée.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-185">We begin billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="7c8f4-186">module complémentaire de toodisable hello ExpressRoute premium</span><span class="sxs-lookup"><span data-stu-id="7c8f4-186">toodisable hello ExpressRoute premium add-on</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c8f4-187">Cette opération peut échouer si vous utilisez des ressources qui sont supérieures à ce qui est autorisé pour le circuit de standard hello.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-187">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

<span data-ttu-id="7c8f4-188">Avant de désactiver le module complémentaire de hello ExpressRoute premium, comprendre hello suivant des critères :</span><span class="sxs-lookup"><span data-stu-id="7c8f4-188">Before disabling hello ExpressRoute premium add-on, understand hello following criteria:</span></span>

* <span data-ttu-id="7c8f4-189">Avant de vous rétrogradez premium toostandard, il se peut que vous devez vous assurer que vous disposez de moins de 10 circuit toohello lié de réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-189">Before you downgrade from premium toostandard, you must make sure that you have fewer than 10 virtual networks linked toohello circuit.</span></span> <span data-ttu-id="7c8f4-190">S’il y en a plus de 10, votre demande de mise à jour échoue et nous appliquons les tarifs Premium.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-190">If you have more than 10, your update request fails, and we bill you at premium rates.</span></span>
* <span data-ttu-id="7c8f4-191">Vous devez dissocier tous les réseaux virtuels dans d'autres régions géopolitiques.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-191">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="7c8f4-192">Si vous ne le faites pas, votre demande de mise à jour échoue et nous appliquons les tarifs Premium.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-192">If you don't unlink all your virtual networks, your update request fails and we bill you at premium rates.</span></span>
* <span data-ttu-id="7c8f4-193">Pour l’homologation privée, votre table de routage doit comporter moins de 4 000 routages.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-193">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="7c8f4-194">Si la taille de la table de routage est supérieure à 4 000 itinéraires, la session BGP de hello supprime.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-194">If your route table size is greater than 4,000 routes, hello BGP session drops.</span></span> <span data-ttu-id="7c8f4-195">session de Hello ne sera pas être réactivée jusqu'à ce que le nombre de hello de préfixes publiés est inférieur à 4 000.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-195">hello session won't be reenabled until hello number of advertised prefixes is below 4,000.</span></span>

<span data-ttu-id="7c8f4-196">Vous pouvez désactiver complémentaire hello ExpressRoute pour le circuit existant de hello à l’aide de hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="7c8f4-196">You can disable hello ExpressRoute premium add-on for hello existing circuit by using hello following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Standard
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="7c8f4-197">bande passante du circuit ExpressRoute hello tooupdate</span><span class="sxs-lookup"><span data-stu-id="7c8f4-197">tooupdate hello ExpressRoute circuit bandwidth</span></span>

<span data-ttu-id="7c8f4-198">Pour les options de bande passante hello pris en charge pour le fournisseur, vérifiez hello [FAQ sur ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="7c8f4-198">For hello supported bandwidth options for your provider, check hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="7c8f4-199">Vous pouvez choisir n’importe quelle taille supérieure à la taille de hello de votre circuit existant.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-199">You can pick any size greater than hello size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c8f4-200">Si la capacité inadéquate est sur le port hello existant, vous avez peut-être circuit ExpressRoute de hello toorecreate.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-200">If there is inadequate capacity on hello existing port, you may have toorecreate hello ExpressRoute circuit.</span></span> <span data-ttu-id="7c8f4-201">Vous ne peut pas mettre à niveau de circuit de hello si aucune capacité supplémentaire n’est disponible à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-201">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="7c8f4-202">Vous ne pouvez pas réduire la bande passante hello d’un circuit ExpressRoute sans interruption de service.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-202">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="7c8f4-203">Rétrogradation de la bande passante nécessite vous toodeprovision hello circuit ExpressRoute et puis reconfigurez un circuit ExpressRoute de nouveau.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-203">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit, and then reprovision a new ExpressRoute circuit.</span></span>
>

<span data-ttu-id="7c8f4-204">Après avoir déterminé la taille de hello que vous avez besoin, utilisez hello suivant commande tooresize votre circuit :</span><span class="sxs-lookup"><span data-stu-id="7c8f4-204">After you decide hello size you need, use hello following command tooresize your circuit:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --bandwidth 1000
```

<span data-ttu-id="7c8f4-205">Votre circuit est dimensionnée côté de Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-205">Your circuit is sized up on hello Microsoft side.</span></span> <span data-ttu-id="7c8f4-206">Ensuite, vous devez contacter votre configurations tooupdate de fournisseur de connectivité sur leur toomatch côté cette modification.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-206">Next, you must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="7c8f4-207">Après avoir apporté cette notification, nous commençons à vous de facturation pour l’option de la bande passante hello mis à jour.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-207">After you make this notification, we begin billing you for hello updated bandwidth option.</span></span>

### <a name="toomove-hello-sku-from-metered-toounlimited"></a><span data-ttu-id="7c8f4-208">toomove hello référence (SKU) à partir de toounlimited limitée</span><span class="sxs-lookup"><span data-stu-id="7c8f4-208">toomove hello SKU from metered toounlimited</span></span>

<span data-ttu-id="7c8f4-209">Vous pouvez modifier hello référence (SKU) d’un circuit ExpressRoute à l’aide de hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="7c8f4-209">You can change hello SKU of an ExpressRoute circuit by using hello following example:</span></span>

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-family UnlimitedData
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a><span data-ttu-id="7c8f4-210">classique de toohello toocontrol accès et les environnements de gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="7c8f4-210">toocontrol access toohello classic and Resource Manager environments</span></span>

<span data-ttu-id="7c8f4-211">Passez en revue les instructions hello dans [circuits ExpressRoute de déplacer à partir du modèle de déploiement du Gestionnaire de ressources hello classique toohello](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="7c8f4-211">Review hello instructions in [Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="7c8f4-212">Annulation de l’approvisionnement et suppression d’un circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7c8f4-212">Deprovisioning and deleting an ExpressRoute circuit</span></span>

<span data-ttu-id="7c8f4-213">toodeprovision et supprimer un circuit ExpressRoute, assurez-vous que vous comprenez hello suivant des critères :</span><span class="sxs-lookup"><span data-stu-id="7c8f4-213">toodeprovision and delete an ExpressRoute circuit, make sure you understand hello following criteria:</span></span>

* <span data-ttu-id="7c8f4-214">Vous devez supprimer le lien de tous les réseaux virtuels à partir de hello circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-214">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="7c8f4-215">Si cette opération échoue, vérifiez toosee si les réseaux virtuels sont liés toohello circuit.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-215">If this operation fails, check toosee if any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="7c8f4-216">Si le fournisseur de service du circuit ExpressRoute hello état d’approvisionnement est **Provisioning** ou **configuré**, vous devez collaborer avec votre circuit de hello toodeprovision service fournisseur de leur côté.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-216">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned**, you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="7c8f4-217">Nous continuer tooreserve ressources et vous facturer jusqu'à ce que le fournisseur de services hello termine de circuit de hello désaffectation et nous avertit.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-217">We continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="7c8f4-218">Vous pouvez supprimer le circuit de hello si le fournisseur de services hello a annulé le circuit de hello.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-218">You can delete hello circuit if hello service provider has deprovisioned hello circuit.</span></span> <span data-ttu-id="7c8f4-219">Lorsqu’un circuit est annulé, fournisseur de services hello état d’approvisionnement est défini trop**non préparé**.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-219">When a circuit is deprovisioned, hello service provider provisioning state is set too**Not provisioned**.</span></span> <span data-ttu-id="7c8f4-220">Cela arrête la facturation pour le circuit de hello.</span><span class="sxs-lookup"><span data-stu-id="7c8f4-220">This stops billing for hello circuit.</span></span>

<span data-ttu-id="7c8f4-221">Vous pouvez supprimer votre circuit ExpressRoute en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7c8f4-221">You can delete your ExpressRoute circuit by running hello following command:</span></span>

```azurecli
az network express-route delete  -n MyCircuit -g ExpressRouteResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="7c8f4-222">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7c8f4-222">Next steps</span></span>

<span data-ttu-id="7c8f4-223">Après avoir créé votre circuit, assurez-vous que vous hello tâche suivantes :</span><span class="sxs-lookup"><span data-stu-id="7c8f4-223">After you create your circuit, make sure that you do hello following tasks:</span></span>

* [<span data-ttu-id="7c8f4-224">Créer et modifier le routage le routage pour votre circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7c8f4-224">Create and modify routing for your ExpressRoute circuit</span></span>](howto-routing-cli.md)
* [<span data-ttu-id="7c8f4-225">Lier votre réseau virtuel de tooyour circuit ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="7c8f4-225">Link your virtual network tooyour ExpressRoute circuit</span></span>](howto-linkvnet-cli.md)
