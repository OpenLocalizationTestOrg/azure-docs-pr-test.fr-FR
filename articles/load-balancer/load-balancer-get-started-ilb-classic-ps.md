---
title: "aaaCreate Azure interne l’équilibrage de charge - PowerShell classique | Documents Microsoft"
description: "Découvrez comment toocreate un interne l’équilibrage de charge à l’aide de PowerShell dans le modèle de déploiement classique de hello"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 3be93168-3787-45a5-a194-9124fe386493
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 382db80c42ffab09905513019b72e85a4f9dfeff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a><span data-ttu-id="95158-103">Prise en main de la création d’un équilibreur de charge interne (classique) à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="95158-103">Get started creating an internal load balancer (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="95158-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="95158-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="95158-105">interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="95158-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="95158-106">Services cloud</span><span class="sxs-lookup"><span data-stu-id="95158-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="95158-107">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="95158-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="95158-108">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="95158-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="95158-109">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="95158-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="95158-110">Découvrez comment trop[effectuer ces étapes à l’aide du modèle de gestionnaire de ressources hello](load-balancer-get-started-ilb-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="95158-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="95158-111">Créer un jeu d’équilibrage de charge interne pour les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="95158-111">Create an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="95158-112">toocreate un équilibreur de charge interne défini et hello serveurs qui y enverront leur tooit le trafic, vous disposer de toodo hello :</span><span class="sxs-lookup"><span data-stu-id="95158-112">toocreate an internal load balancer set and hello servers that will send their traffic tooit, you have toodo hello following:</span></span>

1. <span data-ttu-id="95158-113">Créer une instance d’interne l’équilibrage de charge qui sera le point de terminaison hello d’entrant trafic toobe équilibrée entre les serveurs hello d’un jeu d’équilibrage de la charge.</span><span class="sxs-lookup"><span data-stu-id="95158-113">Create an instance of Internal Load Balancing that will be hello endpoint of incoming traffic toobe load balanced across hello servers of a load-balanced set.</span></span>
2. <span data-ttu-id="95158-114">Ajoutez les machines virtuelles toohello qui recevront le trafic entrant de hello correspondantes des points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="95158-114">Add endpoints corresponding toohello virtual machines that will be receiving hello incoming traffic.</span></span>
3. <span data-ttu-id="95158-115">Configurez les serveurs hello qui enverront hello trafic toobe à charge équilibrée toosend leur trafic toohello adresse IP virtuelle (VIP) de l’instance d’équilibrage de charge interne hello.</span><span class="sxs-lookup"><span data-stu-id="95158-115">Configure hello servers that will be sending hello traffic toobe load balanced toosend their traffic toohello virtual IP (VIP) address of hello Internal Load Balancing instance.</span></span>

### <a name="step-1-create-an-internal-load-balancing-instance"></a><span data-ttu-id="95158-116">Étape 1 : Créer une instance d’équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="95158-116">Step 1: Create an Internal Load Balancing instance</span></span>

<span data-ttu-id="95158-117">Pour un service cloud existant ou un service cloud déployé dans un réseau virtuel régional, vous pouvez créer une instance de l’équilibrage de charge interne avec hello suivant de commandes Windows PowerShell :</span><span class="sxs-lookup"><span data-stu-id="95158-117">For an existing cloud service or a cloud service deployed under a regional virtual network, you can create an Internal Load Balancing instance with hello following Windows PowerShell commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of hello subnet within your virtual network>"
$IP="<hello IPv4 address toouse on hello subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

<span data-ttu-id="95158-118">Notez que cette utilisation de hello [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) applet de commande Windows PowerShell utilise hello de paramètres defaultprobe.</span><span class="sxs-lookup"><span data-stu-id="95158-118">Note that this use of hello [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) Windows PowerShell cmdlet uses hello DefaultProbe parameter set.</span></span> <span data-ttu-id="95158-119">Pour plus d'informations sur les jeux de paramètres supplémentaires, consultez [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span><span class="sxs-lookup"><span data-stu-id="95158-119">For more information on additional parameter sets, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span></span>

### <a name="step-2-add-endpoints-toohello-internal-load-balancing-instance"></a><span data-ttu-id="95158-120">Étape 2 : Ajouter l’instance d’équilibrage de charge interne toohello points de terminaison</span><span class="sxs-lookup"><span data-stu-id="95158-120">Step 2: Add endpoints toohello Internal Load Balancing instance</span></span>

<span data-ttu-id="95158-121">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="95158-121">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
$lbsetname="lbset"
$prot="tcp"
$locport=1433
$pubport=1433
$ilb="ilbset"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -Lbset $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

### <a name="step-3-configure-your-servers-toosend-their-traffic-toohello-new-internal-load-balancing-endpoint"></a><span data-ttu-id="95158-122">Étape 3 : Configurer votre toosend serveurs leur trafic toohello nouveau équilibrage de charge interne point de terminaison</span><span class="sxs-lookup"><span data-stu-id="95158-122">Step 3: Configure your servers toosend their traffic toohello new Internal Load Balancing endpoint</span></span>

<span data-ttu-id="95158-123">Vous avez trop configurer serveurs hello dont le trafic est continu toobe à charge équilibrée toouse hello nouvelle adresse IP (hello VIP) de hello instance d’équilibrage de charge interne.</span><span class="sxs-lookup"><span data-stu-id="95158-123">You have too configure hello servers whose traffic is going toobe load balanced toouse hello new IP address (hello VIP) of hello Internal Load Balancing instance.</span></span> <span data-ttu-id="95158-124">Il s’agit d’adresse hello sur quel hello équilibrage de charge interne de l’instance écoute.</span><span class="sxs-lookup"><span data-stu-id="95158-124">This is hello address on which hello Internal Load Balancing instance is listening.</span></span> <span data-ttu-id="95158-125">Dans la plupart des cas, vous devez toojust ajouter ou modifier un enregistrement DNS pour hello VIP de l’instance de l’équilibrage de charge interne hello.</span><span class="sxs-lookup"><span data-stu-id="95158-125">In most cases, you need toojust add or modify a DNS record for hello VIP of hello Internal Load Balancing instance.</span></span>

<span data-ttu-id="95158-126">Si vous avez spécifié l’adresse IP de hello lors de la création de hello d’instance d’équilibrage de charge interne hello, vous disposez déjà d’adresses IP virtuelles hello.</span><span class="sxs-lookup"><span data-stu-id="95158-126">If you specified hello IP address during hello creation of hello Internal Load Balancing instance, you already have hello VIP.</span></span> <span data-ttu-id="95158-127">Sinon, vous pouvez voir VIP hello de hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="95158-127">Otherwise, you can see hello VIP from hello following commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="95158-128">toouse ces commandes, renseignez les valeurs hello et remove hello < et >.</span><span class="sxs-lookup"><span data-stu-id="95158-128">toouse these commands, fill in hello values and remove hello < and >.</span></span> <span data-ttu-id="95158-129">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="95158-129">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="95158-130">À partir de l’affichage hello Hello de commande Get-AzureInternalLoadBalancer, notez l’adresse IP de hello et rendre les serveurs tooyour hello les modifications nécessaires ou tooensure d’enregistrements DNS que le trafic est envoyé toohello VIP.</span><span class="sxs-lookup"><span data-stu-id="95158-130">From hello display of hello Get-AzureInternalLoadBalancer command, note hello IP address and make hello necessary changes tooyour servers or DNS records tooensure that traffic gets sent toohello VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="95158-131">plateforme de Microsoft Azure Hello utilise une adresse IPv4 statique routable publiquement pour un éventail de scénarios d’administration.</span><span class="sxs-lookup"><span data-stu-id="95158-131">hello Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="95158-132">adresse IP de Hello est 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="95158-132">hello IP address is 168.63.129.16.</span></span> <span data-ttu-id="95158-133">Cette adresse IP ne doit pas être bloquée par les pare-feu, car cela peut entraîner un comportement inattendu.</span><span class="sxs-lookup"><span data-stu-id="95158-133">This IP address should not be blocked by any firewalls, because it can cause unexpected behavior.</span></span>
> <span data-ttu-id="95158-134">Avec tooAzure égard équilibrage de charge interne, cette adresse IP est utilisée par l’analyse des sondes de l’état d’intégrité de hello charge équilibrage toodetermine hello pour les ordinateurs virtuels dans un jeu d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="95158-134">With respect tooAzure Internal Load Balancing, this IP address is used by monitoring probes from hello load balancer toodetermine hello health state for virtual machines in a load balanced set.</span></span> <span data-ttu-id="95158-135">Si un groupe de sécurité réseau est utilisé toorestrict virtuels trafic tooAzure dans un jeu d’équilibrage de charge en interne ou tooa appliqué sous-réseau de réseau virtuel, assurez-vous qu’une règle de sécurité réseau est ajoutée tooallow trafic à partir de 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="95158-135">If a Network Security Group is used toorestrict traffic tooAzure virtual machines in an internally load-balanced set or is applied tooa Virtual Network Subnet, ensure that a Network Security Rule is added tooallow traffic from 168.63.129.16.</span></span>

## <a name="example-of-internal-load-balancing"></a><span data-ttu-id="95158-136">Exemple d’équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="95158-136">Example of internal load balancing</span></span>

<span data-ttu-id="95158-137">toostep vous guide dans hello des processus de tooend à la fin de la création d’un jeu d’équilibrage de la charge pour les deux exemples de configuration, consultez hello suivants sections.</span><span class="sxs-lookup"><span data-stu-id="95158-137">toostep you through hello end-tooend process of creating a load-balanced set for two example configurations, see hello following sections.</span></span>

### <a name="an-internet-facing-multi-tier-application"></a><span data-ttu-id="95158-138">Une application multi-niveau sur Internet</span><span class="sxs-lookup"><span data-stu-id="95158-138">An Internet facing, multi-tier application</span></span>

<span data-ttu-id="95158-139">Vous souhaitez tooprovide un service de base de données d’équilibrage de charge pour un ensemble de serveurs de web exposés à Internet.</span><span class="sxs-lookup"><span data-stu-id="95158-139">You want tooprovide a load balanced database service for  a set of Internet-facing web servers.</span></span> <span data-ttu-id="95158-140">Les deux ensembles de serveurs sont hébergés dans un seul service cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="95158-140">Both sets of servers are hosted in a single Azure cloud service.</span></span> <span data-ttu-id="95158-141">TooTCP port 1433 du trafic serveur Web doit être réparti entre deux ordinateurs virtuels dans la couche de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="95158-141">Web server traffic tooTCP port 1433 must be distributed among two virtual machines in hello database tier.</span></span> <span data-ttu-id="95158-142">Figure 1 illustre la configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="95158-142">Figure 1 shows hello configuration.</span></span>

![Jeu d’équilibrage de charge interne pour le niveau de base de données hello](./media/load-balancer-internal-getstarted/IC736321.png)

<span data-ttu-id="95158-144">configuration de Hello se compose d’éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="95158-144">hello configuration consists of hello following:</span></span>

* <span data-ttu-id="95158-145">service cloud existant Hello hébergeant des ordinateurs virtuels de hello est nommé mytestcloud.</span><span class="sxs-lookup"><span data-stu-id="95158-145">hello existing cloud service hosting hello virtual machines is named mytestcloud.</span></span>
* <span data-ttu-id="95158-146">deux serveurs de base de données existante Hello sont nommés DB1 et DB2.</span><span class="sxs-lookup"><span data-stu-id="95158-146">hello two existing database servers are named DB1, DB2.</span></span>
* <span data-ttu-id="95158-147">Serveurs Web dans la couche web de hello connectent toohello des serveurs de base de données dans la couche de base de données hello en utilisant l’adresse IP privée de hello.</span><span class="sxs-lookup"><span data-stu-id="95158-147">Web servers in hello web tier connect toohello database servers in hello database tier by using hello private IP address.</span></span> <span data-ttu-id="95158-148">Une autre option est toouse votre propre DNS pour le réseau virtuel de hello et inscrire manuellement un enregistrement A pour le jeu d’équilibrage de charge interne de hello.</span><span class="sxs-lookup"><span data-stu-id="95158-148">Another option is toouse your own DNS for hello virtual network and manually register an A record for hello internal load balancer set.</span></span>

<span data-ttu-id="95158-149">Hello commandes suivantes configurent une nouvelle instance de l’équilibrage de charge interne nommée **ILBset** et ajoutez des machines virtuelles de points de terminaison toohello correspondant des serveurs de base de données toohello deux :</span><span class="sxs-lookup"><span data-stu-id="95158-149">hello following commands configure a new Internal Load Balancing instance named **ILBset** and add endpoints toohello virtual machines corresponding toohello two database servers:</span></span>

```powershell
$svc="mytestcloud"
$ilb="ilbset"
Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb
$prot="tcp"
$locport=1433
$pubport=1433
$epname="TCP-1433-1433"
$lbsetname="lbset"
$vmname="DB1"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM

$epname="TCP-1433-1433-2"
$vmname="DB2"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

## <a name="remove-an-internal-load-balancing-configuration"></a><span data-ttu-id="95158-150">Supprimer une configuration d’équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="95158-150">Remove an Internal Load Balancing configuration</span></span>

<span data-ttu-id="95158-151">tooremove une machine virtuelle comme un point de terminaison à partir d’une instance d’équilibrage de charge interne, hello utilisation suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="95158-151">tooremove a virtual machine as an endpoint from an internal load balancer instance, use hello following commands:</span></span>

```powershell
$svc="<Cloud service name>"
$vmname="<Name of hello VM>"
$epname="<Name of hello endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="95158-152">toouse ces commandes, renseignez les valeurs hello, suppression hello < et >.</span><span class="sxs-lookup"><span data-stu-id="95158-152">toouse these commands, fill in hello values, removing hello < and >.</span></span>

<span data-ttu-id="95158-153">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="95158-153">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="95158-154">tooremove une instance d’équilibrage de charge interne à partir d’un service cloud, hello utilisation suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="95158-154">tooremove an internal load balancer instance from a cloud service, use hello following commands:</span></span>

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

<span data-ttu-id="95158-155">toouse ces commandes, renseignez les valeur hello et supprimer hello < et >.</span><span class="sxs-lookup"><span data-stu-id="95158-155">toouse these commands, fill in hello value and remove hello < and >.</span></span>

<span data-ttu-id="95158-156">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="95158-156">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a><span data-ttu-id="95158-157">Informations supplémentaires sur les applets de commande de l’équilibreur de charge interne</span><span class="sxs-lookup"><span data-stu-id="95158-157">Additional information about internal load balancer cmdlets</span></span>

<span data-ttu-id="95158-158">tooobtain plus d’informations sur l’équilibrage de charge interne applets de commande, exécutez hello suivant de commandes à partir d’une invite Windows PowerShell :</span><span class="sxs-lookup"><span data-stu-id="95158-158">tooobtain additional information about Internal Load Balancing cmdlets, run hello following commands at a Windows PowerShell prompt:</span></span>

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a><span data-ttu-id="95158-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="95158-159">Next steps</span></span>

[<span data-ttu-id="95158-160">Configurer le mode de distribution d’équilibreur de charge à l’aide de l’affinité d’IP source</span><span class="sxs-lookup"><span data-stu-id="95158-160">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="95158-161">Configuration des paramètres de délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="95158-161">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

