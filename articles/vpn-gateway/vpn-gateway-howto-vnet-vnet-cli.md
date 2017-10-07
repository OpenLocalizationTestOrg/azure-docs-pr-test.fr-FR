---
title: "Connecter le réseau virtuel tooanother réseau virtuel : CLI d’Azure | Documents Microsoft"
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
ms.openlocfilehash: 70113914bcae03c80f9ad133ff081d1cf37fc309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a><span data-ttu-id="66e2e-103">Configurer une connexion de passerelle VPN de réseau virtuel à réseau virtuel à l’aide d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="66e2e-103">Configure a VNet-to-VNet VPN gateway connection using Azure CLI</span></span>

<span data-ttu-id="66e2e-104">Cet article vous montre comment toocreate une connexion de passerelle VPN entre les réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="66e2e-104">This article shows you how toocreate a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="66e2e-105">Hello réseaux virtuels peuvent être hello identiques ou différentes régions, et à partir de hello identiques ou différents abonnements.</span><span class="sxs-lookup"><span data-stu-id="66e2e-105">hello virtual networks can be in hello same or different regions, and from hello same or different subscriptions.</span></span> <span data-ttu-id="66e2e-106">Lors de la connexion des réseaux virtuels à partir de différents abonnements, les abonnements hello n’est pas nécessaire de toobe associé hello même client Active Directory.</span><span class="sxs-lookup"><span data-stu-id="66e2e-106">When connecting VNets from different subscriptions, hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> 

<span data-ttu-id="66e2e-107">étapes de Hello dans cet article appliquent le modèle de déploiement du Gestionnaire de ressources toohello et utilisent CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="66e2e-107">hello steps in this article apply toohello Resource Manager deployment model and use Azure CLI.</span></span> <span data-ttu-id="66e2e-108">Vous pouvez également créer cette configuration à l’aide d’un outil de déploiement différentes ou d’un modèle de déploiement en sélectionnant une option différente de hello suivant liste :</span><span class="sxs-lookup"><span data-stu-id="66e2e-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="66e2e-109">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="66e2e-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="66e2e-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="66e2e-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="66e2e-111">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="66e2e-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="66e2e-112">Portail Azure (classique)</span><span class="sxs-lookup"><span data-stu-id="66e2e-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="66e2e-113">Connexions entre différents modèles de déploiement - Portail Azure</span><span class="sxs-lookup"><span data-stu-id="66e2e-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="66e2e-114">Connexions entre différents modèles de déploiement - PowerShell</span><span class="sxs-lookup"><span data-stu-id="66e2e-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="66e2e-115">Connexion d’un réseau virtuel de réseau virtuel tooanother (au réseau) est tooconnecting comme emplacement d’un site réseau virtuel tooan local.</span><span class="sxs-lookup"><span data-stu-id="66e2e-115">Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="66e2e-116">Les deux types de connectivité utilisent un tooprovide de passerelle VPN un tunnel sécurisé utilisant IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="66e2e-116">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="66e2e-117">Si vos réseaux virtuels sont Bonjour même région, vous souhaiterez peut-être tooconsider les connectant à l’aide de l’homologation de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="66e2e-117">If your VNets are in hello same region, you may want tooconsider connecting them using VNet Peering.</span></span> <span data-ttu-id="66e2e-118">L’homologation de réseaux virtuels (ou VNet Peering) n’utilise pas de passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="66e2e-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="66e2e-119">Pour plus d’informations, consultez l’article [Homologation de réseaux virtuels](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="66e2e-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="66e2e-120">Vous pouvez combiner une communication de réseau virtuel à réseau virtuel avec des configurations multisites.</span><span class="sxs-lookup"><span data-stu-id="66e2e-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="66e2e-121">Cela vous permet d’établir des topologies de réseau qui combinent une connectivité intersite de connectivité de réseau virtuel entre, comme indiqué dans hello suivant schéma :</span><span class="sxs-lookup"><span data-stu-id="66e2e-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in hello following diagram:</span></span>

![À propos des connexions](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <span data-ttu-id="66e2e-123"><a name="why"></a>Pourquoi connecter des réseaux virtuels ?</span><span class="sxs-lookup"><span data-stu-id="66e2e-123"><a name="why"></a>Why connect virtual networks?</span></span>

<span data-ttu-id="66e2e-124">Vous souhaiterez peut-être les réseaux virtuels tooconnect pour hello suivant raisons :</span><span class="sxs-lookup"><span data-stu-id="66e2e-124">You may want tooconnect virtual networks for hello following reasons:</span></span>

* <span data-ttu-id="66e2e-125">**Géo-redondance et présence géographique dans plusieurs régions**</span><span class="sxs-lookup"><span data-stu-id="66e2e-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="66e2e-126">Vous pouvez configurer la géo-réplication ou la synchronisation avec une connectivité sécurisée sans passer par les points de terminaison accessibles sur Internet.</span><span class="sxs-lookup"><span data-stu-id="66e2e-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="66e2e-127">Avec Traffic Manager et l’équilibreur de charge Azure, vous pouvez configurer une charge de travail hautement disponible avec la géo-redondance dans plusieurs régions Azure.</span><span class="sxs-lookup"><span data-stu-id="66e2e-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="66e2e-128">Par exemple important, tooset des SQL Always On avec des groupes de disponibilité répartis dans plusieurs régions Azure.</span><span class="sxs-lookup"><span data-stu-id="66e2e-128">One important example is tooset up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="66e2e-129">**Applications multiniveaux régionales avec une limite d’isolement ou administrative**</span><span class="sxs-lookup"><span data-stu-id="66e2e-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="66e2e-130">Dans hello même région, vous pouvez définir des applications à plusieurs niveaux avec plusieurs réseaux virtuels interconnectés tooisolation ou exigences administratives.</span><span class="sxs-lookup"><span data-stu-id="66e2e-130">Within hello same region, you can set up multi-tier applications with multiple virtual networks connected together due tooisolation or administrative requirements.</span></span>

<span data-ttu-id="66e2e-131">Pour plus d’informations sur les connexions de réseau virtuel à réseau virtuel, consultez hello [FAQ sur le réseau à](#faq) à fin hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="66e2e-131">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span>

### <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="66e2e-132">Quelle procédure dois-je utiliser ?</span><span class="sxs-lookup"><span data-stu-id="66e2e-132">Which set of steps should I use?</span></span>

<span data-ttu-id="66e2e-133">Cet article inclut deux ensembles d’étapes distincts.</span><span class="sxs-lookup"><span data-stu-id="66e2e-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="66e2e-134">Un ensemble d’étapes pour [qui résident dans des réseaux virtuels hello même abonnement](#samesub)et l’autre pour [des réseaux virtuels qui résident dans différents abonnements](#difsub).</span><span class="sxs-lookup"><span data-stu-id="66e2e-134">One set of steps for [VNets that reside in hello same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span>

## <span data-ttu-id="66e2e-135"><a name="samesub"></a>Se connecter à des réseaux virtuels qui se trouvent dans hello même abonnement</span><span class="sxs-lookup"><span data-stu-id="66e2e-135"><a name="samesub"></a>Connect VNets that are in hello same subscription</span></span>

![Diagramme v2v](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="66e2e-137">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="66e2e-137">Before you begin</span></span>

<span data-ttu-id="66e2e-138">Avant de commencer, installez hello dernière version des commandes CLI de hello (version 2.0 ou version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="66e2e-138">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="66e2e-139">Pour plus d’informations sur l’installation des commandes CLI de hello, consultez [installer Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="66e2e-139">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

### <span data-ttu-id="66e2e-140"><a name="Plan"></a>Panifier vos plages d’adresses IP</span><span class="sxs-lookup"><span data-stu-id="66e2e-140"><a name="Plan"></a>Plan your IP address ranges</span></span>

<span data-ttu-id="66e2e-141">Bonjour comme suit, nous créer deux réseaux virtuels, ainsi que leurs sous-réseaux de passerelle respectives et les configurations.</span><span class="sxs-lookup"><span data-stu-id="66e2e-141">In hello following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="66e2e-142">Nous puis créez une connexion VPN entre hello deux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="66e2e-142">We then create a VPN connection between hello two VNets.</span></span> <span data-ttu-id="66e2e-143">Il s’agit des plages d’adresses IP important tooplan hello pour votre configuration réseau.</span><span class="sxs-lookup"><span data-stu-id="66e2e-143">It’s important tooplan hello IP address ranges for your network configuration.</span></span> <span data-ttu-id="66e2e-144">N’oubliez pas que vous devez vous assurer qu’aucune plage de réseaux virtuels ou de réseaux locaux ne se chevauche.</span><span class="sxs-lookup"><span data-stu-id="66e2e-144">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="66e2e-145">Dans ces exemples, nous n’incluons pas de serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="66e2e-145">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="66e2e-146">Si vous souhaitez une résolution de noms pour vos réseaux virtuels, consultez la page [Résolution de noms](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="66e2e-146">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="66e2e-147">Nous utilisons hello valeurs dans les exemples hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="66e2e-147">We use hello following values in hello examples:</span></span>

<span data-ttu-id="66e2e-148">**Valeurs pour TestVNet1 :**</span><span class="sxs-lookup"><span data-stu-id="66e2e-148">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="66e2e-149">Nom du réseau virtuel : TestVNet1</span><span class="sxs-lookup"><span data-stu-id="66e2e-149">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="66e2e-150">Groupe de ressources : TestRG1</span><span class="sxs-lookup"><span data-stu-id="66e2e-150">Resource Group: TestRG1</span></span>
* <span data-ttu-id="66e2e-151">Emplacement : Est des États-Unis</span><span class="sxs-lookup"><span data-stu-id="66e2e-151">Location: East US</span></span>
* <span data-ttu-id="66e2e-152">TestVNet1 : 10.11.0.0/16 et 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="66e2e-152">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="66e2e-153">FrontEnd : 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="66e2e-153">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="66e2e-154">BackEnd : 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="66e2e-154">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="66e2e-155">GatewaySubnet : 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="66e2e-155">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="66e2e-156">GatewayName : VNet1GW</span><span class="sxs-lookup"><span data-stu-id="66e2e-156">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="66e2e-157">Adresse IP publique : VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="66e2e-157">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="66e2e-158">Type de VPN : RouteBased</span><span class="sxs-lookup"><span data-stu-id="66e2e-158">VPNType: RouteBased</span></span>
* <span data-ttu-id="66e2e-159">Connection(1to4) : VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="66e2e-159">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="66e2e-160">Connection(1to5) : VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="66e2e-160">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="66e2e-161">Type de connexion : VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="66e2e-161">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="66e2e-162">**Valeurs pour TestVNet4 :**</span><span class="sxs-lookup"><span data-stu-id="66e2e-162">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="66e2e-163">Nom du réseau virtuel : TestVNet4</span><span class="sxs-lookup"><span data-stu-id="66e2e-163">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="66e2e-164">TestVNet2 : 10.41.0.0/16 et 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="66e2e-164">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="66e2e-165">Serveur frontal : 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="66e2e-165">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="66e2e-166">Serveur principal : 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="66e2e-166">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="66e2e-167">Sous-réseau de passerelle : 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="66e2e-167">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="66e2e-168">Groupe de ressources : TestRG4</span><span class="sxs-lookup"><span data-stu-id="66e2e-168">Resource Group: TestRG4</span></span>
* <span data-ttu-id="66e2e-169">Emplacement : États-Unis de l’Ouest</span><span class="sxs-lookup"><span data-stu-id="66e2e-169">Location: West US</span></span>
* <span data-ttu-id="66e2e-170">Nom de la passerelle : VNet4GW</span><span class="sxs-lookup"><span data-stu-id="66e2e-170">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="66e2e-171">Adresse IP publique : VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="66e2e-171">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="66e2e-172">Type de VPN : RouteBased</span><span class="sxs-lookup"><span data-stu-id="66e2e-172">VPNType: RouteBased</span></span>
* <span data-ttu-id="66e2e-173">Connexion : VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="66e2e-173">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="66e2e-174">Type de connexion : VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="66e2e-174">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="66e2e-175"><a name="Connect"></a>Étape 1 : connecter tooyour abonnement</span><span class="sxs-lookup"><span data-stu-id="66e2e-175"><a name="Connect"></a>Step 1 - Connect tooyour subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <span data-ttu-id="66e2e-176"><a name="TestVNet1"></a>Étape 2 : créez et configurez TestVNet1</span><span class="sxs-lookup"><span data-stu-id="66e2e-176"><a name="TestVNet1"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="66e2e-177">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="66e2e-177">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. <span data-ttu-id="66e2e-178">Créer des sous-réseaux TestVNet1 et hello pour TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="66e2e-178">Create TestVNet1 and hello subnets for TestVNet1.</span></span> <span data-ttu-id="66e2e-179">L’exemple suivant permet de créer un réseau virtuel nommé TestVNet1 et un sous-réseau nommé FrontEnd.</span><span class="sxs-lookup"><span data-stu-id="66e2e-179">This example creates a virtual network named TestVNet1 and a subnet named FrontEnd.</span></span>

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. <span data-ttu-id="66e2e-180">Créer un espace d’adressage supplémentaire pour le sous-réseau du serveur principal hello.</span><span class="sxs-lookup"><span data-stu-id="66e2e-180">Create an additional address space for hello backend subnet.</span></span> <span data-ttu-id="66e2e-181">Notez que dans cette étape, nous spécifier à la fois l’espace d’adressage hello que nous avons créés précédemment et hello espace d’adressage supplémentaire que nous souhaitons tooadd.</span><span class="sxs-lookup"><span data-stu-id="66e2e-181">Notice that in this step, we specify both hello address space that we created earlier, and hello additional address space that we want tooadd.</span></span> <span data-ttu-id="66e2e-182">C’est parce que hello [mise à jour du réseau virtuel az réseau](https://docs.microsoft.com/cli/azure/network/vnet#update) commande remplace les paramètres précédents hello.</span><span class="sxs-lookup"><span data-stu-id="66e2e-182">This is because hello [az network vnet update](https://docs.microsoft.com/cli/azure/network/vnet#update) command overwrites hello previous settings.</span></span> <span data-ttu-id="66e2e-183">Assurez-vous que toospecify tous les préfixes d’adresse hello lors de l’utilisation de cette commande.</span><span class="sxs-lookup"><span data-stu-id="66e2e-183">Make sure toospecify all of hello address prefixes when using this command.</span></span>

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. <span data-ttu-id="66e2e-184">Créer un sous-réseau de back-end hello.</span><span class="sxs-lookup"><span data-stu-id="66e2e-184">Create hello backend subnet.</span></span>
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. <span data-ttu-id="66e2e-185">Créer un sous-réseau de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="66e2e-185">Create hello gateway subnet.</span></span> <span data-ttu-id="66e2e-186">Notez que le sous-réseau passerelle hello est nommé « GatewaySubnet ».</span><span class="sxs-lookup"><span data-stu-id="66e2e-186">Notice that hello gateway subnet is named 'GatewaySubnet'.</span></span> <span data-ttu-id="66e2e-187">Ce nom est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="66e2e-187">This name is required.</span></span> <span data-ttu-id="66e2e-188">Dans cet exemple, sous-réseau de passerelle hello utilise un /27.</span><span class="sxs-lookup"><span data-stu-id="66e2e-188">In this example, hello gateway subnet is using a /27.</span></span> <span data-ttu-id="66e2e-189">Bien qu’il soit possible de toocreate un sous-réseau de passerelle aussi petit que /29, nous vous recommandons de créer un sous-réseau plus grand qui inclut plusieurs adresses en sélectionnant au moins /28 ou /27.</span><span class="sxs-lookup"><span data-stu-id="66e2e-189">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="66e2e-190">Cette opération permettra suffisamment adresses tooaccommodate possibles des configurations supplémentaires que vous pouvez Bonjour futures.</span><span class="sxs-lookup"><span data-stu-id="66e2e-190">This will allow for enough addresses tooaccommodate possible additional configurations that you may want in hello future.</span></span>

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. <span data-ttu-id="66e2e-191">Demander une passerelle publique de toohello alloué toobe adresse IP que vous allez créer pour votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="66e2e-191">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="66e2e-192">Notez que hello AllocationMethod est dynamique.</span><span class="sxs-lookup"><span data-stu-id="66e2e-192">Notice that hello AllocationMethod is Dynamic.</span></span> <span data-ttu-id="66e2e-193">Vous ne pouvez pas spécifier hello adresse IP que vous toouse.</span><span class="sxs-lookup"><span data-stu-id="66e2e-193">You cannot specify hello IP address that you want toouse.</span></span> <span data-ttu-id="66e2e-194">Il est alloué dynamiquement tooyour passerelle.</span><span class="sxs-lookup"><span data-stu-id="66e2e-194">It's dynamically allocated tooyour gateway.</span></span>

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. <span data-ttu-id="66e2e-195">Créer la passerelle de réseau virtuel hello pour TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="66e2e-195">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="66e2e-196">Les configurations de réseau virtuel à réseau virtuel requièrent un VPN de type RouteBased.</span><span class="sxs-lookup"><span data-stu-id="66e2e-196">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="66e2e-197">Si vous exécutez cette commande à l’aide de hello '--aucune - attente' paramètre, vous ne voyez pas vos commentaires ou la sortie.</span><span class="sxs-lookup"><span data-stu-id="66e2e-197">If you run this command using hello '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="66e2e-198">Hello '--aucune - attente' paramètre permet de hello passerelle toocreate en arrière-plan de hello.</span><span class="sxs-lookup"><span data-stu-id="66e2e-198">hello '--no-wait' parameter allows hello gateway toocreate in hello background.</span></span> <span data-ttu-id="66e2e-199">Cela ne signifie pas le terme de la passerelle VPN hello création immédiatement.</span><span class="sxs-lookup"><span data-stu-id="66e2e-199">It does not mean that hello VPN gateway finishes creating immediately.</span></span> <span data-ttu-id="66e2e-200">Création d’une passerelle peut souvent prendre entre 45 minutes ou plus, selon la passerelle de hello référence (SKU) que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="66e2e-200">Creating a gateway can often take 45 minutes or more, depending on hello gateway SKU that you use.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="66e2e-201"><a name="TestVNet4"></a>Étape 3 : créez et configurez TestVNet4</span><span class="sxs-lookup"><span data-stu-id="66e2e-201"><a name="TestVNet4"></a>Step 3 - Create and configure TestVNet4</span></span>

1. <span data-ttu-id="66e2e-202">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="66e2e-202">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. <span data-ttu-id="66e2e-203">Créez TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="66e2e-203">Create TestVNet4.</span></span>

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. <span data-ttu-id="66e2e-204">Créez des sous-réseaux supplémentaires pour TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="66e2e-204">Create additional subnets for TestVNet4.</span></span>

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. <span data-ttu-id="66e2e-205">Créer un sous-réseau de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="66e2e-205">Create hello gateway subnet.</span></span>

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. <span data-ttu-id="66e2e-206">Demandez une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="66e2e-206">Request a Public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. <span data-ttu-id="66e2e-207">Créer la passerelle de réseau virtuel TestVNet4 hello.</span><span class="sxs-lookup"><span data-stu-id="66e2e-207">Create hello TestVNet4 virtual network gateway.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="66e2e-208"><a name="createconnect"></a>Étape 4 : créer des connexions de hello</span><span class="sxs-lookup"><span data-stu-id="66e2e-208"><a name="createconnect"></a>Step 4 - Create hello connections</span></span>

<span data-ttu-id="66e2e-209">Vous avez maintenant deux réseaux virtuels avec des passerelles VPN.</span><span class="sxs-lookup"><span data-stu-id="66e2e-209">You now have two VNets with VPN gateways.</span></span> <span data-ttu-id="66e2e-210">étape suivante de Hello est toocreate connexions de la passerelle VPN entre les passerelles de réseau virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="66e2e-210">hello next step is toocreate VPN gateway connections between hello virtual network gateways.</span></span> <span data-ttu-id="66e2e-211">Si vous avez utilisé les exemples hello ci-dessus, vos passerelles de réseau virtuel sont dans différents groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="66e2e-211">If you used hello examples above, your VNet gateways are in different resource groups.</span></span> <span data-ttu-id="66e2e-212">Lorsque les passerelles se trouvent dans différents groupes de ressources, vous devez tooidentify et ID de ressource hello pour chaque passerelle lors de la connexion.</span><span class="sxs-lookup"><span data-stu-id="66e2e-212">When gateways are in different resource groups, you need tooidentify and specify hello resource IDs for each gateway when making a connection.</span></span> <span data-ttu-id="66e2e-213">Si vos réseaux virtuels sont Bonjour même groupe de ressources, vous pouvez utiliser hello [deuxième ensemble d’instructions](#samerg) , car vous n’avez pas besoin d’ID de ressource toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="66e2e-213">If your VNets are in hello same resource group, you can use hello [second set of instructions](#samerg) because you don't need toospecify hello resource IDs.</span></span>

### <span data-ttu-id="66e2e-214"><a name="diffrg"></a>tooconnect réseaux virtuels qui résident dans différents groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="66e2e-214"><a name="diffrg"></a>tooconnect VNets that reside in different resource groups</span></span>

1. <span data-ttu-id="66e2e-215">Obtenir hello ID de ressource de VNet1GW à partir de la sortie de hello Hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="66e2e-215">Get hello Resource ID of VNet1GW from hello output of hello following command:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="66e2e-216">Dans la sortie de hello, recherchez hello » id : « ligne.</span><span class="sxs-lookup"><span data-stu-id="66e2e-216">In hello output, find hello "id:" line.</span></span> <span data-ttu-id="66e2e-217">les valeurs Hello entre guillemets de hello sont connexion de hello toocreate nécessaires dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="66e2e-217">hello values within hello quotes are needed toocreate hello connection in hello next section.</span></span> <span data-ttu-id="66e2e-218">Copiez ces valeurs tooa éditeur de texte tel que le bloc-notes, afin que vous pouvez facilement collez-les lors de la création de votre connexion.</span><span class="sxs-lookup"><span data-stu-id="66e2e-218">Copy these values tooa text editor, such as Notepad, so that you can easily paste them when creating your connection.</span></span>

  <span data-ttu-id="66e2e-219">Exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="66e2e-219">Example output:</span></span>

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

  <span data-ttu-id="66e2e-220">Copiez les valeurs hello après **« id » :** entre guillemets de hello.</span><span class="sxs-lookup"><span data-stu-id="66e2e-220">Copy hello values after **"id":** within hello quotes.</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. <span data-ttu-id="66e2e-221">Obtenir hello ID de ressource de VNet4GW et copie hello valeurs tooa éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="66e2e-221">Get hello Resource ID of VNet4GW and copy hello values tooa text editor.</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. <span data-ttu-id="66e2e-222">Créer hello TestVNet1 tooTestVNet4 connexion.</span><span class="sxs-lookup"><span data-stu-id="66e2e-222">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="66e2e-223">Dans cette étape, vous créez des connexions de hello à partir de TestVNet1 tooTestVNet4.</span><span class="sxs-lookup"><span data-stu-id="66e2e-223">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="66e2e-224">Il existe une clé partagée est référencée dans les exemples hello.</span><span class="sxs-lookup"><span data-stu-id="66e2e-224">There is a shared key referenced in hello examples.</span></span> <span data-ttu-id="66e2e-225">Vous pouvez utiliser vos propres valeurs pour la clé partagée de hello.</span><span class="sxs-lookup"><span data-stu-id="66e2e-225">You can use your own values for hello shared key.</span></span> <span data-ttu-id="66e2e-226">Hello important est que clé partagée hello doit correspondre pour les deux connexions.</span><span class="sxs-lookup"><span data-stu-id="66e2e-226">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="66e2e-227">Création d’une connexion prend quelques instants toocomplete.</span><span class="sxs-lookup"><span data-stu-id="66e2e-227">Creating a connection takes a short while toocomplete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. <span data-ttu-id="66e2e-228">Créer hello TestVNet4 tooTestVNet1 connexion.</span><span class="sxs-lookup"><span data-stu-id="66e2e-228">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="66e2e-229">Cette étape est similaire toohello une version ultérieure, mais vous créez hello connexion à partir de TestVNet4 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="66e2e-229">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="66e2e-230">Vérifiez que hello partagé clés correspondent.</span><span class="sxs-lookup"><span data-stu-id="66e2e-230">Make sure hello shared keys match.</span></span> <span data-ttu-id="66e2e-231">Il prend quelques minutes de connexion de hello tooestablish.</span><span class="sxs-lookup"><span data-stu-id="66e2e-231">It takes a few minutes tooestablish hello connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. <span data-ttu-id="66e2e-232">Vérifiez vos connexions.</span><span class="sxs-lookup"><span data-stu-id="66e2e-232">Verify your connections.</span></span> <span data-ttu-id="66e2e-233">Consultez [Vérifier votre connexion](#verify).</span><span class="sxs-lookup"><span data-stu-id="66e2e-233">See [Verify your connection](#verify).</span></span>

### <span data-ttu-id="66e2e-234"><a name="samerg"></a>tooconnect réseaux virtuels qui résident dans hello même groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="66e2e-234"><a name="samerg"></a>tooconnect VNets that reside in hello same resource group</span></span>

1. <span data-ttu-id="66e2e-235">Créer hello TestVNet1 tooTestVNet4 connexion.</span><span class="sxs-lookup"><span data-stu-id="66e2e-235">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="66e2e-236">Dans cette étape, vous créez des connexions de hello à partir de TestVNet1 tooTestVNet4.</span><span class="sxs-lookup"><span data-stu-id="66e2e-236">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="66e2e-237">Groupes de ressources hello avis sont hello même dans les exemples hello.</span><span class="sxs-lookup"><span data-stu-id="66e2e-237">Notice hello resource groups are hello same in hello examples.</span></span> <span data-ttu-id="66e2e-238">Vous voyez une clé partagée référencée dans les exemples hello.</span><span class="sxs-lookup"><span data-stu-id="66e2e-238">You also see a shared key referenced in hello examples.</span></span> <span data-ttu-id="66e2e-239">Vous pouvez utiliser vos propres valeurs pour la clé partagée de hello, toutefois, la clé partagée de hello doit correspondre pour les deux connexions.</span><span class="sxs-lookup"><span data-stu-id="66e2e-239">You can use your own values for hello shared key, however, hello shared key must match for both connections.</span></span> <span data-ttu-id="66e2e-240">Création d’une connexion prend quelques instants toocomplete.</span><span class="sxs-lookup"><span data-stu-id="66e2e-240">Creating a connection takes a short while toocomplete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. <span data-ttu-id="66e2e-241">Créer hello TestVNet4 tooTestVNet1 connexion.</span><span class="sxs-lookup"><span data-stu-id="66e2e-241">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="66e2e-242">Cette étape est similaire toohello une version ultérieure, mais vous créez hello connexion à partir de TestVNet4 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="66e2e-242">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="66e2e-243">Vérifiez que hello partagé clés correspondent.</span><span class="sxs-lookup"><span data-stu-id="66e2e-243">Make sure hello shared keys match.</span></span> <span data-ttu-id="66e2e-244">Il prend quelques minutes de connexion de hello tooestablish.</span><span class="sxs-lookup"><span data-stu-id="66e2e-244">It takes a few minutes tooestablish hello connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. <span data-ttu-id="66e2e-245">Vérifiez vos connexions.</span><span class="sxs-lookup"><span data-stu-id="66e2e-245">Verify your connections.</span></span> <span data-ttu-id="66e2e-246">Consultez [Vérifier votre connexion](#verify).</span><span class="sxs-lookup"><span data-stu-id="66e2e-246">See [Verify your connection](#verify).</span></span>

## <span data-ttu-id="66e2e-247"><a name="difsub"></a>Connecter des réseaux virtuels situés dans différents abonnements</span><span class="sxs-lookup"><span data-stu-id="66e2e-247"><a name="difsub"></a>Connect VNets that are in different subscriptions</span></span>

![Diagramme v2v](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

<span data-ttu-id="66e2e-249">Dans ce scénario, nous connectons TestVNet1 et TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="66e2e-249">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="66e2e-250">Hello réseaux virtuels se trouvent à différents abonnements.</span><span class="sxs-lookup"><span data-stu-id="66e2e-250">hello VNets reside different subscriptions.</span></span> <span data-ttu-id="66e2e-251">les abonnements Hello n’est pas nécessaire de toobe associé hello même client Active Directory.</span><span class="sxs-lookup"><span data-stu-id="66e2e-251">hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> <span data-ttu-id="66e2e-252">étapes Hello pour cette configuration ajoutent une connexion au réseau supplémentaire dans l’ordre tooconnect TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="66e2e-252">hello steps for this configuration add an additional VNet-to-VNet connection in order tooconnect TestVNet1 tooTestVNet5.</span></span>

### <span data-ttu-id="66e2e-253"><a name="TestVNet1diff"></a>Étape 5 : créez et configurez TestVNet1</span><span class="sxs-lookup"><span data-stu-id="66e2e-253"><a name="TestVNet1diff"></a>Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="66e2e-254">Ces instructions continuent à partir des étapes hello Bonjour sections précédentes.</span><span class="sxs-lookup"><span data-stu-id="66e2e-254">These instructions continue from hello steps in hello preceding sections.</span></span> <span data-ttu-id="66e2e-255">Vous devez effectuer [étape 1](#Connect) et [étape 2](#TestVNet1) toocreate hello passerelle VPN pour TestVNet1 et configurer TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="66e2e-255">You must complete [Step 1](#Connect) and [Step 2](#TestVNet1) toocreate and configure TestVNet1 and hello VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="66e2e-256">Pour cette configuration, vous n’êtes pas requis toocreate TestVNet4 à partir de la section précédente de hello, bien que si vous créez il, il ne sera pas en conflit avec ces étapes.</span><span class="sxs-lookup"><span data-stu-id="66e2e-256">For this configuration, you are not required toocreate TestVNet4 from hello previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="66e2e-257">Une fois les étapes 1 et 2 effectuées, passez à l’étape 6 (ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="66e2e-257">Once you complete Step 1 and Step 2, continue with Step 6 (below).</span></span>

### <span data-ttu-id="66e2e-258"><a name="verifyranges"></a>Étape 6 : vérifier les plages d’adresses IP hello</span><span class="sxs-lookup"><span data-stu-id="66e2e-258"><a name="verifyranges"></a>Step 6 - Verify hello IP address ranges</span></span>

<span data-ttu-id="66e2e-259">Lorsque vous créez des connexions supplémentaires, il est important tooverify que l’espace d’adressage IP hello de réseau virtuel hello ne se chevauche pas avec les autres plages VNet ou de plages de passerelle de réseau local.</span><span class="sxs-lookup"><span data-stu-id="66e2e-259">When creating additional connections, it's important tooverify that hello IP address space of hello new virtual network does not overlap with any of your other VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="66e2e-260">Dans cet exercice, vous pouvez utiliser hello valeurs pour hello TestVNet5 suivantes :</span><span class="sxs-lookup"><span data-stu-id="66e2e-260">For this exercise, you can use hello following values for hello TestVNet5:</span></span>

<span data-ttu-id="66e2e-261">**Valeurs pour TestVNet5 :**</span><span class="sxs-lookup"><span data-stu-id="66e2e-261">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="66e2e-262">Nom du réseau virtuel : TestVNet5</span><span class="sxs-lookup"><span data-stu-id="66e2e-262">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="66e2e-263">Groupe de ressources : TestRG5</span><span class="sxs-lookup"><span data-stu-id="66e2e-263">Resource Group: TestRG5</span></span>
* <span data-ttu-id="66e2e-264">Emplacement : Japon de l’Est</span><span class="sxs-lookup"><span data-stu-id="66e2e-264">Location: Japan East</span></span>
* <span data-ttu-id="66e2e-265">TestVNet5 : 10.51.0.0/16 et 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="66e2e-265">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="66e2e-266">Serveur frontal : 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="66e2e-266">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="66e2e-267">Serveur principal : 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="66e2e-267">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="66e2e-268">Sous-réseau de passerelle : 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="66e2e-268">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="66e2e-269">Nom de la passerelle : VNet5GW</span><span class="sxs-lookup"><span data-stu-id="66e2e-269">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="66e2e-270">Adresse IP publique : VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="66e2e-270">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="66e2e-271">Type de VPN : RouteBased</span><span class="sxs-lookup"><span data-stu-id="66e2e-271">VPNType: RouteBased</span></span>
* <span data-ttu-id="66e2e-272">Connexion : VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="66e2e-272">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="66e2e-273">Type de connexion : VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="66e2e-273">ConnectionType: VNet2VNet</span></span>

### <span data-ttu-id="66e2e-274"><a name="TestVNet5"></a>Étape 7 : créez et configurez TestVNet5</span><span class="sxs-lookup"><span data-stu-id="66e2e-274"><a name="TestVNet5"></a>Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="66e2e-275">Cette étape doit être effectuée dans le contexte de hello du nouvel abonnement hello, abonnement 5.</span><span class="sxs-lookup"><span data-stu-id="66e2e-275">This step must be done in hello context of hello new subscription, Subscription 5.</span></span> <span data-ttu-id="66e2e-276">Cette partie ne peut être effectuée par administrateur hello dans une autre organisation qui possède l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="66e2e-276">This part may be performed by hello administrator in a different organization that owns hello subscription.</span></span> <span data-ttu-id="66e2e-277">tooswitch entre l’utilisation d’abonnements ' liste des comptes az--tous les ' toolist hello compte tooyour disponible d’abonnements, puis utilisez ' az compte ensemble--abonnement <subscriptionID>' abonnement de toohello tooswitch que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="66e2e-277">tooswitch between subscriptions use 'az account list --all' toolist hello subscriptions available tooyour account, then use 'az account set --subscription <subscriptionID>' tooswitch toohello subscription that you want toouse.</span></span>

1. <span data-ttu-id="66e2e-278">Assurez-vous que vous êtes connectée tooSubscription 5, puis que vous créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="66e2e-278">Make sure you are connected tooSubscription 5, then create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. <span data-ttu-id="66e2e-279">Créez TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="66e2e-279">Create TestVNet5.</span></span>

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. <span data-ttu-id="66e2e-280">Ajoutez des sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="66e2e-280">Add subnets.</span></span>

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. <span data-ttu-id="66e2e-281">Ajouter un sous-réseau de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="66e2e-281">Add hello gateway subnet.</span></span>

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. <span data-ttu-id="66e2e-282">Demandez une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="66e2e-282">Request a public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. <span data-ttu-id="66e2e-283">Créer une passerelle de TestVNet5 hello</span><span class="sxs-lookup"><span data-stu-id="66e2e-283">Create hello TestVNet5 gateway</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="66e2e-284"><a name="connections5"></a>Étape 8 - créer des connexions de hello</span><span class="sxs-lookup"><span data-stu-id="66e2e-284"><a name="connections5"></a>Step 8 - Create hello connections</span></span>

<span data-ttu-id="66e2e-285">Fractionnées cette étape dans deux sessions CLI marqué comme **[1 abonnement]**, et **[abonnement 5]** , car les passerelles hello sont dans des abonnements différents hello.</span><span class="sxs-lookup"><span data-stu-id="66e2e-285">We split this step into two CLI sessions marked as **[Subscription 1]**, and **[Subscription 5]** because hello gateways are in hello different subscriptions.</span></span> <span data-ttu-id="66e2e-286">tooswitch entre l’utilisation d’abonnements ' liste des comptes az--tous les ' toolist hello compte tooyour disponible d’abonnements, puis utilisez ' az compte ensemble--abonnement <subscriptionID>' abonnement de toohello tooswitch que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="66e2e-286">tooswitch between subscriptions use 'az account list --all' toolist hello subscriptions available tooyour account, then use 'az account set --subscription <subscriptionID>' tooswitch toohello subscription that you want toouse.</span></span>

1. <span data-ttu-id="66e2e-287">**[Abonnement 1]**  Se connecter et se connecter tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="66e2e-287">**[Subscription 1]** Log in and connect tooSubscription 1.</span></span> <span data-ttu-id="66e2e-288">Nom de hello tooget et l’ID de hello passerelle à partir de la sortie de hello de commandes suivante d’exécution hello :</span><span class="sxs-lookup"><span data-stu-id="66e2e-288">Run hello following command tooget hello name and ID of hello Gateway from hello output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="66e2e-289">Copier le résultat de hello pour « id : ».</span><span class="sxs-lookup"><span data-stu-id="66e2e-289">Copy hello output for "id:".</span></span> <span data-ttu-id="66e2e-290">Envoi hello ID et nom de hello de hello réseau virtuel (VNet1GW) toohello administrateur de la passerelle de 5 d’abonnement par courrier électronique ou une autre méthode.</span><span class="sxs-lookup"><span data-stu-id="66e2e-290">Send hello ID and hello name of hello VNet gateway (VNet1GW) toohello administrator of Subscription 5 via email or another method.</span></span>

  <span data-ttu-id="66e2e-291">Exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="66e2e-291">Example output:</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. <span data-ttu-id="66e2e-292">**[Abonnement 5]**  Se connecter et se connecter tooSubscription 5.</span><span class="sxs-lookup"><span data-stu-id="66e2e-292">**[Subscription 5]** Log in and connect tooSubscription 5.</span></span> <span data-ttu-id="66e2e-293">Nom de hello tooget et l’ID de hello passerelle à partir de la sortie de hello de commandes suivante d’exécution hello :</span><span class="sxs-lookup"><span data-stu-id="66e2e-293">Run hello following command tooget hello name and ID of hello Gateway from hello output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  <span data-ttu-id="66e2e-294">Copier le résultat de hello pour « id : ».</span><span class="sxs-lookup"><span data-stu-id="66e2e-294">Copy hello output for "id:".</span></span> <span data-ttu-id="66e2e-295">Envoi hello ID et nom de hello de hello réseau virtuel (VNet5GW) toohello administrateur de la passerelle de 1 de l’abonnement par courrier électronique ou une autre méthode.</span><span class="sxs-lookup"><span data-stu-id="66e2e-295">Send hello ID and hello name of hello VNet gateway (VNet5GW) toohello administrator of Subscription 1 via email or another method.</span></span>

3. <span data-ttu-id="66e2e-296">**[Abonnement 1]**  Dans cette étape, vous créez des connexion de hello à partir de TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="66e2e-296">**[Subscription 1]** In this step, you create hello connection from TestVNet1 tooTestVNet5.</span></span> <span data-ttu-id="66e2e-297">Vous pouvez utiliser vos propres valeurs pour la clé partagée de hello, toutefois, la clé partagée de hello doit correspondre pour les deux connexions.</span><span class="sxs-lookup"><span data-stu-id="66e2e-297">You can use your own values for hello shared key, however, hello shared key must match for both connections.</span></span> <span data-ttu-id="66e2e-298">Création d’une connexion peut prendre quelques instants toocomplete.</span><span class="sxs-lookup"><span data-stu-id="66e2e-298">Creating a connection can take a short while toocomplete.</span></span> <span data-ttu-id="66e2e-299">Assurez-vous que vous vous connectez tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="66e2e-299">Make sure you connect tooSubscription 1.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. <span data-ttu-id="66e2e-300">**[Abonnement 5]**  Cette étape est similaire toohello une version ultérieure, mais vous créez hello connexion à partir de TestVNet5 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="66e2e-300">**[Subscription 5]** This step is similar toohello one above, except you are creating hello connection from TestVNet5 tooTestVNet1.</span></span> <span data-ttu-id="66e2e-301">Assurez-vous que hello partagé clés correspondent et que vous vous connectez tooSubscription 5.</span><span class="sxs-lookup"><span data-stu-id="66e2e-301">Make sure that hello shared keys match and that you connect tooSubscription 5.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <span data-ttu-id="66e2e-302"><a name="verify"></a>Vérifiez les connexions hello</span><span class="sxs-lookup"><span data-stu-id="66e2e-302"><a name="verify"></a>Verify hello connections</span></span>
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <span data-ttu-id="66e2e-303"><a name="faq"></a>Forum Aux Questions sur l’interconnexion de réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="66e2e-303"><a name="faq"></a>VNet-to-VNet FAQ</span></span>
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="66e2e-304">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="66e2e-304">Next steps</span></span>

* <span data-ttu-id="66e2e-305">Une fois que votre connexion est terminée, vous pouvez ajouter des machines virtuelles tooyour des réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="66e2e-305">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="66e2e-306">Pour plus d’informations, consultez hello [documentation de Machines virtuelles](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="66e2e-306">For more information, see hello [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="66e2e-307">Pour plus d’informations sur BGP, consultez hello [vue d’ensemble du protocole BGP](vpn-gateway-bgp-overview.md) et [comment tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="66e2e-307">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
