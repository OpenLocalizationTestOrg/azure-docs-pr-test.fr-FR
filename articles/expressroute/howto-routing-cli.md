---
title: "Comment tooconfigure routage pour un circuit ExpressRoute de Azure : CLI | Documents Microsoft"
description: "Cet article vous permet de créer et de configurer l’homologation Microsoft d’un circuit ExpressRoute de hello privé et public. Cet article vous explique également comment toocheck état de hello, mettre à jour ou supprimer des homologations pour votre circuit."
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
ms.date: 07/31/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 33130af050045527cdb316e77821c6d101b6a82a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a><span data-ttu-id="da176-104">Créer et modifier le routage d’un circuit ExpressRoute à l’aide de l’interface CLI</span><span class="sxs-lookup"><span data-stu-id="da176-104">Create and modify routing for an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="da176-105">Cet article vous aide à créer et gérer la configuration de routage pour un circuit ExpressRoute de modèle de déploiement de gestionnaire de ressources hello à l’aide de CLI.</span><span class="sxs-lookup"><span data-stu-id="da176-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using CLI.</span></span> <span data-ttu-id="da176-106">Vous pouvez également vérifier l’état de hello, update ou delete et annuler le déploiement homologations pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="da176-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="da176-107">Si vous souhaitez toouse une autre méthode de toowork avec votre circuit, sélectionnez un article à partir de hello suivant liste :</span><span class="sxs-lookup"><span data-stu-id="da176-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="da176-108">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="da176-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="da176-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="da176-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="da176-110">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="da176-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="da176-111">Vidéo - Homologation privée</span><span class="sxs-lookup"><span data-stu-id="da176-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="da176-112">Vidéo - Homologation publique</span><span class="sxs-lookup"><span data-stu-id="da176-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="da176-113">Vidéo - Homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="da176-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="da176-114">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="da176-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="da176-115">Conditions préalables à la configuration</span><span class="sxs-lookup"><span data-stu-id="da176-115">Configuration prerequisites</span></span>

* <span data-ttu-id="da176-116">Avant de commencer, installez hello dernière version des commandes CLI de hello (version 2.0 ou version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="da176-116">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="da176-117">Pour plus d’informations sur l’installation des commandes CLI de hello, consultez [installer Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="da176-117">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="da176-118">Assurez-vous que vous avez consulté hello [conditions préalables](expressroute-prerequisites.md), [exigences routage](expressroute-routing.md), et [workflow](expressroute-workflows.md) avant de commencer la configuration des pages.</span><span class="sxs-lookup"><span data-stu-id="da176-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflow](expressroute-workflows.md) pages before you begin configuration.</span></span>
* <span data-ttu-id="da176-119">Vous devez disposer d’un circuit ExpressRoute actif.</span><span class="sxs-lookup"><span data-stu-id="da176-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="da176-120">Suivez les instructions de hello trop[créer un circuit ExpressRoute](howto-circuit-cli.md) et circuit hello activé par votre fournisseur de connectivité avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="da176-120">Follow hello instructions too[Create an ExpressRoute circuit](howto-circuit-cli.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="da176-121">Hello circuit ExpressRoute doit être dans un état configuré et activé pour vous, les commandes de hello toobe toorun en mesure de cet article.</span><span class="sxs-lookup"><span data-stu-id="da176-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello commands in this article.</span></span>

<span data-ttu-id="da176-122">Ces instructions s’appliquent uniquement à toocircuits créé avec les fournisseurs de services offrant des services de connectivité de couche 2.</span><span class="sxs-lookup"><span data-stu-id="da176-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="da176-123">Si vous utilisez un fournisseur de services proposant des services gérés de couche 3 (généralement un VPN IP, comme MPLS), votre fournisseur de connectivité configure et gère le routage pour vous.</span><span class="sxs-lookup"><span data-stu-id="da176-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

<span data-ttu-id="da176-124">Vous pouvez configurer une, deux ou les trois homologations (privée Azure, publique Azure et Microsoft) pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="da176-124">You can configure one, two, or all three peerings (Azure private, Azure public, and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="da176-125">Vous pouvez configurer les homologations dans l’ordre de votre choix.</span><span class="sxs-lookup"><span data-stu-id="da176-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="da176-126">Toutefois, il se peut que vous devez vous assurer que vous terminez configuration hello de chacun d’eux à la fois d’homologation.</span><span class="sxs-lookup"><span data-stu-id="da176-126">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="da176-127">Homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="da176-127">Azure private peering</span></span>

<span data-ttu-id="da176-128">Cette section vous permet de créer, obtenir, mettre à jour et supprimer hello Azure configuration d’homologation privée pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="da176-128">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="da176-129">toocreate l’homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="da176-129">toocreate Azure private peering</span></span>

1. <span data-ttu-id="da176-130">Installer la version la plus récente de Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="da176-130">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="da176-131">Vous devez utiliser la version la plus récente hello Hello Azure Interface de ligne de commande (CLI). * hello de révision [conditions préalables](expressroute-prerequisites.md) et [workflows](expressroute-workflows.md) avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="da176-131">You must use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="da176-132">Sélectionnez abonnement hello circuit ExpressRoute de toocreate</span><span class="sxs-lookup"><span data-stu-id="da176-132">Select hello subscription you want toocreate ExpressRoute circuit</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="da176-133">Créez un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="da176-133">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="da176-134">Suivez hello instructions toocreate un [circuit ExpressRoute](howto-circuit-cli.md) et configuré par le fournisseur de connectivité hello.</span><span class="sxs-lookup"><span data-stu-id="da176-134">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="da176-135">Si votre fournisseur de connectivité propose des services de couche 3 gérés, vous pouvez demander votre tooenable de fournisseur de connectivité Azure privé d’homologation pour vous.</span><span class="sxs-lookup"><span data-stu-id="da176-135">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="da176-136">Dans ce cas, vous n’aurez toofollow les instructions figurant dans les sections suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="da176-136">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="da176-137">Toutefois, si votre fournisseur de connectivité ne gère pas le routage, après avoir créé votre circuit, continuer votre configuration à l’aide des étapes hello.</span><span class="sxs-lookup"><span data-stu-id="da176-137">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="da176-138">Vérifiez hello ExpressRoute circuit toomake qu’il est configuré et activé également.</span><span class="sxs-lookup"><span data-stu-id="da176-138">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="da176-139">Utilisez hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="da176-139">Use hello following example:</span></span>

  ```azurecli
  az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
  ```

  <span data-ttu-id="da176-140">réponse de Hello est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="da176-140">hello response is similar toohello following example:</span></span>

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="da176-141">Configurer une homologation privée Azure pour le circuit de hello.</span><span class="sxs-lookup"><span data-stu-id="da176-141">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="da176-142">Assurez-vous que vous disposez des éléments suivants avant de passer aux étapes suivantes de hello de hello :</span><span class="sxs-lookup"><span data-stu-id="da176-142">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="da176-143">/ 30 sous-réseau pour le lien principal de hello.</span><span class="sxs-lookup"><span data-stu-id="da176-143">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="da176-144">sous-réseau de Hello ne doit pas faire partie d’un espace d’adressage réservé pour les réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="da176-144">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="da176-145">/ 30 sous-réseau pour le lien secondaire de hello.</span><span class="sxs-lookup"><span data-stu-id="da176-145">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="da176-146">sous-réseau de Hello ne doit pas faire partie d’un espace d’adressage réservé pour les réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="da176-146">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="da176-147">Un tooestablish ID de VLAN valide cette homologation sur.</span><span class="sxs-lookup"><span data-stu-id="da176-147">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="da176-148">Ne vérifiez qu’aucune autre homologation dans le circuit de hello utilise hello même ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="da176-148">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="da176-149">Un numéro AS pour l'homologation.</span><span class="sxs-lookup"><span data-stu-id="da176-149">AS number for peering.</span></span> <span data-ttu-id="da176-150">Vous pouvez utiliser des numéros à 2 et 4 octets.</span><span class="sxs-lookup"><span data-stu-id="da176-150">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="da176-151">Vous pouvez utiliser un numéro AS privé pour cette homologation.</span><span class="sxs-lookup"><span data-stu-id="da176-151">You can use a private AS number for this peering.</span></span> <span data-ttu-id="da176-152">Veillez à ne pas utiliser le numéro 65515.</span><span class="sxs-lookup"><span data-stu-id="da176-152">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="da176-153">**Facultatif :** un hachage MD5 si vous choisissez toouse une.</span><span class="sxs-lookup"><span data-stu-id="da176-153">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="da176-154">Utilisez hello suivant exemple tooconfigure Azure privé d’homologation pour votre circuit :</span><span class="sxs-lookup"><span data-stu-id="da176-154">Use hello following example tooconfigure Azure private peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  <span data-ttu-id="da176-155">Si vous choisissez toouse un hachage MD5, utilisez hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="da176-155">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="da176-156">Veillez à spécifier votre numéro AS comme ASN d’homologation et non pas comme ASN client.</span><span class="sxs-lookup"><span data-stu-id="da176-156">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  > 

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="da176-157">tooview Azure privé d’homologation détails</span><span class="sxs-lookup"><span data-stu-id="da176-157">tooview Azure private peering details</span></span>

<span data-ttu-id="da176-158">Vous pouvez obtenir les détails de configuration à l’aide de hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="da176-158">You can get configuration details by using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

<span data-ttu-id="da176-159">Hello la sortie est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="da176-159">hello output is similar toohello following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePrivatePeering",
  "ipv6PeeringConfig": null,
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePrivatePeering",
  "peerAsn": 7671,
  "peeringType": "AzurePrivatePeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="da176-160">tooupdate configuration d’homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="da176-160">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="da176-161">Vous pouvez mettre à jour une partie de la configuration de hello à l’aide de hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="da176-161">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="da176-162">Dans cet exemple, hello ID de VLAN de circuit de hello est mise à jour à partir de 100 too500.</span><span class="sxs-lookup"><span data-stu-id="da176-162">In this example, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="da176-163">toodelete l’homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="da176-163">toodelete Azure private peering</span></span>

<span data-ttu-id="da176-164">Vous pouvez supprimer votre configuration d’homologation en exécutant hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="da176-164">You can remove your peering configuration by running hello following example:</span></span>

> [!WARNING]
> <span data-ttu-id="da176-165">Vous devez vous assurer que tous les réseaux virtuels sont dissocier hello circuit ExpressRoute avant d’exécuter cet exemple.</span><span class="sxs-lookup"><span data-stu-id="da176-165">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this example.</span></span> 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a><span data-ttu-id="da176-166">Homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="da176-166">Azure public peering</span></span>

<span data-ttu-id="da176-167">Cette section vous permet de créer, obtenir, mettre à jour et supprimer hello configuration d’homologation publique Azure pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="da176-167">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="da176-168">toocreate l’homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="da176-168">toocreate Azure public peering</span></span>

1. <span data-ttu-id="da176-169">Installer la version la plus récente de Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="da176-169">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="da176-170">Vous devez utiliser la version la plus récente hello Hello Azure Interface de ligne de commande (CLI). * hello de révision [conditions préalables](expressroute-prerequisites.md) et [workflows](expressroute-workflows.md) avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="da176-170">You must use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="da176-171">Sélectionnez l’abonnement hello pour lequel vous souhaitez le circuit ExpressRoute de toocreate.</span><span class="sxs-lookup"><span data-stu-id="da176-171">Select hello subscription for which you want toocreate ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="da176-172">Créez un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="da176-172">Create an ExpressRoute circuit.</span></span>  <span data-ttu-id="da176-173">Suivez hello instructions toocreate un [circuit ExpressRoute](howto-circuit-cli.md) et configuré par le fournisseur de connectivité hello.</span><span class="sxs-lookup"><span data-stu-id="da176-173">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="da176-174">Si votre fournisseur de connectivité propose des services gérés de couche 3, vous pouvez lui demander d’activer l’homologation privée Azure pour vous.</span><span class="sxs-lookup"><span data-stu-id="da176-174">If your connectivity provider offers managed Layer 3 services, you can request that your connectivity provider enables Azure private peering for you.</span></span> <span data-ttu-id="da176-175">Dans ce cas, vous n’aurez toofollow les instructions figurant dans les sections suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="da176-175">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="da176-176">Toutefois, si votre fournisseur de connectivité ne gère pas le routage, après avoir créé votre circuit, continuer votre configuration à l’aide des étapes hello.</span><span class="sxs-lookup"><span data-stu-id="da176-176">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="da176-177">Vérifiez tooensure de circuit ExpressRoute hello il est configuré et activé également.</span><span class="sxs-lookup"><span data-stu-id="da176-177">Check hello ExpressRoute circuit tooensure it is provisioned and also enabled.</span></span> <span data-ttu-id="da176-178">Utilisez hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="da176-178">Use hello following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="da176-179">réponse de Hello est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="da176-179">hello response is similar toohello following example:</span></span>

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="da176-180">Configurer l’homologation publique Azure pour le circuit de hello.</span><span class="sxs-lookup"><span data-stu-id="da176-180">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="da176-181">Assurez-vous que vous disposez des informations suivantes avant de continuer davantage de hello.</span><span class="sxs-lookup"><span data-stu-id="da176-181">Make sure that you have hello following information before you proceed further.</span></span>

  * <span data-ttu-id="da176-182">/ 30 sous-réseau pour le lien principal de hello.</span><span class="sxs-lookup"><span data-stu-id="da176-182">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="da176-183">Ce doit être un préfixe IPv4 public valide.</span><span class="sxs-lookup"><span data-stu-id="da176-183">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="da176-184">/ 30 sous-réseau pour le lien secondaire de hello.</span><span class="sxs-lookup"><span data-stu-id="da176-184">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="da176-185">Ce doit être un préfixe IPv4 public valide.</span><span class="sxs-lookup"><span data-stu-id="da176-185">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="da176-186">Un tooestablish ID de VLAN valide cette homologation sur.</span><span class="sxs-lookup"><span data-stu-id="da176-186">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="da176-187">Ne vérifiez qu’aucune autre homologation dans le circuit de hello utilise hello même ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="da176-187">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="da176-188">Un numéro AS pour l'homologation.</span><span class="sxs-lookup"><span data-stu-id="da176-188">AS number for peering.</span></span> <span data-ttu-id="da176-189">Vous pouvez utiliser des numéros à 2 et 4 octets.</span><span class="sxs-lookup"><span data-stu-id="da176-189">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="da176-190">**Facultatif :** un hachage MD5 si vous choisissez toouse une.</span><span class="sxs-lookup"><span data-stu-id="da176-190">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="da176-191">Exécutez hello suivant exemple tooconfigure Azure public d’homologation pour votre circuit :</span><span class="sxs-lookup"><span data-stu-id="da176-191">Run hello following example tooconfigure Azure public peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  <span data-ttu-id="da176-192">Si vous choisissez toouse un hachage MD5, utilisez hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="da176-192">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="da176-193">Veillez à spécifier votre numéro AS comme ASN d’homologation et non pas comme ASN client.</span><span class="sxs-lookup"><span data-stu-id="da176-193">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="da176-194">tooview Azure public d’homologation détails</span><span class="sxs-lookup"><span data-stu-id="da176-194">tooview Azure public peering details</span></span>

<span data-ttu-id="da176-195">Vous pouvez obtenir les détails de configuration à l’aide de hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="da176-195">You can get configuration details using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

<span data-ttu-id="da176-196">Hello la sortie est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="da176-196">hello output is similar toohello following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePublicPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePublicPeering",
  "peerAsn": 7671,
  "peeringType": "AzurePublicPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="da176-197">tooupdate configuration d’homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="da176-197">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="da176-198">Vous pouvez mettre à jour une partie de la configuration de hello à l’aide de hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="da176-198">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="da176-199">Dans cet exemple, hello ID de VLAN de circuit de hello est mise à jour à partir de too600 200.</span><span class="sxs-lookup"><span data-stu-id="da176-199">In this example, hello VLAN ID of hello circuit is being updated from 200 too600.</span></span>

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="da176-200">toodelete l’homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="da176-200">toodelete Azure public peering</span></span>

<span data-ttu-id="da176-201">Vous pouvez supprimer votre configuration d’homologation en exécutant hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="da176-201">You can remove your peering configuration by running hello following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a><span data-ttu-id="da176-202">Homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="da176-202">Microsoft peering</span></span>

<span data-ttu-id="da176-203">Cette section vous permet de créer, obtenir, mettre à jour et supprimer la configuration d’homologation Microsoft hello pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="da176-203">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="da176-204">Homologation Microsoft des circuits ExpressRoute qui ont été configurés préalable tooAugust 1, 2017 aura tous les préfixes de service publiés par le biais d’homologation de Microsoft hello, même si les filtres de routage ne sont pas définis.</span><span class="sxs-lookup"><span data-stu-id="da176-204">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="da176-205">Homologation Microsoft des circuits ExpressRoute qui sont configurés sur ou après le 1er août 2017 n’aura pas de préfixes publiés jusqu'à ce qu’un filtre de routage est attaché toohello circuit.</span><span class="sxs-lookup"><span data-stu-id="da176-205">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="da176-206">Pour plus d’informations, consultez [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md) (Configurer un filtre d’itinéraire pour l’homologation Microsoft).</span><span class="sxs-lookup"><span data-stu-id="da176-206">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="da176-207">l’homologation de Microsoft toocreate</span><span class="sxs-lookup"><span data-stu-id="da176-207">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="da176-208">Installer la version la plus récente de Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="da176-208">Install hello latest version of Azure CLI.</span></span> <span data-ttu-id="da176-209">Utiliser hello la dernière version de hello Azure Interface de ligne de commande (CLI). * hello de révision [conditions préalables](expressroute-prerequisites.md) et [workflows](expressroute-workflows.md) avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="da176-209">Use hello latest version of hello Azure Command-line Interface (CLI).* Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="da176-210">Sélectionnez l’abonnement hello pour lequel vous souhaitez le circuit ExpressRoute de toocreate.</span><span class="sxs-lookup"><span data-stu-id="da176-210">Select hello subscription for which you want toocreate ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="da176-211">Créez un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="da176-211">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="da176-212">Suivez hello instructions toocreate un [circuit ExpressRoute](howto-circuit-cli.md) et configuré par le fournisseur de connectivité hello.</span><span class="sxs-lookup"><span data-stu-id="da176-212">Follow hello instructions toocreate an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="da176-213">Si votre fournisseur de connectivité propose des services de couche 3 gérés, vous pouvez demander votre tooenable de fournisseur de connectivité Azure privé d’homologation pour vous.</span><span class="sxs-lookup"><span data-stu-id="da176-213">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="da176-214">Dans ce cas, vous n’aurez toofollow les instructions figurant dans les sections suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="da176-214">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="da176-215">Toutefois, si votre fournisseur de connectivité ne gère pas le routage, après avoir créé votre circuit, continuer votre configuration à l’aide des étapes hello.</span><span class="sxs-lookup"><span data-stu-id="da176-215">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>

3. <span data-ttu-id="da176-216">Vérifiez hello ExpressRoute circuit toomake qu’il est configuré et activé également.</span><span class="sxs-lookup"><span data-stu-id="da176-216">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="da176-217">Utilisez hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="da176-217">Use hello following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="da176-218">réponse de Hello est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="da176-218">hello response is similar toohello following example:</span></span>

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. <span data-ttu-id="da176-219">Configurez Microsoft d’homologation pour le circuit de hello.</span><span class="sxs-lookup"><span data-stu-id="da176-219">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="da176-220">Assurez-vous que vous avez hello suivant informations avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="da176-220">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="da176-221">/ 30 sous-réseau pour le lien principal de hello.</span><span class="sxs-lookup"><span data-stu-id="da176-221">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="da176-222">Il doit s’agir d’un préfixe IPv4 public valide vous appartenant et enregistré dans un registre RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="da176-222">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="da176-223">/ 30 sous-réseau pour le lien secondaire de hello.</span><span class="sxs-lookup"><span data-stu-id="da176-223">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="da176-224">Il doit s’agir d’un préfixe IPv4 public valide vous appartenant et enregistré dans un registre RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="da176-224">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="da176-225">Un tooestablish ID de VLAN valide cette homologation sur.</span><span class="sxs-lookup"><span data-stu-id="da176-225">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="da176-226">Ne vérifiez qu’aucune autre homologation dans le circuit de hello utilise hello même ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="da176-226">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="da176-227">Un numéro AS pour l'homologation.</span><span class="sxs-lookup"><span data-stu-id="da176-227">AS number for peering.</span></span> <span data-ttu-id="da176-228">Vous pouvez utiliser des numéros à 2 et 4 octets.</span><span class="sxs-lookup"><span data-stu-id="da176-228">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="da176-229">Publié préfixes : vous devez fournir une liste de tous les préfixes que vous prévoyez tooadvertise sur la session BGP de hello.</span><span class="sxs-lookup"><span data-stu-id="da176-229">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="da176-230">Seuls les préfixes d'adresses IP publiques sont acceptés.</span><span class="sxs-lookup"><span data-stu-id="da176-230">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="da176-231">Si vous envisagez un jeu de préfixes de toosend, vous pouvez envoyer une liste séparée par des virgules.</span><span class="sxs-lookup"><span data-stu-id="da176-231">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="da176-232">Ces préfixes doivent être inscrit tooyou dans un RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="da176-232">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="da176-233">**Facultatif :** client ASN : Si vous ne les préfixes de publicité qui ne sont pas inscrit toohello d’homologation en tant que nombre, vous pouvez spécifier hello en tant que nombre toowhich ils sont inscrits.</span><span class="sxs-lookup"><span data-stu-id="da176-233">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="da176-234">Nom de Registre de routage : Vous pouvez spécifier hello RIR / IRR contre le hello comme nombre et les préfixes sont inscrits.</span><span class="sxs-lookup"><span data-stu-id="da176-234">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="da176-235">**Facultatif :** un hachage MD5 si vous choisissez toouse une.</span><span class="sxs-lookup"><span data-stu-id="da176-235">**Optional -** An MD5 hash if you choose toouse one.</span></span>

   <span data-ttu-id="da176-236">Exécutez hello suivant exemple tooconfigure Microsoft homologation pour votre circuit :</span><span class="sxs-lookup"><span data-stu-id="da176-236">Run hello following example tooconfigure Microsoft peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="tooget-microsoft-peering-details"></a><span data-ttu-id="da176-237">informations d’homologation de tooget Microsoft</span><span class="sxs-lookup"><span data-stu-id="da176-237">tooget Microsoft peering details</span></span>

<span data-ttu-id="da176-238">Vous pouvez obtenir les détails de configuration à l’aide de hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="da176-238">You can get configuration details by using hello following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

<span data-ttu-id="da176-239">Hello la sortie est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="da176-239">hello output is similar toohello following example:</span></span>

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzureMicrosoftPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": {
    "advertisedPublicPrefixes": [
        ""
      ],
     "advertisedPublicPrefixesState": "",
     "customerASN": ,
     "routingRegistryName": ""
  }
  "name": "AzureMicrosoftPeering",
  "peerAsn": ,
  "peeringType": "AzureMicrosoftPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="da176-240">configuration d’homologation de tooupdate Microsoft</span><span class="sxs-lookup"><span data-stu-id="da176-240">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="da176-241">Vous pouvez mettre à jour n’importe quelle partie de la configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="da176-241">You can update any part of hello configuration.</span></span> <span data-ttu-id="da176-242">Hello publiés préfixes de circuit de hello sont mis à jour à partir de too124.1.0.0/24 123.1.0.0/24 Bonjour l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="da176-242">hello advertised prefixes of hello circuit are being updated from 123.1.0.0/24 too124.1.0.0/24 in hello following example:</span></span>

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="da176-243">l’homologation de Microsoft toodelete</span><span class="sxs-lookup"><span data-stu-id="da176-243">toodelete Microsoft peering</span></span>

<span data-ttu-id="da176-244">Vous pouvez supprimer votre configuration d’homologation en exécutant hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="da176-244">You can remove your peering configuration by running hello following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a><span data-ttu-id="da176-245">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="da176-245">Next steps</span></span>

<span data-ttu-id="da176-246">Étape suivante, [lier un circuit ExpressRoute de tooan réseau virtuel](howto-linkvnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="da176-246">Next step, [Link a VNet tooan ExpressRoute circuit](howto-linkvnet-cli.md).</span></span>

* <span data-ttu-id="da176-247">Pour plus d'informations sur les workflows ExpressRoute, consultez [Workflows ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="da176-247">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="da176-248">Pour plus d’informations sur l’homologation du circuit, consultez [Circuits ExpressRoute et domaines de routage](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="da176-248">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="da176-249">Pour plus d’informations sur l’utilisation des réseaux virtuels, consultez la page [Présentation du réseau virtuel](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="da176-249">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>