---
title: "Configuration du routage d’un circuit Azure ExpressRoute avec l’interface CLI | Microsoft Docs"
description: "Cet article est conçu pour vous aider à créer et à approvisionner l’homologation privée, publique et Microsoft d’un circuit ExpressRoute. Cet article vous montre également comment vérifier l'état, mettre à jour ou supprimer des homologations pour votre circuit."
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
ms.openlocfilehash: fbf0bd9a139c22bbd63755f6df445f6596aaccc5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a><span data-ttu-id="ae30d-104">Créer et modifier le routage d’un circuit ExpressRoute à l’aide de l’interface CLI</span><span class="sxs-lookup"><span data-stu-id="ae30d-104">Create and modify routing for an ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="ae30d-105">Cet article est conçu pour vous aider à créer et à gérer la configuration du routage d’un circuit ExpressRoute dans le modèle de déploiement Resource Manager à l’aide de l’interface CLI.</span><span class="sxs-lookup"><span data-stu-id="ae30d-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using CLI.</span></span> <span data-ttu-id="ae30d-106">Vous pouvez également vérifier l’état, mettre à jour ou supprimer et déprovisionner des homologations d’un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ae30d-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="ae30d-107">Si vous souhaitez utiliser une autre méthode pour votre circuit, sélectionnez un article dans la liste suivante :</span><span class="sxs-lookup"><span data-stu-id="ae30d-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ae30d-108">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="ae30d-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="ae30d-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae30d-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="ae30d-110">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="ae30d-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="ae30d-111">Vidéo - Homologation privée</span><span class="sxs-lookup"><span data-stu-id="ae30d-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="ae30d-112">Vidéo - Homologation publique</span><span class="sxs-lookup"><span data-stu-id="ae30d-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="ae30d-113">Vidéo - Homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="ae30d-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="ae30d-114">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="ae30d-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="ae30d-115">Conditions préalables à la configuration</span><span class="sxs-lookup"><span data-stu-id="ae30d-115">Configuration prerequisites</span></span>

* <span data-ttu-id="ae30d-116">Avant de commencer, installez la dernière version des commandes CLI (version 2.0 ou ultérieure).</span><span class="sxs-lookup"><span data-stu-id="ae30d-116">Before beginning, install the latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="ae30d-117">Pour plus d’informations sur l’installation des commandes CLI consultez l’article [Installer l’interface de ligne de commande Azure 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ae30d-117">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="ae30d-118">Veillez à consulter les articles relatifs à la [configuration requise pour ExpressRoute](expressroute-prerequisites.md), à la [configuration requise pour le routage](expressroute-routing.md) et aux [workflows](expressroute-workflows.md) avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="ae30d-118">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflow](expressroute-workflows.md) pages before you begin configuration.</span></span>
* <span data-ttu-id="ae30d-119">Vous devez disposer d’un circuit ExpressRoute actif.</span><span class="sxs-lookup"><span data-stu-id="ae30d-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="ae30d-120">Suivez les instructions permettant de [créer un circuit ExpressRoute](howto-circuit-cli.md) et faites-le activer par votre fournisseur de connectivité avant de poursuivre.</span><span class="sxs-lookup"><span data-stu-id="ae30d-120">Follow the instructions to [Create an ExpressRoute circuit](howto-circuit-cli.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="ae30d-121">Le circuit ExpressRoute doit être dans un état approvisionné et activé pour être en mesure d’exécuter les commandes de cet article.</span><span class="sxs-lookup"><span data-stu-id="ae30d-121">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the commands in this article.</span></span>

<span data-ttu-id="ae30d-122">Ces instructions s'appliquent uniquement aux circuits créés avec des fournisseurs de services proposant des services de connectivité de couche 2.</span><span class="sxs-lookup"><span data-stu-id="ae30d-122">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="ae30d-123">Si vous utilisez un fournisseur de services proposant des services gérés de couche 3 (généralement un VPN IP, comme MPLS), votre fournisseur de connectivité configure et gère le routage pour vous.</span><span class="sxs-lookup"><span data-stu-id="ae30d-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

<span data-ttu-id="ae30d-124">Vous pouvez configurer une, deux ou les trois homologations (privée Azure, publique Azure et Microsoft) pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ae30d-124">You can configure one, two, or all three peerings (Azure private, Azure public, and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="ae30d-125">Vous pouvez configurer les homologations dans l’ordre de votre choix.</span><span class="sxs-lookup"><span data-stu-id="ae30d-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="ae30d-126">Toutefois, vous devez veiller à finaliser une par une la configuration de chaque homologation.</span><span class="sxs-lookup"><span data-stu-id="ae30d-126">However, you must make sure that you complete the configuration of each peering one at a time.</span></span>

## <a name="azure-private-peering"></a><span data-ttu-id="ae30d-127">Homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="ae30d-127">Azure private peering</span></span>

<span data-ttu-id="ae30d-128">Cette section explique comment créer, obtenir, mettre à jour et supprimer la configuration d’homologation privée Azure pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ae30d-128">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="ae30d-129">Pour créer une homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="ae30d-129">To create Azure private peering</span></span>

1. <span data-ttu-id="ae30d-130">Installez la dernière version de l’interface Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ae30d-130">Install the latest version of Azure CLI.</span></span> <span data-ttu-id="ae30d-131">Vous devez utiliser la dernière version de l’interface de ligne de commande (CLI) Azure.* Prenez connaissance de la [configuration requise](expressroute-prerequisites.md) et des [workflows](expressroute-workflows.md) avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="ae30d-131">You must use the latest version of the Azure Command-line Interface (CLI).* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="ae30d-132">Sélectionnez l’abonnement pour lequel vous souhaitez créer le circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ae30d-132">Select the subscription you want to create ExpressRoute circuit</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="ae30d-133">Créez un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ae30d-133">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="ae30d-134">Suivez les instructions permettant de [créer un circuit ExpressRoute](howto-circuit-cli.md) et faites-le approvisionner par votre fournisseur de connectivité.</span><span class="sxs-lookup"><span data-stu-id="ae30d-134">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="ae30d-135">Si votre fournisseur de connectivité propose des services gérés de couche 3, vous pouvez lui demander d’activer l'homologation privée Azure pour vous.</span><span class="sxs-lookup"><span data-stu-id="ae30d-135">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="ae30d-136">Dans ce cas, vous n'aurez pas besoin de suivre les instructions indiquées dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="ae30d-136">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="ae30d-137">Toutefois, si votre fournisseur de connectivité ne gère pas le routage pour vous, après avoir créé votre circuit, continuez la configuration à l’aide de la procédure qui suit.</span><span class="sxs-lookup"><span data-stu-id="ae30d-137">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="ae30d-138">Vérifiez que le circuit ExpressRoute est approvisionné et activé.</span><span class="sxs-lookup"><span data-stu-id="ae30d-138">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="ae30d-139">Consultez l’exemple qui suit :</span><span class="sxs-lookup"><span data-stu-id="ae30d-139">Use the following example:</span></span>

  ```azurecli
  az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
  ```

  <span data-ttu-id="ae30d-140">La réponse ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="ae30d-140">The response is similar to the following example:</span></span>

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

4. <span data-ttu-id="ae30d-141">Configurez l'homologation privée Azure pour le circuit.</span><span class="sxs-lookup"><span data-stu-id="ae30d-141">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="ae30d-142">Assurez-vous de disposer des éléments suivants avant de procéder aux étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="ae30d-142">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="ae30d-143">Un sous-réseau /30 pour le lien principal.</span><span class="sxs-lookup"><span data-stu-id="ae30d-143">A /30 subnet for the primary link.</span></span> <span data-ttu-id="ae30d-144">Le sous-réseau ne doit faire partie d’aucun espace d’adressage réservé aux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="ae30d-144">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="ae30d-145">Un sous-réseau /30 pour le lien secondaire.</span><span class="sxs-lookup"><span data-stu-id="ae30d-145">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="ae30d-146">Le sous-réseau ne doit faire partie d’aucun espace d’adressage réservé aux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="ae30d-146">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="ae30d-147">Un ID VLAN valide pour établir cette homologation.</span><span class="sxs-lookup"><span data-stu-id="ae30d-147">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="ae30d-148">Assurez-vous qu'aucune autre homologation sur le circuit n'utilise le même ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="ae30d-148">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="ae30d-149">Un numéro AS pour l'homologation.</span><span class="sxs-lookup"><span data-stu-id="ae30d-149">AS number for peering.</span></span> <span data-ttu-id="ae30d-150">Vous pouvez utiliser des numéros à 2 et 4 octets.</span><span class="sxs-lookup"><span data-stu-id="ae30d-150">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="ae30d-151">Vous pouvez utiliser un numéro AS privé pour cette homologation.</span><span class="sxs-lookup"><span data-stu-id="ae30d-151">You can use a private AS number for this peering.</span></span> <span data-ttu-id="ae30d-152">Veillez à ne pas utiliser le numéro 65515.</span><span class="sxs-lookup"><span data-stu-id="ae30d-152">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="ae30d-153">**(Facultatif)** Un hachage MD5 si vous choisissez d’en utiliser un.</span><span class="sxs-lookup"><span data-stu-id="ae30d-153">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="ae30d-154">Utilisez l’exemple suivant pour configurer l’homologation privée Azure pour votre circuit :</span><span class="sxs-lookup"><span data-stu-id="ae30d-154">Use the following example to configure Azure private peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  <span data-ttu-id="ae30d-155">Si vous choisissez d’utiliser un hachage MD5, exécutez l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="ae30d-155">If you choose to use an MD5 hash, use the following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="ae30d-156">Veillez à spécifier votre numéro AS comme ASN d’homologation et non pas comme ASN client.</span><span class="sxs-lookup"><span data-stu-id="ae30d-156">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  > 

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="ae30d-157">Pour afficher les détails d’une homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="ae30d-157">To view Azure private peering details</span></span>

<span data-ttu-id="ae30d-158">Vous pouvez obtenir les détails de la configuration à l’aide de l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="ae30d-158">You can get configuration details by using the following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

<span data-ttu-id="ae30d-159">Le résultat ressemble à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="ae30d-159">The output is similar to the following example:</span></span>

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

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="ae30d-160">Pour mettre à jour la configuration d'homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="ae30d-160">To update Azure private peering configuration</span></span>

<span data-ttu-id="ae30d-161">Vous pouvez mettre à jour toute partie de la configuration à l’aide de l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="ae30d-161">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="ae30d-162">Dans cet exemple, l’ID VLAN du circuit est mis à jour de 100 à 500.</span><span class="sxs-lookup"><span data-stu-id="ae30d-162">In this example, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="ae30d-163">Pour supprimer une homologation privée Azure</span><span class="sxs-lookup"><span data-stu-id="ae30d-163">To delete Azure private peering</span></span>

<span data-ttu-id="ae30d-164">Vous pouvez supprimer votre configuration d’homologation en exécutant l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="ae30d-164">You can remove your peering configuration by running the following example:</span></span>

> [!WARNING]
> <span data-ttu-id="ae30d-165">Vous devez vous assurer que tous les réseaux virtuels sont dissociés du circuit ExpressRoute avant d’exécuter cet exemple.</span><span class="sxs-lookup"><span data-stu-id="ae30d-165">You must ensure that all virtual networks are unlinked from the ExpressRoute circuit before running this example.</span></span> 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a><span data-ttu-id="ae30d-166">Homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="ae30d-166">Azure public peering</span></span>

<span data-ttu-id="ae30d-167">Cette section explique comment créer, obtenir, mettre à jour et supprimer la configuration d’homologation publique Azure pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ae30d-167">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="ae30d-168">Pour créer une homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="ae30d-168">To create Azure public peering</span></span>

1. <span data-ttu-id="ae30d-169">Installez la dernière version de l’interface Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ae30d-169">Install the latest version of Azure CLI.</span></span> <span data-ttu-id="ae30d-170">Vous devez utiliser la dernière version de l’interface de ligne de commande (CLI) Azure.* Prenez connaissance de la [configuration requise](expressroute-prerequisites.md) et des [workflows](expressroute-workflows.md) avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="ae30d-170">You must use the latest version of the Azure Command-line Interface (CLI).* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="ae30d-171">Sélectionnez l’abonnement pour lequel vous souhaitez créer le circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ae30d-171">Select the subscription for which you want to create ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="ae30d-172">Créez un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ae30d-172">Create an ExpressRoute circuit.</span></span>  <span data-ttu-id="ae30d-173">Suivez les instructions permettant de [créer un circuit ExpressRoute](howto-circuit-cli.md) et faites-le approvisionner par votre fournisseur de connectivité.</span><span class="sxs-lookup"><span data-stu-id="ae30d-173">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="ae30d-174">Si votre fournisseur de connectivité propose des services gérés de couche 3, vous pouvez lui demander d’activer l’homologation privée Azure pour vous.</span><span class="sxs-lookup"><span data-stu-id="ae30d-174">If your connectivity provider offers managed Layer 3 services, you can request that your connectivity provider enables Azure private peering for you.</span></span> <span data-ttu-id="ae30d-175">Dans ce cas, vous n'aurez pas besoin de suivre les instructions indiquées dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="ae30d-175">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="ae30d-176">Toutefois, si votre fournisseur de connectivité ne gère pas le routage pour vous, après avoir créé votre circuit, continuez la configuration à l’aide de la procédure qui suit.</span><span class="sxs-lookup"><span data-stu-id="ae30d-176">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="ae30d-177">Vérifiez que le circuit ExpressRoute est approvisionné et activé.</span><span class="sxs-lookup"><span data-stu-id="ae30d-177">Check the ExpressRoute circuit to ensure it is provisioned and also enabled.</span></span> <span data-ttu-id="ae30d-178">Consultez l’exemple qui suit :</span><span class="sxs-lookup"><span data-stu-id="ae30d-178">Use the following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="ae30d-179">La réponse ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="ae30d-179">The response is similar to the following example:</span></span>

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

4. <span data-ttu-id="ae30d-180">Configurez l’homologation publique Azure pour le circuit.</span><span class="sxs-lookup"><span data-stu-id="ae30d-180">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="ae30d-181">Assurez-vous que vous disposez des informations suivantes avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="ae30d-181">Make sure that you have the following information before you proceed further.</span></span>

  * <span data-ttu-id="ae30d-182">Un sous-réseau /30 pour le lien principal.</span><span class="sxs-lookup"><span data-stu-id="ae30d-182">A /30 subnet for the primary link.</span></span> <span data-ttu-id="ae30d-183">Ce doit être un préfixe IPv4 public valide.</span><span class="sxs-lookup"><span data-stu-id="ae30d-183">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="ae30d-184">Un sous-réseau /30 pour le lien secondaire.</span><span class="sxs-lookup"><span data-stu-id="ae30d-184">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="ae30d-185">Ce doit être un préfixe IPv4 public valide.</span><span class="sxs-lookup"><span data-stu-id="ae30d-185">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="ae30d-186">Un ID VLAN valide pour établir cette homologation.</span><span class="sxs-lookup"><span data-stu-id="ae30d-186">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="ae30d-187">Assurez-vous qu'aucune autre homologation sur le circuit n'utilise le même ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="ae30d-187">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="ae30d-188">Un numéro AS pour l'homologation.</span><span class="sxs-lookup"><span data-stu-id="ae30d-188">AS number for peering.</span></span> <span data-ttu-id="ae30d-189">Vous pouvez utiliser des numéros à 2 et 4 octets.</span><span class="sxs-lookup"><span data-stu-id="ae30d-189">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="ae30d-190">**(Facultatif)** Un hachage MD5 si vous choisissez d’en utiliser un.</span><span class="sxs-lookup"><span data-stu-id="ae30d-190">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="ae30d-191">Exécutez l’exemple suivant pour configurer l’homologation publique Azure pour votre circuit :</span><span class="sxs-lookup"><span data-stu-id="ae30d-191">Run the following example to configure Azure public peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  <span data-ttu-id="ae30d-192">Si vous choisissez d’utiliser un hachage MD5, exécutez l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="ae30d-192">If you choose to use an MD5 hash, use the following example:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="ae30d-193">Veillez à spécifier votre numéro AS comme ASN d’homologation et non pas comme ASN client.</span><span class="sxs-lookup"><span data-stu-id="ae30d-193">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="ae30d-194">Pour afficher les détails d’une homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="ae30d-194">To view Azure public peering details</span></span>

<span data-ttu-id="ae30d-195">Vous pouvez obtenir les détails de la configuration à l’aide de l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="ae30d-195">You can get configuration details using the following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

<span data-ttu-id="ae30d-196">Le résultat ressemble à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="ae30d-196">The output is similar to the following example:</span></span>

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

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="ae30d-197">Pour mettre à jour la configuration d'homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="ae30d-197">To update Azure public peering configuration</span></span>

<span data-ttu-id="ae30d-198">Vous pouvez mettre à jour toute partie de la configuration à l’aide de l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="ae30d-198">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="ae30d-199">Dans cet exemple, l’ID VLAN du circuit est mis à jour de 200 à 600.</span><span class="sxs-lookup"><span data-stu-id="ae30d-199">In this example, the VLAN ID of the circuit is being updated from 200 to 600.</span></span>

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="ae30d-200">Pour supprimer une homologation publique Azure</span><span class="sxs-lookup"><span data-stu-id="ae30d-200">To delete Azure public peering</span></span>

<span data-ttu-id="ae30d-201">Vous pouvez supprimer votre configuration d’homologation en exécutant l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="ae30d-201">You can remove your peering configuration by running the following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a><span data-ttu-id="ae30d-202">Homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="ae30d-202">Microsoft peering</span></span>

<span data-ttu-id="ae30d-203">Cette section explique comment créer, obtenir, mettre à jour et supprimer la configuration d’homologation Microsoft pour un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ae30d-203">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ae30d-204">L’homologation Microsoft des circuits ExpressRoute qui ont été configurés avant le 1er août 2017 entraînera la publication de tous les préfixes de service via l’homologation Microsoft, même si aucun filtre d’itinéraire n’est défini.</span><span class="sxs-lookup"><span data-stu-id="ae30d-204">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="ae30d-205">L’homologation Microsoft des circuits ExpressRoute qui sont configurés le 1er août 2017 ou après n’entraînera la publication d’aucun préfixe tant qu’un filtre de routage n’aura pas été attaché au circuit.</span><span class="sxs-lookup"><span data-stu-id="ae30d-205">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span> <span data-ttu-id="ae30d-206">Pour plus d’informations, consultez [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md) (Configurer un filtre d’itinéraire pour l’homologation Microsoft).</span><span class="sxs-lookup"><span data-stu-id="ae30d-206">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="ae30d-207">Pour créer une homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="ae30d-207">To create Microsoft peering</span></span>

1. <span data-ttu-id="ae30d-208">Installez la dernière version de l’interface Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ae30d-208">Install the latest version of Azure CLI.</span></span> <span data-ttu-id="ae30d-209">Utilisez la dernière version de l’interface de ligne de commande (CLI) Azure.* Prenez connaissance de la [configuration requise](expressroute-prerequisites.md) et des [workflows](expressroute-workflows.md) avant de commencer la configuration.</span><span class="sxs-lookup"><span data-stu-id="ae30d-209">Use the latest version of the Azure Command-line Interface (CLI).* Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

  ```azurecli
  az login
  ```

  <span data-ttu-id="ae30d-210">Sélectionnez l’abonnement pour lequel vous souhaitez créer le circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ae30d-210">Select the subscription for which you want to create ExpressRoute circuit.</span></span>

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. <span data-ttu-id="ae30d-211">Créez un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ae30d-211">Create an ExpressRoute circuit.</span></span> <span data-ttu-id="ae30d-212">Suivez les instructions permettant de [créer un circuit ExpressRoute](howto-circuit-cli.md) et faites-le approvisionner par votre fournisseur de connectivité.</span><span class="sxs-lookup"><span data-stu-id="ae30d-212">Follow the instructions to create an [ExpressRoute circuit](howto-circuit-cli.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="ae30d-213">Si votre fournisseur de connectivité propose des services gérés de couche 3, vous pouvez lui demander d’activer l'homologation privée Azure pour vous.</span><span class="sxs-lookup"><span data-stu-id="ae30d-213">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="ae30d-214">Dans ce cas, vous n'aurez pas besoin de suivre les instructions indiquées dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="ae30d-214">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="ae30d-215">Toutefois, si votre fournisseur de connectivité ne gère pas le routage pour vous, après avoir créé votre circuit, continuez la configuration à l’aide de la procédure qui suit.</span><span class="sxs-lookup"><span data-stu-id="ae30d-215">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>

3. <span data-ttu-id="ae30d-216">Vérifiez que le circuit ExpressRoute est approvisionné et activé.</span><span class="sxs-lookup"><span data-stu-id="ae30d-216">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="ae30d-217">Consultez l’exemple qui suit :</span><span class="sxs-lookup"><span data-stu-id="ae30d-217">Use the following example:</span></span>

  ```azurecli
  az network express-route list
  ```

  <span data-ttu-id="ae30d-218">La réponse ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="ae30d-218">The response is similar to the following example:</span></span>

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

4. <span data-ttu-id="ae30d-219">Configurez l’homologation Microsoft pour le circuit.</span><span class="sxs-lookup"><span data-stu-id="ae30d-219">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="ae30d-220">Assurez-vous de disposer des informations suivantes avant de poursuivre.</span><span class="sxs-lookup"><span data-stu-id="ae30d-220">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="ae30d-221">Un sous-réseau /30 pour le lien principal.</span><span class="sxs-lookup"><span data-stu-id="ae30d-221">A /30 subnet for the primary link.</span></span> <span data-ttu-id="ae30d-222">Il doit s’agir d’un préfixe IPv4 public valide vous appartenant et enregistré dans un registre RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="ae30d-222">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="ae30d-223">Un sous-réseau /30 pour le lien secondaire.</span><span class="sxs-lookup"><span data-stu-id="ae30d-223">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="ae30d-224">Il doit s’agir d’un préfixe IPv4 public valide vous appartenant et enregistré dans un registre RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="ae30d-224">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="ae30d-225">Un ID VLAN valide pour établir cette homologation.</span><span class="sxs-lookup"><span data-stu-id="ae30d-225">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="ae30d-226">Assurez-vous qu'aucune autre homologation sur le circuit n'utilise le même ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="ae30d-226">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="ae30d-227">Un numéro AS pour l'homologation.</span><span class="sxs-lookup"><span data-stu-id="ae30d-227">AS number for peering.</span></span> <span data-ttu-id="ae30d-228">Vous pouvez utiliser des numéros à 2 et 4 octets.</span><span class="sxs-lookup"><span data-stu-id="ae30d-228">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="ae30d-229">Préfixes publiés : vous devez fournir une liste de tous les préfixes que vous prévoyez de publier sur la session BGP.</span><span class="sxs-lookup"><span data-stu-id="ae30d-229">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="ae30d-230">Seuls les préfixes d'adresses IP publiques sont acceptés.</span><span class="sxs-lookup"><span data-stu-id="ae30d-230">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="ae30d-231">Si vous prévoyez d’envoyer un jeu de préfixes, vous pouvez envoyer une liste séparée par des virgules.</span><span class="sxs-lookup"><span data-stu-id="ae30d-231">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="ae30d-232">Ces préfixes doivent être enregistrés en votre nom dans un registre RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="ae30d-232">These prefixes must be registered to you in an RIR / IRR.</span></span>
  * <span data-ttu-id="ae30d-233">**(Facultatif)** ASN client : si vous publiez des préfixes non enregistrés dans le numéro de système autonome d’homologation, vous pouvez spécifier le numéro de système autonome avec lequel ils sont enregistrés.</span><span class="sxs-lookup"><span data-stu-id="ae30d-233">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
  * <span data-ttu-id="ae30d-234">Nom du registre de routage : vous pouvez spécifier les registres RIR/IRR par rapport auxquels le numéro AS et les préfixes sont enregistrés.</span><span class="sxs-lookup"><span data-stu-id="ae30d-234">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="ae30d-235">**(Facultatif)** Un hachage MD5 si vous choisissez d’en utiliser un.</span><span class="sxs-lookup"><span data-stu-id="ae30d-235">**Optional -** An MD5 hash if you choose to use one.</span></span>

   <span data-ttu-id="ae30d-236">Exécutez l’exemple suivant afin de configurer l’homologation Microsoft pour votre circuit :</span><span class="sxs-lookup"><span data-stu-id="ae30d-236">Run the following example to configure Microsoft peering for your circuit:</span></span>

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="to-get-microsoft-peering-details"></a><span data-ttu-id="ae30d-237">Pour obtenir des détails sur l’homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="ae30d-237">To get Microsoft peering details</span></span>

<span data-ttu-id="ae30d-238">Vous pouvez obtenir les détails de la configuration à l’aide de l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="ae30d-238">You can get configuration details by using the following example:</span></span>

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

<span data-ttu-id="ae30d-239">Le résultat ressemble à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="ae30d-239">The output is similar to the following example:</span></span>

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

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="ae30d-240">Pour mettre à jour la configuration d’homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="ae30d-240">To update Microsoft peering configuration</span></span>

<span data-ttu-id="ae30d-241">Vous pouvez mettre à jour toute partie de la configuration.</span><span class="sxs-lookup"><span data-stu-id="ae30d-241">You can update any part of the configuration.</span></span> <span data-ttu-id="ae30d-242">Les préfixes publiés du circuit sont mis à jour de 123.1.0.0/24 à 124.1.0.0/24 dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="ae30d-242">The advertised prefixes of the circuit are being updated from 123.1.0.0/24 to 124.1.0.0/24 in the following example:</span></span>

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="ae30d-243">Pour supprimer une homologation Microsoft</span><span class="sxs-lookup"><span data-stu-id="ae30d-243">To delete Microsoft peering</span></span>

<span data-ttu-id="ae30d-244">Vous pouvez supprimer votre configuration d’homologation en exécutant l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="ae30d-244">You can remove your peering configuration by running the following example:</span></span>

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a><span data-ttu-id="ae30d-245">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ae30d-245">Next steps</span></span>

<span data-ttu-id="ae30d-246">Ensuite, [liez un réseau virtuel à un circuit ExpressRoute](howto-linkvnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ae30d-246">Next step, [Link a VNet to an ExpressRoute circuit](howto-linkvnet-cli.md).</span></span>

* <span data-ttu-id="ae30d-247">Pour plus d'informations sur les workflows ExpressRoute, consultez [Workflows ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="ae30d-247">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="ae30d-248">Pour plus d’informations sur l’homologation du circuit, consultez [Circuits ExpressRoute et domaines de routage](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="ae30d-248">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="ae30d-249">Pour plus d’informations sur l’utilisation des réseaux virtuels, consultez la page [Présentation du réseau virtuel](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ae30d-249">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>