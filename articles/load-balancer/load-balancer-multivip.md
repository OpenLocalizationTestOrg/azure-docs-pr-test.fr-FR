---
title: aaaMutiple les adresses IP virtuelles pour un service cloud
description: "Vue d’ensemble de plusieurs adresses IP virtuelles et comment tooset plusieurs adresses IP virtuelles sur un service cloud"
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
ms.openlocfilehash: b3e0f2b24968cb75a7064484a09ffe94505bb70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a><span data-ttu-id="915f3-103">Configuration de plusieurs adresses IP virtuelles pour un service cloud</span><span class="sxs-lookup"><span data-stu-id="915f3-103">Configure multiple VIPs for a cloud service</span></span>

<span data-ttu-id="915f3-104">Vous pouvez accéder à des services cloud Azure sur hello Internet public à l’aide d’une adresse IP fournie par Azure.</span><span class="sxs-lookup"><span data-stu-id="915f3-104">You can access Azure cloud services over hello public Internet by using an IP address provided by Azure.</span></span> <span data-ttu-id="915f3-105">Cette adresse IP publique est tooas auxquels une adresse IP virtuelle (adresse IP virtuelle), car il est lié toohello Azure l’équilibrage de charge et hello pas les instances de Machine virtuelle (VM) au sein du service de cloud computing hello.</span><span class="sxs-lookup"><span data-stu-id="915f3-105">This public IP address is referred tooas a VIP (virtual IP) since it is linked toohello Azure load balancer, and not hello Virtual Machine (VM) instances within hello cloud service.</span></span> <span data-ttu-id="915f3-106">Vous pouvez accéder à une instance de machine virtuelle dans un service cloud à l’aide d’une adresse IP virtuelle unique.</span><span class="sxs-lookup"><span data-stu-id="915f3-106">You can access any VM instance within a cloud service by using a single VIP.</span></span>

<span data-ttu-id="915f3-107">Toutefois, il existe des scénarios dans lesquels vous devrez peut-être plusieurs VIP comme un toohello de point d’entrée même service cloud.</span><span class="sxs-lookup"><span data-stu-id="915f3-107">However, there are scenarios in which you may need more than one VIP as an entry point toohello same cloud service.</span></span> <span data-ttu-id="915f3-108">Par exemple, votre service cloud peut héberger plusieurs sites Web qui nécessitent une connectivité SSL à l’aide du port par défaut 443, hello que chaque site est hébergé pour un autre client ou de client.</span><span class="sxs-lookup"><span data-stu-id="915f3-108">For instance, your cloud service may host multiple websites that require SSL connectivity using hello default port of 443, as each site is hosted for a different customer, or tenant.</span></span> <span data-ttu-id="915f3-109">Dans ce scénario, vous devez toohave une autre adresse IP publique pour chaque site Web.</span><span class="sxs-lookup"><span data-stu-id="915f3-109">In this scenario, you need toohave a different public facing IP address for each website.</span></span> <span data-ttu-id="915f3-110">Hello diagramme ci-dessous illustre un hébergement web d’architecture mutualisée classique avec un besoin de certificats SSL multiples sur hello même port public.</span><span class="sxs-lookup"><span data-stu-id="915f3-110">hello diagram below illustrates a typical multi-tenant web hosting with a need for multiple SSL certificates on hello same public port.</span></span>

![Scénario avec plusieurs adresses IP virtuelles SSL](./media/load-balancer-multivip/Figure1.png)

<span data-ttu-id="915f3-112">Dans l’exemple hello ci-dessus, hello d’utiliser toutes les adresses IP virtuelles même port public (443) et le trafic est redirigé tooone ou plus de charge équilibrée de machines virtuelles sur un seul port privé pour hello adresse IP interne du service de cloud hello qui héberge tous les sites Web de hello.</span><span class="sxs-lookup"><span data-stu-id="915f3-112">In hello example above, all VIPs use hello same public port (443) and traffic is redirected tooone or more load balanced VMs on a unique private port for hello internal IP address of hello cloud service hosting all hello websites.</span></span>

> [!NOTE]
> <span data-ttu-id="915f3-113">Une autre situation nécessitant Bonjour utilisez Bonjour plusieurs adresses IP virtuelles héberge plusieurs écouteurs de groupe de disponibilité AlwaysOn de SQL sur le même ensemble d’ordinateurs virtuels de hello.</span><span class="sxs-lookup"><span data-stu-id="915f3-113">Another situation requiring hello use hello multiple VIPs is hosting multiple SQL AlwaysOn availability group listeners on hello same set of Virtual Machines.</span></span>

<span data-ttu-id="915f3-114">Adresses IP virtuelles sont dynamiques par défaut, ce qui signifie que l’adresse IP réelle hello affecté le service de cloud computing toohello peut-être changer au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="915f3-114">VIPs are dynamic by default, which means that hello actual IP address assigned toohello cloud service may change over time.</span></span> <span data-ttu-id="915f3-115">tooprevent que se produise, vous pouvez réserver une adresse IP virtuelle pour votre service.</span><span class="sxs-lookup"><span data-stu-id="915f3-115">tooprevent that from happening, you can reserve a VIP for your service.</span></span> <span data-ttu-id="915f3-116">toolearn en savoir plus sur les adresses IP virtuelles réservées, consultez [adresse IP publique réservée](../virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="915f3-116">toolearn more about reserved VIPs, see [Reserved Public IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span></span>

> [!NOTE]
> <span data-ttu-id="915f3-117">Consultez [Tarification des adresses IP](https://azure.microsoft.com/pricing/details/ip-addresses/) pour plus d’informations sur la tarification des adresses IP virtuelles et réservées.</span><span class="sxs-lookup"><span data-stu-id="915f3-117">Please see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/) for information on pricing on VIPs and reserved IPs.</span></span>

<span data-ttu-id="915f3-118">Vous pouvez utiliser PowerShell tooverify hello utilisés par vos services cloud, les adresses IP virtuelles ainsi ajouter et supprimer des adresses IP virtuelles, associer un point de terminaison tooan VIP et configurer l’équilibrage de charge sur une adresse IP virtuelle spécifique.</span><span class="sxs-lookup"><span data-stu-id="915f3-118">You can use PowerShell tooverify hello VIPs used by your cloud services, as well as add and remove VIPs, associate a VIP tooan endpoint, and configure load balancing on a specific VIP.</span></span>

## <a name="limitations"></a><span data-ttu-id="915f3-119">Limites</span><span class="sxs-lookup"><span data-stu-id="915f3-119">Limitations</span></span>

<span data-ttu-id="915f3-120">À ce stade, les fonctionnalités des adresses IP virtuelles multiples sont toohello limité les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="915f3-120">At this time, Multi VIP functionality is limited toohello following scenarios:</span></span>

* <span data-ttu-id="915f3-121">**IaaS uniquement**.</span><span class="sxs-lookup"><span data-stu-id="915f3-121">**IaaS only**.</span></span> <span data-ttu-id="915f3-122">Vous ne pouvez activer les adresses IP virtuelles multiples que pour les services cloud qui contiennent des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="915f3-122">You can only enable Multi VIP for cloud services that contain VMs.</span></span> <span data-ttu-id="915f3-123">Vous ne pouvez pas utiliser les adresses IP virtuelles multiples dans les scénarios PaaS avec des instances de rôles.</span><span class="sxs-lookup"><span data-stu-id="915f3-123">You cannot use Multi VIP in PaaS scenarios with role instances.</span></span>
* <span data-ttu-id="915f3-124">**PowerShell uniquement**.</span><span class="sxs-lookup"><span data-stu-id="915f3-124">**PowerShell only**.</span></span> <span data-ttu-id="915f3-125">Vous pouvez gérer les adresses IP virtuelles multiples uniquement à l'aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="915f3-125">You can only manage Multi VIP by using PowerShell.</span></span>

<span data-ttu-id="915f3-126">Ces limitations sont temporaires et peuvent changer à tout moment.</span><span class="sxs-lookup"><span data-stu-id="915f3-126">These limitations are temporary, and may change at any time.</span></span> <span data-ttu-id="915f3-127">Modifier la toorevisit que cette page tooverify futures.</span><span class="sxs-lookup"><span data-stu-id="915f3-127">Make sure toorevisit this page tooverify future changes.</span></span>

## <a name="how-tooadd-a-vip-tooa-cloud-service"></a><span data-ttu-id="915f3-128">Service de cloud tooadd une adresse IP virtuelle tooa</span><span class="sxs-lookup"><span data-stu-id="915f3-128">How tooadd a VIP tooa cloud service</span></span>
<span data-ttu-id="915f3-129">service de tooyour tooadd une adresse IP virtuelle, exécutez hello suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="915f3-129">tooadd a VIP tooyour service, run hello following PowerShell command:</span></span>

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

<span data-ttu-id="915f3-130">Cette commande affiche un toohello similaire de résultats suivant l’exemple :</span><span class="sxs-lookup"><span data-stu-id="915f3-130">This command displays a result similar toohello following sample:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-tooremove-a-vip-from-a-cloud-service"></a><span data-ttu-id="915f3-131">Comment tooremove une adresse IP virtuelle à partir d’un service cloud</span><span class="sxs-lookup"><span data-stu-id="915f3-131">How tooremove a VIP from a cloud service</span></span>
<span data-ttu-id="915f3-132">tooremove hello VIP ajouté tooyour service dans l’exemple hello ci-dessus, hello exécution suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="915f3-132">tooremove hello VIP added tooyour service in hello example above, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> <span data-ttu-id="915f3-133">Vous ne pouvez supprimer une adresse IP virtuelle que s’il n’a aucun tooit de points de terminaison associés.</span><span class="sxs-lookup"><span data-stu-id="915f3-133">You can only remove a VIP if it has no endpoints associated tooit.</span></span>


## <a name="how-tooretrieve-vip-information-from-a-cloud-service"></a><span data-ttu-id="915f3-134">Comment les informations tooretrieve adresse IP virtuelle à partir d’un Service Cloud</span><span class="sxs-lookup"><span data-stu-id="915f3-134">How tooretrieve VIP information from a Cloud Service</span></span>
<span data-ttu-id="915f3-135">tooretrieve hello adresses IP virtuelles associés à un service cloud, exécutez hello PowerShell script suivant :</span><span class="sxs-lookup"><span data-stu-id="915f3-135">tooretrieve hello VIPs associated with a cloud service, run hello following PowerShell script:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="915f3-136">script de Hello affiche un toohello similaire de résultats suivant l’exemple :</span><span class="sxs-lookup"><span data-stu-id="915f3-136">hello script displays a result similar toohello following sample:</span></span>

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

<span data-ttu-id="915f3-137">Dans cet exemple, le service de cloud computing hello a 3 VIP :</span><span class="sxs-lookup"><span data-stu-id="915f3-137">In this example, hello cloud service has 3 VIPs:</span></span>

* <span data-ttu-id="915f3-138">**Vip1** est hello l’adresse IP virtuelle par défaut, vous savez que car hello IsDnsProgrammedName a pour valeur tootrue.</span><span class="sxs-lookup"><span data-stu-id="915f3-138">**Vip1** is hello default VIP, you know that because hello value for IsDnsProgrammedName is set tootrue.</span></span>
* <span data-ttu-id="915f3-139">**Vip2** et **Vip3** ne sont pas utilisées étant donné qu’elles n’ont pas d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="915f3-139">**Vip2** and **Vip3** are not used as they do not have any IP addresses.</span></span> <span data-ttu-id="915f3-140">Ils seront uniquement être utilisés si vous associez une adresse IP virtuelle de toohello point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="915f3-140">They will only be used if you associate an endpoint toohello VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="915f3-141">Votre abonnement est uniquement facturé pour les adresses IP virtuelles supplémentaires après leur association à un point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="915f3-141">Your subscription will only be charged for extra VIPs once they are associated with an endpoint.</span></span> <span data-ttu-id="915f3-142">Pour plus d’informations sur la tarification, voir la page [Tarification des adresses IP](https://azure.microsoft.com/pricing/details/ip-addresses/).</span><span class="sxs-lookup"><span data-stu-id="915f3-142">For more information on pricing, see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/).</span></span>

## <a name="how-tooassociate-a-vip-tooan-endpoint"></a><span data-ttu-id="915f3-143">Comment tooassociate une adresse IP virtuelle tooan point de terminaison</span><span class="sxs-lookup"><span data-stu-id="915f3-143">How tooassociate a VIP tooan endpoint</span></span>

<span data-ttu-id="915f3-144">tooassociate une adresse IP virtuelle sur un cloud service tooan point de terminaison, exécutez hello suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="915f3-144">tooassociate a VIP on a cloud service tooan endpoint, run hello following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

<span data-ttu-id="915f3-145">commande Hello crée un point de terminaison toohello lié VIP appelé *Vip2* sur le port *80*et le lie toohello ordinateur virtuel nommé *myVM1* dans un service cloud nommé  *myService* à l’aide de *TCP* sur le port *8080*.</span><span class="sxs-lookup"><span data-stu-id="915f3-145">hello command creates an endpoint linked toohello VIP called *Vip2* on port *80*, and links it toohello VM named *myVM1* in a cloud service named *myService* using *TCP* on port *8080*.</span></span>

<span data-ttu-id="915f3-146">configuration de hello tooverify, exécutez hello suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="915f3-146">tooverify hello configuration, run hello following PowerShell command:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="915f3-147">sortie de Hello semble similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="915f3-147">hello output looks similar toohello following example:</span></span>

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

## <a name="how-tooenable-load-balancing-on-a-specific-vip"></a><span data-ttu-id="915f3-148">Comment tooenable l’équilibrage de charge sur une adresse IP virtuelle spécifique</span><span class="sxs-lookup"><span data-stu-id="915f3-148">How tooenable load balancing on a specific VIP</span></span>

<span data-ttu-id="915f3-149">Vous pouvez associer une adresse IP virtuelle unique à plusieurs machines virtuelles à des fins d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="915f3-149">You can associate a single VIP with multiple virtual machines for load balancing purposes.</span></span> <span data-ttu-id="915f3-150">Par exemple, supposons que vous avez un service cloud nommé *myService*, et deux machines virtuelles nommées *myVM1* et *myVM2*.</span><span class="sxs-lookup"><span data-stu-id="915f3-150">For example, you have a cloud service named *myService*, and two virtual machines named *myVM1* and *myVM2*.</span></span> <span data-ttu-id="915f3-151">Votre service cloud dispose de plusieurs adresses IP virtuelles, dont une nommée *Vip2*.</span><span class="sxs-lookup"><span data-stu-id="915f3-151">And your cloud service has multiple VIPs, one of them named *Vip2*.</span></span> <span data-ttu-id="915f3-152">Si vous souhaitez que tout le trafic tooport de tooensure *81* sur *Vip2* est équilibrée entre *myVM1* et *myVM2* sur le port *8181* , exécutez hello après le script PowerShell :</span><span class="sxs-lookup"><span data-stu-id="915f3-152">If you want tooensure that all traffic tooport *81* on *Vip2* is balanced between *myVM1* and *myVM2* on port *8181*, run hello following PowerShell script:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

<span data-ttu-id="915f3-153">Vous pouvez également mettre à jour votre toouse d’équilibrage de charge une adresse IP virtuelle différente.</span><span class="sxs-lookup"><span data-stu-id="915f3-153">You can also update your load balancer toouse a different VIP.</span></span> <span data-ttu-id="915f3-154">Par exemple, si vous exécutez hello commande PowerShell suivante, vous allez modifier le jeu toouse une adresse IP virtuelle nommée Vip1 d’équilibrage de charge hello :</span><span class="sxs-lookup"><span data-stu-id="915f3-154">For example, if you run hello PowerShell command below, you will change hello load balancing set toouse a VIP named Vip1:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a><span data-ttu-id="915f3-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="915f3-155">Next Steps</span></span>

[<span data-ttu-id="915f3-156">Analyse des journaux d’Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="915f3-156">Log analytics for Azure Load Balance</span></span>](load-balancer-monitor-log.md)

[<span data-ttu-id="915f3-157">Présentation de l’équilibrage de charge accessible sur Internet</span><span class="sxs-lookup"><span data-stu-id="915f3-157">Internet facing load balancer overview</span></span>](load-balancer-internet-overview.md)

[<span data-ttu-id="915f3-158">Prise en main de l’équilibrage de charge accessible sur Internet</span><span class="sxs-lookup"><span data-stu-id="915f3-158">Get started on Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="915f3-159">Présentation du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="915f3-159">Virtual Network Overview</span></span>](../virtual-network/virtual-networks-overview.md)

[<span data-ttu-id="915f3-160">API REST d’adresse IP réservée</span><span class="sxs-lookup"><span data-stu-id="915f3-160">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)
