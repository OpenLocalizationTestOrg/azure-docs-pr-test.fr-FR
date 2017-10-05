---
title: "Connecter un réseau virtuel Azure à un autre réseau virtuel : Azure CLI | Microsoft Docs"
description: "Cet article vous guide dans l’interconnexion de réseaux virtuels avec Azure Resource Manager et Azure CLI."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: ae42f661b39e8b6170fd415d758404fb33009ccc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a><span data-ttu-id="4838b-103">Configurer une connexion de passerelle VPN de réseau virtuel à réseau virtuel à l’aide d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4838b-103">Configure a VNet-to-VNet VPN gateway connection using Azure CLI</span></span>

<span data-ttu-id="4838b-104">Cet article vous explique comment créer une connexion de passerelle VPN entre des réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="4838b-104">This article shows you how to create a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="4838b-105">Les réseaux virtuels peuvent être situés dans des régions identiques ou différentes et appartenir à des abonnements identiques ou différents.</span><span class="sxs-lookup"><span data-stu-id="4838b-105">The virtual networks can be in the same or different regions, and from the same or different subscriptions.</span></span> <span data-ttu-id="4838b-106">Lors de la connexion de réseaux virtuels provenant de différents abonnements, les abonnements ne sont pas tenus d’être associés au même locataire Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4838b-106">When connecting VNets from different subscriptions, the subscriptions do not need to be associated with the same Active Directory tenant.</span></span> 

<span data-ttu-id="4838b-107">Les étapes mentionnées dans cet article s’appliquent au modèle de déploiement Resource Manager et utilisent Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="4838b-107">The steps in this article apply to the Resource Manager deployment model and use Azure CLI.</span></span> <span data-ttu-id="4838b-108">Vous pouvez également créer cette configuration à l’aide d’un autre outil ou modèle de déploiement en sélectionnant une option différente dans la liste suivante :</span><span class="sxs-lookup"><span data-stu-id="4838b-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4838b-109">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="4838b-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="4838b-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4838b-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="4838b-111">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="4838b-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="4838b-112">Portail Azure (classique)</span><span class="sxs-lookup"><span data-stu-id="4838b-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="4838b-113">Connexions entre différents modèles de déploiement - Portail Azure</span><span class="sxs-lookup"><span data-stu-id="4838b-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="4838b-114">Connexions entre différents modèles de déploiement - PowerShell</span><span class="sxs-lookup"><span data-stu-id="4838b-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="4838b-115">La connexion entre deux réseaux virtuels est semblable à la connexion d’un réseau virtuel à un emplacement de site local.</span><span class="sxs-lookup"><span data-stu-id="4838b-115">Connecting a virtual network to another virtual network (VNet-to-VNet) is similar to connecting a VNet to an on-premises site location.</span></span> <span data-ttu-id="4838b-116">Les deux types de connectivité font appel à une passerelle VPN pour offrir un tunnel sécurisé utilisant Ipsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="4838b-116">Both connectivity types use a VPN gateway to provide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="4838b-117">Si vos réseaux virtuels sont situés dans la même région, vous souhaiterez peut-être les connecter à l’aide de VNet Peering.</span><span class="sxs-lookup"><span data-stu-id="4838b-117">If your VNets are in the same region, you may want to consider connecting them using VNet Peering.</span></span> <span data-ttu-id="4838b-118">L’homologation de réseaux virtuels (ou VNet Peering) n’utilise pas de passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="4838b-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="4838b-119">Pour plus d’informations, consultez l’article [Homologation de réseaux virtuels](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4838b-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="4838b-120">Vous pouvez combiner une communication de réseau virtuel à réseau virtuel avec des configurations multisites.</span><span class="sxs-lookup"><span data-stu-id="4838b-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="4838b-121">Vous établissez ainsi des topologies réseau qui combinent une connectivité entre différents locaux et une connectivité entre différents réseaux virtuels, comme indiqué dans le schéma suivant :</span><span class="sxs-lookup"><span data-stu-id="4838b-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in the following diagram:</span></span>

![À propos des connexions](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <span data-ttu-id="4838b-123"><a name="why"></a>Pourquoi connecter des réseaux virtuels ?</span><span class="sxs-lookup"><span data-stu-id="4838b-123"><a name="why"></a>Why connect virtual networks?</span></span>

<span data-ttu-id="4838b-124">Vous pouvez décider de connecter des réseaux virtuels pour les raisons suivantes :</span><span class="sxs-lookup"><span data-stu-id="4838b-124">You may want to connect virtual networks for the following reasons:</span></span>

* <span data-ttu-id="4838b-125">**Géo-redondance et présence géographique dans plusieurs régions**</span><span class="sxs-lookup"><span data-stu-id="4838b-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="4838b-126">Vous pouvez configurer la géo-réplication ou la synchronisation avec une connectivité sécurisée sans passer par les points de terminaison accessibles sur Internet.</span><span class="sxs-lookup"><span data-stu-id="4838b-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="4838b-127">Avec Traffic Manager et l’équilibreur de charge Azure, vous pouvez configurer une charge de travail hautement disponible avec la géo-redondance dans plusieurs régions Azure.</span><span class="sxs-lookup"><span data-stu-id="4838b-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="4838b-128">Vous pouvez par exemple configurer SQL Always On avec des groupes de disponibilité répartis dans différentes régions Azure.</span><span class="sxs-lookup"><span data-stu-id="4838b-128">One important example is to set up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="4838b-129">**Applications multiniveaux régionales avec une limite d’isolement ou administrative**</span><span class="sxs-lookup"><span data-stu-id="4838b-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="4838b-130">Dans la même région, vous pouvez configurer des applications multiniveaux avec plusieurs réseaux virtuels interconnectés pour des besoins d’isolement ou d’administration.</span><span class="sxs-lookup"><span data-stu-id="4838b-130">Within the same region, you can set up multi-tier applications with multiple virtual networks connected together due to isolation or administrative requirements.</span></span>

<span data-ttu-id="4838b-131">Pour plus d’informations sur les connexions de réseau virtuel à réseau virtuel, consultez le [Forum Aux Questions sur l’interconnexion de réseaux virtuels](#faq) à la fin de cet article.</span><span class="sxs-lookup"><span data-stu-id="4838b-131">For more information about VNet-to-VNet connections, see the [VNet-to-VNet FAQ](#faq) at the end of this article.</span></span>

### <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="4838b-132">Quelle procédure dois-je utiliser ?</span><span class="sxs-lookup"><span data-stu-id="4838b-132">Which set of steps should I use?</span></span>

<span data-ttu-id="4838b-133">Cet article inclut deux ensembles d’étapes distincts.</span><span class="sxs-lookup"><span data-stu-id="4838b-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="4838b-134">L’un des ensembles est destiné aux [réseaux virtuels qui se trouvent dans le même abonnement](#samesub), et l’autre aux [réseaux virtuels qui se trouvent dans des abonnements différents](#difsub).</span><span class="sxs-lookup"><span data-stu-id="4838b-134">One set of steps for [VNets that reside in the same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span>

## <span data-ttu-id="4838b-135"><a name="samesub"></a>Connecter des réseaux virtuels situés dans le même abonnement</span><span class="sxs-lookup"><span data-stu-id="4838b-135"><a name="samesub"></a>Connect VNets that are in the same subscription</span></span>

![Diagramme v2v](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="4838b-137">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="4838b-137">Before you begin</span></span>

<span data-ttu-id="4838b-138">Avant de commencer, installez la dernière version des commandes CLI (version 2.0 ou ultérieure).</span><span class="sxs-lookup"><span data-stu-id="4838b-138">Before beginning, install the latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="4838b-139">Pour plus d’informations sur l’installation des commandes CLI consultez l’article [Installer l’interface de ligne de commande Azure 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4838b-139">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

### <span data-ttu-id="4838b-140"><a name="Plan"></a>Panifier vos plages d’adresses IP</span><span class="sxs-lookup"><span data-stu-id="4838b-140"><a name="Plan"></a>Plan your IP address ranges</span></span>

<span data-ttu-id="4838b-141">Dans les étapes suivantes, nous allons créer deux réseaux virtuels avec leurs sous-réseaux de passerelle respectifs et leur configuration.</span><span class="sxs-lookup"><span data-stu-id="4838b-141">In the following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="4838b-142">Nous allons ensuite créer une connexion VPN entre les deux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="4838b-142">We then create a VPN connection between the two VNets.</span></span> <span data-ttu-id="4838b-143">Il est important de planifier les plages d’adresses IP pour votre configuration réseau.</span><span class="sxs-lookup"><span data-stu-id="4838b-143">It’s important to plan the IP address ranges for your network configuration.</span></span> <span data-ttu-id="4838b-144">N’oubliez pas que vous devez vous assurer qu’aucune plage de réseaux virtuels ou de réseaux locaux ne se chevauche.</span><span class="sxs-lookup"><span data-stu-id="4838b-144">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="4838b-145">Dans ces exemples, nous n’incluons pas de serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="4838b-145">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="4838b-146">Si vous souhaitez une résolution de noms pour vos réseaux virtuels, consultez la page [Résolution de noms](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="4838b-146">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="4838b-147">Nous utilisons les valeurs suivantes dans les exemples :</span><span class="sxs-lookup"><span data-stu-id="4838b-147">We use the following values in the examples:</span></span>

<span data-ttu-id="4838b-148">**Valeurs pour TestVNet1 :**</span><span class="sxs-lookup"><span data-stu-id="4838b-148">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="4838b-149">Nom du réseau virtuel : TestVNet1</span><span class="sxs-lookup"><span data-stu-id="4838b-149">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="4838b-150">Groupe de ressources : TestRG1</span><span class="sxs-lookup"><span data-stu-id="4838b-150">Resource Group: TestRG1</span></span>
* <span data-ttu-id="4838b-151">Emplacement : Est des États-Unis</span><span class="sxs-lookup"><span data-stu-id="4838b-151">Location: East US</span></span>
* <span data-ttu-id="4838b-152">TestVNet1 : 10.11.0.0/16 et 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="4838b-152">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="4838b-153">FrontEnd : 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4838b-153">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="4838b-154">BackEnd : 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4838b-154">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="4838b-155">GatewaySubnet : 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="4838b-155">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="4838b-156">GatewayName : VNet1GW</span><span class="sxs-lookup"><span data-stu-id="4838b-156">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="4838b-157">Adresse IP publique : VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="4838b-157">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="4838b-158">Type de VPN : RouteBased</span><span class="sxs-lookup"><span data-stu-id="4838b-158">VPNType: RouteBased</span></span>
* <span data-ttu-id="4838b-159">Connection(1to4) : VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="4838b-159">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="4838b-160">Connection(1to5) : VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="4838b-160">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="4838b-161">Type de connexion : VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="4838b-161">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="4838b-162">**Valeurs pour TestVNet4 :**</span><span class="sxs-lookup"><span data-stu-id="4838b-162">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="4838b-163">Nom du réseau virtuel : TestVNet4</span><span class="sxs-lookup"><span data-stu-id="4838b-163">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="4838b-164">TestVNet2 : 10.41.0.0/16 et 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="4838b-164">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="4838b-165">Serveur frontal : 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4838b-165">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="4838b-166">Serveur principal : 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4838b-166">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="4838b-167">Sous-réseau de passerelle : 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="4838b-167">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="4838b-168">Groupe de ressources : TestRG4</span><span class="sxs-lookup"><span data-stu-id="4838b-168">Resource Group: TestRG4</span></span>
* <span data-ttu-id="4838b-169">Emplacement : États-Unis de l’Ouest</span><span class="sxs-lookup"><span data-stu-id="4838b-169">Location: West US</span></span>
* <span data-ttu-id="4838b-170">Nom de la passerelle : VNet4GW</span><span class="sxs-lookup"><span data-stu-id="4838b-170">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="4838b-171">Adresse IP publique : VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="4838b-171">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="4838b-172">Type de VPN : RouteBased</span><span class="sxs-lookup"><span data-stu-id="4838b-172">VPNType: RouteBased</span></span>
* <span data-ttu-id="4838b-173">Connexion : VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="4838b-173">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="4838b-174">Type de connexion : VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="4838b-174">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="4838b-175"><a name="Connect"></a>Étape 1 : connectez-vous à votre abonnement</span><span class="sxs-lookup"><span data-stu-id="4838b-175"><a name="Connect"></a>Step 1 - Connect to your subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <span data-ttu-id="4838b-176"><a name="TestVNet1"></a>Étape 2 : créez et configurez TestVNet1</span><span class="sxs-lookup"><span data-stu-id="4838b-176"><a name="TestVNet1"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="4838b-177">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="4838b-177">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. <span data-ttu-id="4838b-178">Créez TestVNet1 et les sous-réseaux de TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="4838b-178">Create TestVNet1 and the subnets for TestVNet1.</span></span> <span data-ttu-id="4838b-179">L’exemple suivant permet de créer un réseau virtuel nommé TestVNet1 et un sous-réseau nommé FrontEnd.</span><span class="sxs-lookup"><span data-stu-id="4838b-179">This example creates a virtual network named TestVNet1 and a subnet named FrontEnd.</span></span>

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. <span data-ttu-id="4838b-180">Créez un espace d’adressage supplémentaire pour le sous-réseau principal.</span><span class="sxs-lookup"><span data-stu-id="4838b-180">Create an additional address space for the backend subnet.</span></span> <span data-ttu-id="4838b-181">Notez que dans cette étape, nous spécifions l’espace d’adressage créé précédemment et l’espace d’adressage supplémentaires que nous souhaitons ajouter.</span><span class="sxs-lookup"><span data-stu-id="4838b-181">Notice that in this step, we specify both the address space that we created earlier, and the additional address space that we want to add.</span></span> <span data-ttu-id="4838b-182">Cela vient du fait que la [mise à jour du réseau virtuel du réseau az](https://docs.microsoft.com/cli/azure/network/vnet#update) écrase les paramètres précédents.</span><span class="sxs-lookup"><span data-stu-id="4838b-182">This is because the [az network vnet update](https://docs.microsoft.com/cli/azure/network/vnet#update) command overwrites the previous settings.</span></span> <span data-ttu-id="4838b-183">Veillez à spécifier tous les préfixes d’adresse lors de l’utilisation de cette commande.</span><span class="sxs-lookup"><span data-stu-id="4838b-183">Make sure to specify all of the address prefixes when using this command.</span></span>

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. <span data-ttu-id="4838b-184">Créez le sous-réseau principal.</span><span class="sxs-lookup"><span data-stu-id="4838b-184">Create the backend subnet.</span></span>
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. <span data-ttu-id="4838b-185">Créez le sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="4838b-185">Create the gateway subnet.</span></span> <span data-ttu-id="4838b-186">Notez que le sous-réseau de passerelle est nommé GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="4838b-186">Notice that the gateway subnet is named 'GatewaySubnet'.</span></span> <span data-ttu-id="4838b-187">Ce nom est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="4838b-187">This name is required.</span></span> <span data-ttu-id="4838b-188">Dans cet exemple, le sous-réseau de passerelle utilise /27.</span><span class="sxs-lookup"><span data-stu-id="4838b-188">In this example, the gateway subnet is using a /27.</span></span> <span data-ttu-id="4838b-189">Bien qu’il soit possible de créer un sous-réseau de passerelle aussi petit que /29, nous vous recommandons de créer un sous-réseau plus vaste qui inclut un plus grand nombre d’adresses en sélectionnant au moins /28 ou /27.</span><span class="sxs-lookup"><span data-stu-id="4838b-189">While it is possible to create a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="4838b-190">Cela permettra à un nombre suffisant d’adresses de s’adapter à de possibles configurations supplémentaires possibles que vous êtes susceptible de souhaiter par la suite.</span><span class="sxs-lookup"><span data-stu-id="4838b-190">This will allow for enough addresses to accommodate possible additional configurations that you may want in the future.</span></span>

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. <span data-ttu-id="4838b-191">Demandez l’allocation d’une adresse IP publique à la passerelle que vous allez créer pour votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="4838b-191">Request a public IP address to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="4838b-192">Notez que la valeur AllocationMethod est dynamique.</span><span class="sxs-lookup"><span data-stu-id="4838b-192">Notice that the AllocationMethod is Dynamic.</span></span> <span data-ttu-id="4838b-193">Vous ne pouvez pas spécifier l’adresse IP que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="4838b-193">You cannot specify the IP address that you want to use.</span></span> <span data-ttu-id="4838b-194">Elle est allouée à votre passerelle de façon dynamique.</span><span class="sxs-lookup"><span data-stu-id="4838b-194">It's dynamically allocated to your gateway.</span></span>

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. <span data-ttu-id="4838b-195">Créez la passerelle de réseau virtuel pour TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="4838b-195">Create the virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="4838b-196">Les configurations de réseau virtuel à réseau virtuel requièrent un VPN de type RouteBased.</span><span class="sxs-lookup"><span data-stu-id="4838b-196">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="4838b-197">Si vous exécutez cette commande à l’aide du paramètre « --no-wait », vous ne voyez aucun commentaire ni sortie.</span><span class="sxs-lookup"><span data-stu-id="4838b-197">If you run this command using the '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="4838b-198">Le paramètre ’--no-wait’ permet à la passerelle d’être créée en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="4838b-198">The '--no-wait' parameter allows the gateway to create in the background.</span></span> <span data-ttu-id="4838b-199">Cela ne signifie pas que la passerelle VPN termine la création immédiatement.</span><span class="sxs-lookup"><span data-stu-id="4838b-199">It does not mean that the VPN gateway finishes creating immediately.</span></span> <span data-ttu-id="4838b-200">La création d’une passerelle nécessite généralement au moins 45 minutes, selon la référence SKU de passerelle utilisée.</span><span class="sxs-lookup"><span data-stu-id="4838b-200">Creating a gateway can often take 45 minutes or more, depending on the gateway SKU that you use.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="4838b-201"><a name="TestVNet4"></a>Étape 3 : créez et configurez TestVNet4</span><span class="sxs-lookup"><span data-stu-id="4838b-201"><a name="TestVNet4"></a>Step 3 - Create and configure TestVNet4</span></span>

1. <span data-ttu-id="4838b-202">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="4838b-202">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. <span data-ttu-id="4838b-203">Créez TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="4838b-203">Create TestVNet4.</span></span>

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. <span data-ttu-id="4838b-204">Créez des sous-réseaux supplémentaires pour TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="4838b-204">Create additional subnets for TestVNet4.</span></span>

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. <span data-ttu-id="4838b-205">Créez le sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="4838b-205">Create the gateway subnet.</span></span>

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. <span data-ttu-id="4838b-206">Demandez une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="4838b-206">Request a Public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. <span data-ttu-id="4838b-207">Créez la passerelle de réseau virtuel TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="4838b-207">Create the TestVNet4 virtual network gateway.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="4838b-208"><a name="createconnect"></a>Étape 4 : créez les connexions</span><span class="sxs-lookup"><span data-stu-id="4838b-208"><a name="createconnect"></a>Step 4 - Create the connections</span></span>

<span data-ttu-id="4838b-209">Vous avez maintenant deux réseaux virtuels avec des passerelles VPN.</span><span class="sxs-lookup"><span data-stu-id="4838b-209">You now have two VNets with VPN gateways.</span></span> <span data-ttu-id="4838b-210">L’étape suivante consiste à créer des connexions à la passerelle VPN entre les passerelles de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="4838b-210">The next step is to create VPN gateway connections between the virtual network gateways.</span></span> <span data-ttu-id="4838b-211">Si vous avez utilisé les exemples ci-dessus, vos passerelles de réseau virtuel se trouvent dans différents groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="4838b-211">If you used the examples above, your VNet gateways are in different resource groups.</span></span> <span data-ttu-id="4838b-212">Lorsque les passerelles se trouvent dans différents groupes de ressources, vous devez identifier et spécifier l’ID de ressource pour chaque passerelle lors de la connexion.</span><span class="sxs-lookup"><span data-stu-id="4838b-212">When gateways are in different resource groups, you need to identify and specify the resource IDs for each gateway when making a connection.</span></span> <span data-ttu-id="4838b-213">Si vos réseaux virtuels sont dans le même groupe de ressources, vous pouvez utiliser le [deuxième ensemble d’instructions](#samerg) , dans la mesure où il n’est pas nécessaire de spécifier les ID de ressource.</span><span class="sxs-lookup"><span data-stu-id="4838b-213">If your VNets are in the same resource group, you can use the [second set of instructions](#samerg) because you don't need to specify the resource IDs.</span></span>

### <span data-ttu-id="4838b-214"><a name="diffrg"></a>Connexion de réseaux virtuels qui se trouvent dans différents groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="4838b-214"><a name="diffrg"></a>To connect VNets that reside in different resource groups</span></span>

1. <span data-ttu-id="4838b-215">Obtenez l’ID de ressource de VNet1GW à partir de la sortie de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4838b-215">Get the Resource ID of VNet1GW from the output of the following command:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="4838b-216">Dans la sortie, recherchez la ligne « id: ».</span><span class="sxs-lookup"><span data-stu-id="4838b-216">In the output, find the "id:" line.</span></span> <span data-ttu-id="4838b-217">Les valeurs entre guillemets sont nécessaires pour créer la connexion dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="4838b-217">The values within the quotes are needed to create the connection in the next section.</span></span> <span data-ttu-id="4838b-218">Copiez ces valeurs dans un éditeur de texte, tel que Bloc-notes, afin de pouvoir les coller facilement lors de la création de la connexion.</span><span class="sxs-lookup"><span data-stu-id="4838b-218">Copy these values to a text editor, such as Notepad, so that you can easily paste them when creating your connection.</span></span>

  <span data-ttu-id="4838b-219">Exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="4838b-219">Example output:</span></span>

  ```
  "activeActive": false, 
  "bgpSettings": { 
    "asn": 65515, 
    "bgpPeeringAddress": "10.12.255.30", 
    "peerWeight": 0 
   }, 
  "enableBgp": false, 
  "etag": "W/\"ecb42bc5-c176-44e1-802f-b0ce2962ac04\"", 
  "gatewayDefaultSite": null, 
  "gatewayType": "Vpn", 
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW", 
  "ipConfigurations":
  ```

  <span data-ttu-id="4838b-220">Copiez les valeurs situées après **« id » :** entre les guillemets.</span><span class="sxs-lookup"><span data-stu-id="4838b-220">Copy the values after **"id":** within the quotes.</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. <span data-ttu-id="4838b-221">Obtenez l’ID de ressource de VNet4GW et copiez les valeurs dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="4838b-221">Get the Resource ID of VNet4GW and copy the values to a text editor.</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. <span data-ttu-id="4838b-222">Créez la connexion de TestVNet1 à TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="4838b-222">Create the TestVNet1 to TestVNet4 connection.</span></span> <span data-ttu-id="4838b-223">Lors de cette étape, vous créez la connexion de TestVNet1 à TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="4838b-223">In this step, you create the connection from TestVNet1 to TestVNet4.</span></span> <span data-ttu-id="4838b-224">Une clé partagée est référencée dans les exemples.</span><span class="sxs-lookup"><span data-stu-id="4838b-224">There is a shared key referenced in the examples.</span></span> <span data-ttu-id="4838b-225">Vous pouvez utiliser vos propres valeurs pour cette clé partagée.</span><span class="sxs-lookup"><span data-stu-id="4838b-225">You can use your own values for the shared key.</span></span> <span data-ttu-id="4838b-226">Il est important que la clé partagée corresponde aux deux connexions.</span><span class="sxs-lookup"><span data-stu-id="4838b-226">The important thing is that the shared key must match for both connections.</span></span> <span data-ttu-id="4838b-227">La création d’une connexion prend quelques instants.</span><span class="sxs-lookup"><span data-stu-id="4838b-227">Creating a connection takes a short while to complete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. <span data-ttu-id="4838b-228">Créez la connexion de TestVNet4 à TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="4838b-228">Create the TestVNet4 to TestVNet1 connection.</span></span> <span data-ttu-id="4838b-229">Cette étape est similaire à celle présentée ci-dessus, sauf que vous créez la connexion de TestVNet4 à TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="4838b-229">This step is similar to the one above, except you are creating the connection from TestVNet4 to TestVNet1.</span></span> <span data-ttu-id="4838b-230">Vérifiez que les clés partagées correspondent.</span><span class="sxs-lookup"><span data-stu-id="4838b-230">Make sure the shared keys match.</span></span> <span data-ttu-id="4838b-231">L’établissement de la connexion prend quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="4838b-231">It takes a few minutes to establish the connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. <span data-ttu-id="4838b-232">Vérifiez vos connexions.</span><span class="sxs-lookup"><span data-stu-id="4838b-232">Verify your connections.</span></span> <span data-ttu-id="4838b-233">Consultez [Vérifier votre connexion](#verify).</span><span class="sxs-lookup"><span data-stu-id="4838b-233">See [Verify your connection](#verify).</span></span>

### <span data-ttu-id="4838b-234"><a name="samerg"></a>Pour connecter des réseaux virtuels qui se trouvent dans le même groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="4838b-234"><a name="samerg"></a>To connect VNets that reside in the same resource group</span></span>

1. <span data-ttu-id="4838b-235">Créez la connexion de TestVNet1 à TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="4838b-235">Create the TestVNet1 to TestVNet4 connection.</span></span> <span data-ttu-id="4838b-236">Lors de cette étape, vous créez la connexion de TestVNet1 à TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="4838b-236">In this step, you create the connection from TestVNet1 to TestVNet4.</span></span> <span data-ttu-id="4838b-237">Notez que les groupes de ressources sont les mêmes dans les exemples.</span><span class="sxs-lookup"><span data-stu-id="4838b-237">Notice the resource groups are the same in the examples.</span></span> <span data-ttu-id="4838b-238">Une clé partagée est également référencée dans les exemples.</span><span class="sxs-lookup"><span data-stu-id="4838b-238">You also see a shared key referenced in the examples.</span></span> <span data-ttu-id="4838b-239">Vous pouvez utiliser vos propres valeurs pour la clé partagée, toutefois, cette dernière doit correspondre aux deux connexions.</span><span class="sxs-lookup"><span data-stu-id="4838b-239">You can use your own values for the shared key, however, the shared key must match for both connections.</span></span> <span data-ttu-id="4838b-240">La création d’une connexion prend quelques instants.</span><span class="sxs-lookup"><span data-stu-id="4838b-240">Creating a connection takes a short while to complete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. <span data-ttu-id="4838b-241">Créez la connexion de TestVNet4 à TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="4838b-241">Create the TestVNet4 to TestVNet1 connection.</span></span> <span data-ttu-id="4838b-242">Cette étape est similaire à celle présentée ci-dessus, sauf que vous créez la connexion de TestVNet4 à TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="4838b-242">This step is similar to the one above, except you are creating the connection from TestVNet4 to TestVNet1.</span></span> <span data-ttu-id="4838b-243">Vérifiez que les clés partagées correspondent.</span><span class="sxs-lookup"><span data-stu-id="4838b-243">Make sure the shared keys match.</span></span> <span data-ttu-id="4838b-244">L’établissement de la connexion prend quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="4838b-244">It takes a few minutes to establish the connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. <span data-ttu-id="4838b-245">Vérifiez vos connexions.</span><span class="sxs-lookup"><span data-stu-id="4838b-245">Verify your connections.</span></span> <span data-ttu-id="4838b-246">Consultez [Vérifier votre connexion](#verify).</span><span class="sxs-lookup"><span data-stu-id="4838b-246">See [Verify your connection](#verify).</span></span>

## <span data-ttu-id="4838b-247"><a name="difsub"></a>Connecter des réseaux virtuels situés dans différents abonnements</span><span class="sxs-lookup"><span data-stu-id="4838b-247"><a name="difsub"></a>Connect VNets that are in different subscriptions</span></span>

![Diagramme v2v](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

<span data-ttu-id="4838b-249">Dans ce scénario, nous connectons TestVNet1 et TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="4838b-249">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="4838b-250">Les réseaux virtuels se trouvent dans différents abonnements.</span><span class="sxs-lookup"><span data-stu-id="4838b-250">The VNets reside different subscriptions.</span></span> <span data-ttu-id="4838b-251">Les abonnements ne sont pas tenus d’être associés au même locataire Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4838b-251">The subscriptions do not need to be associated with the same Active Directory tenant.</span></span> <span data-ttu-id="4838b-252">Cette configuration nécessite l’ajout d’une connexion supplémentaire entre réseaux virtuels pour connecter TestVNet1 à TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="4838b-252">The steps for this configuration add an additional VNet-to-VNet connection in order to connect TestVNet1 to TestVNet5.</span></span>

### <span data-ttu-id="4838b-253"><a name="TestVNet1diff"></a>Étape 5 : créez et configurez TestVNet1</span><span class="sxs-lookup"><span data-stu-id="4838b-253"><a name="TestVNet1diff"></a>Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="4838b-254">Ces instructions sont la suite des étapes décrites dans les sections précédentes.</span><span class="sxs-lookup"><span data-stu-id="4838b-254">These instructions continue from the steps in the preceding sections.</span></span> <span data-ttu-id="4838b-255">Vous devez terminer les étapes [1](#Connect) et [2](#TestVNet1) pour créer et configurer TestVNet1 et la passerelle VPN pour TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="4838b-255">You must complete [Step 1](#Connect) and [Step 2](#TestVNet1) to create and configure TestVNet1 and the VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="4838b-256">Pour cette configuration, il n’est pas nécessaire de créer TestVNet4 à partir de la section précédente. Néanmoins, si vous la créez, elle n’entrera pas en conflit avec ces étapes.</span><span class="sxs-lookup"><span data-stu-id="4838b-256">For this configuration, you are not required to create TestVNet4 from the previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="4838b-257">Une fois les étapes 1 et 2 effectuées, passez à l’étape 6 (ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="4838b-257">Once you complete Step 1 and Step 2, continue with Step 6 (below).</span></span>

### <span data-ttu-id="4838b-258"><a name="verifyranges"></a>Étape 6 : vérifiez les plages d’adresses IP</span><span class="sxs-lookup"><span data-stu-id="4838b-258"><a name="verifyranges"></a>Step 6 - Verify the IP address ranges</span></span>

<span data-ttu-id="4838b-259">Lors de la création de connexions supplémentaires, il est important de s’assurer que l’espace d’adressage IP du nouveau réseau virtuel ne chevauche aucune de vos autres plages de réseaux virtuels ou de passerelles de réseau locales.</span><span class="sxs-lookup"><span data-stu-id="4838b-259">When creating additional connections, it's important to verify that the IP address space of the new virtual network does not overlap with any of your other VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="4838b-260">Pour cet exercice, vous pouvez utiliser les valeurs suivantes pour TestVNet5 :</span><span class="sxs-lookup"><span data-stu-id="4838b-260">For this exercise, you can use the following values for the TestVNet5:</span></span>

<span data-ttu-id="4838b-261">**Valeurs pour TestVNet5 :**</span><span class="sxs-lookup"><span data-stu-id="4838b-261">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="4838b-262">Nom du réseau virtuel : TestVNet5</span><span class="sxs-lookup"><span data-stu-id="4838b-262">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="4838b-263">Groupe de ressources : TestRG5</span><span class="sxs-lookup"><span data-stu-id="4838b-263">Resource Group: TestRG5</span></span>
* <span data-ttu-id="4838b-264">Emplacement : Japon de l’Est</span><span class="sxs-lookup"><span data-stu-id="4838b-264">Location: Japan East</span></span>
* <span data-ttu-id="4838b-265">TestVNet5 : 10.51.0.0/16 et 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="4838b-265">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="4838b-266">Serveur frontal : 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4838b-266">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="4838b-267">Serveur principal : 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4838b-267">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="4838b-268">Sous-réseau de passerelle : 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="4838b-268">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="4838b-269">Nom de la passerelle : VNet5GW</span><span class="sxs-lookup"><span data-stu-id="4838b-269">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="4838b-270">Adresse IP publique : VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="4838b-270">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="4838b-271">Type de VPN : RouteBased</span><span class="sxs-lookup"><span data-stu-id="4838b-271">VPNType: RouteBased</span></span>
* <span data-ttu-id="4838b-272">Connexion : VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="4838b-272">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="4838b-273">Type de connexion : VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="4838b-273">ConnectionType: VNet2VNet</span></span>

### <span data-ttu-id="4838b-274"><a name="TestVNet5"></a>Étape 7 : créez et configurez TestVNet5</span><span class="sxs-lookup"><span data-stu-id="4838b-274"><a name="TestVNet5"></a>Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="4838b-275">Cette étape doit être effectuée dans le cadre du nouvel abonnement, Abonnement 5.</span><span class="sxs-lookup"><span data-stu-id="4838b-275">This step must be done in the context of the new subscription, Subscription 5.</span></span> <span data-ttu-id="4838b-276">Cette partie peut être effectuée par l’administrateur dans une organisation différente qui possède l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="4838b-276">This part may be performed by the administrator in a different organization that owns the subscription.</span></span> <span data-ttu-id="4838b-277">Pour basculer entre les abonnements, utilisez ’az account list --all’ pour répertorier les abonnements disponibles pour votre compte, puis ’az account set --subscription <subscriptionID>’ pour basculer vers l’abonnement que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="4838b-277">To switch between subscriptions use 'az account list --all' to list the subscriptions available to your account, then use 'az account set --subscription <subscriptionID>' to switch to the subscription that you want to use.</span></span>

1. <span data-ttu-id="4838b-278">Assurez-vous d’être connecté à Abonnement 5, puis créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="4838b-278">Make sure you are connected to Subscription 5, then create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. <span data-ttu-id="4838b-279">Créez TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="4838b-279">Create TestVNet5.</span></span>

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. <span data-ttu-id="4838b-280">Ajoutez des sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="4838b-280">Add subnets.</span></span>

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. <span data-ttu-id="4838b-281">Ajoutez le sous-réseau de passerelle.</span><span class="sxs-lookup"><span data-stu-id="4838b-281">Add the gateway subnet.</span></span>

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. <span data-ttu-id="4838b-282">Demandez une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="4838b-282">Request a public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. <span data-ttu-id="4838b-283">Créer la passerelle TestVNet5</span><span class="sxs-lookup"><span data-stu-id="4838b-283">Create the TestVNet5 gateway</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="4838b-284"><a name="connections5"></a>Étape 8 : créez les connexions</span><span class="sxs-lookup"><span data-stu-id="4838b-284"><a name="connections5"></a>Step 8 - Create the connections</span></span>

<span data-ttu-id="4838b-285">Étant donné que les passerelles se trouvent dans différents abonnements, nous avons divisé cette étape en deux sessions CLI notées **[Abonnement 1]** et **[Abonnement 5]**.</span><span class="sxs-lookup"><span data-stu-id="4838b-285">We split this step into two CLI sessions marked as **[Subscription 1]**, and **[Subscription 5]** because the gateways are in the different subscriptions.</span></span> <span data-ttu-id="4838b-286">Pour basculer entre les abonnements, utilisez ’az account list --all’ pour répertorier les abonnements disponibles pour votre compte, puis ’az account set --subscription <subscriptionID>’ pour basculer vers l’abonnement que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="4838b-286">To switch between subscriptions use 'az account list --all' to list the subscriptions available to your account, then use 'az account set --subscription <subscriptionID>' to switch to the subscription that you want to use.</span></span>

1. <span data-ttu-id="4838b-287">**[Abonnement 1]** Ouvrez une session et connectez-vous à Abonnement 1.</span><span class="sxs-lookup"><span data-stu-id="4838b-287">**[Subscription 1]** Log in and connect to Subscription 1.</span></span> <span data-ttu-id="4838b-288">Exécutez la commande suivante pour obtenir le nom et l’ID de la passerelle à partir de la sortie :</span><span class="sxs-lookup"><span data-stu-id="4838b-288">Run the following command to get the name and ID of the Gateway from the output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="4838b-289">Copiez la sortie pour « id: ».</span><span class="sxs-lookup"><span data-stu-id="4838b-289">Copy the output for "id:".</span></span> <span data-ttu-id="4838b-290">Envoyez l’ID et le nom de la passerelle de réseau virtuel (VNet1GW) à l’administrateur de Abonnement 5 via e-mail ou une autre méthode.</span><span class="sxs-lookup"><span data-stu-id="4838b-290">Send the ID and the name of the VNet gateway (VNet1GW) to the administrator of Subscription 5 via email or another method.</span></span>

  <span data-ttu-id="4838b-291">Exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="4838b-291">Example output:</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. <span data-ttu-id="4838b-292">**[Abonnement 5]** Ouvrez une session et connectez-vous à Abonnement 5.</span><span class="sxs-lookup"><span data-stu-id="4838b-292">**[Subscription 5]** Log in and connect to Subscription 5.</span></span> <span data-ttu-id="4838b-293">Exécutez la commande suivante pour obtenir le nom et l’ID de la passerelle à partir de la sortie :</span><span class="sxs-lookup"><span data-stu-id="4838b-293">Run the following command to get the name and ID of the Gateway from the output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  <span data-ttu-id="4838b-294">Copiez la sortie pour « id: ».</span><span class="sxs-lookup"><span data-stu-id="4838b-294">Copy the output for "id:".</span></span> <span data-ttu-id="4838b-295">Envoyez l’ID et le nom de la passerelle de réseau virtuel (VNet5GW) à l’administrateur de Abonnement 1 via e-mail ou une autre méthode.</span><span class="sxs-lookup"><span data-stu-id="4838b-295">Send the ID and the name of the VNet gateway (VNet5GW) to the administrator of Subscription 1 via email or another method.</span></span>

3. <span data-ttu-id="4838b-296">**[Abonnement 1]** Dans cette étape, vous créez la connexion de TestVNet1 à TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="4838b-296">**[Subscription 1]** In this step, you create the connection from TestVNet1 to TestVNet5.</span></span> <span data-ttu-id="4838b-297">Vous pouvez utiliser vos propres valeurs pour la clé partagée, toutefois, cette dernière doit correspondre aux deux connexions.</span><span class="sxs-lookup"><span data-stu-id="4838b-297">You can use your own values for the shared key, however, the shared key must match for both connections.</span></span> <span data-ttu-id="4838b-298">La création d’une connexion peut prendre quelques instants.</span><span class="sxs-lookup"><span data-stu-id="4838b-298">Creating a connection can take a short while to complete.</span></span> <span data-ttu-id="4838b-299">Veillez à vous connecter à Abonnement 1.</span><span class="sxs-lookup"><span data-stu-id="4838b-299">Make sure you connect to Subscription 1.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. <span data-ttu-id="4838b-300">**[Abonnement 5]** Cette étape est similaire à celle présentée ci-dessus, sauf que vous créez la connexion de TestVNet5 à TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="4838b-300">**[Subscription 5]** This step is similar to the one above, except you are creating the connection from TestVNet5 to TestVNet1.</span></span> <span data-ttu-id="4838b-301">Assurez-vous que les clés partagées correspondent et que vous vous connectez à Abonnement 5.</span><span class="sxs-lookup"><span data-stu-id="4838b-301">Make sure that the shared keys match and that you connect to Subscription 5.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <span data-ttu-id="4838b-302"><a name="verify"></a>Vérifier les connexions</span><span class="sxs-lookup"><span data-stu-id="4838b-302"><a name="verify"></a>Verify the connections</span></span>
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <span data-ttu-id="4838b-303"><a name="faq"></a>Forum Aux Questions sur l’interconnexion de réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="4838b-303"><a name="faq"></a>VNet-to-VNet FAQ</span></span>
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="4838b-304">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4838b-304">Next steps</span></span>

* <span data-ttu-id="4838b-305">Une fois la connexion achevée, vous pouvez ajouter des machines virtuelles à vos réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="4838b-305">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="4838b-306">Pour plus d’informations, consultez la [documentation relative aux machines virtuelles](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="4838b-306">For more information, see the [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="4838b-307">Pour plus d’informations sur le protocole BGP, consultez les articles [Vue d’ensemble du protocole BGP](vpn-gateway-bgp-overview.md) et [Comment configurer BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4838b-307">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
