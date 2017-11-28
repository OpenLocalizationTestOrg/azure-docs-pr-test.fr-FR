---
title: Plusieurs adresses IP virtuelles par service cloud
description: "Vue d’ensemble de multiVIP et définition de plusieurs adresses IP virtuelles sur un service cloud"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 85f6d26a-3df5-4b8e-96a1-92b2793b5284
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: f40e0501eed8d5f296e7c79d8a35705a695ae6fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a><span data-ttu-id="6133b-103">Configuration de plusieurs adresses IP virtuelles pour un service cloud</span><span class="sxs-lookup"><span data-stu-id="6133b-103">Configure multiple VIPs for a cloud service</span></span>

<span data-ttu-id="6133b-104">Vous pouvez accéder aux services cloud Azure via Internet à l’aide d’une adresse IP fournie par Azure.</span><span class="sxs-lookup"><span data-stu-id="6133b-104">You can access Azure cloud services over the public Internet by using an IP address provided by Azure.</span></span> <span data-ttu-id="6133b-105">Cette adresse IP publique est appelée adresse IP virtuelle, car elle est liée à l’équilibrage de charge Azure et non aux instances de la machine virtuelle (VM) dans le service cloud.</span><span class="sxs-lookup"><span data-stu-id="6133b-105">This public IP address is referred to as a VIP (virtual IP) since it is linked to the Azure load balancer, and not the Virtual Machine (VM) instances within the cloud service.</span></span> <span data-ttu-id="6133b-106">Vous pouvez accéder à une instance de machine virtuelle dans un service cloud à l’aide d’une adresse IP virtuelle unique.</span><span class="sxs-lookup"><span data-stu-id="6133b-106">You can access any VM instance within a cloud service by using a single VIP.</span></span>

<span data-ttu-id="6133b-107">Toutefois, il existe des scénarios dans lesquels vous pouvez avoir besoin de plusieurs adresses IP virtuelles comme point d’entrée vers le même service cloud.</span><span class="sxs-lookup"><span data-stu-id="6133b-107">However, there are scenarios in which you may need more than one VIP as an entry point to the same cloud service.</span></span> <span data-ttu-id="6133b-108">Par exemple, votre service cloud peut héberger plusieurs sites web qui exigent une connexion SSL à l’aide du port 443 par défaut, chaque site étant hébergé pour un autre client ou locataire.</span><span class="sxs-lookup"><span data-stu-id="6133b-108">For instance, your cloud service may host multiple websites that require SSL connectivity using the default port of 443, as each site is hosted for a different customer, or tenant.</span></span> <span data-ttu-id="6133b-109">Dans ce scénario, vous devez avoir une adresse IP publique différente pour chaque site Web.</span><span class="sxs-lookup"><span data-stu-id="6133b-109">In this scenario, you need to have a different public facing IP address for each website.</span></span> <span data-ttu-id="6133b-110">Le diagramme suivant illustre un hébergement Web mutualisé typique nécessitant plusieurs certificats SSL sur le même port public.</span><span class="sxs-lookup"><span data-stu-id="6133b-110">The diagram below illustrates a typical multi-tenant web hosting with a need for multiple SSL certificates on the same public port.</span></span>

![Scénario avec plusieurs adresses IP virtuelles SSL](./media/load-balancer-multivip/Figure1.png)

<span data-ttu-id="6133b-112">Dans l’exemple ci-dessus, toutes les adresses IP virtuelles utilisent le même port public (443) et le trafic est redirigé vers une ou plusieurs machines virtuelles à équilibrage de charge sur un seul port privé de l’adresse IP interne du service cloud qui héberge les sites Web.</span><span class="sxs-lookup"><span data-stu-id="6133b-112">In the example above, all VIPs use the same public port (443) and traffic is redirected to one or more load balanced VMs on a unique private port for the internal IP address of the cloud service hosting all the websites.</span></span>

> [!NOTE]
> <span data-ttu-id="6133b-113">L’hébergement de plusieurs écouteurs de groupe de disponibilité SQL AlwaysOn dans le même jeu de machines virtuelles nécessite également l’utilisation de plusieurs adresses IP virtuelles.</span><span class="sxs-lookup"><span data-stu-id="6133b-113">Another situation requiring the use the multiple VIPs is hosting multiple SQL AlwaysOn availability group listeners on the same set of Virtual Machines.</span></span>

<span data-ttu-id="6133b-114">Les adresses IP virtuelles sont dynamiques par défaut, ce qui signifie que l’adresse IP réelle affectée au service cloud peut changer au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="6133b-114">VIPs are dynamic by default, which means that the actual IP address assigned to the cloud service may change over time.</span></span> <span data-ttu-id="6133b-115">Pour éviter cela, vous pouvez réserver une adresse IP virtuelle pour votre service.</span><span class="sxs-lookup"><span data-stu-id="6133b-115">To prevent that from happening, you can reserve a VIP for your service.</span></span> <span data-ttu-id="6133b-116">Pour plus d’informations sur les adresses IP virtuelles réservées, consultez [Adresses IP publiques réservées](../virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="6133b-116">To learn more about reserved VIPs, see [Reserved Public IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6133b-117">Consultez [Tarification des adresses IP](https://azure.microsoft.com/pricing/details/ip-addresses/) pour plus d’informations sur la tarification des adresses IP virtuelles et réservées.</span><span class="sxs-lookup"><span data-stu-id="6133b-117">Please see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/) for information on pricing on VIPs and reserved IPs.</span></span>

<span data-ttu-id="6133b-118">Vous pouvez utiliser PowerShell pour vérifier les adresses IP virtuelles utilisées par vos services cloud, ainsi qu’ajouter et supprimer des adresses IP virtuelles, associer une adresse IP virtuelle à un point de terminaison et configurer l’équilibrage de charge sur une adresse IP virtuelle spécifique.</span><span class="sxs-lookup"><span data-stu-id="6133b-118">You can use PowerShell to verify the VIPs used by your cloud services, as well as add and remove VIPs, associate a VIP to an endpoint, and configure load balancing on a specific VIP.</span></span>

## <a name="limitations"></a><span data-ttu-id="6133b-119">Limitations</span><span class="sxs-lookup"><span data-stu-id="6133b-119">Limitations</span></span>

<span data-ttu-id="6133b-120">À ce stade, la fonctionnalité d'adresses IP virtuelles multiples est limitée aux scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="6133b-120">At this time, Multi VIP functionality is limited to the following scenarios:</span></span>

* <span data-ttu-id="6133b-121">**IaaS uniquement**.</span><span class="sxs-lookup"><span data-stu-id="6133b-121">**IaaS only**.</span></span> <span data-ttu-id="6133b-122">Vous ne pouvez activer les adresses IP virtuelles multiples que pour les services cloud qui contiennent des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="6133b-122">You can only enable Multi VIP for cloud services that contain VMs.</span></span> <span data-ttu-id="6133b-123">Vous ne pouvez pas utiliser les adresses IP virtuelles multiples dans les scénarios PaaS avec des instances de rôles.</span><span class="sxs-lookup"><span data-stu-id="6133b-123">You cannot use Multi VIP in PaaS scenarios with role instances.</span></span>
* <span data-ttu-id="6133b-124">**PowerShell uniquement**.</span><span class="sxs-lookup"><span data-stu-id="6133b-124">**PowerShell only**.</span></span> <span data-ttu-id="6133b-125">Vous pouvez gérer les adresses IP virtuelles multiples uniquement à l'aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6133b-125">You can only manage Multi VIP by using PowerShell.</span></span>

<span data-ttu-id="6133b-126">Ces limitations sont temporaires et peuvent changer à tout moment.</span><span class="sxs-lookup"><span data-stu-id="6133b-126">These limitations are temporary, and may change at any time.</span></span> <span data-ttu-id="6133b-127">N'oubliez pas de revenir sur cette page pour consulter les modifications.</span><span class="sxs-lookup"><span data-stu-id="6133b-127">Make sure to revisit this page to verify future changes.</span></span>

## <a name="how-to-add-a-vip-to-a-cloud-service"></a><span data-ttu-id="6133b-128">Ajout d’une adresse IP virtuelle à un service cloud</span><span class="sxs-lookup"><span data-stu-id="6133b-128">How to add a VIP to a cloud service</span></span>
<span data-ttu-id="6133b-129">Pour ajouter une adresse IP virtuelle à votre service, exécutez la commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="6133b-129">To add a VIP to your service, run the following PowerShell command:</span></span>

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

<span data-ttu-id="6133b-130">Cette commande affiche un résultat semblable à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6133b-130">This command displays a result similar to the following sample:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-to-remove-a-vip-from-a-cloud-service"></a><span data-ttu-id="6133b-131">Suppression d’une adresse IP virtuelle d’un service cloud</span><span class="sxs-lookup"><span data-stu-id="6133b-131">How to remove a VIP from a cloud service</span></span>
<span data-ttu-id="6133b-132">Pour supprimer l’adresse IP virtuelle ajoutée à votre service dans l’exemple ci-dessus, exécutez la commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="6133b-132">To remove the VIP added to your service in the example above, run the following PowerShell command:</span></span>

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> <span data-ttu-id="6133b-133">Vous ne pouvez supprimer une adresse IP virtuelle que si aucun point de terminaison ne lui est associé.</span><span class="sxs-lookup"><span data-stu-id="6133b-133">You can only remove a VIP if it has no endpoints associated to it.</span></span>


## <a name="how-to-retrieve-vip-information-from-a-cloud-service"></a><span data-ttu-id="6133b-134">Récupération des informations de l’adresse IP virtuelle à partir d’un service cloud</span><span class="sxs-lookup"><span data-stu-id="6133b-134">How to retrieve VIP information from a Cloud Service</span></span>
<span data-ttu-id="6133b-135">Pour récupérer les adresses IP virtuelles associées à un service cloud, exécutez le script PowerShell suivant :</span><span class="sxs-lookup"><span data-stu-id="6133b-135">To retrieve the VIPs associated with a cloud service, run the following PowerShell script:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="6133b-136">Le script affiche un résultat semblable à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6133b-136">The script displays a result similar to the following sample:</span></span>

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

<span data-ttu-id="6133b-137">Dans cet exemple, le service cloud a trois adresses IP virtuelles (Vip) :</span><span class="sxs-lookup"><span data-stu-id="6133b-137">In this example, the cloud service has 3 VIPs:</span></span>

* <span data-ttu-id="6133b-138">**Vip1** est l’adresse IP virtuelle par défaut, comme en atteste la valeur de IsDnsProgrammedName définie sur true.</span><span class="sxs-lookup"><span data-stu-id="6133b-138">**Vip1** is the default VIP, you know that because the value for IsDnsProgrammedName is set to true.</span></span>
* <span data-ttu-id="6133b-139">**Vip2** et **Vip3** ne sont pas utilisées étant donné qu’elles n’ont pas d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="6133b-139">**Vip2** and **Vip3** are not used as they do not have any IP addresses.</span></span> <span data-ttu-id="6133b-140">Elles servent uniquement si vous associez un point de terminaison à l’adresse IP virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6133b-140">They will only be used if you associate an endpoint to the VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="6133b-141">Votre abonnement est uniquement facturé pour les adresses IP virtuelles supplémentaires après leur association à un point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="6133b-141">Your subscription will only be charged for extra VIPs once they are associated with an endpoint.</span></span> <span data-ttu-id="6133b-142">Pour plus d’informations sur la tarification, voir la page [Tarification des adresses IP](https://azure.microsoft.com/pricing/details/ip-addresses/).</span><span class="sxs-lookup"><span data-stu-id="6133b-142">For more information on pricing, see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/).</span></span>

## <a name="how-to-associate-a-vip-to-an-endpoint"></a><span data-ttu-id="6133b-143">Association d’une adresse IP virtuelle à un point de terminaison</span><span class="sxs-lookup"><span data-stu-id="6133b-143">How to associate a VIP to an endpoint</span></span>

<span data-ttu-id="6133b-144">Pour associer une adresse IP virtuelle sur un service cloud à un point de terminaison, exécutez la commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="6133b-144">To associate a VIP on a cloud service to an endpoint, run the following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

<span data-ttu-id="6133b-145">La commande crée un point de terminaison lié à l’adresse IP virtuelle appelée *Vip2* sur le port *80*, ainsi que des liens vers la machine virtuelle nommée *myVM1* dans un service cloud nommé *myService* à l’aide de *TCP* sur le port *8080*.</span><span class="sxs-lookup"><span data-stu-id="6133b-145">The command creates an endpoint linked to the VIP called *Vip2* on port *80*, and links it to the VM named *myVM1* in a cloud service named *myService* using *TCP* on port *8080*.</span></span>

<span data-ttu-id="6133b-146">Pour vérifier la configuration, exécutez la commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="6133b-146">To verify the configuration, run the following PowerShell command:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="6133b-147">Le résultat ressemble à l’exemple qui suit :</span><span class="sxs-lookup"><span data-stu-id="6133b-147">The output looks similar to the following example:</span></span>

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         : 191.238.74.13
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

## <a name="how-to-enable-load-balancing-on-a-specific-vip"></a><span data-ttu-id="6133b-148">Activation de l’équilibrage de charge sur une adresse IP virtuelle spécifique</span><span class="sxs-lookup"><span data-stu-id="6133b-148">How to enable load balancing on a specific VIP</span></span>

<span data-ttu-id="6133b-149">Vous pouvez associer une adresse IP virtuelle unique à plusieurs machines virtuelles à des fins d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="6133b-149">You can associate a single VIP with multiple virtual machines for load balancing purposes.</span></span> <span data-ttu-id="6133b-150">Par exemple, supposons que vous avez un service cloud nommé *myService*, et deux machines virtuelles nommées *myVM1* et *myVM2*.</span><span class="sxs-lookup"><span data-stu-id="6133b-150">For example, you have a cloud service named *myService*, and two virtual machines named *myVM1* and *myVM2*.</span></span> <span data-ttu-id="6133b-151">Votre service cloud dispose de plusieurs adresses IP virtuelles, dont une nommée *Vip2*.</span><span class="sxs-lookup"><span data-stu-id="6133b-151">And your cloud service has multiple VIPs, one of them named *Vip2*.</span></span> <span data-ttu-id="6133b-152">Si vous souhaitez vous assurer que l’ensemble du trafic vers le port *81* sur *Vip2* est équilibré entre *myVM1* et *myVM2* sur le port *8181*, exécutez le script PowerShell suivant :</span><span class="sxs-lookup"><span data-stu-id="6133b-152">If you want to ensure that all traffic to port *81* on *Vip2* is balanced between *myVM1* and *myVM2* on port *8181*, run the following PowerShell script:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

<span data-ttu-id="6133b-153">Vous pouvez également mettre à jour votre équilibrage de charge pour utiliser une adresse IP virtuelle différente.</span><span class="sxs-lookup"><span data-stu-id="6133b-153">You can also update your load balancer to use a different VIP.</span></span> <span data-ttu-id="6133b-154">Par exemple, si vous exécutez la commande PowerShell suivante, vous modifiez le jeu d’équilibrage de la charge, afin qu’il utilise une adresse IP virtuelle nommée Vip1 :</span><span class="sxs-lookup"><span data-stu-id="6133b-154">For example, if you run the PowerShell command below, you will change the load balancing set to use a VIP named Vip1:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a><span data-ttu-id="6133b-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6133b-155">Next Steps</span></span>

[<span data-ttu-id="6133b-156">Analyse des journaux d’Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="6133b-156">Log analytics for Azure Load Balance</span></span>](load-balancer-monitor-log.md)

[<span data-ttu-id="6133b-157">Présentation de l’équilibrage de charge accessible sur Internet</span><span class="sxs-lookup"><span data-stu-id="6133b-157">Internet facing load balancer overview</span></span>](load-balancer-internet-overview.md)

[<span data-ttu-id="6133b-158">Prise en main de l’équilibrage de charge accessible sur Internet</span><span class="sxs-lookup"><span data-stu-id="6133b-158">Get started on Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="6133b-159">Présentation du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="6133b-159">Virtual Network Overview</span></span>](../virtual-network/virtual-networks-overview.md)

[<span data-ttu-id="6133b-160">API REST d’adresse IP réservée</span><span class="sxs-lookup"><span data-stu-id="6133b-160">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)
