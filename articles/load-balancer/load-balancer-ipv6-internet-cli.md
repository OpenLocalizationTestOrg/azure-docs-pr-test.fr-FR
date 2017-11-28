---
title: "équilibrage de charge aaaCreate une côté Internet avec IPv6 - CLI d’Azure | Documents Microsoft"
description: "Découvrez comment toocreate un Internet exposés à équilibrage de charge avec IPv6 à l’aide du Gestionnaire de ressources Azure hello CLI d’Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "IPv6, équilibreur de charge azure, double pile, adresse ip publique, ipv6 natif, mobile, iot"
ms.assetid: a1957c9c-9c1d-423e-9d5c-d71449bc1f37
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 7ff75ac90d74a74e3d0c27672b36fbd955a086a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-hello-azure-cli"></a><span data-ttu-id="da02b-104">Créer un Internet exposés à équilibrage de charge avec IPv6 dans Azure Resource Manager à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="da02b-104">Create an Internet facing load balancer with IPv6 in Azure Resource Manager using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="da02b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="da02b-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="da02b-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="da02b-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="da02b-107">Modèle</span><span class="sxs-lookup"><span data-stu-id="da02b-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="da02b-108">Un équilibrage de charge Azure est de type Couche 4 (TCP, UDP).</span><span class="sxs-lookup"><span data-stu-id="da02b-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="da02b-109">équilibrage de charge Hello offre une haute disponibilité en répartissant le trafic entrant entre les instances de service intègre dans les services de cloud computing ou les machines virtuelles dans un jeu d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="da02b-109">hello load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="da02b-110">Azure Load Balancer peut également présenter ces services sur plusieurs ports, plusieurs adresses IP ou les deux.</span><span class="sxs-lookup"><span data-stu-id="da02b-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="da02b-111">Exemple de scénario de déploiement</span><span class="sxs-lookup"><span data-stu-id="da02b-111">Example deployment scenario</span></span>

<span data-ttu-id="da02b-112">Hello diagramme suivant illustre la solution d’équilibrage de charge de hello en cours de déploiement à l’aide du modèle d’exemple hello décrit dans cet article.</span><span class="sxs-lookup"><span data-stu-id="da02b-112">hello following diagram illustrates hello load balancing solution being deployed using hello example template described in this article.</span></span>

![Scénario d’équilibreur de charge](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

<span data-ttu-id="da02b-114">Dans ce scénario, vous allez créer hello suivant des ressources Azure :</span><span class="sxs-lookup"><span data-stu-id="da02b-114">In this scenario you will create hello following Azure resources:</span></span>

* <span data-ttu-id="da02b-115">deux machines virtuelles ;</span><span class="sxs-lookup"><span data-stu-id="da02b-115">two virtual machines (VMs)</span></span>
* <span data-ttu-id="da02b-116">une interface de réseau virtuel pour chaque machine virtuelle avec des adresses IPv4 et IPv6 affectées ;</span><span class="sxs-lookup"><span data-stu-id="da02b-116">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>
* <span data-ttu-id="da02b-117">un équilibrage de charge accessible sur Internet avec une adresse IP publique IPv4 et IPv6 ;</span><span class="sxs-lookup"><span data-stu-id="da02b-117">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="da02b-118">un toothat à haute disponibilité contient des machines virtuelles de hello deux</span><span class="sxs-lookup"><span data-stu-id="da02b-118">an Availability Set toothat contains hello two VMs</span></span>
* <span data-ttu-id="da02b-119">deux charge équilibrage règles toomap hello VIP toohello privés points de terminaison publics</span><span class="sxs-lookup"><span data-stu-id="da02b-119">two load balancing rules toomap hello public VIPs toohello private endpoints</span></span>

## <a name="deploying-hello-solution-using-hello-azure-cli"></a><span data-ttu-id="da02b-120">Déploiement de solution hello à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="da02b-120">Deploying hello solution using hello Azure CLI</span></span>

<span data-ttu-id="da02b-121">Hello suit montrent comment toocreate une connecté à Internet l’équilibrage de charge à l’aide du Gestionnaire de ressources Azure avec l’interface CLI.</span><span class="sxs-lookup"><span data-stu-id="da02b-121">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="da02b-122">Avec Azure Resource Manager, chaque ressource est créé et configuré individuellement et puis rassembler toocreate une ressource.</span><span class="sxs-lookup"><span data-stu-id="da02b-122">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a resource.</span></span>

<span data-ttu-id="da02b-123">toodeploy un équilibreur de charge, que vous créez et configurez les hello objets suivants :</span><span class="sxs-lookup"><span data-stu-id="da02b-123">toodeploy a load balancer, you create and configure hello following objects:</span></span>

* <span data-ttu-id="da02b-124">Configuration d’adresses IP frontales : contient les adresses IP publiques pour le trafic réseau entrant.</span><span class="sxs-lookup"><span data-stu-id="da02b-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="da02b-125">Pool d’adresses principal - contient des interfaces réseau (NIC) pour le trafic réseau tooreceive de hello machines virtuelles à partir de l’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="da02b-125">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="da02b-126">Règles d’équilibrage de charge - contient des règles de mappage d’un port public sur tooport d’équilibrage de charge hello dans un pool d’adresses de serveur principal hello.</span><span class="sxs-lookup"><span data-stu-id="da02b-126">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="da02b-127">Les règles NAT de trafic entrant - contient des règles de mappage d’un port public sur le port de tooa d’équilibrage de charge hello pour un ordinateur virtuel spécifique dans le pool d’adresses principal hello.</span><span class="sxs-lookup"><span data-stu-id="da02b-127">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="da02b-128">Sondes - contient la disponibilité de toocheck les sondes utilisées de contrôle d’intégrité des instances de machines virtuelles dans un pool d’adresses de serveur principal hello.</span><span class="sxs-lookup"><span data-stu-id="da02b-128">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="da02b-129">Pour plus d’informations, consultez [Prise en charge d’un équilibreur de charge par Azure Resource Manager](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="da02b-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-your-cli-environment-toouse-azure-resource-manager"></a><span data-ttu-id="da02b-130">Configurer votre toouse d’environnement CLI Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="da02b-130">Set up your CLI environment toouse Azure Resource Manager</span></span>

<span data-ttu-id="da02b-131">Pour cet exemple, nous utilisons des outils d’interface CLI hello dans une fenêtre de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="da02b-131">For this example, we are running hello CLI tools in a PowerShell command window.</span></span> <span data-ttu-id="da02b-132">Nous n’utilisons pas d’applets de commande PowerShell Azure hello, mais nous utilisons la lisibilité tooimprove de fonctionnalités et la réutilisation script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="da02b-132">We are not using hello Azure PowerShell cmdlets but we use PowerShell's scripting capabilities tooimprove readability and reuse.</span></span>

1. <span data-ttu-id="da02b-133">Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) et suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="da02b-133">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="da02b-134">Exécutez hello **mode config azure** le mode commande tooswitch tooResource Manager.</span><span class="sxs-lookup"><span data-stu-id="da02b-134">Run hello **azure config mode** command tooswitch tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="da02b-135">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="da02b-135">Expected output:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="da02b-136">Connectez-vous à tooAzure et obtenir la liste des abonnements.</span><span class="sxs-lookup"><span data-stu-id="da02b-136">Sign in tooAzure and get a list of subscriptions.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="da02b-137">À l’invite, entrez vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="da02b-137">Enter your Azure credentials when prompted.</span></span>

    ```azurecli
    azure account list
    ```

    <span data-ttu-id="da02b-138">Choisissez abonnement hello toouse.</span><span class="sxs-lookup"><span data-stu-id="da02b-138">Pick hello subscription you want toouse.</span></span> <span data-ttu-id="da02b-139">Prenez note de l’Id d’abonnement hello pour l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="da02b-139">Make note of hello subscription Id for hello next step.</span></span>

4. <span data-ttu-id="da02b-140">Configurer les variables PowerShell pour une utilisation avec les commandes CLI hello.</span><span class="sxs-lookup"><span data-stu-id="da02b-140">Set up PowerShell variables for use with hello CLI commands.</span></span>

    ```powershell
    $subscriptionid = "########-####-####-####-############"  # enter subscription id
    $location = "southcentralus"
    $rgName = "pscontosorg1southctrlus09152016"
    $vnetName = "contosoIPv4Vnet"
    $vnetPrefix = "10.0.0.0/16"
    $subnet1Name = "clicontosoIPv4Subnet1"
    $subnet1Prefix = "10.0.0.0/24"
    $subnet2Name = "clicontosoIPv4Subnet2"
    $subnet2Prefix = "10.0.1.0/24"
    $dnsLabel = "contoso09152016"
    $lbName = "myIPv4IPv6Lb"
    ```

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a><span data-ttu-id="da02b-141">Créer un groupe de ressources, un équilibrage de charge, un réseau virtuel et des sous-réseaux</span><span class="sxs-lookup"><span data-stu-id="da02b-141">Create a resource group, a load balancer, a virtual network, and subnets</span></span>

1. <span data-ttu-id="da02b-142">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="da02b-142">Create a resource group</span></span>

    ```azurecli
    azure group create $rgName $location
    ```

2. <span data-ttu-id="da02b-143">Créer un équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="da02b-143">Create a load balancer</span></span>

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. <span data-ttu-id="da02b-144">Créez un réseau virtuel (VNet).</span><span class="sxs-lookup"><span data-stu-id="da02b-144">Create a virtual network (VNet).</span></span>

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    <span data-ttu-id="da02b-145">Créez deux sous-réseaux dans ce réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="da02b-145">Create two subnets in this VNet.</span></span>

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-hello-front-end-pool"></a><span data-ttu-id="da02b-146">Créer des adresses IP publiques pour le pool frontal de hello</span><span class="sxs-lookup"><span data-stu-id="da02b-146">Create public IP addresses for hello front-end pool</span></span>

1. <span data-ttu-id="da02b-147">Configurer les variables PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="da02b-147">Set up hello PowerShell variables</span></span>

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. <span data-ttu-id="da02b-148">Créer un public hello frontal IP pool d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="da02b-148">Create a public IP address hello front-end IP pool.</span></span>

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="da02b-149">équilibrage de charge Hello utilise le nom de domaine hello de l’adresse IP publique hello comme son nom de domaine complet.</span><span class="sxs-lookup"><span data-stu-id="da02b-149">hello load balancer uses hello domain label of hello public IP as its FQDN.</span></span> <span data-ttu-id="da02b-150">Cette une modification à partir d’un déploiement classique, ce qui utilise le nom du service cloud hello comme hello d’équilibrage de charge nom de domaine complet.</span><span class="sxs-lookup"><span data-stu-id="da02b-150">This a change from classic deployment, which uses hello cloud service name as hello load balancer FQDN.</span></span>
    > <span data-ttu-id="da02b-151">Dans cet exemple, hello nom de domaine complet est *contoso09152016.southcentralus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="da02b-151">In this example, hello FQDN is *contoso09152016.southcentralus.cloudapp.azure.com*.</span></span>

## <a name="create-front-end-and-back-end-pools"></a><span data-ttu-id="da02b-152">Créer ds pools frontaux et principaux</span><span class="sxs-lookup"><span data-stu-id="da02b-152">Create front-end and back-end pools</span></span>

<span data-ttu-id="da02b-153">Cet exemple crée le pool IP frontal hello qui reçoit le trafic réseau entrant du hello sur l’équilibrage de charge hello et pool d’adresses IP hello principal où pool frontal de hello envoie le trafic à charge équilibrée hello.</span><span class="sxs-lookup"><span data-stu-id="da02b-153">This example creates hello front-end IP pool that receives hello incoming network traffic on hello load balancer and hello back-end IP pool where hello front-end pool sends hello load balanced network traffic.</span></span>

1. <span data-ttu-id="da02b-154">Configurer les variables PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="da02b-154">Set up hello PowerShell variables</span></span>

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. <span data-ttu-id="da02b-155">Créez un pool IP frontal association d’adresse IP publique hello créé dans l’étape précédente de hello et équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="da02b-155">Create a front-end IP pool associating hello public IP created in hello previous step and hello load balancer.</span></span>

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-hello-probe-nat-rules-and-lb-rules"></a><span data-ttu-id="da02b-156">Créer une sonde de hello, des règles NAT et des règles d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="da02b-156">Create hello probe, NAT rules, and LB rules</span></span>

<span data-ttu-id="da02b-157">Cet exemple crée hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="da02b-157">This example creates hello following items:</span></span>

* <span data-ttu-id="da02b-158">un toocheck de règle de sonde de connectivité tooTCP port 80</span><span class="sxs-lookup"><span data-stu-id="da02b-158">a probe rule toocheck for connectivity tooTCP port 80</span></span>
* <span data-ttu-id="da02b-159">un NAT règle tootranslate tout le trafic entrant sur le port 3389 tooport 3389 pour RDP<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="da02b-159">a NAT rule tootranslate all incoming traffic on port 3389 tooport 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="da02b-160">un NAT règle tootranslate tout le trafic entrant sur le port 3391 tooport 3389 pour RDP<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="da02b-160">a NAT rule tootranslate all incoming traffic on port 3391 tooport 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="da02b-161">un toobalance de règle d’équilibrage de charge tout le trafic entrant sur le port 80 tooport 80 sur hello adresses dans le pool principal d’hello.</span><span class="sxs-lookup"><span data-stu-id="da02b-161">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>

<span data-ttu-id="da02b-162"><sup>1</sup> les règles NAT sont instance de machine virtuelle spécifique associé tooa derrière un équilibreur de charge hello.</span><span class="sxs-lookup"><span data-stu-id="da02b-162"><sup>1</sup> NAT rules are associated tooa specific virtual machine instance behind hello load balancer.</span></span> <span data-ttu-id="da02b-163">le trafic réseau de Hello arrivant sur le port 3389 est envoyé ordinateur virtuel spécifique de toohello et de port associé à une règle NAT hello.</span><span class="sxs-lookup"><span data-stu-id="da02b-163">hello network traffic arriving on port 3389 is sent toohello specific virtual machine and port associated with hello NAT rule.</span></span> <span data-ttu-id="da02b-164">Vous devez spécifier un protocole (TCP ou UDP) pour une règle NAT.</span><span class="sxs-lookup"><span data-stu-id="da02b-164">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="da02b-165">Les deux protocoles ne peut pas être assigné toohello même port.</span><span class="sxs-lookup"><span data-stu-id="da02b-165">Both protocols can't be assigned toohello same port.</span></span>

1. <span data-ttu-id="da02b-166">Configurer les variables PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="da02b-166">Set up hello PowerShell variables</span></span>

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. <span data-ttu-id="da02b-167">Création de la sonde de hello</span><span class="sxs-lookup"><span data-stu-id="da02b-167">Create hello probe</span></span>

    <span data-ttu-id="da02b-168">Hello exemple suivant crée une sonde TCP vérifie pour le port connectivité tooback-end TCP 80 toutes les 15 secondes.</span><span class="sxs-lookup"><span data-stu-id="da02b-168">hello following example creates a TCP probe that checks for connectivity tooback-end TCP port 80 every 15 seconds.</span></span> <span data-ttu-id="da02b-169">Il marque ressources principales de hello indisponible après deux échecs consécutifs.</span><span class="sxs-lookup"><span data-stu-id="da02b-169">It will mark hello back-end resource unavailable after two consecutive failures.</span></span>

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. <span data-ttu-id="da02b-170">Créer des règles NAT entrantes qui autorisent les connexions RDP ressources de back-end toohello</span><span class="sxs-lookup"><span data-stu-id="da02b-170">Create inbound NAT rules that allow RDP connections toohello back-end resources</span></span>

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. <span data-ttu-id="da02b-171">Créer des règles qui envoient le trafic toodifferent les ports de back-end en fonction de la requête hello frontal a reçu un équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="da02b-171">Create a load balancer rules that send traffic toodifferent back-end ports depending on which front end received hello request</span></span>

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. <span data-ttu-id="da02b-172">Vérifier vos paramètres</span><span class="sxs-lookup"><span data-stu-id="da02b-172">Check your settings</span></span>

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    <span data-ttu-id="da02b-173">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="da02b-173">Expected output:</span></span>

        info:    Executing command network lb show
        info:    Looking up hello load balancer "myIPv4IPv6Lb"
        data:    Id                              : /subscriptions/########-####-####-####-############/resourceGroups/pscontosorg1southctrlus09152016/providers/Microsoft.Network/loadBalancers/myIPv4IPv6Lb
        data:    Name                            : myIPv4IPv6Lb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : southcentralus
        data:    Provisioning state              : Succeeded
        data:
        data:    Frontend IP configurations:
        data:    Name             Provisioning state  Private IP allocation  Private IP   Subnet  Public IP
        data:    ---------------  ------------------  ---------------------  -----------  ------  ---------
        data:    FrontendVipIPv4  Succeeded           Dynamic                                     myIPv4Vip
        data:    FrontendVipIPv6  Succeeded           Dynamic                                     myIPv6Vip
        data:
        data:    Probes:
        data:    Name                 Provisioning state  Protocol  Port  Path  Interval  Count
        data:    -------------------  ------------------  --------  ----  ----  --------  -----
        data:    ProbeForIPv4AndIPv6  Succeeded           Tcp       80          15        2
        data:
        data:    Backend Address Pools:
        data:    Name             Provisioning state
        data:    ---------------  ------------------
        data:    BackendPoolIPv4  Succeeded
        data:    BackendPoolIPv6  Succeeded
        data:
        data:    Load Balancing Rules:
        data:    Name                  Provisioning state  Load distribution  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    --------------------  ------------------  -----------------  --------  -------------  ------------  ------------------  -----------------------
        data:    LBRuleForIPv4-Port80  Succeeded           Default            Tcp       80             80            false               4
        data:    LBRuleForIPv6-Port80  Succeeded           Default            Tcp       80             8080          false               4
        data:
        data:    Inbound NAT Rules:
        data:    Name                 Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    -------------------  ------------------  --------  -------------  ------------  ------------------  -----------------------
        data:    NatRule-For-Rdp-VM1  Succeeded           Tcp       3389           3389          false               4
        data:    NatRule-For-Rdp-VM2  Succeeded           Tcp       3391           3389          false               4
        info:    network lb show

## <a name="create-nics"></a><span data-ttu-id="da02b-174">Créer des cartes réseau</span><span class="sxs-lookup"><span data-stu-id="da02b-174">Create NICs</span></span>

<span data-ttu-id="da02b-175">Créer des cartes réseau et les associer à tooNAT règles, des règles d’équilibrage de charge et des sondes.</span><span class="sxs-lookup"><span data-stu-id="da02b-175">Create NICs and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="da02b-176">Configurer les variables PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="da02b-176">Set up hello PowerShell variables</span></span>

    ```powershell
    $nic1Name = "myIPv4IPv6Nic1"
    $nic2Name = "myIPv4IPv6Nic2"
    $subnet1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet1Name"
    $subnet2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet2Name"
    $backendAddressPoolV4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV4Name"
    $backendAddressPoolV6Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV6Name"
    $natRule1V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule1V4Name"
    $natRule2V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule2V4Name"
    ```

2. <span data-ttu-id="da02b-177">Créez une carte réseau pour chaque instance principale et ajoutez une configuration IPv6.</span><span class="sxs-lookup"><span data-stu-id="da02b-177">Create a NIC for each back-end and add an IPv6 configuration.</span></span>

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-hello-back-end-vm-resources-and-attach-each-nic"></a><span data-ttu-id="da02b-178">Créer des ressources d’ordinateur virtuel principal hello et joindre chaque carte réseau</span><span class="sxs-lookup"><span data-stu-id="da02b-178">Create hello back-end VM resources and attach each NIC</span></span>

<span data-ttu-id="da02b-179">toocreate machines virtuelles, vous devez disposer d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="da02b-179">toocreate VMs, you must have a storage account.</span></span> <span data-ttu-id="da02b-180">Pour l’équilibrage de charge, machines virtuelles de hello doivent toobe les membres d’un ensemble de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="da02b-180">For load balancing, hello VMs need toobe members of an availability set.</span></span> <span data-ttu-id="da02b-181">Pour plus d’informations sur la création des machines virtuelles, consultez la section [Création d’une machine virtuelle Windows à l’aide de Resource Manager et de PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="da02b-181">For more information about creating VMs, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="da02b-182">Configurer les variables PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="da02b-182">Set up hello PowerShell variables</span></span>

    ```powershell
    $storageAccountName = "ps08092016v6sa0"
    $availabilitySetName = "myIPv4IPv6AvailabilitySet"
    $vm1Name = "myIPv4IPv6VM1"
    $vm2Name = "myIPv4IPv6VM2"
    $nic1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic1Name"
    $nic2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic2Name"
    $disk1Name = "WindowsVMosDisk1"
    $disk2Name = "WindowsVMosDisk2"
    $osDisk1Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk1Name.vhd"
    $osDisk2Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk2Name.vhd"
    $imageurn "MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest"
    $vmUserName = "vmUser"
    $mySecurePassword = "PlainTextPassword*1"
    ```

    > [!WARNING]
    > <span data-ttu-id="da02b-183">Cet exemple utilise hello username et password pour les machines virtuelles de hello en texte clair.</span><span class="sxs-lookup"><span data-stu-id="da02b-183">This example uses hello username and password for hello VMs in clear text.</span></span> <span data-ttu-id="da02b-184">Approprié doit être vigilant lorsqu’à l’aide des informations d’identification Bonjour effacer.</span><span class="sxs-lookup"><span data-stu-id="da02b-184">Appropriate care must be taken when using credentials in hello clear.</span></span> <span data-ttu-id="da02b-185">Pour obtenir une méthode plus sécurisée de la gestion des informations d’identification dans PowerShell, consultez hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="da02b-185">For a more secure method of handling credentials in PowerShell, see hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

2. <span data-ttu-id="da02b-186">Créer l’ensemble de compte et la disponibilité du stockage hello</span><span class="sxs-lookup"><span data-stu-id="da02b-186">Create hello storage account and availability set</span></span>

    <span data-ttu-id="da02b-187">Vous pouvez utiliser un compte de stockage existant lorsque vous créez des machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="da02b-187">You may use an existing storage account when you create hello VMs.</span></span> <span data-ttu-id="da02b-188">Hello commande suivante crée un nouveau compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="da02b-188">hello following command creates a new storage account.</span></span>

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    <span data-ttu-id="da02b-189">Ensuite, créez le groupe à haute disponibilité hello.</span><span class="sxs-lookup"><span data-stu-id="da02b-189">Next, create hello availability set.</span></span>

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. <span data-ttu-id="da02b-190">Créer des machines virtuelles de hello avec des cartes réseau de hello associé</span><span class="sxs-lookup"><span data-stu-id="da02b-190">Create hello virtual machines with hello associated NICs</span></span>

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a><span data-ttu-id="da02b-191">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="da02b-191">Next steps</span></span>

[<span data-ttu-id="da02b-192">Prise en main de la configuration d’un équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="da02b-192">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="da02b-193">Configuration d'un mode de distribution d'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="da02b-193">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="da02b-194">Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="da02b-194">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
