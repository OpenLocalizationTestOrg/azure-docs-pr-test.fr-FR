---
title: "Connecter un réseau virtuel Azure à un autre réseau virtuel : PowerShell | Microsoft Docs"
description: "Cet article vous guide dans l’interconnexion de réseaux virtuels avec Azure Resource Manager et PowerShell"
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
ms.openlocfilehash: 8c42c0046ccaa98c572134042fbbb7e883ef93c3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a><span data-ttu-id="d5db5-103">Configurer une connexion de passerelle VPN de réseau virtuel à réseau virtuel à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="d5db5-103">Configure a VNet-to-VNet VPN gateway connection using PowerShell</span></span>

<span data-ttu-id="d5db5-104">Cet article vous explique comment créer une connexion de passerelle VPN entre des réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="d5db5-104">This article shows you how to create a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="d5db5-105">Les réseaux virtuels peuvent être situés dans des régions identiques ou différentes et appartenir à des abonnements identiques ou différents.</span><span class="sxs-lookup"><span data-stu-id="d5db5-105">The virtual networks can be in the same or different regions, and from the same or different subscriptions.</span></span> <span data-ttu-id="d5db5-106">Lors de la connexion de réseaux virtuels provenant de différents abonnements, les abonnements ne sont pas tenus d’être associés au même locataire Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d5db5-106">When connecting VNets from different subscriptions, the subscriptions do not need to be associated with the same Active Directory tenant.</span></span> 

<span data-ttu-id="d5db5-107">Les étapes mentionnées dans cet article s’appliquent au modèle de déploiement Resource Manager et utilisent PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d5db5-107">The steps in this article apply to the Resource Manager deployment model and use PowerShell.</span></span> <span data-ttu-id="d5db5-108">Vous pouvez également créer cette configuration à l’aide d’un autre outil ou modèle de déploiement en sélectionnant une option différente dans la liste suivante :</span><span class="sxs-lookup"><span data-stu-id="d5db5-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d5db5-109">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="d5db5-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="d5db5-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d5db5-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="d5db5-111">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="d5db5-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="d5db5-112">Portail Azure (classique)</span><span class="sxs-lookup"><span data-stu-id="d5db5-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="d5db5-113">Connexions entre différents modèles de déploiement - Portail Azure</span><span class="sxs-lookup"><span data-stu-id="d5db5-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="d5db5-114">Connexions entre différents modèles de déploiement - PowerShell</span><span class="sxs-lookup"><span data-stu-id="d5db5-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="d5db5-115">La connexion entre deux réseaux virtuels est semblable à la connexion d’un réseau virtuel à un emplacement de site local.</span><span class="sxs-lookup"><span data-stu-id="d5db5-115">Connecting a virtual network to another virtual network (VNet-to-VNet) is similar to connecting a VNet to an on-premises site location.</span></span> <span data-ttu-id="d5db5-116">Les deux types de connectivité font appel à une passerelle VPN pour offrir un tunnel sécurisé utilisant Ipsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="d5db5-116">Both connectivity types use a VPN gateway to provide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="d5db5-117">Si vos réseaux virtuels sont situés dans la même région, vous souhaiterez peut-être les connecter à l’aide de VNet Peering.</span><span class="sxs-lookup"><span data-stu-id="d5db5-117">If your VNets are in the same region, you may want to consider connecting them using VNet Peering.</span></span> <span data-ttu-id="d5db5-118">L’homologation de réseaux virtuels (ou VNet Peering) n’utilise pas de passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="d5db5-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="d5db5-119">Pour plus d’informations, consultez l’article [Homologation de réseaux virtuels](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d5db5-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="d5db5-120">Vous pouvez combiner une communication de réseau virtuel à réseau virtuel avec des configurations multisites.</span><span class="sxs-lookup"><span data-stu-id="d5db5-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="d5db5-121">Vous établissez ainsi des topologies réseau qui combinent une connectivité entre différents locaux et une connectivité entre différents réseaux virtuels, comme indiqué dans le schéma suivant :</span><span class="sxs-lookup"><span data-stu-id="d5db5-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in the following diagram:</span></span>

![À propos des connexions](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a><span data-ttu-id="d5db5-123">Pourquoi connecter des réseaux virtuels ?</span><span class="sxs-lookup"><span data-stu-id="d5db5-123">Why connect virtual networks?</span></span>

<span data-ttu-id="d5db5-124">Vous pouvez décider de connecter des réseaux virtuels pour les raisons suivantes :</span><span class="sxs-lookup"><span data-stu-id="d5db5-124">You may want to connect virtual networks for the following reasons:</span></span>

* <span data-ttu-id="d5db5-125">**Géo-redondance et présence géographique dans plusieurs régions**</span><span class="sxs-lookup"><span data-stu-id="d5db5-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="d5db5-126">Vous pouvez configurer la géo-réplication ou la synchronisation avec une connectivité sécurisée sans passer par les points de terminaison accessibles sur Internet.</span><span class="sxs-lookup"><span data-stu-id="d5db5-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="d5db5-127">Avec Traffic Manager et l’équilibreur de charge Azure, vous pouvez configurer une charge de travail hautement disponible avec la géo-redondance dans plusieurs régions Azure.</span><span class="sxs-lookup"><span data-stu-id="d5db5-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="d5db5-128">Vous pouvez par exemple configurer SQL Always On avec des groupes de disponibilité répartis dans différentes régions Azure.</span><span class="sxs-lookup"><span data-stu-id="d5db5-128">One important example is to set up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="d5db5-129">**Applications multiniveaux régionales avec une limite d’isolement ou administrative**</span><span class="sxs-lookup"><span data-stu-id="d5db5-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="d5db5-130">Dans la même région, vous pouvez configurer des applications multiniveaux avec plusieurs réseaux virtuels interconnectés pour des besoins d’isolement ou d’administration.</span><span class="sxs-lookup"><span data-stu-id="d5db5-130">Within the same region, you can set up multi-tier applications with multiple virtual networks connected together due to isolation or administrative requirements.</span></span>

<span data-ttu-id="d5db5-131">Pour plus d’informations sur les connexions de réseau virtuel à réseau virtuel, consultez le [Forum Aux Questions sur l’interconnexion de réseaux virtuels](#faq) à la fin de cet article.</span><span class="sxs-lookup"><span data-stu-id="d5db5-131">For more information about VNet-to-VNet connections, see the [VNet-to-VNet FAQ](#faq) at the end of this article.</span></span>

## <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="d5db5-132">Quelle procédure dois-je utiliser ?</span><span class="sxs-lookup"><span data-stu-id="d5db5-132">Which set of steps should I use?</span></span>

<span data-ttu-id="d5db5-133">Cet article inclut deux ensembles d’étapes distincts.</span><span class="sxs-lookup"><span data-stu-id="d5db5-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="d5db5-134">L’un des ensembles est destiné aux [réseaux virtuels qui se trouvent dans le même abonnement](#samesub), et l’autre aux [réseaux virtuels qui se trouvent dans des abonnements différents](#difsub).</span><span class="sxs-lookup"><span data-stu-id="d5db5-134">One set of steps for [VNets that reside in the same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span> <span data-ttu-id="d5db5-135">La principale différence réside dans le fait que vous puissiez ou non créer et configurer toutes les ressources de passerelle et de réseau virtuel au sein de la même session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d5db5-135">The key difference between the sets is whether you can create and configure all virtual network and gateway resources within the same PowerShell session.</span></span>

<span data-ttu-id="d5db5-136">Les étapes de cet article utilisent les variables déclarées au début de chaque section.</span><span class="sxs-lookup"><span data-stu-id="d5db5-136">The steps in this article use variables that are declared at the beginning of each section.</span></span> <span data-ttu-id="d5db5-137">Si vous travaillez déjà avec des réseaux virtuels existants, modifiez les variables pour les adapter aux paramètres de votre propre environnement.</span><span class="sxs-lookup"><span data-stu-id="d5db5-137">If you already are working with existing VNets, modify the variables to reflect the settings in your own environment.</span></span> <span data-ttu-id="d5db5-138">Si vous souhaitez une résolution de noms pour vos réseaux virtuels, consultez la page [Résolution de noms](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="d5db5-138">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

## <span data-ttu-id="d5db5-139"><a name="samesub"></a>Connexion de réseaux virtuels situés dans le même abonnement</span><span class="sxs-lookup"><span data-stu-id="d5db5-139"><a name="samesub"></a>How to connect VNets that are in the same subscription</span></span>

![Diagramme v2v](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="d5db5-141">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="d5db5-141">Before you begin</span></span>

<span data-ttu-id="d5db5-142">Au préalable, vous devez installer la dernière version des applets de commande PowerShell Azure Resource Manager, au moins la version 4.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d5db5-142">Before beginning, you need to install the latest version of the Azure Resource Manager PowerShell cmdlets, at least 4.0 or later.</span></span> <span data-ttu-id="d5db5-143">Pour plus d’informations sur l’installation des applets de commande PowerShell, consultez [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d5db5-143">For more information about installing the PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="d5db5-144"><a name="Step1"></a>Étape 1 : planifier vos plages d’adresses IP</span><span class="sxs-lookup"><span data-stu-id="d5db5-144"><a name="Step1"></a>Step 1 - Plan your IP address ranges</span></span>

<span data-ttu-id="d5db5-145">Dans les étapes suivantes, nous allons créer deux réseaux virtuels avec leurs sous-réseaux de passerelle respectifs et leur configuration.</span><span class="sxs-lookup"><span data-stu-id="d5db5-145">In the following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="d5db5-146">Nous allons ensuite créer une connexion VPN entre les deux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="d5db5-146">We then create a VPN connection between the two VNets.</span></span> <span data-ttu-id="d5db5-147">Il est important de planifier les plages d’adresses IP pour votre configuration réseau.</span><span class="sxs-lookup"><span data-stu-id="d5db5-147">It’s important to plan the IP address ranges for your network configuration.</span></span> <span data-ttu-id="d5db5-148">N’oubliez pas que vous devez vous assurer qu’aucune plage de réseaux virtuels ou de réseaux locaux ne se chevauche.</span><span class="sxs-lookup"><span data-stu-id="d5db5-148">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="d5db5-149">Dans ces exemples, nous n’incluons pas de serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="d5db5-149">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="d5db5-150">Si vous souhaitez une résolution de noms pour vos réseaux virtuels, consultez la page [Résolution de noms](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="d5db5-150">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="d5db5-151">Nous utilisons les valeurs suivantes dans les exemples :</span><span class="sxs-lookup"><span data-stu-id="d5db5-151">We use the following values in the examples:</span></span>

<span data-ttu-id="d5db5-152">**Valeurs pour TestVNet1 :**</span><span class="sxs-lookup"><span data-stu-id="d5db5-152">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="d5db5-153">Nom du réseau virtuel : TestVNet1</span><span class="sxs-lookup"><span data-stu-id="d5db5-153">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="d5db5-154">Groupe de ressources : TestRG1</span><span class="sxs-lookup"><span data-stu-id="d5db5-154">Resource Group: TestRG1</span></span>
* <span data-ttu-id="d5db5-155">Emplacement : Est des États-Unis</span><span class="sxs-lookup"><span data-stu-id="d5db5-155">Location: East US</span></span>
* <span data-ttu-id="d5db5-156">TestVNet1 : 10.11.0.0/16 et 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="d5db5-156">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="d5db5-157">FrontEnd : 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="d5db5-157">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="d5db5-158">BackEnd : 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="d5db5-158">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="d5db5-159">GatewaySubnet : 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="d5db5-159">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="d5db5-160">GatewayName : VNet1GW</span><span class="sxs-lookup"><span data-stu-id="d5db5-160">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="d5db5-161">Adresse IP publique : VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="d5db5-161">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="d5db5-162">Type de VPN : RouteBased</span><span class="sxs-lookup"><span data-stu-id="d5db5-162">VPNType: RouteBased</span></span>
* <span data-ttu-id="d5db5-163">Connection(1to4) : VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="d5db5-163">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="d5db5-164">Connection(1to5) : VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="d5db5-164">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="d5db5-165">Type de connexion : VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="d5db5-165">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="d5db5-166">**Valeurs pour TestVNet4 :**</span><span class="sxs-lookup"><span data-stu-id="d5db5-166">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="d5db5-167">Nom du réseau virtuel : TestVNet4</span><span class="sxs-lookup"><span data-stu-id="d5db5-167">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="d5db5-168">TestVNet2 : 10.41.0.0/16 et 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="d5db5-168">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="d5db5-169">Serveur frontal : 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="d5db5-169">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="d5db5-170">Serveur principal : 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="d5db5-170">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="d5db5-171">Sous-réseau de passerelle : 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="d5db5-171">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="d5db5-172">Groupe de ressources : TestRG4</span><span class="sxs-lookup"><span data-stu-id="d5db5-172">Resource Group: TestRG4</span></span>
* <span data-ttu-id="d5db5-173">Emplacement : États-Unis de l’Ouest</span><span class="sxs-lookup"><span data-stu-id="d5db5-173">Location: West US</span></span>
* <span data-ttu-id="d5db5-174">Nom de la passerelle : VNet4GW</span><span class="sxs-lookup"><span data-stu-id="d5db5-174">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="d5db5-175">Adresse IP publique : VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="d5db5-175">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="d5db5-176">Type de VPN : RouteBased</span><span class="sxs-lookup"><span data-stu-id="d5db5-176">VPNType: RouteBased</span></span>
* <span data-ttu-id="d5db5-177">Connexion : VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="d5db5-177">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="d5db5-178">Type de connexion : VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="d5db5-178">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="d5db5-179"><a name="Step2"></a>Étape 2 : créez et configurez TestVNet1</span><span class="sxs-lookup"><span data-stu-id="d5db5-179"><a name="Step2"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="d5db5-180">Déclarez vos variables.</span><span class="sxs-lookup"><span data-stu-id="d5db5-180">Declare your variables.</span></span> <span data-ttu-id="d5db5-181">Cet exemple déclare les variables avec les valeurs de cet exercice.</span><span class="sxs-lookup"><span data-stu-id="d5db5-181">This example declares the variables using the values for this exercise.</span></span> <span data-ttu-id="d5db5-182">Dans la plupart des cas, vous devez remplacer les valeurs par les vôtres.</span><span class="sxs-lookup"><span data-stu-id="d5db5-182">In most cases, you should replace the values with your own.</span></span> <span data-ttu-id="d5db5-183">Cependant, vous pouvez utiliser ces variables si vous exécutez la procédure pour vous familiariser avec ce type de configuration.</span><span class="sxs-lookup"><span data-stu-id="d5db5-183">However, you can use these variables if you are running through the steps to become familiar with this type of configuration.</span></span> <span data-ttu-id="d5db5-184">Si besoin, modifiez les variables, puis copiez et collez-les dans la console PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d5db5-184">Modify the variables if needed, then copy and paste them into your PowerShell console.</span></span>

  ```powershell
  $Sub1 = "Replace_With_Your_Subcription_Name"
  $RG1 = "TestRG1"
  $Location1 = "East US"
  $VNetName1 = "TestVNet1"
  $FESubName1 = "FrontEnd"
  $BESubName1 = "Backend"
  $GWSubName1 = "GatewaySubnet"
  $VNetPrefix11 = "10.11.0.0/16"
  $VNetPrefix12 = "10.12.0.0/16"
  $FESubPrefix1 = "10.11.0.0/24"
  $BESubPrefix1 = "10.12.0.0/24"
  $GWSubPrefix1 = "10.12.255.0/27"
  $GWName1 = "VNet1GW"
  $GWIPName1 = "VNet1GWIP"
  $GWIPconfName1 = "gwipconf1"
  $Connection14 = "VNet1toVNet4"
  $Connection15 = "VNet1toVNet5"
  ```

2. <span data-ttu-id="d5db5-185">Se connecter à votre compte.</span><span class="sxs-lookup"><span data-stu-id="d5db5-185">Connect to your account.</span></span> <span data-ttu-id="d5db5-186">Utilisez l’exemple suivant pour faciliter votre connexion :</span><span class="sxs-lookup"><span data-stu-id="d5db5-186">Use the following example to help you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="d5db5-187">Vérifiez les abonnements associés au compte.</span><span class="sxs-lookup"><span data-stu-id="d5db5-187">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="d5db5-188">Spécifiez l’abonnement que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="d5db5-188">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. <span data-ttu-id="d5db5-189">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="d5db5-189">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. <span data-ttu-id="d5db5-190">Créez les configurations de sous-réseau pour TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="d5db5-190">Create the subnet configurations for TestVNet1.</span></span> <span data-ttu-id="d5db5-191">Cet exemple crée un réseau virtuel nommé TestVNet1 et trois sous-réseaux nommés GatewaySubnet, FrontEnd et Backend.</span><span class="sxs-lookup"><span data-stu-id="d5db5-191">This example creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="d5db5-192">Lorsque vous remplacez les valeurs, pensez à toujours nommer votre sous-réseau de passerelle « GatewaySubnet ».</span><span class="sxs-lookup"><span data-stu-id="d5db5-192">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="d5db5-193">Si vous le nommez autrement, la création de votre passerelle échoue.</span><span class="sxs-lookup"><span data-stu-id="d5db5-193">If you name it something else, your gateway creation fails.</span></span>

  <span data-ttu-id="d5db5-194">L’exemple suivant utilise les variables définies précédemment.</span><span class="sxs-lookup"><span data-stu-id="d5db5-194">The following example uses the variables that you set earlier.</span></span> <span data-ttu-id="d5db5-195">Dans cet exemple, le sous-réseau de passerelle utilise /27.</span><span class="sxs-lookup"><span data-stu-id="d5db5-195">In this example, the gateway subnet is using a /27.</span></span> <span data-ttu-id="d5db5-196">Bien qu’il soit possible de créer un sous-réseau de passerelle aussi petit que /29, nous vous recommandons de créer un sous-réseau plus vaste qui inclut un plus grand nombre d’adresses en sélectionnant au moins /28 ou /27.</span><span class="sxs-lookup"><span data-stu-id="d5db5-196">While it is possible to create a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="d5db5-197">Cela permettra à un nombre suffisant d’adresses de s’adapter à de possibles configurations supplémentaires possibles que vous êtes susceptible de souhaiter par la suite.</span><span class="sxs-lookup"><span data-stu-id="d5db5-197">This will allow for enough addresses to accommodate possible additional configurations that you may want in the future.</span></span>

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. <span data-ttu-id="d5db5-198">Créez TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="d5db5-198">Create TestVNet1.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. <span data-ttu-id="d5db5-199">Demandez l’allocation d’une adresse IP publique à la passerelle que vous allez créer pour votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="d5db5-199">Request a public IP address to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="d5db5-200">Notez que la valeur AllocationMethod est dynamique.</span><span class="sxs-lookup"><span data-stu-id="d5db5-200">Notice that the AllocationMethod is Dynamic.</span></span> <span data-ttu-id="d5db5-201">Vous ne pouvez pas spécifier l’adresse IP que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="d5db5-201">You cannot specify the IP address that you want to use.</span></span> <span data-ttu-id="d5db5-202">Elle est allouée à votre passerelle de façon dynamique.</span><span class="sxs-lookup"><span data-stu-id="d5db5-202">It's dynamically allocated to your gateway.</span></span> 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="d5db5-203">Créez la configuration de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="d5db5-203">Create the gateway configuration.</span></span> <span data-ttu-id="d5db5-204">La configuration de la passerelle définit le sous-réseau et l’adresse IP publique à utiliser.</span><span class="sxs-lookup"><span data-stu-id="d5db5-204">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="d5db5-205">Utilisez l’exemple pour créer la configuration de votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="d5db5-205">Use the example to create your gateway configuration.</span></span>

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. <span data-ttu-id="d5db5-206">Créez la passerelle pour TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="d5db5-206">Create the gateway for TestVNet1.</span></span> <span data-ttu-id="d5db5-207">Dans cette étape, vous créez la passerelle de réseau virtuel de votre TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="d5db5-207">In this step, you create the virtual network gateway for your TestVNet1.</span></span> <span data-ttu-id="d5db5-208">Les configurations de réseau virtuel à réseau virtuel requièrent un VPN de type RouteBased.</span><span class="sxs-lookup"><span data-stu-id="d5db5-208">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="d5db5-209">La création d’une passerelle nécessite généralement au moins 45 minutes, selon la référence SKU de passerelle sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="d5db5-209">Creating a gateway can often take 45 minutes or more, depending on the selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a><span data-ttu-id="d5db5-210">Étape 3 : créez et configurez TestVNet4</span><span class="sxs-lookup"><span data-stu-id="d5db5-210">Step 3 - Create and configure TestVNet4</span></span>

<span data-ttu-id="d5db5-211">Une fois que vous avez configuré TestVNet1, créez TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="d5db5-211">Once you've configured TestVNet1, create TestVNet4.</span></span> <span data-ttu-id="d5db5-212">Suivez les étapes ci-dessous, en remplaçant les valeurs par les vôtres si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d5db5-212">Follow the steps below, replacing the values with your own when needed.</span></span> <span data-ttu-id="d5db5-213">Cette étape peut être réalisée dans la même session PowerShell, car elle se trouve dans le même abonnement.</span><span class="sxs-lookup"><span data-stu-id="d5db5-213">This step can be done within the same PowerShell session because it is in the same subscription.</span></span>

1. <span data-ttu-id="d5db5-214">Déclarez vos variables.</span><span class="sxs-lookup"><span data-stu-id="d5db5-214">Declare your variables.</span></span> <span data-ttu-id="d5db5-215">Veillez à remplacer les valeurs par celles que vous souhaitez utiliser pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="d5db5-215">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

  ```powershell
  $RG4 = "TestRG4"
  $Location4 = "West US"
  $VnetName4 = "TestVNet4"
  $FESubName4 = "FrontEnd"
  $BESubName4 = "Backend"
  $GWSubName4 = "GatewaySubnet"
  $VnetPrefix41 = "10.41.0.0/16"
  $VnetPrefix42 = "10.42.0.0/16"
  $FESubPrefix4 = "10.41.0.0/24"
  $BESubPrefix4 = "10.42.0.0/24"
  $GWSubPrefix4 = "10.42.255.0/27"
  $GWName4 = "VNet4GW"
  $GWIPName4 = "VNet4GWIP"
  $GWIPconfName4 = "gwipconf4"
  $Connection41 = "VNet4toVNet1"
  ```
2. <span data-ttu-id="d5db5-216">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="d5db5-216">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. <span data-ttu-id="d5db5-217">Créez les configurations de sous-réseau pour TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="d5db5-217">Create the subnet configurations for TestVNet4.</span></span>

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. <span data-ttu-id="d5db5-218">Créez TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="d5db5-218">Create TestVNet4.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. <span data-ttu-id="d5db5-219">Demandez une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="d5db5-219">Request a public IP address.</span></span>

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. <span data-ttu-id="d5db5-220">Créez la configuration de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="d5db5-220">Create the gateway configuration.</span></span>

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. <span data-ttu-id="d5db5-221">Créer la passerelle TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="d5db5-221">Create the TestVNet4 gateway.</span></span> <span data-ttu-id="d5db5-222">La création d’une passerelle nécessite généralement au moins 45 minutes, selon la référence SKU de passerelle sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="d5db5-222">Creating a gateway can often take 45 minutes or more, depending on the selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-the-connections"></a><span data-ttu-id="d5db5-223">Étape 4 : créez les connexions</span><span class="sxs-lookup"><span data-stu-id="d5db5-223">Step 4 - Create the connections</span></span>

1. <span data-ttu-id="d5db5-224">Obtenez les passerelles de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="d5db5-224">Get both virtual network gateways.</span></span> <span data-ttu-id="d5db5-225">Si les deux passerelles appartiennent au même abonnement, comme dans l’exemple, vous pouvez effectuer cette étape dans la même session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d5db5-225">If both of the gateways are in the same subscription, as they are in the example, you can complete this step in the same PowerShell session.</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. <span data-ttu-id="d5db5-226">Créez la connexion de TestVNet1 à TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="d5db5-226">Create the TestVNet1 to TestVNet4 connection.</span></span> <span data-ttu-id="d5db5-227">Lors de cette étape, vous créez la connexion de TestVNet1 à TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="d5db5-227">In this step, you create the connection from TestVNet1 to TestVNet4.</span></span> <span data-ttu-id="d5db5-228">Une clé partagée est référencée dans les exemples.</span><span class="sxs-lookup"><span data-stu-id="d5db5-228">You'll see a shared key referenced in the examples.</span></span> <span data-ttu-id="d5db5-229">Vous pouvez utiliser vos propres valeurs pour cette clé partagée.</span><span class="sxs-lookup"><span data-stu-id="d5db5-229">You can use your own values for the shared key.</span></span> <span data-ttu-id="d5db5-230">Il est important que la clé partagée corresponde aux deux connexions.</span><span class="sxs-lookup"><span data-stu-id="d5db5-230">The important thing is that the shared key must match for both connections.</span></span> <span data-ttu-id="d5db5-231">La création d’une connexion peut prendre quelques instants.</span><span class="sxs-lookup"><span data-stu-id="d5db5-231">Creating a connection can take a short while to complete.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. <span data-ttu-id="d5db5-232">Créez la connexion de TestVNet4 à TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="d5db5-232">Create the TestVNet4 to TestVNet1 connection.</span></span> <span data-ttu-id="d5db5-233">Cette étape est similaire à celle présentée ci-dessus, sauf que vous créez la connexion de TestVNet4 à TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="d5db5-233">This step is similar to the one above, except you are creating the connection from TestVNet4 to TestVNet1.</span></span> <span data-ttu-id="d5db5-234">Vérifiez que les clés partagées correspondent.</span><span class="sxs-lookup"><span data-stu-id="d5db5-234">Make sure the shared keys match.</span></span> <span data-ttu-id="d5db5-235">Après quelques minutes, la connexion est établie.</span><span class="sxs-lookup"><span data-stu-id="d5db5-235">The connection will be established after a few minutes.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="d5db5-236">Vérifiez votre connexion.</span><span class="sxs-lookup"><span data-stu-id="d5db5-236">Verify your connection.</span></span> <span data-ttu-id="d5db5-237">Consultez la section [Vérification de votre connexion](#verify).</span><span class="sxs-lookup"><span data-stu-id="d5db5-237">See the section [How to verify your connection](#verify).</span></span>

## <span data-ttu-id="d5db5-238"><a name="difsub"></a>Connexion de réseaux virtuels situés dans différents abonnements</span><span class="sxs-lookup"><span data-stu-id="d5db5-238"><a name="difsub"></a>How to connect VNets that are in different subscriptions</span></span>

![Diagramme v2v](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

<span data-ttu-id="d5db5-240">Dans ce scénario, nous connectons TestVNet1 et TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="d5db5-240">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="d5db5-241">TestVNet1 et TestVNet5 se trouvent dans des abonnements différents.</span><span class="sxs-lookup"><span data-stu-id="d5db5-241">TestVNet1 and TestVNet5 reside in a different subscription.</span></span> <span data-ttu-id="d5db5-242">Les abonnements ne sont pas tenus d’être associés au même locataire Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d5db5-242">The subscriptions do not need to be associated with the same Active Directory tenant.</span></span> <span data-ttu-id="d5db5-243">La différence entre ce processus et le précédent réside dans le fait qu’une partie des étapes de configuration doit être exécutée dans une session PowerShell distincte dans le contexte d’un deuxième abonnement.</span><span class="sxs-lookup"><span data-stu-id="d5db5-243">The difference between these steps and the previous set is that some of the configuration steps need to be performed in a separate PowerShell session in the context of the second subscription.</span></span> <span data-ttu-id="d5db5-244">notamment lorsque les deux abonnements appartiennent à différentes organisations.</span><span class="sxs-lookup"><span data-stu-id="d5db5-244">Especially when the two subscriptions belong to different organizations.</span></span>

### <a name="step-5---create-and-configure-testvnet1"></a><span data-ttu-id="d5db5-245">Étape 5 : créez et configurez TestVNet1</span><span class="sxs-lookup"><span data-stu-id="d5db5-245">Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="d5db5-246">Vous devez terminer les étapes [1](#Step1) et [2](#Step2) de la section précédente pour créer et configurer TestVNet1 et la passerelle VPN pour TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="d5db5-246">You must complete [Step 1](#Step1) and [Step 2](#Step2) from the previous section to create and configure TestVNet1 and the VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="d5db5-247">Pour cette configuration, vous n’êtes pas obligé de créer TestVNet4 de la section précédente. Même si vous le créez, ce dernier n’entrera pas en conflit avec ces étapes.</span><span class="sxs-lookup"><span data-stu-id="d5db5-247">For this configuration, you are not required to create TestVNet4 from the previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="d5db5-248">Une fois les étapes 1 et 2 effectuées, passez à l’étape 6 pour créer TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="d5db5-248">Once you complete Step 1 and Step 2, continue with Step 6 to create TestVNet5.</span></span> 

### <a name="step-6---verify-the-ip-address-ranges"></a><span data-ttu-id="d5db5-249">Étape 6 : vérifiez les plages d’adresses IP</span><span class="sxs-lookup"><span data-stu-id="d5db5-249">Step 6 - Verify the IP address ranges</span></span>

<span data-ttu-id="d5db5-250">Il est important de s’assurer que l’espace d’adressage IP du nouveau réseau virtuel TestVNet5 ne chevauche aucune de vos plages de réseaux virtuels ou de passerelles de réseau locales.</span><span class="sxs-lookup"><span data-stu-id="d5db5-250">It is important to make sure that the IP address space of the new virtual network, TestVNet5, does not overlap with any of your VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="d5db5-251">Dans cet exemple, les réseaux virtuels peuvent appartenir à différentes organisations.</span><span class="sxs-lookup"><span data-stu-id="d5db5-251">In this example, the virtual networks may belong to different organizations.</span></span> <span data-ttu-id="d5db5-252">Pour cet exercice, vous pouvez utiliser les valeurs suivantes pour TestVNet5 :</span><span class="sxs-lookup"><span data-stu-id="d5db5-252">For this exercise, you can use the following values for the TestVNet5:</span></span>

<span data-ttu-id="d5db5-253">**Valeurs pour TestVNet5 :**</span><span class="sxs-lookup"><span data-stu-id="d5db5-253">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="d5db5-254">Nom du réseau virtuel : TestVNet5</span><span class="sxs-lookup"><span data-stu-id="d5db5-254">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="d5db5-255">Groupe de ressources : TestRG5</span><span class="sxs-lookup"><span data-stu-id="d5db5-255">Resource Group: TestRG5</span></span>
* <span data-ttu-id="d5db5-256">Emplacement : Japon de l’Est</span><span class="sxs-lookup"><span data-stu-id="d5db5-256">Location: Japan East</span></span>
* <span data-ttu-id="d5db5-257">TestVNet5 : 10.51.0.0/16 et 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="d5db5-257">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="d5db5-258">Serveur frontal : 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="d5db5-258">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="d5db5-259">Serveur principal : 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="d5db5-259">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="d5db5-260">Sous-réseau de passerelle : 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="d5db5-260">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="d5db5-261">Nom de la passerelle : VNet5GW</span><span class="sxs-lookup"><span data-stu-id="d5db5-261">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="d5db5-262">Adresse IP publique : VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="d5db5-262">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="d5db5-263">Type de VPN : RouteBased</span><span class="sxs-lookup"><span data-stu-id="d5db5-263">VPNType: RouteBased</span></span>
* <span data-ttu-id="d5db5-264">Connexion : VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="d5db5-264">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="d5db5-265">Type de connexion : VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="d5db5-265">ConnectionType: VNet2VNet</span></span>

### <a name="step-7---create-and-configure-testvnet5"></a><span data-ttu-id="d5db5-266">Étape 7 : créez et configurez TestVNet5</span><span class="sxs-lookup"><span data-stu-id="d5db5-266">Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="d5db5-267">Cette étape doit être effectuée dans le cadre du nouvel abonnement.</span><span class="sxs-lookup"><span data-stu-id="d5db5-267">This step must be done in the context of the new subscription.</span></span> <span data-ttu-id="d5db5-268">Cette partie peut être effectuée par l’administrateur dans une organisation différente qui possède l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="d5db5-268">This part may be performed by the administrator in a different organization that owns the subscription.</span></span>

1. <span data-ttu-id="d5db5-269">Déclarez vos variables.</span><span class="sxs-lookup"><span data-stu-id="d5db5-269">Declare your variables.</span></span> <span data-ttu-id="d5db5-270">Veillez à remplacer les valeurs par celles que vous souhaitez utiliser pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="d5db5-270">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

  ```powershell
  $Sub5 = "Replace_With_the_New_Subcription_Name"
  $RG5 = "TestRG5"
  $Location5 = "Japan East"
  $VnetName5 = "TestVNet5"
  $FESubName5 = "FrontEnd"
  $BESubName5 = "Backend"
  $GWSubName5 = "GatewaySubnet"
  $VnetPrefix51 = "10.51.0.0/16"
  $VnetPrefix52 = "10.52.0.0/16"
  $FESubPrefix5 = "10.51.0.0/24"
  $BESubPrefix5 = "10.52.0.0/24"
  $GWSubPrefix5 = "10.52.255.0/27"
  $GWName5 = "VNet5GW"
  $GWIPName5 = "VNet5GWIP"
  $GWIPconfName5 = "gwipconf5"
  $Connection51 = "VNet5toVNet1"
  ```
2. <span data-ttu-id="d5db5-271">Connectez-vous à l’abonnement 5.</span><span class="sxs-lookup"><span data-stu-id="d5db5-271">Connect to subscription 5.</span></span> <span data-ttu-id="d5db5-272">Ouvrez la console PowerShell et connectez-vous à votre compte.</span><span class="sxs-lookup"><span data-stu-id="d5db5-272">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="d5db5-273">Utilisez l’exemple suivant pour faciliter votre connexion :</span><span class="sxs-lookup"><span data-stu-id="d5db5-273">Use the following sample to help you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="d5db5-274">Vérifiez les abonnements associés au compte.</span><span class="sxs-lookup"><span data-stu-id="d5db5-274">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="d5db5-275">Spécifiez l’abonnement que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="d5db5-275">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. <span data-ttu-id="d5db5-276">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="d5db5-276">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. <span data-ttu-id="d5db5-277">Créez les configurations de sous-réseau pour TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="d5db5-277">Create the subnet configurations for TestVNet5.</span></span>

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. <span data-ttu-id="d5db5-278">Créez TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="d5db5-278">Create TestVNet5.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. <span data-ttu-id="d5db5-279">Demandez une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="d5db5-279">Request a public IP address.</span></span>

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="d5db5-280">Créez la configuration de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="d5db5-280">Create the gateway configuration.</span></span>

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. <span data-ttu-id="d5db5-281">Créez la passerelle TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="d5db5-281">Create the TestVNet5 gateway.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-the-connections"></a><span data-ttu-id="d5db5-282">Étape 8 : créez les connexions</span><span class="sxs-lookup"><span data-stu-id="d5db5-282">Step 8 - Create the connections</span></span>

<span data-ttu-id="d5db5-283">Dans cet exemple, étant donné que les passerelles se trouvent dans différents abonnements, nous avons divisé cette étape en deux sessions PowerShell notées [Abonnement 1] et [Abonnement 5].</span><span class="sxs-lookup"><span data-stu-id="d5db5-283">In this example, because the gateways are in the different subscriptions, we've split this step into two PowerShell sessions marked as [Subscription 1] and [Subscription 5].</span></span>

1. <span data-ttu-id="d5db5-284">**[Abonnement 1]** Obtenez la passerelle de réseau virtuel pour Abonnement 1.</span><span class="sxs-lookup"><span data-stu-id="d5db5-284">**[Subscription 1]** Get the virtual network gateway for Subscription 1.</span></span> <span data-ttu-id="d5db5-285">Se connecter et se connecter à Abonnement 1 avant d’exécuter l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="d5db5-285">Log in and connect to Subscription 1 before running the following example:</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  <span data-ttu-id="d5db5-286">Copiez la sortie des éléments suivants et envoyez-la à l’administrateur d’Abonnement 5 par message électronique ou une autre méthode.</span><span class="sxs-lookup"><span data-stu-id="d5db5-286">Copy the output of the following elements and send these to the administrator of Subscription 5 via email or another method.</span></span>

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  <span data-ttu-id="d5db5-287">Ces deux éléments ont des valeurs similaires à l’exemple de sortie suivant :</span><span class="sxs-lookup"><span data-stu-id="d5db5-287">These two elements will have values similar to the following example output:</span></span>

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. <span data-ttu-id="d5db5-288">**[Abonnement 5]** Obtenez la passerelle de réseau virtuel pour Abonnement 5.</span><span class="sxs-lookup"><span data-stu-id="d5db5-288">**[Subscription 5]** Get the virtual network gateway for Subscription 5.</span></span> <span data-ttu-id="d5db5-289">Se connecter et se connecter à Abonnement 5 avant d’exécuter l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="d5db5-289">Log in and connect to Subscription 5 before running the following example:</span></span>

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  <span data-ttu-id="d5db5-290">Copiez la sortie des éléments suivants et envoyez-la à l’administrateur d’Abonnement 1 par message électronique ou une autre méthode.</span><span class="sxs-lookup"><span data-stu-id="d5db5-290">Copy the output of the following elements and send these to the administrator of Subscription 1 via email or another method.</span></span>

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  <span data-ttu-id="d5db5-291">Ces deux éléments ont des valeurs similaires à l’exemple de sortie suivant :</span><span class="sxs-lookup"><span data-stu-id="d5db5-291">These two elements will have values similar to the following example output:</span></span>

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. <span data-ttu-id="d5db5-292">**[Abonnement 1]** Créez la connexion TestVNet1 à TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="d5db5-292">**[Subscription 1]** Create the TestVNet1 to TestVNet5 connection.</span></span> <span data-ttu-id="d5db5-293">Dans cette étape, vous créez la connexion de TestVNet1 à TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="d5db5-293">In this step, you create the connection from TestVNet1 to TestVNet5.</span></span> <span data-ttu-id="d5db5-294">La différence réside dans le fait que $vnet5gw ne peut pas être obtenu directement, car il se trouve dans un abonnement différent.</span><span class="sxs-lookup"><span data-stu-id="d5db5-294">The difference here is that $vnet5gw cannot be obtained directly because it is in a different subscription.</span></span> <span data-ttu-id="d5db5-295">Vous devez créer un objet PowerShell avec les valeurs communiquées par Abonnement 1 dans les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="d5db5-295">You will need to create a new PowerShell object with the values communicated from Subscription 1 in the steps above.</span></span> <span data-ttu-id="d5db5-296">Utilisez l’exemple ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d5db5-296">Use the example below.</span></span> <span data-ttu-id="d5db5-297">Remplacez le nom, l’ID et la clé partagée par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="d5db5-297">Replace the Name, Id, and shared key with your own values.</span></span> <span data-ttu-id="d5db5-298">Il est important que la clé partagée corresponde aux deux connexions.</span><span class="sxs-lookup"><span data-stu-id="d5db5-298">The important thing is that the shared key must match for both connections.</span></span> <span data-ttu-id="d5db5-299">La création d’une connexion peut prendre quelques instants.</span><span class="sxs-lookup"><span data-stu-id="d5db5-299">Creating a connection can take a short while to complete.</span></span>

  <span data-ttu-id="d5db5-300">Se connecter à Abonnement 1 avant d’exécuter l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="d5db5-300">Connect to Subscription 1 before running the following example:</span></span>

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="d5db5-301">**[Abonnement 5]** Créez la connexion TestVNet5 à TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="d5db5-301">**[Subscription 5]** Create the TestVNet5 to TestVNet1 connection.</span></span> <span data-ttu-id="d5db5-302">Cette étape est similaire à celle présentée ci-dessus, sauf que vous créez la connexion de TestVNet5 à TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="d5db5-302">This step is similar to the one above, except you are creating the connection from TestVNet5 to TestVNet1.</span></span> <span data-ttu-id="d5db5-303">La procédure de création d’un objet PowerShell basé sur les valeurs obtenues à partir d’Abonnement 1 s’applique également ici.</span><span class="sxs-lookup"><span data-stu-id="d5db5-303">The same process of creating a PowerShell object based on the values obtained from Subscription 1 applies here as well.</span></span> <span data-ttu-id="d5db5-304">Dans cette étape, vérifiez que les clés partagées correspondent.</span><span class="sxs-lookup"><span data-stu-id="d5db5-304">In this step, be sure that the shared keys match.</span></span>

  <span data-ttu-id="d5db5-305">Se connecter à Abonnement 5 avant d’exécuter l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="d5db5-305">Connect to Subscription 5 before running the following example:</span></span>

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <span data-ttu-id="d5db5-306"><a name="verify"></a>Vérification d’une connexion</span><span class="sxs-lookup"><span data-stu-id="d5db5-306"><a name="verify"></a>How to verify a connection</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="d5db5-307"><a name="faq"></a>Forum Aux Questions sur l’interconnexion de réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="d5db5-307"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="d5db5-308">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d5db5-308">Next steps</span></span>

* <span data-ttu-id="d5db5-309">Une fois la connexion achevée, vous pouvez ajouter des machines virtuelles à vos réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="d5db5-309">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="d5db5-310">Pour plus d’informations, consultez la [documentation relative aux machines virtuelles](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) .</span><span class="sxs-lookup"><span data-stu-id="d5db5-310">See the [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) for more information.</span></span>
* <span data-ttu-id="d5db5-311">Pour plus d’informations sur le protocole BGP, consultez les articles [Vue d’ensemble du protocole BGP](vpn-gateway-bgp-overview.md) et [Comment configurer BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d5db5-311">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>