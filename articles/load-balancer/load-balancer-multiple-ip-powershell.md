---
title: "aaaLoad équilibrage sur plusieurs configurations IP dans Azure | Documents Microsoft"
description: "Équilibrage de charge sur des configurations IP principales et secondaires."
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: annahar
ms.openlocfilehash: fe1cdb317350942ff759229491c2025e98dd24a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a><span data-ttu-id="e0890-103">Équilibrage de charge sur plusieurs configurations IP avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0890-103">Load balancing on multiple IP configurations using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e0890-104">Portail</span><span class="sxs-lookup"><span data-stu-id="e0890-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="e0890-105">INTERFACE DE LIGNE DE COMMANDE</span><span class="sxs-lookup"><span data-stu-id="e0890-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="e0890-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0890-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="e0890-107">Cet article décrit comment toouse équilibrage de charge Azure avec adresse IP de plusieurs adresses sur une interface réseau secondaire (NIC).</span><span class="sxs-lookup"><span data-stu-id="e0890-107">This article describes how toouse Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="e0890-108">Avec ce scénario, nous disposons de deux machines virtuelles exécutant Windows, chacune avec une carte réseau principale et secondaire.</span><span class="sxs-lookup"><span data-stu-id="e0890-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="e0890-109">Chacun des hello secondaire cartes réseau ont deux configurations IP.</span><span class="sxs-lookup"><span data-stu-id="e0890-109">Each of hello secondary NICs have two IP configurations.</span></span> <span data-ttu-id="e0890-110">Chaque machine virtuelle héberge les deux sites web contoso.com et fabrikam.com. Chaque site Web est lié tooone de configurations IP hello hello seconde.</span><span class="sxs-lookup"><span data-stu-id="e0890-110">Each VM hosts both websites contoso.com and fabrikam.com. Each website is bound tooone of hello IP configurations on hello secondary NIC.</span></span> <span data-ttu-id="e0890-111">Nous utilisons équilibrage de charge Azure tooexpose deux frontal adresses IP, une pour chaque site Web, toodistribute toohello respectifs IP configuration du trafic pour le site Web de hello.</span><span class="sxs-lookup"><span data-stu-id="e0890-111">We use Azure Load Balancer tooexpose two frontend IP addresses, one for each website, toodistribute traffic toohello respective IP configuration for hello website.</span></span> <span data-ttu-id="e0890-112">Ce scénario utilise hello même numéro de port entre les serveurs frontaux, ainsi que les deux adresses IP du pool principal.</span><span class="sxs-lookup"><span data-stu-id="e0890-112">This scenario uses hello same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![Image du scénario LB](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a><span data-ttu-id="e0890-114">Solde de tooload étapes sur plusieurs configurations IP</span><span class="sxs-lookup"><span data-stu-id="e0890-114">Steps tooload balance on multiple IP configurations</span></span>

<span data-ttu-id="e0890-115">Suivez les étapes de hello ci-dessous le scénario de hello tooachieve présentée dans cet article :</span><span class="sxs-lookup"><span data-stu-id="e0890-115">Follow hello steps below tooachieve hello scenario outlined in this article:</span></span>

1. <span data-ttu-id="e0890-116">Installez Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0890-116">Install Azure PowerShell.</span></span> <span data-ttu-id="e0890-117">Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour plus d’informations sur l’installation hello dernière version de Azure PowerShell, en sélectionnant votre abonnement et l’ouverture de session tooyour compte.</span><span class="sxs-lookup"><span data-stu-id="e0890-117">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>
2. <span data-ttu-id="e0890-118">Créer un groupe de ressources à l’aide de hello suivant les paramètres :</span><span class="sxs-lookup"><span data-stu-id="e0890-118">Create a resource group using hello following settings:</span></span>

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    <span data-ttu-id="e0890-119">Pour plus d’informations, voir l’Étape 2 de [Créer un groupe de ressources](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e0890-119">For more information, see Step 2 of [Create a Resource Group](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

3. <span data-ttu-id="e0890-120">[Créer un groupe à haute disponibilité](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="e0890-120">[Create an Availability Set](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain your VMs.</span></span> <span data-ttu-id="e0890-121">Pour ce scénario, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e0890-121">For this scenario, use hello following command:</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. <span data-ttu-id="e0890-122">Suivez les instructions étapes 3 à 5 de [créer une machine virtuelle Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) création de hello tooprepare d’une machine virtuelle avec une carte réseau. unique de l’article</span><span class="sxs-lookup"><span data-stu-id="e0890-122">Follow instructions steps 3 through 5 in [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) article tooprepare hello creation of a VM with a single NIC.</span></span> <span data-ttu-id="e0890-123">Exécuter une étape 6.1, suivant et servez-vous hello au lieu de l’étape 6.2 :</span><span class="sxs-lookup"><span data-stu-id="e0890-123">Execute step 6.1, and use hello following instead of step 6.2:</span></span>

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    <span data-ttu-id="e0890-124">Accomplissez ensuite les étapes 6.3 à 6.8 de l’article [Créer une machine virtuelle Windows](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e0890-124">Then complete [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) steps 6.3 through 6.8.</span></span>

5. <span data-ttu-id="e0890-125">Ajoutez un deuxième tooeach de configuration IP de hello machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="e0890-125">Add a second IP configuration tooeach of hello VMs.</span></span> <span data-ttu-id="e0890-126">Suivez les instructions de hello dans [affecter plusieurs adresses IP toovirtual machines](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) l’article.</span><span class="sxs-lookup"><span data-stu-id="e0890-126">Follow hello instructions in [Assign multiple IP addresses toovirtual machines](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) article.</span></span> <span data-ttu-id="e0890-127">Utilisez hello suivant les paramètres de configuration :</span><span class="sxs-lookup"><span data-stu-id="e0890-127">Use hello following configuration settings:</span></span>

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    <span data-ttu-id="e0890-128">Il est inutile tooassociate hello secondaire configurations IP avec des adresses IP publiques à des fins de hello de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="e0890-128">You do not need tooassociate hello secondary IP configurations with public IPs for hello purpose of this tutorial.</span></span> <span data-ttu-id="e0890-129">Modifier la partie d’association hello commande tooremove hello publique IP.</span><span class="sxs-lookup"><span data-stu-id="e0890-129">Edit hello command tooremove hello public IP association part.</span></span>

6. <span data-ttu-id="e0890-130">Exécutez à nouveau les étapes 4 à 6 de cet article pour la machine virtuelle VM2.</span><span class="sxs-lookup"><span data-stu-id="e0890-130">Complete steps 4 through 6 of this article again for VM2.</span></span> <span data-ttu-id="e0890-131">Être tooVM2 de nom de machine virtuelle de hello tooreplace que lors de cette opération.</span><span class="sxs-lookup"><span data-stu-id="e0890-131">Be sure tooreplace hello VM name tooVM2 when doing this.</span></span> <span data-ttu-id="e0890-132">Notez que vous n’avez pas besoin toocreate un réseau virtuel pour hello deuxième machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e0890-132">Note that you do not need toocreate a virtual network for hello second VM.</span></span> <span data-ttu-id="e0890-133">Vous pouvez ou non créer un sous-réseau, selon votre cas d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="e0890-133">You may or may not create a new subnet based on your use case.</span></span>

7. <span data-ttu-id="e0890-134">Créez deux adresses IP publiques et les stocker dans les variables appropriées hello comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="e0890-134">Create two public IP addresses and store them in hello appropriate variables as shown:</span></span>

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. <span data-ttu-id="e0890-135">Créez deux configurations IP frontales :</span><span class="sxs-lookup"><span data-stu-id="e0890-135">Create two frontend IP configurations:</span></span>

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. <span data-ttu-id="e0890-136">Créer vos pools d’adresses principaux, une sonde et vos règles d’équilibrage de charge :</span><span class="sxs-lookup"><span data-stu-id="e0890-136">Create your backend address pools, a probe, and your load balancing rules:</span></span>

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. <span data-ttu-id="e0890-137">Une fois les ressources créées, créez votre équilibreur de charge :</span><span class="sxs-lookup"><span data-stu-id="e0890-137">Once you have these resources created, create your load balancer:</span></span>

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. <span data-ttu-id="e0890-138">Ajouter hello deuxième principal adresse serveur frontal et pool IP configuration tooyour nouvellement créé équilibrage de charge :</span><span class="sxs-lookup"><span data-stu-id="e0890-138">Add hello second backend address pool and frontend IP configuration tooyour newly created load balancer:</span></span>

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. <span data-ttu-id="e0890-139">commandes Hello ci-dessous obtenir hello cartes d’interface réseau, puis ajoutez que les deux configurations IP de chaque pool d’adresses principales du secondaire NIC toohello Hello l’équilibrage de charge :</span><span class="sxs-lookup"><span data-stu-id="e0890-139">hello commands below get hello NICs and then add both IP configurations of each secondary NIC toohello backend address pool of hello load balancer:</span></span>

    ```powershell
    $nic1 = Get-AzureRmNetworkInterface -Name "VM1-NIC2" -ResourceGroupName "MyResourcegroup";
    $nic2 = Get-AzureRmNetworkInterface -Name "VM2-NIC2" -ResourceGroupName "MyResourcegroup";

    $nic1.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic1.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);
    $nic2.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic2.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);

    $mylb = $mylb | Set-AzureRmLoadBalancer

    $nic1 | Set-AzureRmNetworkInterface
    $nic2 | Set-AzureRmNetworkInterface
    ```

13. <span data-ttu-id="e0890-140">Enfin, vous devez configurer DNS ressource enregistrements toopoint toohello respectifs adresse IP frontale de hello équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="e0890-140">Finally, you must configure DNS resource records toopoint toohello respective frontend IP address of hello Load Balancer.</span></span> <span data-ttu-id="e0890-141">Vous pouvez héberger vos domaines dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="e0890-141">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="e0890-142">Pour plus d’informations sur l’utilisation d’Azure DNS avec un équilibrage de charge, voir [Utiliser Azure DNS avec d’autres services Azure](../dns/dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="e0890-142">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0890-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e0890-143">Next steps</span></span>
- <span data-ttu-id="e0890-144">En savoir plus sur le fonctionnement des services de l’équilibrage de charge toocombine dans Azure dans [à l’aide des services d’équilibrage de charge dans Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span><span class="sxs-lookup"><span data-stu-id="e0890-144">Learn more about how toocombine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="e0890-145">Découvrez comment vous pouvez utiliser différents types de journaux dans Azure toomanage et résoudre les problèmes d’équilibrage de charge dans [journal analytique pour l’équilibrage de charge Azure](../load-balancer/load-balancer-monitor-log.md).</span><span class="sxs-lookup"><span data-stu-id="e0890-145">Learn how you can use different types of logs in Azure toomanage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
