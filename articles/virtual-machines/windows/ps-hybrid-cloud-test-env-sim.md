---
title: environnement de test de cloud hybride aaaSimulated | Documents Microsoft
description: "Créez une simulation d'environnement de cloud hybride pour exécuter des tests informatiques ou de développement, à l'aide de deux réseaux virtuels Azure et d'une connexion de réseau virtuel à réseau virtuel."
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ca5bf294-8172-44a9-8fed-d6f38d345364
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: 6063022e373c2b3564e040c4fbee122e2438974b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-simulated-hybrid-cloud-environment-for-testing"></a><span data-ttu-id="53326-103">Configuration d’une simulation d’environnement de cloud hybride à des fins de test</span><span class="sxs-lookup"><span data-stu-id="53326-103">Set up a simulated hybrid cloud environment for testing</span></span>
<span data-ttu-id="53326-104">Cet article vous présente la création d'un environnement de cloud hybride simulé avec Microsoft Azure à l'aide de deux réseaux virtuels Azure.</span><span class="sxs-lookup"><span data-stu-id="53326-104">This article steps you through creating a simulated hybrid cloud environment with Microsoft Azure using two Azure virtual networks.</span></span> <span data-ttu-id="53326-105">Voici la configuration obtenue de hello.</span><span class="sxs-lookup"><span data-stu-id="53326-105">Here is hello resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="53326-106">Elle simule un environnement de production cloud hybride et est constituée des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="53326-106">This simulates a hybrid cloud production environment and consists of:</span></span>

* <span data-ttu-id="53326-107">Un réseau simulé et simplifiée local hébergé dans un réseau virtuel Azure (réseau virtuel hello labo de test).</span><span class="sxs-lookup"><span data-stu-id="53326-107">A simulated and simplified on-premises network hosted in an Azure virtual network (hello TestLab virtual network).</span></span>
* <span data-ttu-id="53326-108">Un réseau virtuel entre sites simulé hébergé dans Azure (TestVNET).</span><span class="sxs-lookup"><span data-stu-id="53326-108">A simulated cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="53326-109">Connexion au réseau entre les réseaux virtuels hello deux.</span><span class="sxs-lookup"><span data-stu-id="53326-109">A VNet-to-VNet connection between hello two virtual networks.</span></span>
* <span data-ttu-id="53326-110">Un contrôleur de domaine secondaire dans le réseau virtuel de TestVNET hello.</span><span class="sxs-lookup"><span data-stu-id="53326-110">A secondary domain controller in hello TestVNET virtual network.</span></span>

<span data-ttu-id="53326-111">Elle fournit une base et un point de départ commun pour :</span><span class="sxs-lookup"><span data-stu-id="53326-111">This provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="53326-112">Développer et tester des applications dans une simulation d’environnement de cloud hybride.</span><span class="sxs-lookup"><span data-stu-id="53326-112">Develop and test applications in a simulated hybrid cloud environment.</span></span>
* <span data-ttu-id="53326-113">Créer des configurations de test des ordinateurs, certains au sein du réseau virtuel du labo de test hello et certaines au sein du réseau virtuel hello TestVNET, charges de travail informatique en nuage hybride toosimulate.</span><span class="sxs-lookup"><span data-stu-id="53326-113">Create test configurations of computers, some within hello TestLab virtual network and some within hello TestVNET virtual network, toosimulate hybrid cloud-based IT workloads.</span></span>

<span data-ttu-id="53326-114">Il existe quatre principales phases toosetting, cet environnement de test de cloud hybride :</span><span class="sxs-lookup"><span data-stu-id="53326-114">There are four major phases toosetting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="53326-115">Configurer un réseau virtuel de hello labo de test.</span><span class="sxs-lookup"><span data-stu-id="53326-115">Configure hello TestLab virtual network.</span></span>
2. <span data-ttu-id="53326-116">Créer un réseau virtuel intersite de hello.</span><span class="sxs-lookup"><span data-stu-id="53326-116">Create hello cross-premises virtual network.</span></span>
3. <span data-ttu-id="53326-117">Créer un réseau VPN hello au réseau.</span><span class="sxs-lookup"><span data-stu-id="53326-117">Create hello VNet-to-VNet VPN connection.</span></span>
4. <span data-ttu-id="53326-118">Configurer DC2.</span><span class="sxs-lookup"><span data-stu-id="53326-118">Configure DC2.</span></span> 

<span data-ttu-id="53326-119">Cette configuration nécessite un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="53326-119">This configuration requires an Azure subscription.</span></span> <span data-ttu-id="53326-120">Si vous avez un abonnement MSDN ou Visual Studio, consultez [Crédit Azure mensuel pour les abonnés Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="53326-120">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

> [!NOTE]
> <span data-ttu-id="53326-121">Les machines virtuelles et les passerelles de réseau virtuel dans Azure entraînent des frais lors de leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="53326-121">Virtual machines and virtual network gateways in Azure incur an ongoing monetary cost when they are running.</span></span> <span data-ttu-id="53326-122">Ce coût est facturé en fonction de votre abonnement MSDN ou de votre abonnement payant.</span><span class="sxs-lookup"><span data-stu-id="53326-122">This cost is billed against your MSDN or paid subscription.</span></span> <span data-ttu-id="53326-123">La passerelle VPN Azure est implémentée comme un ensemble de deux machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="53326-123">An Azure VPN gateway is implemented as a set of two Azure virtual machines.</span></span> <span data-ttu-id="53326-124">toominimize les coûts de hello, créer l’environnement de test hello et réalisez votre nécessaires test et démonstration aussi rapidement que possible.</span><span class="sxs-lookup"><span data-stu-id="53326-124">toominimize hello costs, create hello test environment and perform your needed testing and demonstration as quickly as possible.</span></span>
> 
> 

## <a name="phase-1-configure-hello-testlab-virtual-network"></a><span data-ttu-id="53326-125">Phase 1 : Configurer le réseau virtuel de hello labo de test</span><span class="sxs-lookup"><span data-stu-id="53326-125">Phase 1: Configure hello TestLab virtual network</span></span>
<span data-ttu-id="53326-126">Utilisez les instructions hello hello [environnement de test Configuration de Base](https://technet.microsoft.com/library/mt771177.aspx) rubrique tooconfigure hello DC1, APP1 et CLIENT1 ordinateurs Bonjour réseau virtuel Azure nommé labo de test.</span><span class="sxs-lookup"><span data-stu-id="53326-126">Use hello instructions in hello [Base Configuration test environment](https://technet.microsoft.com/library/mt771177.aspx) topic tooconfigure hello DC1, APP1, and CLIENT1 computers in hello Azure virtual network named TestLab.</span></span> 

<span data-ttu-id="53326-127">Ensuite, démarrez une invite de commandes Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="53326-127">Next, start an Azure PowerShell prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="53326-128">Hello ensembles de commande suivants utiliser Azure PowerShell 1.0 et versions ultérieur.</span><span class="sxs-lookup"><span data-stu-id="53326-128">hello following command sets use Azure PowerShell 1.0 and later.</span></span>
> 
> 

<span data-ttu-id="53326-129">Tooyour compte de connexion.</span><span class="sxs-lookup"><span data-stu-id="53326-129">Sign in tooyour account.</span></span>

    Login-AzureRMAccount

<span data-ttu-id="53326-130">Obtenir le nom de votre abonnement à l’aide de hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="53326-130">Get your subscription name using hello following command.</span></span>

    Get-AzureRMSubscription | Sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="53326-131">Définissez votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="53326-131">Set your Azure subscription.</span></span> <span data-ttu-id="53326-132">Utilisez hello même abonnement que vous avez utilisé toobuild votre configuration de base à la Phase 1.</span><span class="sxs-lookup"><span data-stu-id="53326-132">Use hello same subscription that you used toobuild your base configuration in Phase 1.</span></span> <span data-ttu-id="53326-133">Remplacez tout le contenu du devis hello, notamment hello < et >, avec le nom correct de hello.</span><span class="sxs-lookup"><span data-stu-id="53326-133">Replace everything within hello quotes, including hello < and > characters, with hello correct name.</span></span>

    $subscr="<subscription name>"
    Get-AzureRmSubscription –SubscriptionName $subscr | Select-AzureRmSubscription

<span data-ttu-id="53326-134">Ensuite, ajoutez un passerelle sous-réseau toohello labo de test réseau virtuel de votre configuration de base, qui sera utilisé toohost hello passerelle Azure.</span><span class="sxs-lookup"><span data-stu-id="53326-134">Next, add a gateway subnet toohello TestLab virtual network of your base configuration, which will be used toohost hello Azure gateway.</span></span>

    $rgName="<name of your resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $vnet=Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name TestLab
    Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 10.255.255.248/29 -VirtualNetwork $vnet
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet

<span data-ttu-id="53326-135">Ensuite, demander une passerelle de toohello publique des tooassign d’adresse IP pour le réseau virtuel de hello labo de test.</span><span class="sxs-lookup"><span data-stu-id="53326-135">Next, request a public IP address tooassign toohello gateway for hello TestLab virtual network.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestLab_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic

<span data-ttu-id="53326-136">Ensuite, créez votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="53326-136">Next, create your gateway.</span></span>

    $vnet=Get-AzureRmVirtualNetwork -Name TestLab -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name TestLab_GWConfig -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id 
    New-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="53326-137">Gardez à l’esprit que les nouvelles passerelles peuvent prendre 20 minutes ou plus toocreate.</span><span class="sxs-lookup"><span data-stu-id="53326-137">Keep in mind that new gateways can take 20 minutes or more toocreate.</span></span>

<span data-ttu-id="53326-138">Hello portail Azure sur votre ordinateur local, connectez-vous avec les informations d’identification CORP\User1 de hello tooDC1.</span><span class="sxs-lookup"><span data-stu-id="53326-138">From hello Azure portal on your local computer, connect tooDC1 with hello CORP\User1 credentials.</span></span> <span data-ttu-id="53326-139">domaine CORP de hello tooconfigure afin que les utilisateurs et les ordinateurs utilisent leur contrôleur de domaine local pour l’authentification, exécutez ces commandes à partir d’une invite de commandes de Windows PowerShell de niveau administrateur sur DC1.</span><span class="sxs-lookup"><span data-stu-id="53326-139">tooconfigure hello CORP domain so that computers and users use their local domain controller for authentication, run these commands from an administrator-level Windows PowerShell command prompt on DC1.</span></span>

    New-ADReplicationSite -Name "TestLab" 
    New-ADReplicationSite -Name "TestVNET"
    New-ADReplicationSubnet -Name "10.0.0.0/8" -Site "TestLab"
    New-ADReplicationSubnet -Name "192.168.0.0/16" -Site "TestVNET"

<span data-ttu-id="53326-140">Ceci est votre configuration actuelle.</span><span class="sxs-lookup"><span data-stu-id="53326-140">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph1.png)

## <a name="phase-2-create-hello-testvnet-virtual-network"></a><span data-ttu-id="53326-141">Phase 2 : Créer le réseau virtuel de hello TestVNET</span><span class="sxs-lookup"><span data-stu-id="53326-141">Phase 2: Create hello TestVNET virtual network</span></span>
<span data-ttu-id="53326-142">D’abord créer le réseau virtuel de TestVNET hello et protéger à l’aide d’un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="53326-142">First, create hello TestVNET virtual network and protect it with a network security group.</span></span>

    $rgName="<name of hello resource group that you used for your TestLab virtual network>"
    $locName="<Azure location name where you placed hello TestLab virtual network, such as West US>"
    $locShortName="<Azure location name from $locName in all lowercase letters with spaces removed. Example:  westus>"
    $testSubnet=New-AzureRMVirtualNetworkSubnetConfig -Name "TestSubnet" -AddressPrefix 192.168.0.0/24
    $gatewaySubnet=New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix 192.168.255.248/29
    New-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName -Location $locName -AddressPrefix 192.168.0.0/16 -Subnet $testSubnet,$gatewaySubnet –DNSServer 10.0.0.4
    $rule1=New-AzureRMNetworkSecurityRuleConfig -Name "RDPTraffic" -Description "Allow RDP tooall VMs on hello subnet" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 3389
    New-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName -Location $locShortName -SecurityRules $rule1
    $vnet=Get-AzureRMVirtualNetwork -ResourceGroupName $rgName -Name TestVNET
    $nsg=Get-AzureRMNetworkSecurityGroup -Name "TestSubnet" -ResourceGroupName $rgName
    Set-AzureRMVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet" -AddressPrefix 192.168.0.0/24 -NetworkSecurityGroup $nsg

<span data-ttu-id="53326-143">Ensuite, demande un toobe d’adresse IP publique allouée toohello passerelle pour réseau virtuel de TestVNET hello et créer votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="53326-143">Next, request a public IP address toobe allocated toohello gateway for hello TestVNET virtual network and create your gateway.</span></span>

    $gwpip=New-AzureRmPublicIpAddress -Name TestVNET_pip -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $vnet=Get-AzureRmVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
    $gwipconfig=New-AzureRmVirtualNetworkGatewayIpConfig -Name "TestVNET_GWConfig" -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
    New-AzureRmVirtualNetworkGateway -Name "TestVNET_GW" -ResourceGroupName $rgName -Location $locName -IpConfigurations $gwipconfig -GatewayType Vpn -VpnType RouteBased

<span data-ttu-id="53326-144">Ceci est votre configuration actuelle.</span><span class="sxs-lookup"><span data-stu-id="53326-144">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph2.png)

## <a name="phase-3-create-hello-vnet-to-vnet-connection"></a><span data-ttu-id="53326-145">Phase 3 : Créer des connexions de hello au réseau</span><span class="sxs-lookup"><span data-stu-id="53326-145">Phase 3: Create hello VNet-to-VNet connection</span></span>
<span data-ttu-id="53326-146">Tout d'abord, obtenez une clé prépartagée, aléatoire, à chiffrement fort, de 32 caractères auprès de votre administrateur réseau ou de sécurité.</span><span class="sxs-lookup"><span data-stu-id="53326-146">First, obtain a random, cryptographically strong, 32-character pre-shared key from your network or security administrator.</span></span> <span data-ttu-id="53326-147">Vous pouvez également utiliser les informations de hello à [créer une chaîne aléatoire pour une clé prépartagée IPsec](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) tooobtain une clé prépartagée.</span><span class="sxs-lookup"><span data-stu-id="53326-147">Alternately, use hello information at [Create a random string for an IPsec preshared key](http://social.technet.microsoft.com/wiki/contents/articles/32330.create-a-random-string-for-an-ipsec-preshared-key.aspx) tooobtain a pre-shared key.</span></span>

<span data-ttu-id="53326-148">Ensuite, utilisez ces commandes toocreate hello au réseau VPN de connexion, ce qui peut prendre quelques toocomplete de temps.</span><span class="sxs-lookup"><span data-stu-id="53326-148">Next, use these commands toocreate hello VNet-to-VNet VPN connection, which can take some time toocomplete.</span></span>

    $sharedKey="<pre-shared key value>"
    $gwTestLab=Get-AzureRmVirtualNetworkGateway -Name TestLab_GW -ResourceGroupName $rgName
    $gwTestVNET=Get-AzureRmVirtualNetworkGateway -Name TestVNET_GW -ResourceGroupName $rgName
    New-AzureRmVirtualNetworkGatewayConnection -Name TestLab_to_TestVNET -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestLab -VirtualNetworkGateway2 $gwTestVNET -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey
    New-AzureRmVirtualNetworkGatewayConnection -Name TestVNET_to_TestLab -ResourceGroupName $rgName -VirtualNetworkGateway1 $gwTestVNET -VirtualNetworkGateway2 $gwTestLab -Location $locName -ConnectionType Vnet2Vnet -SharedKey $sharedKey

<span data-ttu-id="53326-149">Après quelques minutes, la connexion de hello doit être établie.</span><span class="sxs-lookup"><span data-stu-id="53326-149">After a few minutes, hello connection should be established.</span></span>

<span data-ttu-id="53326-150">Ceci est votre configuration actuelle.</span><span class="sxs-lookup"><span data-stu-id="53326-150">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph3.png)

## <a name="phase-4-configure-dc2"></a><span data-ttu-id="53326-151">Phase 4 : configurer DC2</span><span class="sxs-lookup"><span data-stu-id="53326-151">Phase 4: Configure DC2</span></span>
<span data-ttu-id="53326-152">Créez d’abord une machine virtuelle pour DC2.</span><span class="sxs-lookup"><span data-stu-id="53326-152">First, create a virtual machine for DC2.</span></span> <span data-ttu-id="53326-153">Exécutez ces commandes à l’invite de commande Azure PowerShell hello sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="53326-153">Run these commands at hello Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<hello storage account name for hello base configuration>"
    $vnet=Get-AzureRMVirtualNetwork -Name TestVNET -ResourceGroupName $rgName
    $pip=New-AzureRMPublicIpAddress -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name DC2-NIC -ResourceGroupName $rgName -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -PrivateIpAddress 192.168.0.4
    $vm=New-AzureRMVMConfig -VMName DC2 -VMSize Standard_A1
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestVNET-ADDSDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name ADDS-Data -DiskSizeInGB 20 -VhdUri $vhdURI  -CreateOption empty
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for DC2."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName DC2 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/DC2-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name DC2-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="53326-154">Connectez-vous ensuite toohello DC2 machine virtuelle à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="53326-154">Next, connect toohello new DC2 virtual machine from hello Azure portal.</span></span>

<span data-ttu-id="53326-155">Ensuite, configurez un trafic de tooallow de règle de pare-feu Windows pour le test de connectivité de base.</span><span class="sxs-lookup"><span data-stu-id="53326-155">Next, configure a Windows Firewall rule tooallow traffic for basic connectivity testing.</span></span> <span data-ttu-id="53326-156">À partir d’une invite de commandes Windows PowerShell de niveau administrateur sur DC2, exécutez ces commandes.</span><span class="sxs-lookup"><span data-stu-id="53326-156">From an administrator-level Windows PowerShell command prompt on DC2, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc1.corp.contoso.com

<span data-ttu-id="53326-157">commande ping de Hello doit aboutir à quatre réponses de réussite de l’adresse IP 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="53326-157">hello ping command should result in four successful replies from IP address 10.0.0.4.</span></span> <span data-ttu-id="53326-158">Ceci est un test de trafic entre hello connexion de réseau virtuel à réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="53326-158">This is a test of traffic across hello VNet-to-VNet connection.</span></span>

<span data-ttu-id="53326-159">Ensuite, ajoutez hello disque de données supplémentaire sur DC2 en tant que nouveau volume avec la lettre de lecteur hello F:.</span><span class="sxs-lookup"><span data-stu-id="53326-159">Next, add hello extra data disk on DC2 as a new volume with hello drive letter F:.</span></span>

1. <span data-ttu-id="53326-160">Dans le volet gauche hello du Gestionnaire de serveur, cliquez sur **File and Storage Services**, puis cliquez sur **disques**.</span><span class="sxs-lookup"><span data-stu-id="53326-160">In hello left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="53326-161">Dans le volet du sommaire hello, Bonjour **disques** , cliquez sur **disque 2** (avec hello **Partition** défini trop**inconnu**).</span><span class="sxs-lookup"><span data-stu-id="53326-161">In hello contents pane, in hello **Disks** group, click **disk 2** (with hello **Partition** set too**Unknown**).</span></span>
3. <span data-ttu-id="53326-162">Cliquez sur **Tâches**, puis sur **Nouveau volume**.</span><span class="sxs-lookup"><span data-stu-id="53326-162">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="53326-163">Sur hello avant de commencer, page de hello Assistant Nouveau Volume, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="53326-163">On hello Before you begin page of hello New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="53326-164">Sur le serveur hello Select de hello et page de disque, cliquez sur **Disk 2**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="53326-164">On hello Select hello server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="53326-165">À l’invite, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="53326-165">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="53326-166">Dans spécifier la taille de page de volume hello hello de hello, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="53326-166">On hello Specify hello size of hello volume page, click **Next**.</span></span>
7. <span data-ttu-id="53326-167">Hello Assign tooa lecteur lettre ou un dossier de page, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="53326-167">On hello Assign tooa drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="53326-168">Dans la page des paramètres système hello sélectionner un fichier, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="53326-168">On hello Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="53326-169">Dans hello page Confirmer les sélections, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="53326-169">On hello Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="53326-170">Lorsque vous avez terminé, cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="53326-170">When complete, click **Close**.</span></span>

<span data-ttu-id="53326-171">Ensuite, configurez DC2 en tant que contrôleur de domaine répliqué pour le domaine corp.contoso.com hello.</span><span class="sxs-lookup"><span data-stu-id="53326-171">Next, configure DC2 as a replica domain controller for hello corp.contoso.com domain.</span></span> <span data-ttu-id="53326-172">Exécutez ces commandes à partir de l’invite de commandes Windows PowerShell hello sur DC2.</span><span class="sxs-lookup"><span data-stu-id="53326-172">Run these commands from hello Windows PowerShell command prompt on DC2.</span></span>

    Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
    Install-ADDSDomainController -Credential (Get-Credential CORP\User1) -DomainName "corp.contoso.com" -InstallDns:$true -DatabasePath "F:\NTDS" -LogPath "F:\Logs" -SysvolPath "F:\SYSVOL"

<span data-ttu-id="53326-173">Notez que vous êtes invité à toosupply à la fois hello CORP\User1 le mot de passe et un mot de passe en Mode de restauration des Services annuaire (DSRM) et toorestart DC2.</span><span class="sxs-lookup"><span data-stu-id="53326-173">Note that you are prompted toosupply both hello CORP\User1 password and a Directory Services Restore Mode (DSRM) password, and toorestart DC2.</span></span>

<span data-ttu-id="53326-174">Maintenant que hello TestVNET réseau virtuel n’a son propre serveur DNS (DC2), vous devez configurer ce serveur DNS toouse de réseau virtuel TestVNET hello.</span><span class="sxs-lookup"><span data-stu-id="53326-174">Now that hello TestVNET virtual network has its own DNS server (DC2), you must configure hello TestVNET virtual network toouse this DNS server.</span></span>

1. <span data-ttu-id="53326-175">Dans le volet gauche de hello Hello portail Azure, cliquez sur icône de réseaux virtuels hello, puis cliquez sur **TestVNET**.</span><span class="sxs-lookup"><span data-stu-id="53326-175">In hello left pane of hello Azure portal, click hello virtual networks icon, and then click **TestVNET**.</span></span>
2. <span data-ttu-id="53326-176">Sur hello **paramètres** , cliquez sur **serveurs DNS**.</span><span class="sxs-lookup"><span data-stu-id="53326-176">On hello **Settings** tab, click **DNS servers**.</span></span>
3. <span data-ttu-id="53326-177">Dans **serveur DNS principal**, type **192.168.0.4** tooreplace 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="53326-177">In **Primary DNS server**, type **192.168.0.4** tooreplace 10.0.0.4.</span></span>
4. <span data-ttu-id="53326-178">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="53326-178">Click **Save**.</span></span>

<span data-ttu-id="53326-179">Ceci est votre configuration actuelle.</span><span class="sxs-lookup"><span data-stu-id="53326-179">This is your current configuration.</span></span> 

![](./media/ps-hybrid-cloud-test-env-sim/virtual-machines-windows-ps-hybrid-cloud-test-env-sim-ph4.png)

<span data-ttu-id="53326-180">Votre environnement de cloud hybride simulé est maintenant prêt pour les tests.</span><span class="sxs-lookup"><span data-stu-id="53326-180">Your simulated hybrid cloud environment is now ready for testing.</span></span>

## <a name="next-step"></a><span data-ttu-id="53326-181">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="53326-181">Next step</span></span>
* <span data-ttu-id="53326-182">Configurez une [application métier basée sur le web](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) dans cet environnement.</span><span class="sxs-lookup"><span data-stu-id="53326-182">Set up a [web-based, line of business application](ps-hybrid-cloud-test-env-lob.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in this environment.</span></span>

