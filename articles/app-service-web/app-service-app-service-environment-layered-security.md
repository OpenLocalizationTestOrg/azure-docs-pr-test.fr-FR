---
title: "Architecture de sécurité en couche avec les environnements App Service"
description: "Implémentation d’une architecture de sécurité en couche avec les environnements App Service."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 73ce0213-bd3e-4876-b1ed-5ecad4ad5601
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: stefsch
ms.openlocfilehash: 0fb02c13f99a8f4a46e0142c20da3b152c809b6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a><span data-ttu-id="c589c-103">Implémentation d’une architecture de sécurité en couche avec les environnements App Service</span><span class="sxs-lookup"><span data-stu-id="c589c-103">Implementing a Layered Security Architecture with App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="c589c-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="c589c-104">Overview</span></span>
<span data-ttu-id="c589c-105">Dans la mesure où les environnements App Service fournissent un environnement d’exécution isolé déployé dans un réseau virtuel, les développeurs peuvent créer une architecture de sécurité en couche offrant différents niveaux d’accès réseau pour chaque couche application physique.</span><span class="sxs-lookup"><span data-stu-id="c589c-105">Since App Service Environments provide an isolated runtime environment deployed into a virtual network, developers can create a layered security architecture providing differing levels of network access for each physical application tier.</span></span>

<span data-ttu-id="c589c-106">Un souhait commun est de masquer les API principales de l’accès Internet général, et d’autoriser uniquement les API à être appelées par les applications web en amont.</span><span class="sxs-lookup"><span data-stu-id="c589c-106">A common desire is to hide API back-ends from general Internet access, and only allow APIs to be called by upstream web apps.</span></span>  <span data-ttu-id="c589c-107">Les [groupes de sécurité réseau (NSG)][NetworkSecurityGroups] peuvent être utilisés sur des sous-réseaux contenant des environnements App Service pour restreindre l’accès public aux applications API.</span><span class="sxs-lookup"><span data-stu-id="c589c-107">[Network security groups (NSGs)][NetworkSecurityGroups] can be used on subnets containing App Service Environments to restrict public access to API applications.</span></span>

<span data-ttu-id="c589c-108">Le schéma ci-dessous présente un exemple d’architecture avec une application WebAPI déployée dans un environnement App Service.</span><span class="sxs-lookup"><span data-stu-id="c589c-108">The diagram below shows an example architecture with a WebAPI based app deployed on an App Service Environment.</span></span>  <span data-ttu-id="c589c-109">Trois instances d’application web distinctes, déployées sur trois environnements App Service distincts, effectuent des appels principaux à la même application WebAPI.</span><span class="sxs-lookup"><span data-stu-id="c589c-109">Three separate web app instances, deployed on three separate App Service Environments, make back-end calls to the same WebAPI app.</span></span>

![Architecture conceptuelle][ConceptualArchitecture] 

<span data-ttu-id="c589c-111">Les symboles « plus » verts indiquent que le groupe de sécurité réseau sur le sous-réseau contenant « apiase » autorise les appels entrants des applications web en amont, ainsi que les appels internes.</span><span class="sxs-lookup"><span data-stu-id="c589c-111">The green plus signs indicate that the network security group on the subnet containing "apiase" allows inbound calls from the upstream web apps, as well calls from itself.</span></span>  <span data-ttu-id="c589c-112">Toutefois, le même groupe de sécurité réseau refuse explicitement l’accès au trafic entrant général à partir d’Internet.</span><span class="sxs-lookup"><span data-stu-id="c589c-112">However the same network security group explicitly denies access to general inbound traffic from the Internet.</span></span> 

<span data-ttu-id="c589c-113">Le reste de cette rubrique décrit les étapes nécessaires pour configurer le groupe de sécurité réseau sur le sous-réseau contenant « apiase ».</span><span class="sxs-lookup"><span data-stu-id="c589c-113">The remainder of this topic walks through the steps needed to configure the network security group on the subnet containing "apiase".</span></span>

## <a name="determining-the-network-behavior"></a><span data-ttu-id="c589c-114">Détermination du comportement réseau</span><span class="sxs-lookup"><span data-stu-id="c589c-114">Determining the Network Behavior</span></span>
<span data-ttu-id="c589c-115">Pour savoir quelles règles de sécurité réseau sont nécessaires, vous devez déterminer les clients réseau qui seront autorisés à atteindre l’environnement App Service contenant l’application API et les clients qui seront bloqués.</span><span class="sxs-lookup"><span data-stu-id="c589c-115">In order to know what network security rules are needed, you need to determine which network clients will be allowed to reach the App Service Environment containing the API app, and which clients will be blocked.</span></span>

<span data-ttu-id="c589c-116">Étant donné que les [groupes de sécurité réseau (NSG)][NetworkSecurityGroups] sont appliqués aux sous-réseaux et que les environnements App Service sont déployés dans des sous-réseaux, les règles contenues dans un NSG s’appliquent à **toutes** les applications s’exécutant dans un environnement App Service.</span><span class="sxs-lookup"><span data-stu-id="c589c-116">Since [network security groups (NSGs)][NetworkSecurityGroups] are applied to subnets, and App Service Environments are deployed into subnets, the rules contained in an NSG apply to **all** apps running on an App Service Environment.</span></span>  <span data-ttu-id="c589c-117">À l’aide de l’exemple d’architecture de cet article, une fois qu’un groupe de sécurité réseau est appliqué au sous-réseau contenant « apiase », toutes les applications s’exécutant dans l’environnement App Service « apiase » seront protégées par le même ensemble de règles de sécurité.</span><span class="sxs-lookup"><span data-stu-id="c589c-117">Using the sample architecture for this article, once a network security group is applied to the subnet containing "apiase", all apps running on the "apiase" App Service Environment will be protected by the same set of security rules.</span></span> 

* <span data-ttu-id="c589c-118">**Déterminer l’adresse IP sortante des appelants en amont :** quelles sont les adresses IP des appelants en amont ?</span><span class="sxs-lookup"><span data-stu-id="c589c-118">**Determine the outbound IP address of upstream callers:**  What is the IP address or addresses of the upstream callers?</span></span>  <span data-ttu-id="c589c-119">L’accès de ces adresses devra être explicitement autorisé dans le NSG.</span><span class="sxs-lookup"><span data-stu-id="c589c-119">These addresses will need to be explicitly allowed access in the NSG.</span></span>  <span data-ttu-id="c589c-120">Les appels entre les environnements App Service étant considérés comme des appels « Internet », cela signifie que l’accès de l’adresse IP sortante affectée à chacun des trois environnements App Service en amont doit être autorisé dans le NSG pour le sous-réseau « apiase ».</span><span class="sxs-lookup"><span data-stu-id="c589c-120">Since calls between App Service Environments are considered "Internet" calls, this means the outbound IP address assigned to each of the three upstream App Service Environments needs to be allowed access in the NSG for the "apiase" subnet.</span></span>   <span data-ttu-id="c589c-121">Pour plus d’informations sur la détermination de l’adresse IP sortante pour les applications s’exécutant dans un environnement App Service, consultez l’article de présentation [Architecture réseau][NetworkArchitecture].</span><span class="sxs-lookup"><span data-stu-id="c589c-121">For more details on determining the outbound IP address for apps running in an App Service Environment see the [Network Architecture][NetworkArchitecture] Overview article.</span></span>
* <span data-ttu-id="c589c-122">**L’application API principale devra-t-elle s’appeler elle-même ?**</span><span class="sxs-lookup"><span data-stu-id="c589c-122">**Will the back-end API app need to call itself?**</span></span>  <span data-ttu-id="c589c-123">Un point subtil et parfois négligé est le scénario dans lequel l’application principale doit s’appeler elle-même.</span><span class="sxs-lookup"><span data-stu-id="c589c-123">A sometimes overlooked and subtle point is the scenario where the back-end application needs to call itself.</span></span>  <span data-ttu-id="c589c-124">Si une application API principale dans un environnement App Service doit s’appeler elle-même, elle est également traitée comme un appel « Internet ».</span><span class="sxs-lookup"><span data-stu-id="c589c-124">If a back-end API application on an App Service Environment needs to call itself, this is also treated as an "Internet" call.</span></span>  <span data-ttu-id="c589c-125">Dans l’exemple d’architecture, cela nécessite également d’autoriser l’accès à partir de l’adresse IP sortante de l’environnement App Service « apiase ».</span><span class="sxs-lookup"><span data-stu-id="c589c-125">In the sample architecture this requires allowing access from the outbound IP address of the "apiase" App Service Environment as well.</span></span>

## <a name="setting-up-the-network-security-group"></a><span data-ttu-id="c589c-126">Configuration du groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="c589c-126">Setting up the Network Security Group</span></span>
<span data-ttu-id="c589c-127">Une fois que l’ensemble d’adresses IP sortantes est connu, l’étape suivante consiste à créer un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="c589c-127">Once the set of outbound IP addresses are known, the next step is to construct a network security group.</span></span>  <span data-ttu-id="c589c-128">Les groupes de sécurité réseau peuvent être créés pour les réseaux virtuels reposant sur Resource Manager, ainsi que les réseaux virtuels classiques.</span><span class="sxs-lookup"><span data-stu-id="c589c-128">Network security groups can be created for both Resource Manager based virtual networks, as well as classic virtual networks.</span></span>  <span data-ttu-id="c589c-129">Les exemples ci-dessous illustrent la création et la configuration d’un groupe de sécurité réseau sur un réseau virtuel classique à l’aide de Powershell.</span><span class="sxs-lookup"><span data-stu-id="c589c-129">The examples below show creating and configuring an NSG on a classic virtual network using Powershell.</span></span>

<span data-ttu-id="c589c-130">Pour l’exemple d’architecture, les environnements sont situés dans le sud du centre des États-Unis (South Central US), donc un NSG vide est créé dans cette région :</span><span class="sxs-lookup"><span data-stu-id="c589c-130">For the sample architecture, the environments are located in South Central US, so an empty NSG is created in that region:</span></span>

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

<span data-ttu-id="c589c-131">Tout d’abord, une règle d’autorisation explicite est ajoutée pour l’infrastructure de gestion Azure, comme indiqué dans l’article sur le [trafic entrant][InboundTraffic] pour les environnements App Service.</span><span class="sxs-lookup"><span data-stu-id="c589c-131">First an explicit allow rule is added for the Azure management infrastructure as noted in the article on [inbound traffic][InboundTraffic] for App Service Environments.</span></span>

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

<span data-ttu-id="c589c-132">Ensuite, deux règles sont ajoutées pour autoriser les appels HTTP et HTTPS à partir du premier environnement App Service en amont (« fe1ase »).</span><span class="sxs-lookup"><span data-stu-id="c589c-132">Next, two rules are added to allow HTTP and HTTPS calls from the first upstream App Service Environment ("fe1ase").</span></span>

    #Grant access to requests from the first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="c589c-133">Effacez et recommencez pour les deuxième et troisième environnements App Service en amont (« fe2ase » et « fe3ase »).</span><span class="sxs-lookup"><span data-stu-id="c589c-133">Rinse and repeat for the second and third upstream App Service Environments ("fe2ase"and "fe3ase").</span></span>

    #Grant access to requests from the second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access to requests from the third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="c589c-134">Enfin, accordez l’accès à l’adresse IP sortante de l’environnement App Service de l’API principale afin qu’elle puisse s’appeler elle-même.</span><span class="sxs-lookup"><span data-stu-id="c589c-134">Lastly, grant access to the outbound IP address of the back-end API's App Service Environment so that it can call back into itself.</span></span>

    #Allow apps on the apiase environment to call back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="c589c-135">Aucune autre règle de sécurité réseau ne doit être configurée car chaque NSG possède un ensemble de règles par défaut qui bloquent l’accès entrant à partir d’Internet par défaut.</span><span class="sxs-lookup"><span data-stu-id="c589c-135">No other network security rules need to be configured because every NSG has a set of default rules that block inbound access from the Internet by default.</span></span>

<span data-ttu-id="c589c-136">La liste complète des règles du groupe de sécurité réseau est affichée ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c589c-136">The full list of rules in the network security group are shown below.</span></span>  <span data-ttu-id="c589c-137">Notez la façon dont la dernière règle, mise en surbrillance, bloque l’accès entrant de tous les appelants autres que ceux auxquels l’accès a été explicitement accordé.</span><span class="sxs-lookup"><span data-stu-id="c589c-137">Note how the last rule, which is highlighted, blocks inbound access from all callers other than those which have been explicitly granted access.</span></span>

![Configuration de NSG][NSGConfiguration] 

<span data-ttu-id="c589c-139">L’étape finale consiste à appliquer le NSG au sous-réseau qui contient l’environnement App Service « apiase ».</span><span class="sxs-lookup"><span data-stu-id="c589c-139">The final step is to apply the NSG to the subnet that contains the "apiase" App Service Environment.</span></span>  

     #Apply the NSG to the backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

<span data-ttu-id="c589c-140">Avec le NSG appliqué au sous-réseau, seuls les trois environnements App Service en amont et l’environnement App Service contenant l’API principale sont autorisés à appeler dans l’environnement « apiase ».</span><span class="sxs-lookup"><span data-stu-id="c589c-140">With the NSG applied to the subnet, only the three upstream App Service Environments, and the App Service Environment containing the API back-end, are allowed to call into the "apiase" environment.</span></span>

## <a name="additional-links-and-information"></a><span data-ttu-id="c589c-141">Informations et liens supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c589c-141">Additional Links and Information</span></span>
<span data-ttu-id="c589c-142">Tous les articles et procédures concernant les environnements App Service sont disponibles dans le [fichier Lisez-moi des environnements App Service](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="c589c-142">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="c589c-143">Informations sur les [groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="c589c-143">Information about [network security groups](../virtual-network/virtual-networks-nsg.md).</span></span> 

<span data-ttu-id="c589c-144">Présentation des [adresses IP sortantes][NetworkArchitecture] et des environnements App Service.</span><span class="sxs-lookup"><span data-stu-id="c589c-144">Understanding [outbound IP addresses][NetworkArchitecture] and App Service Environments.</span></span>

<span data-ttu-id="c589c-145">[Ports réseau][InboundTraffic] utilisés par les environnements App Service.</span><span class="sxs-lookup"><span data-stu-id="c589c-145">[Network ports][InboundTraffic] used by App Service Environments.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
