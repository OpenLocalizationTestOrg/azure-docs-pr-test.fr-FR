---
title: "aaaSecurely connexion tooBackEnd ressources à partir d’un environnement App Service"
description: "Découvrez comment toosecurely connecter toobackend ressources à partir d’un environnement App Service."
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
ms.openlocfilehash: 6311d3fc301512ea3c4ed8f14f268f75755aa415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="securely-connecting-toobackend-resources-from-an-app-service-environment"></a><span data-ttu-id="6575d-103">En toute sécurité connexion tooBackend ressources à partir d’un environnement App Service</span><span class="sxs-lookup"><span data-stu-id="6575d-103">Securely Connecting tooBackend Resources from an App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="6575d-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="6575d-104">Overview</span></span>
<span data-ttu-id="6575d-105">Dans la mesure où un environnement App Service est toujours créé dans **soit** un réseau virtuel Azure Resource Manager, **ou** un modèle de déploiement classique [réseau virtuel] [ virtualnetwork], exclusivement sur le réseau virtuel de hello peuvent transférer des connexions sortantes depuis une ressources principales du tooother environnement App Service.</span><span class="sxs-lookup"><span data-stu-id="6575d-105">Since an App Service Environment is always created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model [virtual network][virtualnetwork], outbound connections from an App Service Environment tooother backend resources can flow exclusively over hello virtual network.</span></span>  <span data-ttu-id="6575d-106">Suite à une modification récente effectuée en juin 2016, les environnements ASE peuvent également être déployés dans les réseaux virtuels qui utilisent soit des plages d’adresses publiques soit des espaces d’adressage RFC1918 (par exemple, des adresses privées).</span><span class="sxs-lookup"><span data-stu-id="6575d-106">With a recent change made in June 2016, ASEs can also be deployed into virtual networks that use either public address ranges, or RFC1918 address spaces (i.e. private addresses).</span></span>  

<span data-ttu-id="6575d-107">Par exemple, un serveur SQL Server peut être en cours d'exécution sur un cluster de machines virtuelles dont le port 1433 est verrouillé.</span><span class="sxs-lookup"><span data-stu-id="6575d-107">For example, there may be a SQL Server running on a cluster of virtual machines with port 1433 locked down.</span></span>  <span data-ttu-id="6575d-108">point de terminaison Hello peut-être ACLd tooonly autoriser l’accès à d’autres ressources sur hello même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="6575d-108">hello endpoint may be ACLd tooonly allow access from other resources on hello same virtual network.</span></span>  

<span data-ttu-id="6575d-109">Comme autre exemple, des points de terminaison sensibles peuvent exécuter localement et être tooAzure connecté via une [Site-à-Site] [ SiteToSite] ou [Azure ExpressRoute] [ ExpressRoute] connexions.</span><span class="sxs-lookup"><span data-stu-id="6575d-109">As another example, sensitive endpoints may run on-premises and be connected tooAzure via either [Site-to-Site][SiteToSite] or [Azure ExpressRoute][ExpressRoute] connections.</span></span>  <span data-ttu-id="6575d-110">Par conséquent, seules les ressources dans des réseaux virtuels connectés toohello Site à Site ou ExpressRoute tunnels sont tooaccess en mesure de points de terminaison de local.</span><span class="sxs-lookup"><span data-stu-id="6575d-110">As a result, only resources in virtual networks connected toohello Site-to-Site or ExpressRoute tunnels will be able tooaccess on-premises endpoints.</span></span>

<span data-ttu-id="6575d-111">Pour l’ensemble de ces scénarios, les applications s’exécutant sur un environnement App Service être toosecurely en mesure de se connectera toohello divers serveurs et ressources.</span><span class="sxs-lookup"><span data-stu-id="6575d-111">For all of these scenarios, apps running on an App Service Environment will be able toosecurely connect toohello various servers and resources.</span></span>  <span data-ttu-id="6575d-112">Le trafic sortant à partir d’applications qui s’exécutent dans un points de terminaison tooprivate environnement App Service Bonjour même réseau virtuel (ou connecté toohello même réseau virtuel), sera uniquement flux de réseau virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="6575d-112">Outbound traffic from apps running in an App Service Environment tooprivate endpoints in hello same virtual network (or connected toohello same virtual network), will only flow over hello virtual network.</span></span>  <span data-ttu-id="6575d-113">Tooprivate le trafic sortant points de terminaison ne seront pas déborder hello Internet public.</span><span class="sxs-lookup"><span data-stu-id="6575d-113">Outbound traffic tooprivate endpoints will not flow over hello public Internet.</span></span>

<span data-ttu-id="6575d-114">Un inconvénient s’applique toooutbound trafic à partir d’un tooendpoints environnement App Service dans un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="6575d-114">One caveat applies toooutbound traffic from an App Service Environment tooendpoints within a virtual network.</span></span>  <span data-ttu-id="6575d-115">Environnements de Service d’application ne peut pas atteindre les points de terminaison des machines virtuelles situées dans hello **même** sous-réseau hello environnement App Service.</span><span class="sxs-lookup"><span data-stu-id="6575d-115">App Service Environments cannot reach endpoints of virtual machines located in hello **same** subnet as hello App Service Environment.</span></span>  <span data-ttu-id="6575d-116">Cela normalement ne doit pas être un problème tant que les environnements App Service sont déployés dans un sous-réseau réservé pour une utilisation exclusive par uniquement hello environnement App Service.</span><span class="sxs-lookup"><span data-stu-id="6575d-116">This normally should not be a problem as long as App Service Environments are deployed into a subnet reserved for exclusive use by only hello App Service Environment.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a><span data-ttu-id="6575d-117">Connectivité sortante et configuration DNS requise</span><span class="sxs-lookup"><span data-stu-id="6575d-117">Outbound Connectivity and DNS Requirements</span></span>
<span data-ttu-id="6575d-118">Pour une environnement App Service de toofunction correctement, il requiert points de terminaison de toovarious un accès sortant.</span><span class="sxs-lookup"><span data-stu-id="6575d-118">For an App Service Environment toofunction properly, it requires outbound access toovarious endpoints.</span></span> <span data-ttu-id="6575d-119">Une liste complète des points de terminaison externes hello utilisé par un environnement app service est Bonjour section « Connectivité de réseau requis » Hello [Configuration du réseau pour ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) l’article.</span><span class="sxs-lookup"><span data-stu-id="6575d-119">A full list of hello external endpoints used by an ASE is in hello "Required Network Connectivity" section of hello [Network Configuration for ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) article.</span></span>

<span data-ttu-id="6575d-120">Les environnements App Service nécessitent une infrastructure DNS valide configurée pour le réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="6575d-120">App Service Environments require a valid DNS infrastructure configured for hello virtual network.</span></span>  <span data-ttu-id="6575d-121">Si pour n’importe quel hello raison configuration DNS est modifiée après la création d’un environnement App Service, les développeurs peuvent forcer un toopick environnement App Service de configuration DNS de la nouvelle hello.</span><span class="sxs-lookup"><span data-stu-id="6575d-121">If for any reason hello DNS configuration is changed after an App Service Environment has been created, developers can force an App Service Environment toopick up hello new DNS configuration.</span></span>  <span data-ttu-id="6575d-122">Déclenchement d’un redémarrage environnement propagée à l’aide d’icône « Redémarrer » hello en haut hello Hello environnement App Service blade de gestion dans le portail de hello entraîne toopick d’environnement hello nouvelle configuration de DNS hello.</span><span class="sxs-lookup"><span data-stu-id="6575d-122">Triggering a rolling environment reboot using hello "Restart" icon located at hello top of hello App Service Environment management blade in hello portal will cause hello environment toopick up hello new DNS configuration.</span></span>

<span data-ttu-id="6575d-123">Il est également recommandé que tous les serveurs DNS personnalisés sur le réseau virtuel de hello être configuré à l’avance toocreating de temps préalable un environnement App Service.</span><span class="sxs-lookup"><span data-stu-id="6575d-123">It is also recommended that any custom DNS servers on hello vnet be setup ahead of time prior toocreating an App Service Environment.</span></span>  <span data-ttu-id="6575d-124">Si la configuration de DNS d’un réseau virtuel est modifiée pendant la création d’un environnement App Service, qui entraîne au basculement de processus de création d’environnement App Service hello.</span><span class="sxs-lookup"><span data-stu-id="6575d-124">If a virtual network's DNS configuration is changed while an App Service Environment is being created, that will result in hello App Service Environment creation process failing.</span></span>  <span data-ttu-id="6575d-125">De la même manière, si un serveur DNS personnalisé existe sur hello autre extrémité d’une passerelle VPN et le serveur DNS de hello est inaccessible ou indisponible, hello environnement App Service processus de création échoue également.</span><span class="sxs-lookup"><span data-stu-id="6575d-125">In a similar vein, if a custom DNS server exists on hello other end of a VPN gateway, and hello DNS server is unreachable or unavailable, hello App Service Environment creation process will also fail.</span></span>

## <a name="connecting-tooa-sql-server"></a><span data-ttu-id="6575d-126">Tooa de connexion SQL Server</span><span class="sxs-lookup"><span data-stu-id="6575d-126">Connecting tooa SQL Server</span></span>
<span data-ttu-id="6575d-127">Une configuration courante de SQL Server comprend un point de terminaison qui écoute sur le port 1433 :</span><span class="sxs-lookup"><span data-stu-id="6575d-127">A common SQL Server configuration has an endpoint listening on port 1433:</span></span>

![Point de terminaison de SQL Server][SqlServerEndpoint]

<span data-ttu-id="6575d-129">Il existe deux approches pour restreindre le point de terminaison toothis le trafic :</span><span class="sxs-lookup"><span data-stu-id="6575d-129">There are two approaches for restricting traffic toothis endpoint:</span></span>

* <span data-ttu-id="6575d-130">[Listes de contrôle d'accès réseau][NetworkAccessControlLists] (ACL réseau)</span><span class="sxs-lookup"><span data-stu-id="6575d-130">[Network Access Control Lists][NetworkAccessControlLists] (Network ACLs)</span></span>
* <span data-ttu-id="6575d-131">[Groupes de sécurité réseau][NetworkSecurityGroups]</span><span class="sxs-lookup"><span data-stu-id="6575d-131">[Network Security Groups][NetworkSecurityGroups]</span></span>

## <a name="restricting-access-with-a-network-acl"></a><span data-ttu-id="6575d-132">Restriction de l'accès à l'aide d'une ACL réseau</span><span class="sxs-lookup"><span data-stu-id="6575d-132">Restricting Access With a Network ACL</span></span>
<span data-ttu-id="6575d-133">Le port 1433 peut être sécurisé à l'aide d'une liste de contrôle d'accès réseau.</span><span class="sxs-lookup"><span data-stu-id="6575d-133">Port 1433 can be secured using a network access control list.</span></span>  <span data-ttu-id="6575d-134">exemple Hello ci-dessous d’autorisation client résout provenant à l’intérieur d’un réseau virtuel, et bloque l’accès tooall autres clients.</span><span class="sxs-lookup"><span data-stu-id="6575d-134">hello example below whitelists client addresses originating from inside of a virtual network, and blocks access tooall other clients.</span></span>

![Exemple de liste de contrôle d'accès réseau][NetworkAccessControlListExample]

<span data-ttu-id="6575d-136">Toutes les applications en cours d’exécution dans l’environnement App Service dans hello même réseau virtuel hello SQL Server sera l’instance de SQL Server en mesure de tooconnect toohello à l’aide de hello **réseau virtuel interne** adresse IP pour la machine virtuelle de SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="6575d-136">Any applications running in App Service Environment in hello same virtual network as hello SQL Server will be able tooconnect toohello SQL Server instance using hello **VNet internal** IP address for hello SQL Server virtual machine.</span></span>  

<span data-ttu-id="6575d-137">chaîne de connexion exemple Hello ci-dessous références hello SQL Server à l’aide de son adresse IP privée.</span><span class="sxs-lookup"><span data-stu-id="6575d-137">hello example connection string below references hello SQL Server using its private IP address.</span></span>

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

<span data-ttu-id="6575d-138">Bien que la machine virtuelle de hello a également un point de terminaison public, des tentatives de connexion à l’aide de l’adresse IP hello seront rejetées en raison de réseau de hello ACL.</span><span class="sxs-lookup"><span data-stu-id="6575d-138">Although hello virtual machine has a public endpoint as well, connection attempts using hello public IP address will be rejected because of hello network ACL.</span></span> 

## <a name="restricting-access-with-a-network-security-group"></a><span data-ttu-id="6575d-139">Restriction de l'accès à l'aide d'un groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="6575d-139">Restricting Access With a Network Security Group</span></span>
<span data-ttu-id="6575d-140">Un groupe de sécurité réseau constitue une autre approche de sécurisation de l'accès.</span><span class="sxs-lookup"><span data-stu-id="6575d-140">An alternative approach for securing access is with a network security group.</span></span>  <span data-ttu-id="6575d-141">Groupes de sécurité réseau peuvent être appliqué tooindividual virtuels, ou un sous-réseau tooa contenant des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="6575d-141">Network security groups can be applied tooindividual virtual machines, or tooa subnet containing virtual machines.</span></span>

<span data-ttu-id="6575d-142">Tout d’abord un groupe de sécurité réseau doit toobe créé :</span><span class="sxs-lookup"><span data-stu-id="6575d-142">First a network security group needs toobe created:</span></span>

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

<span data-ttu-id="6575d-143">Restreindre l’accès tooonly le trafic de réseau virtuel interne est très simple avec un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="6575d-143">Restricting access tooonly VNet internal traffic is very simple with a network security group.</span></span>  <span data-ttu-id="6575d-144">règles par défaut de Hello dans un groupe de sécurité réseau autoriser uniquement l’accès à partir d’autres clients du réseau Bonjour même réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="6575d-144">hello default rules in a network security group only allow access from other network clients in hello same virtual network.</span></span>

<span data-ttu-id="6575d-145">Par conséquent verrouillage tooSQL d’accès serveur est aussi simple que l’application d’un groupe de sécurité réseau avec ses ordinateurs virtuels par défaut règles tooeither hello exécutant SQL Server, ou un sous-réseau hello contenant des machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="6575d-145">As a result locking down access tooSQL Server is as simple as applying a network security group with its default rules tooeither hello virtual machines running SQL Server, or hello subnet containing hello virtual machines.</span></span>

<span data-ttu-id="6575d-146">exemple Hello ci-dessous s’applique à un sous-réseau toohello conteneur groupe de sécurité réseau :</span><span class="sxs-lookup"><span data-stu-id="6575d-146">hello sample below applies a network security group toohello containing subnet:</span></span>

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

<span data-ttu-id="6575d-147">résultat final de Hello est un ensemble de règles de sécurité qui bloquent l’accès externe, tout en autorisant un accès réseau virtuel interne :</span><span class="sxs-lookup"><span data-stu-id="6575d-147">hello end result is a set of security rules that block external access, while allowing VNet internal access:</span></span>

![Règles de sécurité réseau par défaut][DefaultNetworkSecurityRules]

## <a name="getting-started"></a><span data-ttu-id="6575d-149">Prise en main</span><span class="sxs-lookup"><span data-stu-id="6575d-149">Getting started</span></span>
<span data-ttu-id="6575d-150">Tous les articles et comment-de pour les environnements App Service sont disponibles dans hello [fichier Lisezmoi pour les environnements de Service d’Application](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="6575d-150">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="6575d-151">tooget démarré avec les environnements de Service d’application, consultez [Introduction tooApp environnement de Service][IntroToAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="6575d-151">tooget started with App Service Environments, see [Introduction tooApp Service Environment][IntroToAppServiceEnvironment]</span></span>

<span data-ttu-id="6575d-152">Pour plus d’informations sur le contrôle du trafic entrant tooyour environnement App Service, consultez [contrôler le trafic entrant tooan environnement App Service][ControlInboundASE]</span><span class="sxs-lookup"><span data-stu-id="6575d-152">For details around controlling inbound traffic tooyour App Service Environment, see [Controlling inbound traffic tooan App Service Environment][ControlInboundASE]</span></span>

<span data-ttu-id="6575d-153">Pour plus d’informations sur la plateforme Azure App Service de hello, consultez [Azure App Service][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="6575d-153">For more information about hello Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

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
