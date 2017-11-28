---
title: "Connexion sécurisée à des ressources de backend à partir d'un environnement App Service"
description: "Découvrez comment connecter de façon sécurisée des ressources de backend à partir d'un environnement App Service."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: f82eb283-a6e7-4923-a00b-4b4ccf7c4b5b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 0b6d3a47dc429c469b37c2c74f546cfeca580358
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="securely-connecting-to-backend-resources-from-an-app-service-environment"></a><span data-ttu-id="5dc12-103">Connexion sécurisée à des ressources de backend à partir d'un environnement App Service</span><span class="sxs-lookup"><span data-stu-id="5dc12-103">Securely Connecting to Backend Resources from an App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="5dc12-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="5dc12-104">Overview</span></span>
<span data-ttu-id="5dc12-105">Étant donné qu’un environnement App Service est toujours créé **soit** dans un réseau virtuel Azure Resource Manager **ou** un [réseau virtuel][virtualnetwork] de modèle de déploiement classique, les connexions sortantes d’un environnement App Service à destination d’autres ressources de back-end peuvent passer exclusivement sur le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="5dc12-105">Since an App Service Environment is always created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model [virtual network][virtualnetwork], outbound connections from an App Service Environment to other backend resources can flow exclusively over the virtual network.</span></span>  <span data-ttu-id="5dc12-106">Grâce à une modification récente effectuée en juin 2016, les ASE peuvent également être déployés dans les réseaux virtuels qui utilisent soit des plages d’adresses publiques soit des espaces d’adressage RFC1918 (par exemple,</span><span class="sxs-lookup"><span data-stu-id="5dc12-106">With a recent change made in June 2016, ASEs can also be deployed into virtual networks that use either public address ranges, or RFC1918 address spaces (i.e.</span></span> <span data-ttu-id="5dc12-107">des adresses privées).</span><span class="sxs-lookup"><span data-stu-id="5dc12-107">private addresses).</span></span>  

<span data-ttu-id="5dc12-108">Par exemple, un serveur SQL Server peut être en cours d'exécution sur un cluster de machines virtuelles dont le port 1433 est verrouillé.</span><span class="sxs-lookup"><span data-stu-id="5dc12-108">For example, there may be a SQL Server running on a cluster of virtual machines with port 1433 locked down.</span></span>  <span data-ttu-id="5dc12-109">Le point de terminaison peut être placé dans une liste de contrôle d'accès pour autoriser uniquement l'accès à partir d'autres ressources se trouvant sur le même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="5dc12-109">The endpoint may be ACLd to only allow access from other resources on the same virtual network.</span></span>  

<span data-ttu-id="5dc12-110">De même, les points de terminaison sensibles peuvent s'exécuter localement et être connectés à Azure via des connexions [de site à site][SiteToSite] ou [Azure ExpressRoute][ExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="5dc12-110">As another example, sensitive endpoints may run on-premises and be connected to Azure via either [Site-to-Site][SiteToSite] or [Azure ExpressRoute][ExpressRoute] connections.</span></span>  <span data-ttu-id="5dc12-111">Par conséquent, seules les ressources des réseaux virtuels connectés aux tunnels site à site ou ExpressRoute peuvent accéder aux points de terminaison locaux.</span><span class="sxs-lookup"><span data-stu-id="5dc12-111">As a result, only resources in virtual networks connected to the Site-to-Site or ExpressRoute tunnels will be able to access on-premises endpoints.</span></span>

<span data-ttu-id="5dc12-112">Pour tous ces scénarios, les applications s'exécutant dans un environnement App Service peuvent se connecter de façon sécurisée aux différents serveurs et aux différentes ressources.</span><span class="sxs-lookup"><span data-stu-id="5dc12-112">For all of these scenarios, apps running on an App Service Environment will be able to securely connect to the various servers and resources.</span></span>  <span data-ttu-id="5dc12-113">Le trafic sortant à partir d'applications qui s'exécutent dans un environnement App Service vers des points de terminaison privés se trouvant sur le même réseau virtuel (ou connectés au même réseau virtuel) circulent uniquement sur le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="5dc12-113">Outbound traffic from apps running in an App Service Environment to private endpoints in the same virtual network (or connected to the same virtual network), will only flow over the virtual network.</span></span>  <span data-ttu-id="5dc12-114">Le trafic sortant vers des points de terminaison privés ne circule pas via le réseau Internet public.</span><span class="sxs-lookup"><span data-stu-id="5dc12-114">Outbound traffic to private endpoints will not flow over the public Internet.</span></span>

<span data-ttu-id="5dc12-115">L’inconvénient est que le trafic sortant à partir d’un environnement App Service circule vers des points de terminaison se trouvant sur un réseau virtuel .</span><span class="sxs-lookup"><span data-stu-id="5dc12-115">One caveat applies to outbound traffic from an App Service Environment to endpoints within a virtual network.</span></span>  <span data-ttu-id="5dc12-116">Les environnements App Service ne peuvent pas atteindre les points de terminaison de machines virtuelles situées dans le **même** sous-réseau que l'environnement App Service.</span><span class="sxs-lookup"><span data-stu-id="5dc12-116">App Service Environments cannot reach endpoints of virtual machines located in the **same** subnet as the App Service Environment.</span></span>  <span data-ttu-id="5dc12-117">Cela ne devrait normalement pas poser de problème tant que les environnements App Service sont déployés dans un sous-réseau réservé à un usage exclusif par l'environnement App Service.</span><span class="sxs-lookup"><span data-stu-id="5dc12-117">This normally should not be a problem as long as App Service Environments are deployed into a subnet reserved for exclusive use by only the App Service Environment.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a><span data-ttu-id="5dc12-118">Connectivité sortante et configuration DNS requise</span><span class="sxs-lookup"><span data-stu-id="5dc12-118">Outbound Connectivity and DNS Requirements</span></span>
<span data-ttu-id="5dc12-119">Pour qu’un environnement App Service fonctionne correctement, il requiert un accès sortant à différents points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="5dc12-119">For an App Service Environment to function properly, it requires outbound access to various endpoints.</span></span> <span data-ttu-id="5dc12-120">Une liste complète des points de terminaison externes utilisés par un ASE est disponible dans la section « Connectivité réseau requise » de l’article [Configuration réseau pour ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) .</span><span class="sxs-lookup"><span data-stu-id="5dc12-120">A full list of the external endpoints used by an ASE is in the "Required Network Connectivity" section of the [Network Configuration for ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) article.</span></span>

<span data-ttu-id="5dc12-121">Les environnements App Service nécessitent une infrastructure DNS valide configurée pour le réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="5dc12-121">App Service Environments require a valid DNS infrastructure configured for the virtual network.</span></span>  <span data-ttu-id="5dc12-122">Si, pour une raison quelconque, la configuration DNS est modifiée après la création d'un environnement App Service, les développeurs peuvent forcer un environnement App Service à récupérer la nouvelle configuration DNS.</span><span class="sxs-lookup"><span data-stu-id="5dc12-122">If for any reason the DNS configuration is changed after an App Service Environment has been created, developers can force an App Service Environment to pick up the new DNS configuration.</span></span>  <span data-ttu-id="5dc12-123">Le déclenchement d'un redémarrage d'un environnement propagé à l'aide de l'icône « Redémarrer » située en haut du panneau de gestion de l'environnement App Service du portail force l'environnement à récupérer la nouvelle configuration DNS.</span><span class="sxs-lookup"><span data-stu-id="5dc12-123">Triggering a rolling environment reboot using the "Restart" icon located at the top of the App Service Environment management blade in the portal will cause the environment to pick up the new DNS configuration.</span></span>

<span data-ttu-id="5dc12-124">Il est également recommandé de configurer les serveurs DNS personnalisés sur le réseau virtuel à l'avance, avant de créer un environnement App Service.</span><span class="sxs-lookup"><span data-stu-id="5dc12-124">It is also recommended that any custom DNS servers on the vnet be setup ahead of time prior to creating an App Service Environment.</span></span>  <span data-ttu-id="5dc12-125">Si la configuration DNS d'un réseau virtuel est modifiée pendant la création d'un environnement App Service, alors le processus de création de l'environnement App Service échouera.</span><span class="sxs-lookup"><span data-stu-id="5dc12-125">If a virtual network's DNS configuration is changed while an App Service Environment is being created, that will result in the App Service Environment creation process failing.</span></span>  <span data-ttu-id="5dc12-126">De même, s’il existe un serveur DNS personnalisé à l’autre extrémité d’une passerelle VPN et que le serveur DNS n’est pas accessible ou disponible, le processus de création d’un environnement App Service échoue également.</span><span class="sxs-lookup"><span data-stu-id="5dc12-126">In a similar vein, if a custom DNS server exists on the other end of a VPN gateway, and the DNS server is unreachable or unavailable, the App Service Environment creation process will also fail.</span></span>

## <a name="connecting-to-a-sql-server"></a><span data-ttu-id="5dc12-127">Connexion à un serveur SQL Server</span><span class="sxs-lookup"><span data-stu-id="5dc12-127">Connecting to a SQL Server</span></span>
<span data-ttu-id="5dc12-128">Une configuration courante de SQL Server comprend un point de terminaison qui écoute sur le port 1433 :</span><span class="sxs-lookup"><span data-stu-id="5dc12-128">A common SQL Server configuration has an endpoint listening on port 1433:</span></span>

![Point de terminaison de SQL Server][SqlServerEndpoint]

<span data-ttu-id="5dc12-130">Pour limiter le trafic sur ce point de terminaison, vous avez le choix entre deux approches :</span><span class="sxs-lookup"><span data-stu-id="5dc12-130">There are two approaches for restricting traffic to this endpoint:</span></span>

* <span data-ttu-id="5dc12-131">[Listes de contrôle d'accès réseau][NetworkAccessControlLists] (ACL réseau)</span><span class="sxs-lookup"><span data-stu-id="5dc12-131">[Network Access Control Lists][NetworkAccessControlLists] (Network ACLs)</span></span>
* <span data-ttu-id="5dc12-132">[Groupes de sécurité réseau][NetworkSecurityGroups]</span><span class="sxs-lookup"><span data-stu-id="5dc12-132">[Network Security Groups][NetworkSecurityGroups]</span></span>

## <a name="restricting-access-with-a-network-acl"></a><span data-ttu-id="5dc12-133">Restriction de l'accès à l'aide d'une ACL réseau</span><span class="sxs-lookup"><span data-stu-id="5dc12-133">Restricting Access With a Network ACL</span></span>
<span data-ttu-id="5dc12-134">Le port 1433 peut être sécurisé à l'aide d'une liste de contrôle d'accès réseau.</span><span class="sxs-lookup"><span data-stu-id="5dc12-134">Port 1433 can be secured using a network access control list.</span></span>  <span data-ttu-id="5dc12-135">L'exemple ci-dessous place dans une liste approuvée les adresses de clients provenant d'un réseau virtuel, et bloque l'accès à tous les autres clients.</span><span class="sxs-lookup"><span data-stu-id="5dc12-135">The example below whitelists client addresses originating from inside of a virtual network, and blocks access to all other clients.</span></span>

![Exemple de liste de contrôle d'accès réseau][NetworkAccessControlListExample]

<span data-ttu-id="5dc12-137">Toutes les applications s'exécutant dans un environnement App Service du même réseau virtuel que le serveur SQL Server peuvent se connecter à l'instance SQL Server à l'aide de l'adresse IP de **réseau virtuel interne** de la machine virtuelle SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5dc12-137">Any applications running in App Service Environment in the same virtual network as the SQL Server will be able to connect to the SQL Server instance using the **VNet internal** IP address for the SQL Server virtual machine.</span></span>  

<span data-ttu-id="5dc12-138">L'exemple de chaîne de connexion ci-dessous fait référence au serveur SQL Server en utilisant son adresse IP privée.</span><span class="sxs-lookup"><span data-stu-id="5dc12-138">The example connection string below references the SQL Server using its private IP address.</span></span>

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

<span data-ttu-id="5dc12-139">Même si la machine virtuelle possède également un point de terminaison public, les tentatives de connexion à l'aide de l'adresse IP publique sont rejetées en raison de l'ACL réseau.</span><span class="sxs-lookup"><span data-stu-id="5dc12-139">Although the virtual machine has a public endpoint as well, connection attempts using the public IP address will be rejected because of the network ACL.</span></span> 

## <a name="restricting-access-with-a-network-security-group"></a><span data-ttu-id="5dc12-140">Restriction de l'accès à l'aide d'un groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="5dc12-140">Restricting Access With a Network Security Group</span></span>
<span data-ttu-id="5dc12-141">Un groupe de sécurité réseau constitue une autre approche de sécurisation de l'accès.</span><span class="sxs-lookup"><span data-stu-id="5dc12-141">An alternative approach for securing access is with a network security group.</span></span>  <span data-ttu-id="5dc12-142">Les groupes de sécurité réseau peuvent être appliqués à des machines virtuelles individuelles ou à un sous-réseau comprenant des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="5dc12-142">Network security groups can be applied to individual virtual machines, or to a subnet containing virtual machines.</span></span>

<span data-ttu-id="5dc12-143">Un groupe de sécurité réseau doit tout d'abord être créé :</span><span class="sxs-lookup"><span data-stu-id="5dc12-143">First a network security group needs to be created:</span></span>

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

<span data-ttu-id="5dc12-144">Il est très simple de restreindre l'accès exclusivement au trafic d'un réseau virtuel interne à l'aide d'un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="5dc12-144">Restricting access to only VNet internal traffic is very simple with a network security group.</span></span>  <span data-ttu-id="5dc12-145">Les règles par défaut d'un groupe de sécurité réseau autorisent l'accès uniquement à partir d'autres clients réseau du même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="5dc12-145">The default rules in a network security group only allow access from other network clients in the same virtual network.</span></span>

<span data-ttu-id="5dc12-146">Par conséquent, il est aussi simple de verrouiller l'accès à SQL Server que d'appliquer un groupe de sécurité réseau avec ses règles par défaut aux machines virtuelles exécutant SQL Server ou au sous-réseau comprenant des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="5dc12-146">As a result locking down access to SQL Server is as simple as applying a network security group with its default rules to either the virtual machines running SQL Server, or the subnet containing the virtual machines.</span></span>

<span data-ttu-id="5dc12-147">L'exemple ci-dessous applique un groupe de sécurité réseau au sous-réseau conteneur :</span><span class="sxs-lookup"><span data-stu-id="5dc12-147">The sample below applies a network security group to the containing subnet:</span></span>

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

<span data-ttu-id="5dc12-148">Le résultat final est un ensemble de règles de sécurité qui bloquent l'accès externe, tout en autorisant l'accès au réseau virtuel interne :</span><span class="sxs-lookup"><span data-stu-id="5dc12-148">The end result is a set of security rules that block external access, while allowing VNet internal access:</span></span>

![Règles de sécurité réseau par défaut][DefaultNetworkSecurityRules]

## <a name="getting-started"></a><span data-ttu-id="5dc12-150">Prise en main</span><span class="sxs-lookup"><span data-stu-id="5dc12-150">Getting started</span></span>
<span data-ttu-id="5dc12-151">Tous les articles et procédures concernant les environnements App Service sont disponibles dans le [fichier Lisez-moi des environnements App Service](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="5dc12-151">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="5dc12-152">Pour bien démarrer avec les environnements App Service, consultez [Présentation de l’environnement App Service][IntroToAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="5dc12-152">To get started with App Service Environments, see [Introduction to App Service Environment][IntroToAppServiceEnvironment]</span></span>

<span data-ttu-id="5dc12-153">Pour plus d'informations sur le contrôle du trafic entrant vers votre environnement App Service, consultez [Contrôle du trafic entrant vers un environnement App Service][ControlInboundASE]</span><span class="sxs-lookup"><span data-stu-id="5dc12-153">For details around controlling inbound traffic to your App Service Environment, see [Controlling inbound traffic to an App Service Environment][ControlInboundASE]</span></span>

<span data-ttu-id="5dc12-154">Pour plus d’informations sur la plateforme Azure App Service, consultez la rubrique [Azure App Service][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="5dc12-154">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[ControlInboundTraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[NetworkAccessControlLists]: https://azure.microsoft.com/documentation/articles/virtual-networks-acl/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ControlInboundASE]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/ 

<!-- IMAGES -->
[SqlServerEndpoint]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/SqlServerEndpoint01.png
[NetworkAccessControlListExample]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/NetworkAcl01.png
[DefaultNetworkSecurityRules]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/DefaultNetworkSecurityRules01.png 
