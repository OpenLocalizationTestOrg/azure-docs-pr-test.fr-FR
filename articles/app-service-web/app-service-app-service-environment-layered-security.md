---
title: "aaaLayered Architecture de sécurité avec les environnements de Service d’application"
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
ms.openlocfilehash: 0627ba6fa849908506fe62c451c888c147cabc03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a><span data-ttu-id="1d78f-103">Implémentation d’une architecture de sécurité en couche avec les environnements App Service</span><span class="sxs-lookup"><span data-stu-id="1d78f-103">Implementing a Layered Security Architecture with App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="1d78f-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="1d78f-104">Overview</span></span>
<span data-ttu-id="1d78f-105">Dans la mesure où les environnements App Service fournissent un environnement d’exécution isolé déployé dans un réseau virtuel, les développeurs peuvent créer une architecture de sécurité en couche offrant différents niveaux d’accès réseau pour chaque couche application physique.</span><span class="sxs-lookup"><span data-stu-id="1d78f-105">Since App Service Environments provide an isolated runtime environment deployed into a virtual network, developers can create a layered security architecture providing differing levels of network access for each physical application tier.</span></span>

<span data-ttu-id="1d78f-106">Une volonté commune est toohide API principaux à partir d’un accès général à Internet et autoriser uniquement les toobe API appelée par les applications web en amont.</span><span class="sxs-lookup"><span data-stu-id="1d78f-106">A common desire is toohide API back-ends from general Internet access, and only allow APIs toobe called by upstream web apps.</span></span>  <span data-ttu-id="1d78f-107">[Groupes de sécurité (NSG) réseau] [ NetworkSecurityGroups] peut être utilisé sur les sous-réseaux contenant des applications de tooAPI les environnements App Service toorestrict accès public.</span><span class="sxs-lookup"><span data-stu-id="1d78f-107">[Network security groups (NSGs)][NetworkSecurityGroups] can be used on subnets containing App Service Environments toorestrict public access tooAPI applications.</span></span>

<span data-ttu-id="1d78f-108">diagramme de Hello ci-dessous illustre une architecture de l’exemple avec une application en fonction de WebAPI déployée sur un environnement App Service.</span><span class="sxs-lookup"><span data-stu-id="1d78f-108">hello diagram below shows an example architecture with a WebAPI based app deployed on an App Service Environment.</span></span>  <span data-ttu-id="1d78f-109">Trois instances d’application web distinct, déployés sur trois environnements de Service application distincts, rendre principal appelle toohello même WebAPI application.</span><span class="sxs-lookup"><span data-stu-id="1d78f-109">Three separate web app instances, deployed on three separate App Service Environments, make back-end calls toohello same WebAPI app.</span></span>

![Architecture conceptuelle][ConceptualArchitecture] 

<span data-ttu-id="1d78f-111">Hello signes plus verts indiquent que hello le groupe de sécurité réseau sur le sous-réseau hello contenant « apiase » permet à des applications web en amont, les appels entrants à partir de hello en tant qu’appels bien à partir de lui-même.</span><span class="sxs-lookup"><span data-stu-id="1d78f-111">hello green plus signs indicate that hello network security group on hello subnet containing "apiase" allows inbound calls from hello upstream web apps, as well calls from itself.</span></span>  <span data-ttu-id="1d78f-112">Toutefois, hello même groupe de sécurité réseau refuse explicitement l’accès toogeneral le trafic à partir de hello Internet entrant.</span><span class="sxs-lookup"><span data-stu-id="1d78f-112">However hello same network security group explicitly denies access toogeneral inbound traffic from hello Internet.</span></span> 

<span data-ttu-id="1d78f-113">reste Hello de cette rubrique Guide le groupe de sécurité réseau hello étapes nécessaires tooconfigure hello sur sous-réseau hello contenant « apiase ».</span><span class="sxs-lookup"><span data-stu-id="1d78f-113">hello remainder of this topic walks through hello steps needed tooconfigure hello network security group on hello subnet containing "apiase".</span></span>

## <a name="determining-hello-network-behavior"></a><span data-ttu-id="1d78f-114">Hello déterminant le comportement de réseau</span><span class="sxs-lookup"><span data-stu-id="1d78f-114">Determining hello Network Behavior</span></span>
<span data-ttu-id="1d78f-115">Commande tooknow sécurité du réseau les règles sont nécessaires, vous devez toodetermine les clients du réseau peut tooreach hello environnement App Service contenant hello API d’application et les clients qui seront bloqués.</span><span class="sxs-lookup"><span data-stu-id="1d78f-115">In order tooknow what network security rules are needed, you need toodetermine which network clients will be allowed tooreach hello App Service Environment containing hello API app, and which clients will be blocked.</span></span>

<span data-ttu-id="1d78f-116">Étant donné que [réseau des groupes de sécurité (NSG)] [ NetworkSecurityGroups] sont appliqués toosubnets et environnements de Service d’application sont déployés dans des sous-réseaux, les règles de hello contenues dans un groupe de sécurité réseau s’appliquent trop**tous les** applications qui s’exécutent sur un environnement App Service.</span><span class="sxs-lookup"><span data-stu-id="1d78f-116">Since [network security groups (NSGs)][NetworkSecurityGroups] are applied toosubnets, and App Service Environments are deployed into subnets, hello rules contained in an NSG apply too**all** apps running on an App Service Environment.</span></span>  <span data-ttu-id="1d78f-117">Exemple d’architecture hello pour cet article, une fois qu’un groupe de sécurité réseau est sous-réseau toohello appliqué contenant « apiase », toutes les applications qui s’exécutent sur hello » apiase « environnement App Service seront protégé par hello même définir des règles de sécurité.</span><span class="sxs-lookup"><span data-stu-id="1d78f-117">Using hello sample architecture for this article, once a network security group is applied toohello subnet containing "apiase", all apps running on hello "apiase" App Service Environment will be protected by hello same set of security rules.</span></span> 

* <span data-ttu-id="1d78f-118">**Déterminer l’adresse IP sortante de hello des appelants en amont :** What hello IP ou les adresses des appelants en amont de hello ?</span><span class="sxs-lookup"><span data-stu-id="1d78f-118">**Determine hello outbound IP address of upstream callers:**  What is hello IP address or addresses of hello upstream callers?</span></span>  <span data-ttu-id="1d78f-119">Ces adresses devez toobe explicitement autorisé à accéder hello groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="1d78f-119">These addresses will need toobe explicitly allowed access in hello NSG.</span></span>  <span data-ttu-id="1d78f-120">Étant donné que les appels entre les environnements App Service sont considérés comme des appels de « Internet », cela signifie que tooeach hello sortant IP adresse attribuée de hello trois en amont les environnements App Service besoins toobe hello groupe de sécurité réseau pour le sous-réseau de « apiase » hello autorisé à accéder.</span><span class="sxs-lookup"><span data-stu-id="1d78f-120">Since calls between App Service Environments are considered "Internet" calls, this means hello outbound IP address assigned tooeach of hello three upstream App Service Environments needs toobe allowed access in hello NSG for hello "apiase" subnet.</span></span>   <span data-ttu-id="1d78f-121">Pour plus d’informations sur la détermination des adresse IP sortante de hello pour les applications en cours d’exécution dans un environnement App Service voir hello [Architecture réseau] [ NetworkArchitecture] l’article de vue d’ensemble.</span><span class="sxs-lookup"><span data-stu-id="1d78f-121">For more details on determining hello outbound IP address for apps running in an App Service Environment see hello [Network Architecture][NetworkArchitecture] Overview article.</span></span>
* <span data-ttu-id="1d78f-122">**Application d’API hello principal devez toocall lui-même ?**</span><span class="sxs-lookup"><span data-stu-id="1d78f-122">**Will hello back-end API app need toocall itself?**</span></span>  <span data-ttu-id="1d78f-123">Un point de parfois négligé et plus subtil est scénario hello où hello principal application a besoin toocall lui-même.</span><span class="sxs-lookup"><span data-stu-id="1d78f-123">A sometimes overlooked and subtle point is hello scenario where hello back-end application needs toocall itself.</span></span>  <span data-ttu-id="1d78f-124">Si une application API de serveur principal sur un environnement App Service doit toocall proprement dit, il est également traité comme un appel de « Internet ».</span><span class="sxs-lookup"><span data-stu-id="1d78f-124">If a back-end API application on an App Service Environment needs toocall itself, this is also treated as an "Internet" call.</span></span>  <span data-ttu-id="1d78f-125">Dans l’exemple d’architecture hello cela nécessite l’accès de l’adresse IP sortante de hello Hello « apiase « environnement App Service ainsi.</span><span class="sxs-lookup"><span data-stu-id="1d78f-125">In hello sample architecture this requires allowing access from hello outbound IP address of hello "apiase" App Service Environment as well.</span></span>

## <a name="setting-up-hello-network-security-group"></a><span data-ttu-id="1d78f-126">Configuration de hello groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="1d78f-126">Setting up hello Network Security Group</span></span>
<span data-ttu-id="1d78f-127">Une fois la hello de sortant des adresses IP sont connues, étape suivante de hello est tooconstruct un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="1d78f-127">Once hello set of outbound IP addresses are known, hello next step is tooconstruct a network security group.</span></span>  <span data-ttu-id="1d78f-128">Les groupes de sécurité réseau peuvent être créés pour les réseaux virtuels reposant sur Resource Manager, ainsi que les réseaux virtuels classiques.</span><span class="sxs-lookup"><span data-stu-id="1d78f-128">Network security groups can be created for both Resource Manager based virtual networks, as well as classic virtual networks.</span></span>  <span data-ttu-id="1d78f-129">exemples Hello ci-dessous montrent la création et la configuration d’un groupe de sécurité réseau sur un réseau virtuel classique à l’aide de Powershell.</span><span class="sxs-lookup"><span data-stu-id="1d78f-129">hello examples below show creating and configuring an NSG on a classic virtual network using Powershell.</span></span>

<span data-ttu-id="1d78f-130">Pour un exemple d’architecture hello, environnements de hello sont situés dans Amérique du Sud, un groupe de sécurité réseau vide est créé dans cette région :</span><span class="sxs-lookup"><span data-stu-id="1d78f-130">For hello sample architecture, hello environments are located in South Central US, so an empty NSG is created in that region:</span></span>

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

<span data-ttu-id="1d78f-131">D’abord explicite Autoriser la règle est ajoutée pour l’infrastructure de gestion Azure hello comme indiqué dans l’article de hello sur [le trafic entrant] [ InboundTraffic] pour les environnements de Service d’application.</span><span class="sxs-lookup"><span data-stu-id="1d78f-131">First an explicit allow rule is added for hello Azure management infrastructure as noted in hello article on [inbound traffic][InboundTraffic] for App Service Environments.</span></span>

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

<span data-ttu-id="1d78f-132">Ensuite, deux règles sont ajoutées tooallow HTTP et HTTPS des appels à partir de hello première en amont environnement App Service (« fe1ase »).</span><span class="sxs-lookup"><span data-stu-id="1d78f-132">Next, two rules are added tooallow HTTP and HTTPS calls from hello first upstream App Service Environment ("fe1ase").</span></span>

    #Grant access toorequests from hello first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="1d78f-133">Rincer et répétez l’opération pour hello deuxième et troisième en amont App Service environnements (« fe2ase » et « fe3ase »).</span><span class="sxs-lookup"><span data-stu-id="1d78f-133">Rinse and repeat for hello second and third upstream App Service Environments ("fe2ase"and "fe3ase").</span></span>

    #Grant access toorequests from hello second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access toorequests from hello third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="1d78f-134">Enfin, accorder l’accès toohello adresse IP sortante de l’environnement App Service de l’API hello principal afin qu’il peut rappeler dans elle-même.</span><span class="sxs-lookup"><span data-stu-id="1d78f-134">Lastly, grant access toohello outbound IP address of hello back-end API's App Service Environment so that it can call back into itself.</span></span>

    #Allow apps on hello apiase environment toocall back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="1d78f-135">Aucune autre règle de sécurité réseau ne doivent toobe configuré, car chaque groupe de sécurité réseau comporte un ensemble de règles par défaut qui bloquent l’accès entrant à partir de hello Internet par défaut.</span><span class="sxs-lookup"><span data-stu-id="1d78f-135">No other network security rules need toobe configured because every NSG has a set of default rules that block inbound access from hello Internet by default.</span></span>

<span data-ttu-id="1d78f-136">la liste complète des règles dans le groupe de sécurité réseau hello Hello sont indiquées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1d78f-136">hello full list of rules in hello network security group are shown below.</span></span>  <span data-ttu-id="1d78f-137">Notez comment hello dernière règle, qui est mis en surbrillance, bloque l’accès entrant à partir de tous les appelants autres que ceux qui ont été explicitement accordé l’accès.</span><span class="sxs-lookup"><span data-stu-id="1d78f-137">Note how hello last rule, which is highlighted, blocks inbound access from all callers other than those which have been explicitly granted access.</span></span>

![Configuration de NSG][NSGConfiguration] 

<span data-ttu-id="1d78f-139">étape finale de Hello est un sous-réseau de toohello tooapply hello NSG contenant hello » apiase « environnement App Service.</span><span class="sxs-lookup"><span data-stu-id="1d78f-139">hello final step is tooapply hello NSG toohello subnet that contains hello "apiase" App Service Environment.</span></span>  

     #Apply hello NSG toohello backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

<span data-ttu-id="1d78f-140">Avec hello NSG appliqué toohello sous-réseau, seuls hello trois environnements de Service d’application en amont et hello hello contenant d’environnement App Service API back-end, sont autorisés toocall dans l’environnement de « apiase » hello.</span><span class="sxs-lookup"><span data-stu-id="1d78f-140">With hello NSG applied toohello subnet, only hello three upstream App Service Environments, and hello App Service Environment containing hello API back-end, are allowed toocall into hello "apiase" environment.</span></span>

## <a name="additional-links-and-information"></a><span data-ttu-id="1d78f-141">Informations et liens supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1d78f-141">Additional Links and Information</span></span>
<span data-ttu-id="1d78f-142">Tous les articles et comment-de pour les environnements App Service sont disponibles dans hello [fichier Lisezmoi pour les environnements de Service d’Application](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="1d78f-142">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="1d78f-143">Informations sur les [groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="1d78f-143">Information about [network security groups](../virtual-network/virtual-networks-nsg.md).</span></span> 

<span data-ttu-id="1d78f-144">Présentation des [adresses IP sortantes][NetworkArchitecture] et des environnements App Service.</span><span class="sxs-lookup"><span data-stu-id="1d78f-144">Understanding [outbound IP addresses][NetworkArchitecture] and App Service Environments.</span></span>

<span data-ttu-id="1d78f-145">[Ports réseau][InboundTraffic] utilisés par les environnements App Service.</span><span class="sxs-lookup"><span data-stu-id="1d78f-145">[Network ports][InboundTraffic] used by App Service Environments.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
