---
title: "Créer un équilibrage de charge accessible sur Internet avec IPv6 - interface de ligne de commande Azure | Microsoft Docs"
description: "Découvrir comment créer un équilibrage de charge accessible sur Internet avec IPv6 dans Azure Resource Manager, à l’aide de l’interface de ligne de commande Azure"
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
ms.openlocfilehash: efb4771800c42df544c3cc37d1d164045fdcaf3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-the-azure-cli"></a><span data-ttu-id="02b73-104">Créer un équilibrage de charge accessible sur Internet avec IPv6 dans Azure Resource Manager, à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="02b73-104">Create an Internet facing load balancer with IPv6 in Azure Resource Manager using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="02b73-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="02b73-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="02b73-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="02b73-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="02b73-107">Modèle</span><span class="sxs-lookup"><span data-stu-id="02b73-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="02b73-108">Un équilibrage de charge Azure est de type Couche 4 (TCP, UDP).</span><span class="sxs-lookup"><span data-stu-id="02b73-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="02b73-109">L’équilibrage de charge offre une disponibilité élevée en distribuant le trafic entrant parmi les instances de service saines dans les services cloud ou les machines virtuelles dans un jeu d’équilibrage de la charge.</span><span class="sxs-lookup"><span data-stu-id="02b73-109">The load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="02b73-110">Azure Load Balancer peut également présenter ces services sur plusieurs ports, plusieurs adresses IP ou les deux.</span><span class="sxs-lookup"><span data-stu-id="02b73-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="02b73-111">Exemple de scénario de déploiement</span><span class="sxs-lookup"><span data-stu-id="02b73-111">Example deployment scenario</span></span>

<span data-ttu-id="02b73-112">Le diagramme suivant illustre la solution d’équilibrage de charge déployée à l’aide de l’exemple de modèle décrit dans cet article.</span><span class="sxs-lookup"><span data-stu-id="02b73-112">The following diagram illustrates the load balancing solution being deployed using the example template described in this article.</span></span>

![Scénario d’équilibreur de charge](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

<span data-ttu-id="02b73-114">Dans ce scénario, vous allez créer les ressources Azure suivantes :</span><span class="sxs-lookup"><span data-stu-id="02b73-114">In this scenario you will create the following Azure resources:</span></span>

* <span data-ttu-id="02b73-115">deux machines virtuelles ;</span><span class="sxs-lookup"><span data-stu-id="02b73-115">two virtual machines (VMs)</span></span>
* <span data-ttu-id="02b73-116">une interface de réseau virtuel pour chaque machine virtuelle avec des adresses IPv4 et IPv6 affectées ;</span><span class="sxs-lookup"><span data-stu-id="02b73-116">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>
* <span data-ttu-id="02b73-117">un équilibrage de charge accessible sur Internet avec une adresse IP publique IPv4 et IPv6 ;</span><span class="sxs-lookup"><span data-stu-id="02b73-117">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="02b73-118">un groupe à haute disponibilité contenant les deux machines virtuelles ;</span><span class="sxs-lookup"><span data-stu-id="02b73-118">an Availability Set to that contains the two VMs</span></span>
* <span data-ttu-id="02b73-119">deux règles d’équilibrage de charge pour mapper les adresses IP virtuelles publiques sur les points de terminaison privés.</span><span class="sxs-lookup"><span data-stu-id="02b73-119">two load balancing rules to map the public VIPs to the private endpoints</span></span>

## <a name="deploying-the-solution-using-the-azure-cli"></a><span data-ttu-id="02b73-120">Déploiement de la solution à l’aide de l’interface de ligne de commande (CLI) Azure</span><span class="sxs-lookup"><span data-stu-id="02b73-120">Deploying the solution using the Azure CLI</span></span>

<span data-ttu-id="02b73-121">Les étapes suivantes expliquent comment créer un équilibrage de charge accessible sur Internet à l'aide d'Azure Resource Manager avec CLI.</span><span class="sxs-lookup"><span data-stu-id="02b73-121">The following steps show how to create an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="02b73-122">Avec Azure Resource Manager, toutes les ressources sont créées et configurées individuellement, puis rassemblées pour en créer une unique.</span><span class="sxs-lookup"><span data-stu-id="02b73-122">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a resource.</span></span>

<span data-ttu-id="02b73-123">Pour déployer un équilibrage de charge, vous devez créer et configurer les objets suivants :</span><span class="sxs-lookup"><span data-stu-id="02b73-123">To deploy a load balancer, you create and configure the following objects:</span></span>

* <span data-ttu-id="02b73-124">Configuration d’adresses IP frontales : contient les adresses IP publiques pour le trafic réseau entrant.</span><span class="sxs-lookup"><span data-stu-id="02b73-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="02b73-125">Pool d’adresses principales : contient des interfaces réseau (NIC) pour que les machines virtuelles puissent recevoir le trafic réseau de l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="02b73-125">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="02b73-126">Règles d’équilibrage de charge : contient des règles de mappage d’un port public situé sur l’équilibrage de charge pour le pool d’adresses principales.</span><span class="sxs-lookup"><span data-stu-id="02b73-126">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="02b73-127">Règles NAT entrantes : contient des règles de mappage d’un port public situé sur l’équilibrage de charge vers le port d’une machine virtuelle spécifique située dans le pool d’adresses principales.</span><span class="sxs-lookup"><span data-stu-id="02b73-127">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="02b73-128">Sondes : contient les sondes d’intégrité utilisées pour vérifier la disponibilité des instances de machines virtuelles du pool d’adresses principales.</span><span class="sxs-lookup"><span data-stu-id="02b73-128">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="02b73-129">Pour plus d’informations, consultez [Prise en charge d’un équilibreur de charge par Azure Resource Manager](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="02b73-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-your-cli-environment-to-use-azure-resource-manager"></a><span data-ttu-id="02b73-130">Configurer votre environnement d’interface de ligne de commande pour utiliser Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="02b73-130">Set up your CLI environment to use Azure Resource Manager</span></span>

<span data-ttu-id="02b73-131">Pour cet exemple, nous utilisons les outils d’interface de ligne de commande dans une fenêtre de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="02b73-131">For this example, we are running the CLI tools in a PowerShell command window.</span></span> <span data-ttu-id="02b73-132">Nous n’utilisons pas les applets de commande Microsoft Azure PowerShell mais utilisons les fonctionnalités de script PowerShell afin d’améliorer la lisibilité et la réutilisation.</span><span class="sxs-lookup"><span data-stu-id="02b73-132">We are not using the Azure PowerShell cmdlets but we use PowerShell's scripting capabilities to improve readability and reuse.</span></span>

1. <span data-ttu-id="02b73-133">Si vous n’avez jamais utilisé l’interface de ligne de commande Azure, consultez [Installation et configuration de l’interface de ligne de commande Azure](../cli-install-nodejs.md) et suivez les instructions jusqu’à l’étape vous invitant à sélectionner votre compte et votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="02b73-133">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="02b73-134">Exécutez la commande **azure config mode** afin d’activer le mode Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="02b73-134">Run the **azure config mode** command to switch to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="02b73-135">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="02b73-135">Expected output:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="02b73-136">Connectez-vous à Azure afin de consulter une liste de vos abonnements.</span><span class="sxs-lookup"><span data-stu-id="02b73-136">Sign in to Azure and get a list of subscriptions.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="02b73-137">À l’invite, entrez vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="02b73-137">Enter your Azure credentials when prompted.</span></span>

    ```azurecli
    azure account list
    ```

    <span data-ttu-id="02b73-138">Sélectionnez l’abonnement que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="02b73-138">Pick the subscription you want to use.</span></span> <span data-ttu-id="02b73-139">Prenez note de l’ID d’abonnement pour la prochaine étape.</span><span class="sxs-lookup"><span data-stu-id="02b73-139">Make note of the subscription Id for the next step.</span></span>

4. <span data-ttu-id="02b73-140">Configurez des variables PowerShell à utiliser avec les commandes d’interface de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="02b73-140">Set up PowerShell variables for use with the CLI commands.</span></span>

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

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a><span data-ttu-id="02b73-141">Créer un groupe de ressources, un équilibrage de charge, un réseau virtuel et des sous-réseaux</span><span class="sxs-lookup"><span data-stu-id="02b73-141">Create a resource group, a load balancer, a virtual network, and subnets</span></span>

1. <span data-ttu-id="02b73-142">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="02b73-142">Create a resource group</span></span>

    ```azurecli
    azure group create $rgName $location
    ```

2. <span data-ttu-id="02b73-143">Créer un équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="02b73-143">Create a load balancer</span></span>

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. <span data-ttu-id="02b73-144">Créez un réseau virtuel (VNet).</span><span class="sxs-lookup"><span data-stu-id="02b73-144">Create a virtual network (VNet).</span></span>

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    <span data-ttu-id="02b73-145">Créez deux sous-réseaux dans ce réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="02b73-145">Create two subnets in this VNet.</span></span>

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-the-front-end-pool"></a><span data-ttu-id="02b73-146">Créer des adresses IP publiques pour le pool frontal</span><span class="sxs-lookup"><span data-stu-id="02b73-146">Create public IP addresses for the front-end pool</span></span>

1. <span data-ttu-id="02b73-147">Configurer les variables PowerShell</span><span class="sxs-lookup"><span data-stu-id="02b73-147">Set up the PowerShell variables</span></span>

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. <span data-ttu-id="02b73-148">Créez une adresse IP publique pour le pool frontal.</span><span class="sxs-lookup"><span data-stu-id="02b73-148">Create a public IP address the front-end IP pool.</span></span>

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="02b73-149">L’équilibreur de charge utilise l’étiquette du domaine de l’adresse IP publique en tant que nom de domaine complet (FQDN).</span><span class="sxs-lookup"><span data-stu-id="02b73-149">The load balancer uses the domain label of the public IP as its FQDN.</span></span> <span data-ttu-id="02b73-150">Cet usage diffère d’un déploiement classique qui utilise le service cloud en tant que nom de domaine complet de l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="02b73-150">This a change from classic deployment, which uses the cloud service name as the load balancer FQDN.</span></span>
    > <span data-ttu-id="02b73-151">Dans cet exemple, le nom de domaine complet est *contoso09152016.southcentralus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="02b73-151">In this example, the FQDN is *contoso09152016.southcentralus.cloudapp.azure.com*.</span></span>

## <a name="create-front-end-and-back-end-pools"></a><span data-ttu-id="02b73-152">Créer ds pools frontaux et principaux</span><span class="sxs-lookup"><span data-stu-id="02b73-152">Create front-end and back-end pools</span></span>

<span data-ttu-id="02b73-153">Cet exemple crée le pool d’IP frontal qui reçoit le trafic réseau entrant pour l’équilibrage de charge et le pool d’IP principal où le pool frontal envoie le trafic de réseau équilibré.</span><span class="sxs-lookup"><span data-stu-id="02b73-153">This example creates the front-end IP pool that receives the incoming network traffic on the load balancer and the back-end IP pool where the front-end pool sends the load balanced network traffic.</span></span>

1. <span data-ttu-id="02b73-154">Configurer les variables PowerShell</span><span class="sxs-lookup"><span data-stu-id="02b73-154">Set up the PowerShell variables</span></span>

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. <span data-ttu-id="02b73-155">Créez un pool d’IP frontal associant l’IP publique créée lors de l’étape précédente et l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="02b73-155">Create a front-end IP pool associating the public IP created in the previous step and the load balancer.</span></span>

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-the-probe-nat-rules-and-lb-rules"></a><span data-ttu-id="02b73-156">Créer la sonde, les règles NAT et les règles LB</span><span class="sxs-lookup"><span data-stu-id="02b73-156">Create the probe, NAT rules, and LB rules</span></span>

<span data-ttu-id="02b73-157">Cet exemple crée les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="02b73-157">This example creates the following items:</span></span>

* <span data-ttu-id="02b73-158">une règle de sonde dédiée à la détection de connectivité sur le port TCP 80 ;</span><span class="sxs-lookup"><span data-stu-id="02b73-158">a probe rule to check for connectivity to TCP port 80</span></span>
* <span data-ttu-id="02b73-159">une règle NAT pour transférer l’ensemble du trafic entrant sur le port 3389 vers le port 3389 pour RDP<sup>1</sup> ;</span><span class="sxs-lookup"><span data-stu-id="02b73-159">a NAT rule to translate all incoming traffic on port 3389 to port 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="02b73-160">une règle NAT pour transférer l’ensemble du trafic entrant sur le port 3391 vers le port 3389 pour RDP<sup>1</sup> ;</span><span class="sxs-lookup"><span data-stu-id="02b73-160">a NAT rule to translate all incoming traffic on port 3391 to port 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="02b73-161">une règle d’équilibrage de charge pour équilibrer tout le trafic entrant sur le port 80 vers le port 80 des adresses du pool principal ;</span><span class="sxs-lookup"><span data-stu-id="02b73-161">a load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool.</span></span>

<span data-ttu-id="02b73-162"><sup>1</sup> Les règles NAT sont associées à une instance de machine virtuelle spécifique derrière l’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="02b73-162"><sup>1</sup> NAT rules are associated to a specific virtual machine instance behind the load balancer.</span></span> <span data-ttu-id="02b73-163">Le trafic réseau arrivant sur le port 3389 est envoyé à la machine virtuelle spécifique sur le port 22 associé à la règle NAT.</span><span class="sxs-lookup"><span data-stu-id="02b73-163">The network traffic arriving on port 3389 is sent to the specific virtual machine and port associated with the NAT rule.</span></span> <span data-ttu-id="02b73-164">Vous devez spécifier un protocole (TCP ou UDP) pour une règle NAT.</span><span class="sxs-lookup"><span data-stu-id="02b73-164">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="02b73-165">Il est impossible d'attribuer les deux protocoles au même port.</span><span class="sxs-lookup"><span data-stu-id="02b73-165">Both protocols can't be assigned to the same port.</span></span>

1. <span data-ttu-id="02b73-166">Configurer les variables PowerShell</span><span class="sxs-lookup"><span data-stu-id="02b73-166">Set up the PowerShell variables</span></span>

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. <span data-ttu-id="02b73-167">Créer la sonde</span><span class="sxs-lookup"><span data-stu-id="02b73-167">Create the probe</span></span>

    <span data-ttu-id="02b73-168">L’exemple suivant illustre la création d’une sonde TCP qui détecte la connectivité au port TCP principal 80 toutes les 15 secondes.</span><span class="sxs-lookup"><span data-stu-id="02b73-168">The following example creates a TCP probe that checks for connectivity to back-end TCP port 80 every 15 seconds.</span></span> <span data-ttu-id="02b73-169">Elle marque la ressource principale comme indisponible après deux échecs consécutifs.</span><span class="sxs-lookup"><span data-stu-id="02b73-169">It will mark the back-end resource unavailable after two consecutive failures.</span></span>

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. <span data-ttu-id="02b73-170">Créer des règles NAT entrantes qui prennent en charge les connexions RDP aux ressources principales</span><span class="sxs-lookup"><span data-stu-id="02b73-170">Create inbound NAT rules that allow RDP connections to the back-end resources</span></span>

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. <span data-ttu-id="02b73-171">Créer des règles d’équilibrage de charge qui transmettent le trafic sur différents ports principaux en fonction du port frontal de réception de la requête</span><span class="sxs-lookup"><span data-stu-id="02b73-171">Create a load balancer rules that send traffic to different back-end ports depending on which front end received the request</span></span>

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. <span data-ttu-id="02b73-172">Vérifier vos paramètres</span><span class="sxs-lookup"><span data-stu-id="02b73-172">Check your settings</span></span>

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    <span data-ttu-id="02b73-173">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="02b73-173">Expected output:</span></span>

        info:    Executing command network lb show
        info:    Looking up the load balancer "myIPv4IPv6Lb"
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

## <a name="create-nics"></a><span data-ttu-id="02b73-174">Créer des cartes réseau</span><span class="sxs-lookup"><span data-stu-id="02b73-174">Create NICs</span></span>

<span data-ttu-id="02b73-175">Créer des cartes réseau et associez-les à des règles NAT, des règles d’équilibrage de charge et des sondes.</span><span class="sxs-lookup"><span data-stu-id="02b73-175">Create NICs and associate them to NAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="02b73-176">Configurer les variables PowerShell</span><span class="sxs-lookup"><span data-stu-id="02b73-176">Set up the PowerShell variables</span></span>

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

2. <span data-ttu-id="02b73-177">Créez une carte réseau pour chaque instance principale et ajoutez une configuration IPv6.</span><span class="sxs-lookup"><span data-stu-id="02b73-177">Create a NIC for each back-end and add an IPv6 configuration.</span></span>

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-the-back-end-vm-resources-and-attach-each-nic"></a><span data-ttu-id="02b73-178">Créer les ressources de machines virtuelles principales et associer chaque carte réseau</span><span class="sxs-lookup"><span data-stu-id="02b73-178">Create the back-end VM resources and attach each NIC</span></span>

<span data-ttu-id="02b73-179">Pour créer des machines virtuelles, vous devez disposer d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="02b73-179">To create VMs, you must have a storage account.</span></span> <span data-ttu-id="02b73-180">Pour l’équilibrage de charge, les machines virtuelles doivent être membres d’un groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="02b73-180">For load balancing, the VMs need to be members of an availability set.</span></span> <span data-ttu-id="02b73-181">Pour plus d’informations sur la création des machines virtuelles, consultez la section [Création d’une machine virtuelle Windows à l’aide de Resource Manager et de PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="02b73-181">For more information about creating VMs, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="02b73-182">Configurer les variables PowerShell</span><span class="sxs-lookup"><span data-stu-id="02b73-182">Set up the PowerShell variables</span></span>

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
    > <span data-ttu-id="02b73-183">Cet exemple utilise le nom d’utilisateur et le mot de passe pour les machines virtuelles, en texte clair.</span><span class="sxs-lookup"><span data-stu-id="02b73-183">This example uses the username and password for the VMs in clear text.</span></span> <span data-ttu-id="02b73-184">Prenez des précautions particulières lors de l’utilisation des informations d’identification en texte clair.</span><span class="sxs-lookup"><span data-stu-id="02b73-184">Appropriate care must be taken when using credentials in the clear.</span></span> <span data-ttu-id="02b73-185">Pour découvrir une méthode sécurisée de traitement des informations d’identification dans PowerShell, consultez l’applet de commande [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) .</span><span class="sxs-lookup"><span data-stu-id="02b73-185">For a more secure method of handling credentials in PowerShell, see the [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

2. <span data-ttu-id="02b73-186">Créer le compte de stockage et le groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="02b73-186">Create the storage account and availability set</span></span>

    <span data-ttu-id="02b73-187">Vous pouvez utilise un compte de stockage existant lors de la création des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="02b73-187">You may use an existing storage account when you create the VMs.</span></span> <span data-ttu-id="02b73-188">La commande suivante génère un nouveau compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="02b73-188">The following command creates a new storage account.</span></span>

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    <span data-ttu-id="02b73-189">Ensuite, créez le groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="02b73-189">Next, create the availability set.</span></span>

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. <span data-ttu-id="02b73-190">Créer les machines virtuelles avec les cartes réseau associées</span><span class="sxs-lookup"><span data-stu-id="02b73-190">Create the virtual machines with the associated NICs</span></span>

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a><span data-ttu-id="02b73-191">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="02b73-191">Next steps</span></span>

[<span data-ttu-id="02b73-192">Prise en main de la configuration d’un équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="02b73-192">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="02b73-193">Configuration d'un mode de distribution d'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="02b73-193">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="02b73-194">Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="02b73-194">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
