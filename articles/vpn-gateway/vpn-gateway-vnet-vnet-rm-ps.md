---
title: "Se connecter à un réseau virtuel de tooanother réseau virtuel Azure : PowerShell | Documents Microsoft"
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
ms.openlocfilehash: 2da30c76867cc3f71d040e63e0dd15d153e15c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a><span data-ttu-id="afaf6-103">Configurer une connexion de passerelle VPN de réseau virtuel à réseau virtuel à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="afaf6-103">Configure a VNet-to-VNet VPN gateway connection using PowerShell</span></span>

<span data-ttu-id="afaf6-104">Cet article vous montre comment toocreate une connexion de passerelle VPN entre les réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="afaf6-104">This article shows you how toocreate a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="afaf6-105">Hello réseaux virtuels peuvent être hello identiques ou différentes régions, et à partir de hello identiques ou différents abonnements.</span><span class="sxs-lookup"><span data-stu-id="afaf6-105">hello virtual networks can be in hello same or different regions, and from hello same or different subscriptions.</span></span> <span data-ttu-id="afaf6-106">Lors de la connexion des réseaux virtuels à partir de différents abonnements, les abonnements hello n’est pas nécessaire de toobe associé hello même client Active Directory.</span><span class="sxs-lookup"><span data-stu-id="afaf6-106">When connecting VNets from different subscriptions, hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> 

<span data-ttu-id="afaf6-107">étapes de Hello dans cet article appliquent le modèle de déploiement du Gestionnaire de ressources toohello et utilisant de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afaf6-107">hello steps in this article apply toohello Resource Manager deployment model and use PowerShell.</span></span> <span data-ttu-id="afaf6-108">Vous pouvez également créer cette configuration à l’aide d’un outil de déploiement différentes ou d’un modèle de déploiement en sélectionnant une option différente de hello suivant liste :</span><span class="sxs-lookup"><span data-stu-id="afaf6-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="afaf6-109">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="afaf6-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="afaf6-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="afaf6-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="afaf6-111">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="afaf6-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="afaf6-112">Portail Azure (classique)</span><span class="sxs-lookup"><span data-stu-id="afaf6-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="afaf6-113">Connexions entre différents modèles de déploiement - Portail Azure</span><span class="sxs-lookup"><span data-stu-id="afaf6-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="afaf6-114">Connexions entre différents modèles de déploiement - PowerShell</span><span class="sxs-lookup"><span data-stu-id="afaf6-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="afaf6-115">Connexion d’un réseau virtuel de réseau virtuel tooanother (au réseau) est tooconnecting comme emplacement d’un site réseau virtuel tooan local.</span><span class="sxs-lookup"><span data-stu-id="afaf6-115">Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="afaf6-116">Les deux types de connectivité utilisent un tooprovide de passerelle VPN un tunnel sécurisé utilisant IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="afaf6-116">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="afaf6-117">Si vos réseaux virtuels sont Bonjour même région, vous souhaiterez peut-être tooconsider les connectant à l’aide de l’homologation de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="afaf6-117">If your VNets are in hello same region, you may want tooconsider connecting them using VNet Peering.</span></span> <span data-ttu-id="afaf6-118">L’homologation de réseaux virtuels (ou VNet Peering) n’utilise pas de passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="afaf6-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="afaf6-119">Pour plus d’informations, consultez l’article [Homologation de réseaux virtuels](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="afaf6-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="afaf6-120">Vous pouvez combiner une communication de réseau virtuel à réseau virtuel avec des configurations multisites.</span><span class="sxs-lookup"><span data-stu-id="afaf6-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="afaf6-121">Cela vous permet d’établir des topologies de réseau qui combinent une connectivité intersite de connectivité de réseau virtuel entre, comme indiqué dans hello suivant schéma :</span><span class="sxs-lookup"><span data-stu-id="afaf6-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in hello following diagram:</span></span>

![À propos des connexions](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a><span data-ttu-id="afaf6-123">Pourquoi connecter des réseaux virtuels ?</span><span class="sxs-lookup"><span data-stu-id="afaf6-123">Why connect virtual networks?</span></span>

<span data-ttu-id="afaf6-124">Vous souhaiterez peut-être les réseaux virtuels tooconnect pour hello suivant raisons :</span><span class="sxs-lookup"><span data-stu-id="afaf6-124">You may want tooconnect virtual networks for hello following reasons:</span></span>

* <span data-ttu-id="afaf6-125">**Géo-redondance et présence géographique dans plusieurs régions**</span><span class="sxs-lookup"><span data-stu-id="afaf6-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="afaf6-126">Vous pouvez configurer la géo-réplication ou la synchronisation avec une connectivité sécurisée sans passer par les points de terminaison accessibles sur Internet.</span><span class="sxs-lookup"><span data-stu-id="afaf6-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="afaf6-127">Avec Traffic Manager et l’équilibreur de charge Azure, vous pouvez configurer une charge de travail hautement disponible avec la géo-redondance dans plusieurs régions Azure.</span><span class="sxs-lookup"><span data-stu-id="afaf6-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="afaf6-128">Par exemple important, tooset des SQL Always On avec des groupes de disponibilité répartis dans plusieurs régions Azure.</span><span class="sxs-lookup"><span data-stu-id="afaf6-128">One important example is tooset up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="afaf6-129">**Applications multiniveaux régionales avec une limite d’isolement ou administrative**</span><span class="sxs-lookup"><span data-stu-id="afaf6-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="afaf6-130">Dans hello même région, vous pouvez définir des applications à plusieurs niveaux avec plusieurs réseaux virtuels interconnectés tooisolation ou exigences administratives.</span><span class="sxs-lookup"><span data-stu-id="afaf6-130">Within hello same region, you can set up multi-tier applications with multiple virtual networks connected together due tooisolation or administrative requirements.</span></span>

<span data-ttu-id="afaf6-131">Pour plus d’informations sur les connexions de réseau virtuel à réseau virtuel, consultez hello [FAQ sur le réseau à](#faq) à fin hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="afaf6-131">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span>

## <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="afaf6-132">Quelle procédure dois-je utiliser ?</span><span class="sxs-lookup"><span data-stu-id="afaf6-132">Which set of steps should I use?</span></span>

<span data-ttu-id="afaf6-133">Cet article inclut deux ensembles d’étapes distincts.</span><span class="sxs-lookup"><span data-stu-id="afaf6-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="afaf6-134">Un ensemble d’étapes pour [qui résident dans des réseaux virtuels hello même abonnement](#samesub)et l’autre pour [des réseaux virtuels qui résident dans différents abonnements](#difsub).</span><span class="sxs-lookup"><span data-stu-id="afaf6-134">One set of steps for [VNets that reside in hello same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span> <span data-ttu-id="afaf6-135">Bonjour principale différence entre les jeux de hello est que vous pouvez créer et configurer toutes les ressources réseau et passerelle virtuels au sein de hello même session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afaf6-135">hello key difference between hello sets is whether you can create and configure all virtual network and gateway resources within hello same PowerShell session.</span></span>

<span data-ttu-id="afaf6-136">Hello étapes dans cet article utilisent les variables qui sont déclarées au début de hello de chaque section.</span><span class="sxs-lookup"><span data-stu-id="afaf6-136">hello steps in this article use variables that are declared at hello beginning of each section.</span></span> <span data-ttu-id="afaf6-137">Si vous travaillez déjà avec les réseaux virtuels existants, modifier des paramètres hello variables tooreflect hello votre propre environnement.</span><span class="sxs-lookup"><span data-stu-id="afaf6-137">If you already are working with existing VNets, modify hello variables tooreflect hello settings in your own environment.</span></span> <span data-ttu-id="afaf6-138">Si vous souhaitez une résolution de noms pour vos réseaux virtuels, consultez la page [Résolution de noms](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="afaf6-138">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

## <span data-ttu-id="afaf6-139"><a name="samesub"></a>Comment tooconnect des réseaux virtuels qui se trouvent dans hello même abonnement</span><span class="sxs-lookup"><span data-stu-id="afaf6-139"><a name="samesub"></a>How tooconnect VNets that are in hello same subscription</span></span>

![Diagramme v2v](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="afaf6-141">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="afaf6-141">Before you begin</span></span>

<span data-ttu-id="afaf6-142">Avant de commencer, vous devez tooinstall hello dernière version de hello Azure Resource Manager applets de commande PowerShell, au moins 4.0 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="afaf6-142">Before beginning, you need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets, at least 4.0 or later.</span></span> <span data-ttu-id="afaf6-143">Pour plus d’informations sur l’installation des applets de commande PowerShell hello, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="afaf6-143">For more information about installing hello PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="afaf6-144"><a name="Step1"></a>Étape 1 : planifier vos plages d’adresses IP</span><span class="sxs-lookup"><span data-stu-id="afaf6-144"><a name="Step1"></a>Step 1 - Plan your IP address ranges</span></span>

<span data-ttu-id="afaf6-145">Bonjour comme suit, nous créer deux réseaux virtuels, ainsi que leurs sous-réseaux de passerelle respectives et les configurations.</span><span class="sxs-lookup"><span data-stu-id="afaf6-145">In hello following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="afaf6-146">Nous puis créez une connexion VPN entre hello deux réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="afaf6-146">We then create a VPN connection between hello two VNets.</span></span> <span data-ttu-id="afaf6-147">Il s’agit des plages d’adresses IP important tooplan hello pour votre configuration réseau.</span><span class="sxs-lookup"><span data-stu-id="afaf6-147">It’s important tooplan hello IP address ranges for your network configuration.</span></span> <span data-ttu-id="afaf6-148">N’oubliez pas que vous devez vous assurer qu’aucune plage de réseaux virtuels ou de réseaux locaux ne se chevauche.</span><span class="sxs-lookup"><span data-stu-id="afaf6-148">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="afaf6-149">Dans ces exemples, nous n’incluons pas de serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="afaf6-149">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="afaf6-150">Si vous souhaitez une résolution de noms pour vos réseaux virtuels, consultez la page [Résolution de noms](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="afaf6-150">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="afaf6-151">Nous utilisons hello valeurs dans les exemples hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="afaf6-151">We use hello following values in hello examples:</span></span>

<span data-ttu-id="afaf6-152">**Valeurs pour TestVNet1 :**</span><span class="sxs-lookup"><span data-stu-id="afaf6-152">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="afaf6-153">Nom du réseau virtuel : TestVNet1</span><span class="sxs-lookup"><span data-stu-id="afaf6-153">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="afaf6-154">Groupe de ressources : TestRG1</span><span class="sxs-lookup"><span data-stu-id="afaf6-154">Resource Group: TestRG1</span></span>
* <span data-ttu-id="afaf6-155">Emplacement : Est des États-Unis</span><span class="sxs-lookup"><span data-stu-id="afaf6-155">Location: East US</span></span>
* <span data-ttu-id="afaf6-156">TestVNet1 : 10.11.0.0/16 et 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="afaf6-156">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="afaf6-157">FrontEnd : 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="afaf6-157">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="afaf6-158">BackEnd : 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="afaf6-158">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="afaf6-159">GatewaySubnet : 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="afaf6-159">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="afaf6-160">GatewayName : VNet1GW</span><span class="sxs-lookup"><span data-stu-id="afaf6-160">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="afaf6-161">Adresse IP publique : VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="afaf6-161">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="afaf6-162">Type de VPN : RouteBased</span><span class="sxs-lookup"><span data-stu-id="afaf6-162">VPNType: RouteBased</span></span>
* <span data-ttu-id="afaf6-163">Connection(1to4) : VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="afaf6-163">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="afaf6-164">Connection(1to5) : VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="afaf6-164">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="afaf6-165">Type de connexion : VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="afaf6-165">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="afaf6-166">**Valeurs pour TestVNet4 :**</span><span class="sxs-lookup"><span data-stu-id="afaf6-166">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="afaf6-167">Nom du réseau virtuel : TestVNet4</span><span class="sxs-lookup"><span data-stu-id="afaf6-167">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="afaf6-168">TestVNet2 : 10.41.0.0/16 et 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="afaf6-168">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="afaf6-169">Serveur frontal : 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="afaf6-169">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="afaf6-170">Serveur principal : 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="afaf6-170">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="afaf6-171">Sous-réseau de passerelle : 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="afaf6-171">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="afaf6-172">Groupe de ressources : TestRG4</span><span class="sxs-lookup"><span data-stu-id="afaf6-172">Resource Group: TestRG4</span></span>
* <span data-ttu-id="afaf6-173">Emplacement : États-Unis de l’Ouest</span><span class="sxs-lookup"><span data-stu-id="afaf6-173">Location: West US</span></span>
* <span data-ttu-id="afaf6-174">Nom de la passerelle : VNet4GW</span><span class="sxs-lookup"><span data-stu-id="afaf6-174">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="afaf6-175">Adresse IP publique : VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="afaf6-175">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="afaf6-176">Type de VPN : RouteBased</span><span class="sxs-lookup"><span data-stu-id="afaf6-176">VPNType: RouteBased</span></span>
* <span data-ttu-id="afaf6-177">Connexion : VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="afaf6-177">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="afaf6-178">Type de connexion : VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="afaf6-178">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="afaf6-179"><a name="Step2"></a>Étape 2 : créez et configurez TestVNet1</span><span class="sxs-lookup"><span data-stu-id="afaf6-179"><a name="Step2"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="afaf6-180">Déclarez vos variables.</span><span class="sxs-lookup"><span data-stu-id="afaf6-180">Declare your variables.</span></span> <span data-ttu-id="afaf6-181">Cet exemple déclare les variables de hello en utilisant les valeurs de hello pour cet exercice.</span><span class="sxs-lookup"><span data-stu-id="afaf6-181">This example declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="afaf6-182">Dans la plupart des cas, vous devez remplacer les valeurs hello par les vôtres.</span><span class="sxs-lookup"><span data-stu-id="afaf6-182">In most cases, you should replace hello values with your own.</span></span> <span data-ttu-id="afaf6-183">Toutefois, vous pouvez utiliser ces variables si vous exécutez via toobecome d’étapes hello familiarisé avec ce type de configuration.</span><span class="sxs-lookup"><span data-stu-id="afaf6-183">However, you can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="afaf6-184">Modifier les variables hello si nécessaire, puis copiez et collez-les dans votre console PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afaf6-184">Modify hello variables if needed, then copy and paste them into your PowerShell console.</span></span>

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

2. <span data-ttu-id="afaf6-185">Se connecter tooyour compte.</span><span class="sxs-lookup"><span data-stu-id="afaf6-185">Connect tooyour account.</span></span> <span data-ttu-id="afaf6-186">Utilisez hello suivant toohelp exemple que vous connectez :</span><span class="sxs-lookup"><span data-stu-id="afaf6-186">Use hello following example toohelp you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="afaf6-187">Vérifiez les abonnements hello pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="afaf6-187">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="afaf6-188">Spécifiez un abonnement hello que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="afaf6-188">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. <span data-ttu-id="afaf6-189">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="afaf6-189">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. <span data-ttu-id="afaf6-190">Créer des configurations de sous-réseaux pour TestVNet1 hello.</span><span class="sxs-lookup"><span data-stu-id="afaf6-190">Create hello subnet configurations for TestVNet1.</span></span> <span data-ttu-id="afaf6-191">Cet exemple crée un réseau virtuel nommé TestVNet1 et trois sous-réseaux nommés GatewaySubnet, FrontEnd et Backend.</span><span class="sxs-lookup"><span data-stu-id="afaf6-191">This example creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="afaf6-192">Lorsque vous remplacez les valeurs, pensez à toujours nommer votre sous-réseau de passerelle « GatewaySubnet ».</span><span class="sxs-lookup"><span data-stu-id="afaf6-192">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="afaf6-193">Si vous le nommez autrement, la création de votre passerelle échoue.</span><span class="sxs-lookup"><span data-stu-id="afaf6-193">If you name it something else, your gateway creation fails.</span></span>

  <span data-ttu-id="afaf6-194">Hello exemple suivant utilise des variables de hello que vous avez définis précédemment.</span><span class="sxs-lookup"><span data-stu-id="afaf6-194">hello following example uses hello variables that you set earlier.</span></span> <span data-ttu-id="afaf6-195">Dans cet exemple, sous-réseau de passerelle hello utilise un /27.</span><span class="sxs-lookup"><span data-stu-id="afaf6-195">In this example, hello gateway subnet is using a /27.</span></span> <span data-ttu-id="afaf6-196">Bien qu’il soit possible de toocreate un sous-réseau de passerelle aussi petit que /29, nous vous recommandons de créer un sous-réseau plus grand qui inclut plusieurs adresses en sélectionnant au moins /28 ou /27.</span><span class="sxs-lookup"><span data-stu-id="afaf6-196">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="afaf6-197">Cette opération permettra suffisamment adresses tooaccommodate possibles des configurations supplémentaires que vous pouvez Bonjour futures.</span><span class="sxs-lookup"><span data-stu-id="afaf6-197">This will allow for enough addresses tooaccommodate possible additional configurations that you may want in hello future.</span></span>

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. <span data-ttu-id="afaf6-198">Créez TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="afaf6-198">Create TestVNet1.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. <span data-ttu-id="afaf6-199">Demander une passerelle publique de toohello alloué toobe adresse IP que vous allez créer pour votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="afaf6-199">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="afaf6-200">Notez que hello AllocationMethod est dynamique.</span><span class="sxs-lookup"><span data-stu-id="afaf6-200">Notice that hello AllocationMethod is Dynamic.</span></span> <span data-ttu-id="afaf6-201">Vous ne pouvez pas spécifier hello adresse IP que vous toouse.</span><span class="sxs-lookup"><span data-stu-id="afaf6-201">You cannot specify hello IP address that you want toouse.</span></span> <span data-ttu-id="afaf6-202">Il est alloué dynamiquement tooyour passerelle.</span><span class="sxs-lookup"><span data-stu-id="afaf6-202">It's dynamically allocated tooyour gateway.</span></span> 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="afaf6-203">Créer la configuration de la passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="afaf6-203">Create hello gateway configuration.</span></span> <span data-ttu-id="afaf6-204">configuration de la passerelle Hello définit le sous-réseau de hello et toouse adresse IP publique de hello.</span><span class="sxs-lookup"><span data-stu-id="afaf6-204">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="afaf6-205">Utilisez hello exemple toocreate votre configuration de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="afaf6-205">Use hello example toocreate your gateway configuration.</span></span>

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. <span data-ttu-id="afaf6-206">Créer la passerelle de hello pour TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="afaf6-206">Create hello gateway for TestVNet1.</span></span> <span data-ttu-id="afaf6-207">Dans cette étape, vous créez passerelle de réseau virtuel hello pour votre TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="afaf6-207">In this step, you create hello virtual network gateway for your TestVNet1.</span></span> <span data-ttu-id="afaf6-208">Les configurations de réseau virtuel à réseau virtuel requièrent un VPN de type RouteBased.</span><span class="sxs-lookup"><span data-stu-id="afaf6-208">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="afaf6-209">Création d’une passerelle peut souvent prendre entre 45 minutes ou plus, selon la passerelle sélectionnée de hello référence (SKU).</span><span class="sxs-lookup"><span data-stu-id="afaf6-209">Creating a gateway can often take 45 minutes or more, depending on hello selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a><span data-ttu-id="afaf6-210">Étape 3 : créez et configurez TestVNet4</span><span class="sxs-lookup"><span data-stu-id="afaf6-210">Step 3 - Create and configure TestVNet4</span></span>

<span data-ttu-id="afaf6-211">Une fois que vous avez configuré TestVNet1, créez TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="afaf6-211">Once you've configured TestVNet1, create TestVNet4.</span></span> <span data-ttu-id="afaf6-212">Suivez les étapes de hello ci-dessous, en remplaçant les valeurs de hello par votre propre si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="afaf6-212">Follow hello steps below, replacing hello values with your own when needed.</span></span> <span data-ttu-id="afaf6-213">Cette étape peut être effectuée dans hello même session PowerShell, car il est hello même abonnement.</span><span class="sxs-lookup"><span data-stu-id="afaf6-213">This step can be done within hello same PowerShell session because it is in hello same subscription.</span></span>

1. <span data-ttu-id="afaf6-214">Déclarez vos variables.</span><span class="sxs-lookup"><span data-stu-id="afaf6-214">Declare your variables.</span></span> <span data-ttu-id="afaf6-215">Être tooreplace que les valeurs hello avec hello ceux que vous souhaitez toouse pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="afaf6-215">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

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
2. <span data-ttu-id="afaf6-216">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="afaf6-216">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. <span data-ttu-id="afaf6-217">Créer des configurations de sous-réseaux pour TestVNet4 hello.</span><span class="sxs-lookup"><span data-stu-id="afaf6-217">Create hello subnet configurations for TestVNet4.</span></span>

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. <span data-ttu-id="afaf6-218">Créez TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="afaf6-218">Create TestVNet4.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. <span data-ttu-id="afaf6-219">Demandez une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="afaf6-219">Request a public IP address.</span></span>

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. <span data-ttu-id="afaf6-220">Créer la configuration de la passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="afaf6-220">Create hello gateway configuration.</span></span>

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. <span data-ttu-id="afaf6-221">Créez hello TestVNet4 passerelle.</span><span class="sxs-lookup"><span data-stu-id="afaf6-221">Create hello TestVNet4 gateway.</span></span> <span data-ttu-id="afaf6-222">Création d’une passerelle peut souvent prendre entre 45 minutes ou plus, selon la passerelle sélectionnée de hello référence (SKU).</span><span class="sxs-lookup"><span data-stu-id="afaf6-222">Creating a gateway can often take 45 minutes or more, depending on hello selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-hello-connections"></a><span data-ttu-id="afaf6-223">Étape 4 : créer des connexions de hello</span><span class="sxs-lookup"><span data-stu-id="afaf6-223">Step 4 - Create hello connections</span></span>

1. <span data-ttu-id="afaf6-224">Obtenez les passerelles de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="afaf6-224">Get both virtual network gateways.</span></span> <span data-ttu-id="afaf6-225">Si les deux passerelles de hello sont Bonjour même abonnement, comme dans l’exemple de hello, vous pouvez effectuer cette étape Bonjour même session PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afaf6-225">If both of hello gateways are in hello same subscription, as they are in hello example, you can complete this step in hello same PowerShell session.</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. <span data-ttu-id="afaf6-226">Créer hello TestVNet1 tooTestVNet4 connexion.</span><span class="sxs-lookup"><span data-stu-id="afaf6-226">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="afaf6-227">Dans cette étape, vous créez des connexions de hello à partir de TestVNet1 tooTestVNet4.</span><span class="sxs-lookup"><span data-stu-id="afaf6-227">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="afaf6-228">Vous verrez une clé partagée est référencée dans les exemples hello.</span><span class="sxs-lookup"><span data-stu-id="afaf6-228">You'll see a shared key referenced in hello examples.</span></span> <span data-ttu-id="afaf6-229">Vous pouvez utiliser vos propres valeurs pour la clé partagée de hello.</span><span class="sxs-lookup"><span data-stu-id="afaf6-229">You can use your own values for hello shared key.</span></span> <span data-ttu-id="afaf6-230">Hello important est que clé partagée hello doit correspondre pour les deux connexions.</span><span class="sxs-lookup"><span data-stu-id="afaf6-230">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="afaf6-231">Création d’une connexion peut prendre quelques instants toocomplete.</span><span class="sxs-lookup"><span data-stu-id="afaf6-231">Creating a connection can take a short while toocomplete.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. <span data-ttu-id="afaf6-232">Créer hello TestVNet4 tooTestVNet1 connexion.</span><span class="sxs-lookup"><span data-stu-id="afaf6-232">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="afaf6-233">Cette étape est similaire toohello une version ultérieure, mais vous créez hello connexion à partir de TestVNet4 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="afaf6-233">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="afaf6-234">Vérifiez que hello partagé clés correspondent.</span><span class="sxs-lookup"><span data-stu-id="afaf6-234">Make sure hello shared keys match.</span></span> <span data-ttu-id="afaf6-235">Hello connexion sera établie après quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="afaf6-235">hello connection will be established after a few minutes.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="afaf6-236">Vérifiez votre connexion.</span><span class="sxs-lookup"><span data-stu-id="afaf6-236">Verify your connection.</span></span> <span data-ttu-id="afaf6-237">Consultez la section de hello [comment tooverify votre connexion](#verify).</span><span class="sxs-lookup"><span data-stu-id="afaf6-237">See hello section [How tooverify your connection](#verify).</span></span>

## <span data-ttu-id="afaf6-238"><a name="difsub"></a>Comment tooconnect des réseaux virtuels qui se trouvent dans différents abonnements</span><span class="sxs-lookup"><span data-stu-id="afaf6-238"><a name="difsub"></a>How tooconnect VNets that are in different subscriptions</span></span>

![Diagramme v2v](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

<span data-ttu-id="afaf6-240">Dans ce scénario, nous connectons TestVNet1 et TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="afaf6-240">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="afaf6-241">TestVNet1 et TestVNet5 se trouvent dans des abonnements différents.</span><span class="sxs-lookup"><span data-stu-id="afaf6-241">TestVNet1 and TestVNet5 reside in a different subscription.</span></span> <span data-ttu-id="afaf6-242">les abonnements Hello n’est pas nécessaire de toobe associé hello même client Active Directory.</span><span class="sxs-lookup"><span data-stu-id="afaf6-242">hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> <span data-ttu-id="afaf6-243">Hello différences entre ces étapes et hello précédente est que certaines des étapes de configuration hello doivent toobe effectuée dans une autre session de PowerShell dans un contexte hello d’abonnement de deuxième hello.</span><span class="sxs-lookup"><span data-stu-id="afaf6-243">hello difference between these steps and hello previous set is that some of hello configuration steps need toobe performed in a separate PowerShell session in hello context of hello second subscription.</span></span> <span data-ttu-id="afaf6-244">En particulier lorsque les abonnements hello deux appartiennent toodifferent organisations.</span><span class="sxs-lookup"><span data-stu-id="afaf6-244">Especially when hello two subscriptions belong toodifferent organizations.</span></span>

### <a name="step-5---create-and-configure-testvnet1"></a><span data-ttu-id="afaf6-245">Étape 5 : créez et configurez TestVNet1</span><span class="sxs-lookup"><span data-stu-id="afaf6-245">Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="afaf6-246">Vous devez effectuer [étape 1](#Step1) et [étape 2](#Step2) de hello précédente section toocreate et configurer TestVNet1 hello passerelle VPN pour TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="afaf6-246">You must complete [Step 1](#Step1) and [Step 2](#Step2) from hello previous section toocreate and configure TestVNet1 and hello VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="afaf6-247">Pour cette configuration, vous n’êtes pas requis toocreate TestVNet4 à partir de la section précédente de hello, bien que si vous créez il, il ne sera pas en conflit avec ces étapes.</span><span class="sxs-lookup"><span data-stu-id="afaf6-247">For this configuration, you are not required toocreate TestVNet4 from hello previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="afaf6-248">Après avoir terminé l’étape 1 et l’étape 2, passez à l’étape 6 toocreate TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="afaf6-248">Once you complete Step 1 and Step 2, continue with Step 6 toocreate TestVNet5.</span></span> 

### <a name="step-6---verify-hello-ip-address-ranges"></a><span data-ttu-id="afaf6-249">Étape 6 : vérifier les plages d’adresses IP hello</span><span class="sxs-lookup"><span data-stu-id="afaf6-249">Step 6 - Verify hello IP address ranges</span></span>

<span data-ttu-id="afaf6-250">Il est important toomake que l’espace d’adressage IP hello du nouveau réseau virtuel hello TestVNet5, ne se chevauche pas avec les plages VNet ou de plages de passerelle de réseau local.</span><span class="sxs-lookup"><span data-stu-id="afaf6-250">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet5, does not overlap with any of your VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="afaf6-251">Dans cet exemple, les réseaux virtuels hello peuvent appartenir aux organisations de toodifferent.</span><span class="sxs-lookup"><span data-stu-id="afaf6-251">In this example, hello virtual networks may belong toodifferent organizations.</span></span> <span data-ttu-id="afaf6-252">Dans cet exercice, vous pouvez utiliser hello valeurs pour hello TestVNet5 suivantes :</span><span class="sxs-lookup"><span data-stu-id="afaf6-252">For this exercise, you can use hello following values for hello TestVNet5:</span></span>

<span data-ttu-id="afaf6-253">**Valeurs pour TestVNet5 :**</span><span class="sxs-lookup"><span data-stu-id="afaf6-253">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="afaf6-254">Nom du réseau virtuel : TestVNet5</span><span class="sxs-lookup"><span data-stu-id="afaf6-254">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="afaf6-255">Groupe de ressources : TestRG5</span><span class="sxs-lookup"><span data-stu-id="afaf6-255">Resource Group: TestRG5</span></span>
* <span data-ttu-id="afaf6-256">Emplacement : Japon de l’Est</span><span class="sxs-lookup"><span data-stu-id="afaf6-256">Location: Japan East</span></span>
* <span data-ttu-id="afaf6-257">TestVNet5 : 10.51.0.0/16 et 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="afaf6-257">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="afaf6-258">Serveur frontal : 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="afaf6-258">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="afaf6-259">Serveur principal : 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="afaf6-259">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="afaf6-260">Sous-réseau de passerelle : 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="afaf6-260">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="afaf6-261">Nom de la passerelle : VNet5GW</span><span class="sxs-lookup"><span data-stu-id="afaf6-261">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="afaf6-262">Adresse IP publique : VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="afaf6-262">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="afaf6-263">Type de VPN : RouteBased</span><span class="sxs-lookup"><span data-stu-id="afaf6-263">VPNType: RouteBased</span></span>
* <span data-ttu-id="afaf6-264">Connexion : VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="afaf6-264">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="afaf6-265">Type de connexion : VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="afaf6-265">ConnectionType: VNet2VNet</span></span>

### <a name="step-7---create-and-configure-testvnet5"></a><span data-ttu-id="afaf6-266">Étape 7 : créez et configurez TestVNet5</span><span class="sxs-lookup"><span data-stu-id="afaf6-266">Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="afaf6-267">Cette étape doit être effectuée dans le contexte de hello d’abonnement hello.</span><span class="sxs-lookup"><span data-stu-id="afaf6-267">This step must be done in hello context of hello new subscription.</span></span> <span data-ttu-id="afaf6-268">Cette partie ne peut être effectuée par administrateur hello dans une autre organisation qui possède l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="afaf6-268">This part may be performed by hello administrator in a different organization that owns hello subscription.</span></span>

1. <span data-ttu-id="afaf6-269">Déclarez vos variables.</span><span class="sxs-lookup"><span data-stu-id="afaf6-269">Declare your variables.</span></span> <span data-ttu-id="afaf6-270">Être tooreplace que les valeurs hello avec hello ceux que vous souhaitez toouse pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="afaf6-270">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

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
2. <span data-ttu-id="afaf6-271">Se connecter toosubscription 5.</span><span class="sxs-lookup"><span data-stu-id="afaf6-271">Connect toosubscription 5.</span></span> <span data-ttu-id="afaf6-272">Ouvrez la console PowerShell et tooyour compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="afaf6-272">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="afaf6-273">Utilisez hello suivant toohelp exemple que vous connectez :</span><span class="sxs-lookup"><span data-stu-id="afaf6-273">Use hello following sample toohelp you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="afaf6-274">Vérifiez les abonnements hello pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="afaf6-274">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="afaf6-275">Spécifiez un abonnement hello que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="afaf6-275">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. <span data-ttu-id="afaf6-276">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="afaf6-276">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. <span data-ttu-id="afaf6-277">Créer des configurations de sous-réseaux pour TestVNet5 hello.</span><span class="sxs-lookup"><span data-stu-id="afaf6-277">Create hello subnet configurations for TestVNet5.</span></span>

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. <span data-ttu-id="afaf6-278">Créez TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="afaf6-278">Create TestVNet5.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. <span data-ttu-id="afaf6-279">Demandez une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="afaf6-279">Request a public IP address.</span></span>

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="afaf6-280">Créer la configuration de la passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="afaf6-280">Create hello gateway configuration.</span></span>

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. <span data-ttu-id="afaf6-281">Créez hello TestVNet5 passerelle.</span><span class="sxs-lookup"><span data-stu-id="afaf6-281">Create hello TestVNet5 gateway.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-hello-connections"></a><span data-ttu-id="afaf6-282">Étape 8 - créer des connexions de hello</span><span class="sxs-lookup"><span data-stu-id="afaf6-282">Step 8 - Create hello connections</span></span>

<span data-ttu-id="afaf6-283">Dans cet exemple, étant donné que les passerelles hello sont dans des abonnements différents hello, nous avons fractionner cette étape en deux sessions PowerShell marquées comme [1 abonnement] et [abonnement 5].</span><span class="sxs-lookup"><span data-stu-id="afaf6-283">In this example, because hello gateways are in hello different subscriptions, we've split this step into two PowerShell sessions marked as [Subscription 1] and [Subscription 5].</span></span>

1. <span data-ttu-id="afaf6-284">**[Abonnement 1]**  Passerelle de réseau virtuel get hello pour 1 de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="afaf6-284">**[Subscription 1]** Get hello virtual network gateway for Subscription 1.</span></span> <span data-ttu-id="afaf6-285">Se connecter et se connecter tooSubscription 1 avant d’exécuter hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="afaf6-285">Log in and connect tooSubscription 1 before running hello following example:</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  <span data-ttu-id="afaf6-286">Copier le résultat de hello Hello suivant d’éléments et envoyer ces administrateur toohello 5 d’abonnement par courrier électronique ou une autre méthode.</span><span class="sxs-lookup"><span data-stu-id="afaf6-286">Copy hello output of hello following elements and send these toohello administrator of Subscription 5 via email or another method.</span></span>

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  <span data-ttu-id="afaf6-287">Ces deux éléments aura toohello similaire de valeurs suivant l’exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="afaf6-287">These two elements will have values similar toohello following example output:</span></span>

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. <span data-ttu-id="afaf6-288">**[Abonnement 5]**  Passerelle de réseau virtuel get hello pour 5 de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="afaf6-288">**[Subscription 5]** Get hello virtual network gateway for Subscription 5.</span></span> <span data-ttu-id="afaf6-289">Se connecter et se connecter tooSubscription 5 avant d’exécuter hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="afaf6-289">Log in and connect tooSubscription 5 before running hello following example:</span></span>

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  <span data-ttu-id="afaf6-290">Copier le résultat de hello Hello suivant d’éléments et envoyer ces administrateur toohello 1 d’abonnement par courrier électronique ou une autre méthode.</span><span class="sxs-lookup"><span data-stu-id="afaf6-290">Copy hello output of hello following elements and send these toohello administrator of Subscription 1 via email or another method.</span></span>

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  <span data-ttu-id="afaf6-291">Ces deux éléments aura toohello similaire de valeurs suivant l’exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="afaf6-291">These two elements will have values similar toohello following example output:</span></span>

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. <span data-ttu-id="afaf6-292">**[Abonnement 1]**  Créer hello TestVNet1 tooTestVNet5 connexion.</span><span class="sxs-lookup"><span data-stu-id="afaf6-292">**[Subscription 1]** Create hello TestVNet1 tooTestVNet5 connection.</span></span> <span data-ttu-id="afaf6-293">Dans cette étape, vous créez des connexions de hello à partir de TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="afaf6-293">In this step, you create hello connection from TestVNet1 tooTestVNet5.</span></span> <span data-ttu-id="afaf6-294">Hello différence est que vnet5gw $ Impossible d’obtenir directement, car il est dans un autre abonnement.</span><span class="sxs-lookup"><span data-stu-id="afaf6-294">hello difference here is that $vnet5gw cannot be obtained directly because it is in a different subscription.</span></span> <span data-ttu-id="afaf6-295">Vous devez toocreate un nouvel objet PowerShell avec des valeurs hello communiquées à partir de 1 de l’abonnement dans les étapes de hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="afaf6-295">You will need toocreate a new PowerShell object with hello values communicated from Subscription 1 in hello steps above.</span></span> <span data-ttu-id="afaf6-296">Utilisez l’exemple hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="afaf6-296">Use hello example below.</span></span> <span data-ttu-id="afaf6-297">Remplacez hello nom, Id et clé partagée par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="afaf6-297">Replace hello Name, Id, and shared key with your own values.</span></span> <span data-ttu-id="afaf6-298">Hello important est que clé partagée hello doit correspondre pour les deux connexions.</span><span class="sxs-lookup"><span data-stu-id="afaf6-298">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="afaf6-299">Création d’une connexion peut prendre quelques instants toocomplete.</span><span class="sxs-lookup"><span data-stu-id="afaf6-299">Creating a connection can take a short while toocomplete.</span></span>

  <span data-ttu-id="afaf6-300">Se connecter tooSubscription 1 avant d’exécuter hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="afaf6-300">Connect tooSubscription 1 before running hello following example:</span></span>

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="afaf6-301">**[Abonnement 5]**  Créer hello TestVNet5 tooTestVNet1 connexion.</span><span class="sxs-lookup"><span data-stu-id="afaf6-301">**[Subscription 5]** Create hello TestVNet5 tooTestVNet1 connection.</span></span> <span data-ttu-id="afaf6-302">Cette étape est similaire toohello une version ultérieure, mais vous créez hello connexion à partir de TestVNet5 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="afaf6-302">This step is similar toohello one above, except you are creating hello connection from TestVNet5 tooTestVNet1.</span></span> <span data-ttu-id="afaf6-303">Hello même processus de création d’un objet PowerShell selon les valeurs hello obtenues à l’abonnement 1 applique ici.</span><span class="sxs-lookup"><span data-stu-id="afaf6-303">hello same process of creating a PowerShell object based on hello values obtained from Subscription 1 applies here as well.</span></span> <span data-ttu-id="afaf6-304">Dans cette étape, assurez-vous que les clés de hello partagé correspondent.</span><span class="sxs-lookup"><span data-stu-id="afaf6-304">In this step, be sure that hello shared keys match.</span></span>

  <span data-ttu-id="afaf6-305">Se connecter tooSubscription 5 avant d’exécuter hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="afaf6-305">Connect tooSubscription 5 before running hello following example:</span></span>

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <span data-ttu-id="afaf6-306"><a name="verify"></a>Comment tooverify une connexion</span><span class="sxs-lookup"><span data-stu-id="afaf6-306"><a name="verify"></a>How tooverify a connection</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="afaf6-307"><a name="faq"></a>Forum Aux Questions sur l’interconnexion de réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="afaf6-307"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="afaf6-308">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="afaf6-308">Next steps</span></span>

* <span data-ttu-id="afaf6-309">Une fois que votre connexion est terminée, vous pouvez ajouter des machines virtuelles tooyour des réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="afaf6-309">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="afaf6-310">Consultez hello [documentation de Machines virtuelles](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="afaf6-310">See hello [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) for more information.</span></span>
* <span data-ttu-id="afaf6-311">Pour plus d’informations sur BGP, consultez hello [vue d’ensemble du protocole BGP](vpn-gateway-bgp-overview.md) et [comment tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="afaf6-311">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
