---
title: "aaaDMZ exemple – créer un réseau de périmètre tooProtect réseaux avec un pare-feu, UDR et groupe de sécurité réseau | Documents Microsoft"
description: "Créer un réseau de périmètre avec un pare-feu, un itinéraire défini par l’utilisateur (UDR) et des groupes de sécurité réseau (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: dc01ccfb-27b0-4887-8f0b-2792f770ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: cc121f9cd5fe3c3e9ac2c70fbb7d982a80bb345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="example-3--build-a-dmz-tooprotect-networks-with-a-firewall-udr-and-nsg"></a><span data-ttu-id="ded98-103">Exemple 3 : créer un réseau de périmètre tooProtect réseaux avec un pare-feu, UDR et groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="ded98-103">Example 3 – Build a DMZ tooProtect Networks with a Firewall, UDR, and NSG</span></span>
<span data-ttu-id="ded98-104">[Retour toohello Page meilleures pratiques de sécurité limite][HOME]</span><span class="sxs-lookup"><span data-stu-id="ded98-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="ded98-105">Cet exemple va créer un réseau de périmètre avec un pare-feu, quatre serveurs Windows, Routage défini par l’utilisateur (UDR), Transfert IP et groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="ded98-105">This example will create a DMZ with a firewall, four windows servers, User Defined Routing, IP Forwarding, and Network Security Groups.</span></span> <span data-ttu-id="ded98-106">Il vous guide également dans chacun des hello des commandes tooprovide une meilleure compréhension de chaque étape.</span><span class="sxs-lookup"><span data-stu-id="ded98-106">It will also walk through each of hello relevant commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="ded98-107">Il existe également un scénario de trafic section tooprovide un détaillées étape par étape comment le trafic passe par le biais des couches de défense dans hello hello réseau de périmètre.</span><span class="sxs-lookup"><span data-stu-id="ded98-107">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="ded98-108">Enfin, dans la section des références hello est code complet de hello et instruction toobuild cette tootest d’environnement et de faire des essais avec différents scénarios.</span><span class="sxs-lookup"><span data-stu-id="ded98-108">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="ded98-109">![Zone DMZ bidirectionnelle avec NVA, NSG et UDR][1]</span><span class="sxs-lookup"><span data-stu-id="ded98-109">![Bi-directional DMZ with NVA, NSG, and UDR][1]</span></span>

## <a name="environment-setup"></a><span data-ttu-id="ded98-110">Configuration de l’environnement</span><span class="sxs-lookup"><span data-stu-id="ded98-110">Environment Setup</span></span>
<span data-ttu-id="ded98-111">Dans cet exemple, il existe un abonnement qui contient les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="ded98-111">In this example there is a subscription that contains hello following:</span></span>

* <span data-ttu-id="ded98-112">Trois services cloud : « SecSvc001 », « FrontEnd001 » et « BackEnd001 »</span><span class="sxs-lookup"><span data-stu-id="ded98-112">Three cloud services: “SecSvc001”, “FrontEnd001”, and “BackEnd001”</span></span>
* <span data-ttu-id="ded98-113">Un réseau virtuel « CorpNetwork », avec trois sous-réseaux : « SecNet », « FrontEnd » et « BackEnd »</span><span class="sxs-lookup"><span data-stu-id="ded98-113">A Virtual Network “CorpNetwork”, with three subnets: “SecNet”, “FrontEnd”, and “BackEnd”</span></span>
* <span data-ttu-id="ded98-114">Un réseau virtuel, dans cet exemple, un pare-feu, connecté toohello SecNet sous-réseau</span><span class="sxs-lookup"><span data-stu-id="ded98-114">A network virtual appliance, in this example a firewall, connected toohello SecNet subnet</span></span>
* <span data-ttu-id="ded98-115">un serveur Windows Server représentant un serveur web d’application (« IIS01 »),</span><span class="sxs-lookup"><span data-stu-id="ded98-115">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="ded98-116">Deux serveurs Windows Server qui représentent les serveurs principaux d’applications (« AppVM01 », « AppVM02 »)</span><span class="sxs-lookup"><span data-stu-id="ded98-116">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="ded98-117">Un serveur Windows Server qui représente un serveur DNS (« DNS01 »),</span><span class="sxs-lookup"><span data-stu-id="ded98-117">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="ded98-118">Dans la section des références hello ci-dessous, il existe un script PowerShell qui générera la plupart des environnement hello décrite ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="ded98-118">In hello references section below there is a PowerShell script that will build most of hello environment described above.</span></span> <span data-ttu-id="ded98-119">Machines virtuelles de génération hello et réseaux virtuels, bien que s’effectuent par le script d’exemple hello, ne sont pas décrits en détail dans ce document.</span><span class="sxs-lookup"><span data-stu-id="ded98-119">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span>

<span data-ttu-id="ded98-120">environnement de hello toobuild :</span><span class="sxs-lookup"><span data-stu-id="ded98-120">toobuild hello environment:</span></span>

1. <span data-ttu-id="ded98-121">Fichier hello réseau config xml figurant dans la section de références hello (mis à jour avec les noms, l’emplacement et scénario de hello donné toomatch IP adresses)</span><span class="sxs-lookup"><span data-stu-id="ded98-121">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="ded98-122">Variables utilisateur hello script toomatch hello environnement hello de script de mise à jour hello est toobe exécutée (abonnements, les noms de service, etc.)</span><span class="sxs-lookup"><span data-stu-id="ded98-122">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="ded98-123">Exécutez le script de hello dans PowerShell</span><span class="sxs-lookup"><span data-stu-id="ded98-123">Execute hello script in PowerShell</span></span>

<span data-ttu-id="ded98-124">**Remarque**: région hello signifiée Bonjour script PowerShell doit correspondre à la région hello signifiée dans le fichier xml de configuration de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-124">**Note**: hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>

<span data-ttu-id="ded98-125">Une fois hello script s’exécute correctement fallu hello postérieur au script comme suit :</span><span class="sxs-lookup"><span data-stu-id="ded98-125">Once hello script runs successfully hello following post-script steps may be taken:</span></span>

1. <span data-ttu-id="ded98-126">Configurez des règles de pare-feu hello, celle-ci est décrite dans la section hello ci-dessous intitulée : Description de règle de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="ded98-126">Set up hello firewall rules, this is covered in hello section below titled: Firewall Rule Description.</span></span>
2. <span data-ttu-id="ded98-127">Si vous le souhaitez dans la section des références de hello sont deux tooset de scripts de serveur web de hello et le serveur d’applications à un tooallow d’application web simple test avec cette configuration de réseau de périmètre.</span><span class="sxs-lookup"><span data-stu-id="ded98-127">Optionally in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="ded98-128">Une fois hello script s’exécute correctement les règles de pare-feu hello devez toobe terminée, celle-ci est décrite dans la section hello intitulée : règles de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="ded98-128">Once hello script runs successfully hello firewall rules will need toobe completed, this is covered in hello section titled: Firewall Rules.</span></span>

## <a name="user-defined-routing-udr"></a><span data-ttu-id="ded98-129">Itinéraire défini par l’utilisateur (UDR)</span><span class="sxs-lookup"><span data-stu-id="ded98-129">User Defined Routing (UDR)</span></span>
<span data-ttu-id="ded98-130">Par défaut, hello suivant les itinéraires du système est définie en tant que :</span><span class="sxs-lookup"><span data-stu-id="ded98-130">By default, hello following system routes are defined as:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

<span data-ttu-id="ded98-131">Hello VNETLocal est toujours des préfixes d’adresse hello défini de hello réseau virtuel pour ce réseau spécifique (c.-à-d. qu’il ne pourra tooVNet de réseau virtuel en fonction de la façon dont chaque réseau virtuel spécifique est définie).</span><span class="sxs-lookup"><span data-stu-id="ded98-131">hello VNETLocal is always hello defined address prefix(es) of hello VNet for that specific network (ie it will change from VNet tooVNet depending on how each specific VNet is defined).</span></span> <span data-ttu-id="ded98-132">les itinéraires système restantes Hello sont statiques et par défaut comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="ded98-132">hello remaining system routes are static and default as above.</span></span>

<span data-ttu-id="ded98-133">Comme pour la priorité, les itinéraires sont traités via la méthode de correspondance de préfixe plus longue (locales) hello, ainsi hello itinéraire plus spécifique dans la table de hello appliquerait tooa adresse de destination donnée.</span><span class="sxs-lookup"><span data-stu-id="ded98-133">As for priority, routes are processed via hello Longest Prefix Match (LPM) method, thus hello most specific route in hello table would apply tooa given destination address.</span></span>

<span data-ttu-id="ded98-134">Par conséquent, le trafic du (par exemple serveur toohello DNS01, 10.0.2.4) pour le réseau local de hello (10.0.0.0/16) serait routé sur la destination de tooits hello réseau virtuel en raison de l’itinéraire de 10.0.0.0/16 toohello.</span><span class="sxs-lookup"><span data-stu-id="ded98-134">Therefore, traffic (for example toohello DNS01 server, 10.0.2.4) intended for hello local network (10.0.0.0/16) would be routed across hello VNet tooits destination due toohello 10.0.0.0/16 route.</span></span> <span data-ttu-id="ded98-135">En d’autres termes, pour 10.0.2.4, hello 10.0.0.0/16 itinéraire est hello plus spécifique, bien que 0.0.0.0/0 et hello 10.0.0.0/8 pourraient s’appliquent également, mais dans la mesure où elles sont moins spécifiques qu’ils n’affectent pas ce trafic.</span><span class="sxs-lookup"><span data-stu-id="ded98-135">In other words, for 10.0.2.4, hello 10.0.0.0/16 route is hello most specific route, even though hello 10.0.0.0/8 and 0.0.0.0/0 also could apply, but since they are less specific they don’t affect this traffic.</span></span> <span data-ttu-id="ded98-136">Par conséquent, hello trafic too10.0.2.4 aurait un saut suivant de hello réseau virtuel local et transmettre simplement toohello destination.</span><span class="sxs-lookup"><span data-stu-id="ded98-136">Thus hello traffic too10.0.2.4 would have a next hop of hello local VNet and simply route toohello destination.</span></span>

<span data-ttu-id="ded98-137">Si le trafic a été conçu pour 10.1.1.1, par exemple, itinéraire de 10.0.0.0/16 hello semblent ne s’appliquent pas, mais hello 10.0.0.0/8 serait hello plus spécifique, et ce trafic hello serait supprimé (« dipositif noir »), car le saut suivant de hello est Null.</span><span class="sxs-lookup"><span data-stu-id="ded98-137">If traffic was intended for 10.1.1.1 for example, hello 10.0.0.0/16 route wouldn’t apply, but hello 10.0.0.0/8 would be hello most specific, and this hello traffic would be dropped (“black holed”) since hello next hop is Null.</span></span> 

<span data-ttu-id="ded98-138">Si destination de hello n’avez pas appliqué tooany de préfixes d’espaces Null hello ou les préfixes VNETLocal hello, puis suivez les hello moins spécifique Router, 0.0.0.0/0 et être acheminée toohello Internet en tant que tronçon suivant de hello et donc à bord d’internet d’Azure.</span><span class="sxs-lookup"><span data-stu-id="ded98-138">If hello destination didn’t apply tooany of hello Null prefixes or hello VNETLocal prefixes, then it would follow hello least specific route, 0.0.0.0/0 and be routed out toohello Internet as hello next hop and thus out Azure’s internet edge.</span></span>

<span data-ttu-id="ded98-139">S’il existe deux préfixes identiques dans la table d’itinéraires hello, hello Voici hello ordre de préférence basé sur l’attribut de « source » itinéraires hello :</span><span class="sxs-lookup"><span data-stu-id="ded98-139">If there are two identical prefixes in hello route table, hello following is hello order of preference based on hello routes “source” attribute:</span></span>

1. <span data-ttu-id="ded98-140">« VirtualAppliance » = une toohello ajoutés manuellement la table défini par l’utilisateur un itinéraire</span><span class="sxs-lookup"><span data-stu-id="ded98-140">"VirtualAppliance" = A User Defined Route manually added toohello table</span></span>
2. <span data-ttu-id="ded98-141">« VPNGateway » = un itinéraire dynamique BGP (Border lorsqu’il est utilisé avec les réseaux hybrides), ajouté par un protocole réseau dynamique, ces itinéraires peuvent changer au fil du temps comme protocole dynamique de hello reflète automatiquement les modifications dans les ressources réseau</span><span class="sxs-lookup"><span data-stu-id="ded98-141">“VPNGateway” = A Dynamic Route (BGP when used with hybrid networks), added by a dynamic network protocol, these routes may change over time as hello dynamic protocol automatically reflects changes in peered network</span></span>
3. <span data-ttu-id="ded98-142">« Default » = hello système itinéraires, hello entrées statiques hello et de réseau virtuel locales, comme indiqué dans la table d’itinéraires hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="ded98-142">“Default” = hello System Routes, hello local VNet and hello static entries as shown in hello route table above.</span></span>

> [!NOTE]
> <span data-ttu-id="ded98-143">Vous pouvez maintenant utiliser le routage défini par utilisateur (UDR) avec tooforce ExpressRoute et les passerelles VPN sortante et entrantes entre différents locaux trafic appliance virtuelle toobe tooa routé réseau (NVA).</span><span class="sxs-lookup"><span data-stu-id="ded98-143">You can now use User Defined Routing (UDR) with ExpressRoute and VPN Gateways tooforce outbound and inbound cross-premises traffic toobe routed tooa network virtual appliance (NVA).</span></span>
> 
> 

#### <a name="creating-hello-local-routes"></a><span data-ttu-id="ded98-144">Création d’itinéraires locaux hello</span><span class="sxs-lookup"><span data-stu-id="ded98-144">Creating hello local routes</span></span>
<span data-ttu-id="ded98-145">Dans cet exemple, deux tables de routage sont nécessaires, un pour chacun des sous-réseaux de frontales et principales hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-145">In this example, two routing tables are needed, one each for hello Frontend and Backend subnets.</span></span> <span data-ttu-id="ded98-146">Chaque table est chargée avec des itinéraires statiques appropriés pour hello donné de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="ded98-146">Each table is loaded with static routes appropriate for hello given subnet.</span></span> <span data-ttu-id="ded98-147">Pour les besoins de hello de cet exemple, chaque table possède trois itinéraires :</span><span class="sxs-lookup"><span data-stu-id="ded98-147">For hello purpose of this example, each table has three routes:</span></span>

1. <span data-ttu-id="ded98-148">Trafic de sous-réseau local sans tronçon suivant défini tooallow sous-réseau local du trafic toobypass hello pare-feu</span><span class="sxs-lookup"><span data-stu-id="ded98-148">Local subnet traffic with no Next Hop defined tooallow local subnet traffic toobypass hello firewall</span></span>
2. <span data-ttu-id="ded98-149">Le trafic réseau virtuel avec un tronçon suivant défini en tant que pare-feu, cette règle par défaut hello permettant directement tooroute de trafic de réseau virtuel local est ignoré</span><span class="sxs-lookup"><span data-stu-id="ded98-149">Virtual Network traffic with a Next Hop defined as firewall, this overrides hello default rule that allows local VNet traffic tooroute directly</span></span>
3. <span data-ttu-id="ded98-150">Trafic de tous les autres (0/0) avec un tronçon suivant défini comme hello pare-feu</span><span class="sxs-lookup"><span data-stu-id="ded98-150">All remaining traffic (0/0) with a Next Hop defined as hello firewall</span></span>

<span data-ttu-id="ded98-151">Après avoir créé les tables de routage hello, elles sont liées tootheir sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="ded98-151">Once hello routing tables are created they are bound tootheir subnets.</span></span> <span data-ttu-id="ded98-152">Pour la table routage hello frontal sous-réseau, une fois créé et lié toohello sous-réseau doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="ded98-152">For hello Frontend subnet routing table, once created and bound toohello subnet should look like this:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active 
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active


<span data-ttu-id="ded98-153">Pour cet exemple, commandes sont utilisés toobuild la table d’itinéraires hello hello suivantes, ajoutez un itinéraire défini par l’utilisateur et lier sous-réseau de tooa hello itinéraire table (Remarque ; tous les éléments ci-dessous commençant par un signe dollar (par exemple : $BESubnet) sont des variables définies par l’utilisateur à partir de script hello Hello section de référence de ce document) :</span><span class="sxs-lookup"><span data-stu-id="ded98-153">For this example, hello following commands are used toobuild hello route table, add a user defined route, and then bind hello route table tooa subnet (Note; any items below beginning with a dollar sign (e.g.: $BESubnet) are user defined variables from hello script in hello reference section of this document):</span></span>

1. <span data-ttu-id="ded98-154">Première table de routage base hello doit être créé.</span><span class="sxs-lookup"><span data-stu-id="ded98-154">First hello base routing table must be created.</span></span> <span data-ttu-id="ded98-155">Cet extrait de code illustre la création de table hello pour le sous-réseau du serveur principal hello hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-155">This snippet shows hello creation of hello table for hello Backend subnet.</span></span> <span data-ttu-id="ded98-156">Dans le script de hello, une table correspondante est également créée pour le sous-réseau du serveur frontal hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-156">In hello script, a corresponding table is also created for hello Frontend subnet.</span></span>
   
     <span data-ttu-id="ded98-157">New-AzureRouteTable -Name $BERouteTableName \`</span><span class="sxs-lookup"><span data-stu-id="ded98-157">New-AzureRouteTable -Name $BERouteTableName \`</span></span>
   
         -Location $DeploymentLocation `
         -Label "Route table for $BESubnet subnet"
2. <span data-ttu-id="ded98-158">Une fois la table d’itinéraires hello est créée, les itinéraires définis par l’utilisateur spécifiques peuvent être ajoutés.</span><span class="sxs-lookup"><span data-stu-id="ded98-158">Once hello route table is created, specific user defined routes can be added.</span></span> <span data-ttu-id="ded98-159">Dans cet extrait, tout le trafic (0.0.0.0/0) sera routé par le biais d’appareil virtuel hello (une variable, $VMIP [0], est toopass utilisé dans l’adresse IP de hello affecté lors de l’appliance virtuelle hello créé précédemment dans le script de hello).</span><span class="sxs-lookup"><span data-stu-id="ded98-159">In this snipped, all traffic (0.0.0.0/0) will be routed through hello virtual appliance (a variable, $VMIP[0], is used toopass in hello IP address assigned when hello virtual appliance was created earlier in hello script).</span></span> <span data-ttu-id="ded98-160">Dans le script de hello, une règle correspondante est également créée dans la table du serveur frontal hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-160">In hello script, a corresponding rule is also created in hello Frontend table.</span></span>
   
     <span data-ttu-id="ded98-161">Get-AzureRouteTable $BERouteTableName | \`</span><span class="sxs-lookup"><span data-stu-id="ded98-161">Get-AzureRouteTable $BERouteTableName | \`</span></span>
   
         Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
         -NextHopType VirtualAppliance `
         -NextHopIpAddress $VMIP[0]
3. <span data-ttu-id="ded98-162">Hello ci-dessus entrée d’itinéraire remplace l’itinéraire par défaut « 0.0.0.0/0 » hello, mais règle de 10.0.0.0/16 par défaut hello toujours existante qui permettrait et du trafic au sein de tooroute de réseau virtuel hello directement toohello destination pas toohello Appliance virtuelle de réseau.</span><span class="sxs-lookup"><span data-stu-id="ded98-162">hello above route entry will override hello default "0.0.0.0/0" route, but hello default 10.0.0.0/16 rule still existing which would allow traffic within hello VNet tooroute directly toohello destination and not toohello Network Virtual Appliance.</span></span> <span data-ttu-id="ded98-163">toocorrect que cette règle de suivi hello comportement doit être ajoutée.</span><span class="sxs-lookup"><span data-stu-id="ded98-163">toocorrect this behavior hello follow rule must be added.</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
4. <span data-ttu-id="ded98-164">À ce stade est un toobe choix effectué.</span><span class="sxs-lookup"><span data-stu-id="ded98-164">At this point there is a choice toobe made.</span></span> <span data-ttu-id="ded98-165">Tout le trafic achemine avec hello ci-dessus deux itinéraires pare-feu toohello pour l’évaluation, même le trafic au sein d’un sous-réseau unique.</span><span class="sxs-lookup"><span data-stu-id="ded98-165">With hello above two routes all traffic will route toohello firewall for assessment, even traffic within a single subnet.</span></span> <span data-ttu-id="ded98-166">Cela peut s’avérer utile, mais tooallow le trafic au sein d’un tooroute sous-réseau localement sans l’intervention de pare-feu hello une troisième règle très spécifique peut être ajoutée.</span><span class="sxs-lookup"><span data-stu-id="ded98-166">This may be desired, however tooallow traffic within a subnet tooroute locally without involvement from hello firewall a third, very specific rule can be added.</span></span> <span data-ttu-id="ded98-167">Cet itinéraire États destine de n’importe quelle adresse de sous-réseau local de hello peut être simplement il acheminer directement (type de tronçon suivant = VNETLocal).</span><span class="sxs-lookup"><span data-stu-id="ded98-167">This route states that any address destine for hello local subnet can just route there directly (NextHopType = VNETLocal).</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
5. <span data-ttu-id="ded98-168">Enfin, avec hello table de routage créés et remplis avec une itinéraires définis par l’utilisateur, table de hello doit maintenant être lié tooa sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="ded98-168">Finally, with hello routing table created and populated with a user defined routes, hello table must now be bound tooa subnet.</span></span> <span data-ttu-id="ded98-169">Dans le script de hello, table d’itinéraires hello frontal est également lié toohello sous-réseau frontal.</span><span class="sxs-lookup"><span data-stu-id="ded98-169">In hello script, hello front end route table is also bound toohello Frontend subnet.</span></span> <span data-ttu-id="ded98-170">Voici le script de liaison hello pour le sous-réseau de back-end hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-170">Here is hello binding script for hello back end subnet.</span></span>
   
     <span data-ttu-id="ded98-171">Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName \`</span><span class="sxs-lookup"><span data-stu-id="ded98-171">Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName \`</span></span>
   
        -SubnetName $BESubnet `
        -RouteTableName $BERouteTableName

## <a name="ip-forwarding"></a><span data-ttu-id="ded98-172">transfert IP</span><span class="sxs-lookup"><span data-stu-id="ded98-172">IP Forwarding</span></span>
<span data-ttu-id="ded98-173">Un tooUDR de fonctionnalité d’accompagnement, est le transfert IP.</span><span class="sxs-lookup"><span data-stu-id="ded98-173">A companion feature tooUDR, is IP Forwarding.</span></span> <span data-ttu-id="ded98-174">Il s’agit d’un paramètre sur une Appliance virtuelle qui autorise le trafic de tooreceive ne sont pas spécifiquement traités toohello appliance et puis transférer cette destination finale tooits de trafic.</span><span class="sxs-lookup"><span data-stu-id="ded98-174">This is a setting on a Virtual Appliance that allows it tooreceive traffic not specifically addressed toohello appliance and then forward that traffic tooits ultimate destination.</span></span>

<span data-ttu-id="ded98-175">Par exemple, si le trafic à partir de AppVM01 rend un serveur demande toohello DNS01 UDR acheminent ce pare-feu toohello.</span><span class="sxs-lookup"><span data-stu-id="ded98-175">As an example, if traffic from AppVM01 makes a request toohello DNS01 server, UDR would route this toohello firewall.</span></span> <span data-ttu-id="ded98-176">Avec le transfert IP activé, le trafic de hello pour la destination de DNS01 hello (10.0.2.4) sera accepté par l’application hello (10.0.0.4) et ensuite transmis tooits sa destination finale (10.0.2.4).</span><span class="sxs-lookup"><span data-stu-id="ded98-176">With IP Forwarding enabled, hello traffic for hello DNS01 destination (10.0.2.4) will be accepted by hello appliance (10.0.0.4) and then forwarded tooits ultimate destination (10.0.2.4).</span></span> <span data-ttu-id="ded98-177">Sans le transfert IP activé sur hello pare-feu, le trafic ne serait pas accepté par appliance de hello même si la table d’itinéraires hello a pare-feu hello en tant que tronçon suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-177">Without IP Forwarding enabled on hello Firewall, traffic would not be accepted by hello appliance even though hello route table has hello firewall as hello next hop.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ded98-178">Il est critique tooremember tooenable le transfert IP conjointement avec l’utilisateur définie par le routage.</span><span class="sxs-lookup"><span data-stu-id="ded98-178">It’s critical tooremember tooenable IP Forwarding in conjunction with User Defined Routing.</span></span>
> 
> 

<span data-ttu-id="ded98-179">La configuration du transfert IP est une commande unique et peut être exécutée au moment de la création d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ded98-179">Setting up IP Forwarding is a single command and can be done at VM creation time.</span></span> <span data-ttu-id="ded98-180">Pourquoi flux de cet extrait de code exemple hello est vers fin hello du script de hello et regroupé avec les commandes UDR hello :</span><span class="sxs-lookup"><span data-stu-id="ded98-180">For hello flow of this example hello code snippet is towards hello end of hello script and grouped with hello UDR commands:</span></span>

1. <span data-ttu-id="ded98-181">Appeler l’instance de machine virtuelle hello qui est votre appliance virtuelle, hello pare-feu dans ce cas et activer le transfert IP (Remarque ; un élément de début rouge avec un signe dollar (par exemple : $VMName[0]) est une variable définie par l’utilisateur à partir du script hello dans la section de référence hello de ce document.</span><span class="sxs-lookup"><span data-stu-id="ded98-181">Call hello VM instance that is your virtual appliance, hello firewall in this case, and enable IP Forwarding (Note; any item in red beginning with a dollar sign (e.g.: $VMName[0]) is a user defined variable from hello script in hello reference section of this document.</span></span> <span data-ttu-id="ded98-182">Hello zéro entre crochets, [0] représente hello première machine virtuelle dans le tableau hello toowork de script d’exemple hello sans modification de machines virtuelles, hello premier ordinateur virtuel (VM 0) doit être hello pare-feu) :</span><span class="sxs-lookup"><span data-stu-id="ded98-182">hello zero in brackets, [0], represents hello first VM in hello array of VMs, for hello example script toowork without modification, hello first VM (VM 0) must be hello firewall):</span></span>
   
     <span data-ttu-id="ded98-183">Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | \`</span><span class="sxs-lookup"><span data-stu-id="ded98-183">Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | \`</span></span>
   
        Set-AzureIPForwarding -Enable

## <a name="network-security-groups-nsg"></a><span data-ttu-id="ded98-184">Groupes de sécurité réseau (NSG)</span><span class="sxs-lookup"><span data-stu-id="ded98-184">Network Security Groups (NSG)</span></span>
<span data-ttu-id="ded98-185">Dans cet exemple, un groupe NSG est créé, puis chargé avec une seule règle.</span><span class="sxs-lookup"><span data-stu-id="ded98-185">In this example, a NSG group is built and then loaded with a single rule.</span></span> <span data-ttu-id="ded98-186">Ce groupe est ensuite lié uniquement toohello frontales et principales sous-réseaux (pas hello SecNet).</span><span class="sxs-lookup"><span data-stu-id="ded98-186">This group is then bound only toohello Frontend and Backend subnets (not hello SecNet).</span></span> <span data-ttu-id="ded98-187">Déclarative hello règle est en cours de génération :</span><span class="sxs-lookup"><span data-stu-id="ded98-187">Declaratively hello following rule is being built:</span></span>

1. <span data-ttu-id="ded98-188">Tout trafic (tous les ports) à partir de hello Internet toohello réseau virtuel entier (tous les sous-réseaux) est refusé.</span><span class="sxs-lookup"><span data-stu-id="ded98-188">Any traffic (all ports) from hello Internet toohello entire VNet (all subnets) is Denied</span></span>

<span data-ttu-id="ded98-189">Bien que dans cet exemple, on utilise des NSG, son principal objectif est celui d’une couche secondaire de défense contre les erreurs de configuration manuelle.</span><span class="sxs-lookup"><span data-stu-id="ded98-189">Although NSGs are used in this example, it’s main purpose is as a secondary layer of defense against manual misconfiguration.</span></span> <span data-ttu-id="ded98-190">Nous souhaitons tooblock tooeither hello serveur frontal de hello internet le trafic entrant de tous les ou principal des sous-réseaux, le trafic doivent uniquement transitent par hello pare-feu de toohello SecNet sous-réseau (et ensuite, si nécessaire sur toohello frontal ou principal sous-réseaux).</span><span class="sxs-lookup"><span data-stu-id="ded98-190">We want tooblock all inbound traffic from hello internet tooeither hello Frontend or Backend subnets, traffic should only flow through hello SecNet subnet toohello firewall (and then if appropriate on toohello Frontend or Backend subnets).</span></span> <span data-ttu-id="ded98-191">De plus, avec des règles UDR hello en place, tout le trafic qui faites-en hello sous-réseaux frontal ou serveur principal serait dirigé out toohello pare-feu (Merci tooUDR).</span><span class="sxs-lookup"><span data-stu-id="ded98-191">Plus, with hello UDR rules in place, any traffic that did make it into hello Frontend or Backend subnets would be directed out toohello firewall (thanks tooUDR).</span></span> <span data-ttu-id="ded98-192">pare-feu de Hello verriez cela comme un flux asymétrique et tomberaient le trafic sortant de hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-192">hello firewall would see this as an asymmetric flow and would drop hello outbound traffic.</span></span> <span data-ttu-id="ded98-193">Par conséquent, il existe trois couches de hello de protection de sécurité serveur frontal et principal sous-réseaux ; aucun des points de terminaison ouverts sur hello FrontEnd001 et des services de cloud BackEnd001, 2) groupes de sécurité réseau refuser le trafic à partir de 1) hello Internet, pare-feu hello (3) la suppression du trafic asymétrique.</span><span class="sxs-lookup"><span data-stu-id="ded98-193">Thus there are three layers of security protecting hello Frontend and Backend subnets; 1) no open endpoints on hello FrontEnd001 and BackEnd001 cloud services, 2) NSGs denying traffic from hello Internet, 3) hello firewall dropping asymmetric traffic.</span></span>

<span data-ttu-id="ded98-194">Un point intéressant concernant hello groupe de sécurité réseau dans cet exemple est qu’il contient une seule règle, illustrée ci-dessous, qui est toodeny internet trafic toohello réseau virtuel entier qui comprend le sous-réseau de sécurité hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-194">One interesting point regarding hello Network Security Group in this example is that it contains only one rule, shown below, which is toodeny internet traffic toohello entire virtual network which would include hello Security subnet.</span></span> 

    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet `
        from hello Internet" `
        -Type Inbound -Priority 100 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *

<span data-ttu-id="ded98-195">Toutefois, étant donné que hello NSG n’est lié toohello serveur frontal et principal sous-réseaux, règle de hello n’est pas traitée sur le trafic entrant de sous-réseau de sécurité toohello.</span><span class="sxs-lookup"><span data-stu-id="ded98-195">However, since hello NSG is only bound toohello Frontend and Backend subnets, hello rule isn’t processed on traffic inbound toohello Security subnet.</span></span> <span data-ttu-id="ded98-196">Par conséquent, même si la règle de groupe de sécurité réseau hello n’indique aucune adresse tooany du trafic Internet sur le réseau virtuel, de hello car hello que NSG n’a jamais été lié sous-réseau de sécurité toohello, le trafic circule de sous-réseau de sécurité toohello.</span><span class="sxs-lookup"><span data-stu-id="ded98-196">As a result, even though hello NSG rule says no Internet traffic tooany address on hello VNet, because hello NSG was never bound toohello Security subnet, traffic will flow toohello Security subnet.</span></span>

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $FESubnet -VirtualNetworkName $VNetName

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $BESubnet -VirtualNetworkName $VNetName

## <a name="firewall-rules"></a><span data-ttu-id="ded98-197">Règles de pare-feu</span><span class="sxs-lookup"><span data-stu-id="ded98-197">Firewall Rules</span></span>
<span data-ttu-id="ded98-198">Sur le pare-feu hello, règles de transfert devez toobe créé.</span><span class="sxs-lookup"><span data-stu-id="ded98-198">On hello firewall, forwarding rules will need toobe created.</span></span> <span data-ttu-id="ded98-199">Étant donné que les pare-feu hello est le trafic de blocage ou transfert tout entrant, sortant et intra-réseau virtuel de règles de pare-feu sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="ded98-199">Since hello firewall is blocking or forwarding all inbound, outbound, and intra-VNet traffic many firewall rules are needed.</span></span> <span data-ttu-id="ded98-200">En outre, tout le trafic entrant sera atteint adresse IP publique de hello Service de sécurité (sur des ports différents), toobe traitée par le pare-feu hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-200">Also, all inbound traffic will hit hello Security Service public IP address (on different ports), toobe processed by hello firewall.</span></span> <span data-ttu-id="ded98-201">Un flux logique de hello toodiagram avant de configurer ultérieurement des sous-réseaux hello et reprise de tooavoid de règles de pare-feu, il est préférable.</span><span class="sxs-lookup"><span data-stu-id="ded98-201">A best practice is toodiagram hello logical flows before setting up hello subnets and firewall rules tooavoid rework later.</span></span> <span data-ttu-id="ded98-202">Bonjour figure suivante est une vue logique de règles de pare-feu hello pour cet exemple :</span><span class="sxs-lookup"><span data-stu-id="ded98-202">hello following figure is a logical view of hello firewall rules for this example:</span></span>

<span data-ttu-id="ded98-203">![Affichage logique de règles de pare-feu de hello][2]</span><span class="sxs-lookup"><span data-stu-id="ded98-203">![Logical View of hello Firewall Rules][2]</span></span>

> [!NOTE]
> <span data-ttu-id="ded98-204">En fonction de hello Qu'appliance virtuelle de réseau utilisé, les ports de gestion hello peuvent varier.</span><span class="sxs-lookup"><span data-stu-id="ded98-204">Based on hello Network Virtual Appliance used, hello management ports will vary.</span></span> <span data-ttu-id="ded98-205">Dans cet exemple, il est fait référence à un pare-feu Barracuda NextGen Firewall utilisant les ports 22, 801 et 807.</span><span class="sxs-lookup"><span data-stu-id="ded98-205">In this example a Barracuda NextGen Firewall is referenced which uses ports 22, 801, and 807.</span></span> <span data-ttu-id="ded98-206">Veuillez consulter hello appliance fournisseur documentation toofind hello exacte ports utilisés pour la gestion de périphérique hello utilisé.</span><span class="sxs-lookup"><span data-stu-id="ded98-206">Please consult hello appliance vendor documentation toofind hello exact ports used for management of hello device being used.</span></span>
> 
> 

### <a name="logical-rule-description"></a><span data-ttu-id="ded98-207">Description de la logique de règle</span><span class="sxs-lookup"><span data-stu-id="ded98-207">Logical Rule Description</span></span>
<span data-ttu-id="ded98-208">Dans le diagramme de la logique de hello ci-dessus, sous-réseau de sécurité hello n’est pas affiché dans la mesure où le pare-feu de hello est la seule ressource de hello sur ce sous-réseau ce diagramme affiche les règles de pare-feu hello et comment ils logiquement autoriser ou refuser des flux de trafic et pas hello routé chemin d’accès réel.</span><span class="sxs-lookup"><span data-stu-id="ded98-208">In hello logical diagram above, hello security subnet is not shown since hello firewall is hello only resource on that subnet, and this diagram is showing hello firewall rules and how they logically allow or deny traffic flows and not hello actual routed path.</span></span> <span data-ttu-id="ded98-209">En outre, des ports externes hello sélectionnés pour hello le trafic RDP sont des ports sont plus élevées (8014 – 8026) et ont été toosomewhat sélectionné s’alignent hello a deux octets de l’adresse IP locale de hello pour faciliter la lisibilité (par exemple, l’adresse du serveur local 10.0.1.4 est associé port externe 8014), cependant les ports non conflictuel plus élevées peut être utilisées.</span><span class="sxs-lookup"><span data-stu-id="ded98-209">Also, hello external ports selected for hello RDP traffic are higher ranged ports (8014 – 8026) and were selected toosomewhat align with hello last two octets of hello local IP address for easier readability (e.g. local server address 10.0.1.4 is associated with external port 8014), however any higher non-conflicting ports could be used.</span></span>

<span data-ttu-id="ded98-210">Dans cet exemple, nous avons besoin de 7 types de règles, qui se présentent comme suit :</span><span class="sxs-lookup"><span data-stu-id="ded98-210">For this example, we need 7 types of rules, these rule types are described as follows:</span></span>

* <span data-ttu-id="ded98-211">Règles externes (pour le trafic entrant) :</span><span class="sxs-lookup"><span data-stu-id="ded98-211">External Rules (for inbound traffic):</span></span>
  1. <span data-ttu-id="ded98-212">Règle de pare-feu de gestion : Cette règle de redirection de l’application autorise les ports de gestion du trafic toopass toohello de l’appliance virtuelle de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-212">Firewall Management Rule: This App Redirect rule allows traffic toopass toohello management ports of hello network virtual appliance.</span></span>
  2. <span data-ttu-id="ded98-213">Règles de RDP (pour chaque serveur windows) : ces quatre règles (une pour chaque serveur) autorise la gestion de hello des serveurs individuels via RDP.</span><span class="sxs-lookup"><span data-stu-id="ded98-213">RDP Rules (for each windows server): These four rules (one for each server) will allow management of hello individual servers via RDP.</span></span> <span data-ttu-id="ded98-214">Cela pourrait également regroupé dans une règle en fonction des capacités hello Hello Appliance virtuelle de réseau utilisée.</span><span class="sxs-lookup"><span data-stu-id="ded98-214">This could also be bundled into one rule depending on hello capabilities of hello Network Virtual Appliance being used.</span></span>
  3. <span data-ttu-id="ded98-215">Règles de trafic d’application : Il existe deux règles de trafic d’Application, hello tout d’abord pour le trafic de hello frontal web et hello seconde pour le trafic de back-end de hello (par exemple, niveau de toodata serveur web).</span><span class="sxs-lookup"><span data-stu-id="ded98-215">Application Traffic Rules: There are two Application Traffic Rules, hello first for hello front end web traffic, and hello second for hello back end traffic (eg web server toodata tier).</span></span> <span data-ttu-id="ded98-216">configuration de Hello de ces règles dépendra de l’architecture de réseau hello (où sont placés vos serveurs) et flux de trafic (le trafic hello direction du flux, et quels ports sont utilisés).</span><span class="sxs-lookup"><span data-stu-id="ded98-216">hello configuration of these rules will depend on hello network architecture (where your servers are placed) and traffic flows (which direction hello traffic flows, and which ports are used).</span></span>
     * <span data-ttu-id="ded98-217">règle de première Hello permettra de serveur d’applications hello application réelle du trafic tooreach hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-217">hello first rule will allow hello actual application traffic tooreach hello application server.</span></span> <span data-ttu-id="ded98-218">Alors que hello autres règles permettent de sécurité, de gestion, etc., règles d’Application sont ce qu’Autoriser tooaccess d’utilisateurs ou des services externes ou les applications hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-218">While hello other rules allow for security, management, etc., Application Rules are what allow external users or services tooaccess hello application(s).</span></span> <span data-ttu-id="ded98-219">Pour cet exemple, il existe un serveur web sur le port 80, par conséquent, une seule application règle de pare-feu redirige le trafic entrant toohello adresse IP externe, interne adresse IP des serveurs toohello web.</span><span class="sxs-lookup"><span data-stu-id="ded98-219">For this example, there is a single web server on port 80, thus a single firewall application rule will redirect inbound traffic toohello external IP, toohello web servers internal IP address.</span></span> <span data-ttu-id="ded98-220">Hello redirigé session du trafic serait NAT avait toohello interne au serveur.</span><span class="sxs-lookup"><span data-stu-id="ded98-220">hello redirected traffic session would be NAT’d toohello internal server.</span></span>
     * <span data-ttu-id="ded98-221">Hello deuxième règle de trafic d’Application hello règle tooallow hello Web Server tootalk toohello AppVM01 le serveur principal (mais pas AppVM02) via n’importe quel port.</span><span class="sxs-lookup"><span data-stu-id="ded98-221">hello second Application Traffic Rule is hello back end rule tooallow hello Web Server tootalk toohello AppVM01 server (but not AppVM02) via any port.</span></span>
* <span data-ttu-id="ded98-222">Règles internes (pour le trafic réseau virtuel interne)</span><span class="sxs-lookup"><span data-stu-id="ded98-222">Internal Rules (for intra-VNet traffic)</span></span>
  1. <span data-ttu-id="ded98-223">Sortant tooInternet règle : cette règle autorise le trafic à partir de n’importe quel réseau toopass toohello sélectionné réseaux.</span><span class="sxs-lookup"><span data-stu-id="ded98-223">Outbound tooInternet Rule: This rule will allow traffic from any network toopass toohello selected networks.</span></span> <span data-ttu-id="ded98-224">Cette règle est généralement une règle par défaut déjà présent sur le pare-feu hello, mais dans un état désactivé.</span><span class="sxs-lookup"><span data-stu-id="ded98-224">This rule is usually a default rule already on hello firewall, but in a disabled state.</span></span> <span data-ttu-id="ded98-225">Pour cet exemple, cette règle doit être activée.</span><span class="sxs-lookup"><span data-stu-id="ded98-225">This rule should be enabled for this example.</span></span>
  2. <span data-ttu-id="ded98-226">Règle DNS : Cette règle permet uniquement DNS (port 53) le trafic toopass toohello serveurDNS.</span><span class="sxs-lookup"><span data-stu-id="ded98-226">DNS Rule: This rule allows only DNS (port 53) traffic toopass toohello DNS server.</span></span> <span data-ttu-id="ded98-227">Pour cet environnement, la plupart du trafic à partir de hello frontal toohello back-end est bloqué, cette règle permet en particulier DNS à partir de n’importe quel sous-réseau local.</span><span class="sxs-lookup"><span data-stu-id="ded98-227">For this environment most traffic from hello Frontend toohello Backend is blocked, this rule specifically allows DNS from any local subnet.</span></span>
  3. <span data-ttu-id="ded98-228">Sous-réseau tooSubnet règle : cette règle est tooallow n’importe quel serveur DOS de hello sous-réseau tooconnect tooany serveur sur le sous-réseau frontal de hello principal (mais pas hello inverse).</span><span class="sxs-lookup"><span data-stu-id="ded98-228">Subnet tooSubnet Rule: This rule is tooallow any server on hello back end subnet tooconnect tooany server on hello front end subnet (but not hello reverse).</span></span>
* <span data-ttu-id="ded98-229">Règle de prévention de défaillance (pour le trafic qui ne correspond pas hello ci-dessus) :</span><span class="sxs-lookup"><span data-stu-id="ded98-229">Fail-safe Rule (for traffic that doesn’t meet any of hello above):</span></span>
  1. <span data-ttu-id="ded98-230">Refuser toutes les règles de trafic : Cela doit toujours être règle finale de hello (en termes de priorité) et par conséquent si un trafic acheminé échoue toomatch des hello précédant les règles, qu'elles seront supprimées par cette règle.</span><span class="sxs-lookup"><span data-stu-id="ded98-230">Deny All Traffic Rule: This should always be hello final rule (in terms of priority), and as such if a traffic flows fails toomatch any of hello preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="ded98-231">Il s’agit d’une règle par défaut qui est en général activée, et en général, aucune modification n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ded98-231">This is a default rule and usually activated, no modifications are generally needed.</span></span>

> [!TIP]
> <span data-ttu-id="ded98-232">Sur la deuxième règle de trafic d’application hello, n’importe quel port n’est autorisée pour cet exemple simple, un Bonjour scénario réel, des plages de port et l’adresse la plus spécifiques doivent être surface d’attaque hello tooreduce utilisés de cette règle.</span><span class="sxs-lookup"><span data-stu-id="ded98-232">On hello second application traffic rule, any port is allowed for easy of this example, in a real scenario hello most specific port and address ranges should be used tooreduce hello attack surface of this rule.</span></span>
> 
> 

<br />

> [!IMPORTANT]
> <span data-ttu-id="ded98-233">Une fois que tous les hello au-dessus de règles sont créées, il est important priorité hello tooreview chacun le trafic tooensure de règle sera autorisée ou refusée comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="ded98-233">Once all of hello above rules are created, it’s important tooreview hello priority of each rule tooensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="ded98-234">Pour cet exemple, les règles de hello sont dans l’ordre de priorité.</span><span class="sxs-lookup"><span data-stu-id="ded98-234">For this example, hello rules are in priority order.</span></span> <span data-ttu-id="ded98-235">Il est facile toobe verrouillé hors de pare-feu hello échéance toomis ordonné de règles.</span><span class="sxs-lookup"><span data-stu-id="ded98-235">It's easy toobe locked out of hello firewall due toomis-ordered rules.</span></span> <span data-ttu-id="ded98-236">Au minimum, assurez-vous de gestion hello pour le pare-feu hello elle-même est toujours de règle de priorité la plus élevée absolu hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-236">At a minimum, ensure hello management for hello firewall itself is always hello absolute highest priority rule.</span></span>
> 
> 

### <a name="rule-prerequisites"></a><span data-ttu-id="ded98-237">Préalable en matière de règles</span><span class="sxs-lookup"><span data-stu-id="ded98-237">Rule Prerequisites</span></span>
<span data-ttu-id="ded98-238">Une configuration requise pour le pare-feu de hello hello Machine virtuelle en cours d’exécution sont des points de terminaison publics.</span><span class="sxs-lookup"><span data-stu-id="ded98-238">One prerequisite for hello Virtual Machine running hello firewall are public endpoints.</span></span> <span data-ttu-id="ded98-239">Pour le trafic de hello pare-feu tooprocess les points de terminaison publics hello approprié doivent être ouverts.</span><span class="sxs-lookup"><span data-stu-id="ded98-239">For hello firewall tooprocess traffic hello appropriate public endpoints must be open.</span></span> <span data-ttu-id="ded98-240">Il existe trois types de trafic dans cet exemple ; (1) gestion du trafic toocontrol hello pare-feu et les règles de pare-feu, les serveurs windows hello RDP (2) le trafic toocontrol et le trafic d’Application (3).</span><span class="sxs-lookup"><span data-stu-id="ded98-240">There are three types of traffic in this example; 1) Management traffic toocontrol hello firewall and firewall rules, 2) RDP traffic toocontrol hello windows servers, and 3) Application Traffic.</span></span> <span data-ttu-id="ded98-241">Il s’agit hello trois colonnes de types de trafic hello supérieure la moitié de la vue logique de règles de pare-feu hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="ded98-241">These are hello three columns of traffic types in hello upper half of logical view of hello firewall rules above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ded98-242">Un takeway clé ici est tooremember qui **tous les** trafic proviendront via le pare-feu hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-242">A key takeway here is tooremember that **all** traffic will come through hello firewall.</span></span> <span data-ttu-id="ded98-243">C’est le cas toohello de bureau tooremote IIS01 server, même s’il est Bonjour Service de Cloud Front End et de sous-réseau frontal hello tooaccess ce serveur, nous devons tooRDP toohello pare-feu sur port 8014 et laissez demande RDP hello pare-feu tooroute hello en interne toohello IIS01 le Port RDP.</span><span class="sxs-lookup"><span data-stu-id="ded98-243">So tooremote desktop toohello IIS01 server, even though it's in hello Front End Cloud Service and on hello Front End subnet, tooaccess this server we will need tooRDP toohello firewall on port 8014, and then allow hello firewall tooroute hello RDP request internally toohello IIS01 RDP Port.</span></span> <span data-ttu-id="ded98-244">Hello « Se connecter » du portail Azure bouton ne fonctionne pas, car il n’existe aucun tooIIS01 de chemin d’accès RDP direct (pour autant que le portail de hello peut voir).</span><span class="sxs-lookup"><span data-stu-id="ded98-244">hello Azure portal's "Connect" button won't work because there is no direct RDP path tooIIS01 (as far as hello portal can see).</span></span> <span data-ttu-id="ded98-245">Cela signifie que toutes les connexions à partir de hello internet seront toohello Service de sécurité et un Port, par exemple, secscv001.cloudapp.net:xxxx (hello référence diagramme pour le mappage de Port externe et adresse IP interne et le Port de hello ci-dessus).</span><span class="sxs-lookup"><span data-stu-id="ded98-245">This means all connections from hello internet will be toohello Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx (reference hello above diagram for hello mapping of External Port and Internal IP and Port).</span></span>
> 
> 

<span data-ttu-id="ded98-246">Un point de terminaison peuvent être ouverts lors de la création d’ordinateurs virtuels hello ou valider la génération est effectuée dans le script d’exemple hello et indiqué ci-dessous dans cet extrait de code (Remarque ; tout début de l’élément avec un signe dollar (par exemple : $VMName[$i]) est une variable définie par l’utilisateur à partir de script hello hello referen section de ce de ce document.</span><span class="sxs-lookup"><span data-stu-id="ded98-246">An endpoint can be opened either at hello time of VM creation or post build as is done in hello example script and shown below in this code snippet (Note; any item beginning with a dollar sign (e.g.: $VMName[$i]) is a user defined variable from hello script in hello reference section of this document.</span></span> <span data-ttu-id="ded98-247">Hello « $i » entre crochets, [$i], représente hello tableau quantité, pour un ordinateur virtuel spécifique dans un tableau d’ordinateurs virtuels) :</span><span class="sxs-lookup"><span data-stu-id="ded98-247">hello “$i” in brackets, [$i], represents hello array number of a specific VM in an array of VMs):</span></span>

    Add-AzureEndpoint -Name "HTTP" -Protocol tcp -PublicPort 80 -LocalPort 80 `
        -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | `
        Update-AzureVM

<span data-ttu-id="ded98-248">Bien que pas clairement indiqué ici en raison d’utilisation de toohello de variables, mais les points de terminaison sont **uniquement** ouvert sur hello Service de Cloud de sécurité.</span><span class="sxs-lookup"><span data-stu-id="ded98-248">Although not clearly shown here due toohello use of variables, but endpoints are **only** opened on hello Security Cloud Service.</span></span> <span data-ttu-id="ded98-249">Il s’agit de tooensure que tout le trafic entrant est géré (acheminés, NAT avait, supprimée) par le pare-feu hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-249">This is tooensure that all inbound traffic is handled (routed, NAT'd, dropped) by hello firewall.</span></span>

<span data-ttu-id="ded98-250">Un client de gestion sera peut-être toobe installé sur un pare-feu de hello toomanage PC et créer des configurations hello nécessaires.</span><span class="sxs-lookup"><span data-stu-id="ded98-250">A management client will need toobe installed on a PC toomanage hello firewall and create hello configurations needed.</span></span> <span data-ttu-id="ded98-251">Consultez le fournisseur de documentation de votre pare-feu (ou autres NVA) hello sur comment toomanage hello appareil.</span><span class="sxs-lookup"><span data-stu-id="ded98-251">See hello documentation from your firewall (or other NVA) vendor on how toomanage hello device.</span></span> <span data-ttu-id="ded98-252">suite de Hello de cette section et de la section suivante hello, la création de règles de pare-feu, décrit la configuration hello du pare-feu de hello lui-même, via le client de gestion des fournisseurs hello (c'est-à-dire, non hello portail Azure ou PowerShell).</span><span class="sxs-lookup"><span data-stu-id="ded98-252">hello remainder of this section and hello next section, Firewall Rules Creation, will describe hello configuration of hello firewall itself, through hello vendors management client (i.e. not hello Azure portal or PowerShell).</span></span>

<span data-ttu-id="ded98-253">Instructions de téléchargement du client et de connexion toohello Barracuda utilisé dans cet exemple se trouve ici : [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="ded98-253">Instructions for client download and connecting toohello Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="ded98-254">Une fois connecté sur le pare-feu hello mais avant de créer des règles de pare-feu, il existe deux classes d’objet requis qui peuvent faciliter la création de règles hello ; Objets de Service et de réseau.</span><span class="sxs-lookup"><span data-stu-id="ded98-254">Once logged onto hello firewall but before creating firewall rules, there are two prerequisite object classes that can make creating hello rules easier; Network & Service objects.</span></span>

<span data-ttu-id="ded98-255">Pour cet exemple, trois objets réseau nommé doivent être défini (un pour le sous-réseau du serveur frontal hello et sous-réseau du serveur principal hello, également un objet réseau pour l’adresse IP de hello du serveur DNS de hello).</span><span class="sxs-lookup"><span data-stu-id="ded98-255">For this example, three named network objects should be defined (one for hello Frontend subnet and hello Backend subnet, also a network object for hello IP address of hello DNS server).</span></span> <span data-ttu-id="ded98-256">toocreate un réseau nommé ; à partir du tableau de bord hello Barracuda NG administrateur client, accédez d’onglet de configuration toohello, dans la section de Configuration opérationnelle de hello cliquez sur le groupe de règles, puis cliquez sur « Réseaux » sous le menu des objets de pare-feu hello, puis cliquez sur Nouveau dans le menu de modifier des réseaux hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-256">toocreate a named network; starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset, then click “Networks” under hello Firewall Objects menu, then click New in hello Edit Networks menu.</span></span> <span data-ttu-id="ded98-257">objet de réseau Hello peut maintenant être créé, en ajoutant le nom de la hello et un préfixe de hello :</span><span class="sxs-lookup"><span data-stu-id="ded98-257">hello network object can now be created, by adding hello name and hello prefix:</span></span>

<span data-ttu-id="ded98-258">![Créer un objet réseau de serveur frontal][3]</span><span class="sxs-lookup"><span data-stu-id="ded98-258">![Create a FrontEnd Network Object][3]</span></span>

<span data-ttu-id="ded98-259">Cette opération crée un réseau nommé pour le sous-réseau du serveur frontal hello, un objet similaire doit être créé pour hello principal sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="ded98-259">This will create a named network for hello FrontEnd subnet, a similar object should be created for hello BackEnd subnet as well.</span></span> <span data-ttu-id="ded98-260">Maintenant les sous-réseaux hello peuvent être plus facilement référencées par son nom dans les règles de pare-feu hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-260">Now hello subnets can be more easily referenced by name in hello firewall rules.</span></span>

<span data-ttu-id="ded98-261">Pourquoi objet serveur DNS :</span><span class="sxs-lookup"><span data-stu-id="ded98-261">For hello DNS Server Object:</span></span>

<span data-ttu-id="ded98-262">![Créer un objet de serveur DNS][4]</span><span class="sxs-lookup"><span data-stu-id="ded98-262">![Create a DNS Server Object][4]</span></span>

<span data-ttu-id="ded98-263">Cette référence d’adresse IP unique sera utilisée dans une règle DNS plus loin dans le document de hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-263">This single IP address reference will be utilized in a DNS rule later in hello document.</span></span>

<span data-ttu-id="ded98-264">les objets requis deuxième Hello sont des objets de Services.</span><span class="sxs-lookup"><span data-stu-id="ded98-264">hello second prerequisite objects are Services objects.</span></span> <span data-ttu-id="ded98-265">Ces représentent des ports de connexion RDP hello pour chaque serveur.</span><span class="sxs-lookup"><span data-stu-id="ded98-265">These will represent hello RDP connection ports for each server.</span></span> <span data-ttu-id="ded98-266">Étant donné que l’objet de service RDP hello existant est le port RDP toohello liée par défaut, 3389, nouveaux Services peuvent être créés tooallow trafic à partir des ports externes hello (8014-8026).</span><span class="sxs-lookup"><span data-stu-id="ded98-266">Since hello existing RDP service object is bound toohello default RDP port, 3389, new Services can be created tooallow traffic from hello external ports (8014-8026).</span></span> <span data-ttu-id="ded98-267">Hello nouveaux ports peuvent également être ajoutées à service RDP toohello existant, mais pour faciliter la démonstration, vous pouvez créer une règle individuelle pour chaque serveur.</span><span class="sxs-lookup"><span data-stu-id="ded98-267">hello new ports could also be added toohello existing RDP service, but for ease of demonstration, an individual rule for each server can be created.</span></span> <span data-ttu-id="ded98-268">toocreate une nouvelle règle RDP pour un serveur ; démarrage à partir du tableau de bord hello Barracuda NG administrateur client, accédez à onglet de configuration toohello, hello Configuration opérationnelle de section cliquez sur le groupe de règles, puis cliquez sur « Services » sous hello menu des objets de pare-feu, défiler la liste hello des services et sélectionnez hello Service « RDP ».</span><span class="sxs-lookup"><span data-stu-id="ded98-268">toocreate a new RDP rule for a server; starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset, then click “Services” under hello Firewall Objects menu, scroll down hello list of services and select hello “RDP” service.</span></span> <span data-ttu-id="ded98-269">Effectuez un clic droit et sélectionnez Copier, puis avec le bouton droit, cliquez et sélectionnez Coller.</span><span class="sxs-lookup"><span data-stu-id="ded98-269">Right-click and select copy, then right-click and select Paste.</span></span> <span data-ttu-id="ded98-270">Il existe désormais un objet de Service RDP-Copie1 qui peut être modifié.</span><span class="sxs-lookup"><span data-stu-id="ded98-270">There is now a RDP-Copy1 Service Object that can be edited.</span></span> <span data-ttu-id="ded98-271">RDP-Copie1 d’avec le bouton droit et sélectionnez Modifier, hello modifier l’objet Service fenêtre s’affiche comme illustré ici :</span><span class="sxs-lookup"><span data-stu-id="ded98-271">Right-click RDP-Copy1 and select Edit, hello Edit Service Object window will pop up as shown here:</span></span>

<span data-ttu-id="ded98-272">![Copie de la règle RDP par défaut][5]</span><span class="sxs-lookup"><span data-stu-id="ded98-272">![Copy of Default RDP Rule][5]</span></span>

<span data-ttu-id="ded98-273">les valeurs Hello peuvent ensuite être modifié toorepresent hello service RDP pour un serveur spécifique.</span><span class="sxs-lookup"><span data-stu-id="ded98-273">hello values can then be edited toorepresent hello RDP service for a specific server.</span></span> <span data-ttu-id="ded98-274">Pour hello AppVM01 ci-dessus par défaut règle RDP doit tooreflect modifié un nouveau nom de Service, Description, et le Port RDP externe utilisé dans hello diagramme de la Figure 8 (Remarque : les ports hello sont modifiés à partir de hello RDP comme valeur par défaut le port 3389 toohello externe qui est utilisé pour ce un serveur spécifique, dans les cas de hello du Port externe de AppVM01 hello est 8025) service modifié hello est indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ded98-274">For AppVM01 hello above default RDP rule should be modified tooreflect a new Service Name, Description, and external RDP Port used in hello Figure 8 diagram (Note: hello ports are changed from hello RDP default of 3389 toohello external port being used for this specific server, in hello case of AppVM01 hello external Port is 8025) hello modified service is shown below:</span></span>

<span data-ttu-id="ded98-275">![Règle AppVM01][6]</span><span class="sxs-lookup"><span data-stu-id="ded98-275">![AppVM01 Rule][6]</span></span>

<span data-ttu-id="ded98-276">Ce processus doit être répété toocreate Services RDP pour hello restant serveurs ; AppVM02, DNS01 et IIS01.</span><span class="sxs-lookup"><span data-stu-id="ded98-276">This process must be repeated toocreate RDP Services for hello remaining servers; AppVM02, DNS01, and IIS01.</span></span> <span data-ttu-id="ded98-277">Création de Hello de ces Services permettront à la création de règle hello plus simple et plus évidente dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-277">hello creation of these Services will make hello Rule creation simpler and more obvious in hello next section.</span></span>

> [!NOTE]
> <span data-ttu-id="ded98-278">Un service de protocole RDP pour hello pare-feu n’est pas nécessaire pour deux raisons. (1) le premier pare-feu hello VM est une image de Linux en fonction SSH étaient utilisée sur le port 22 pour la gestion des ordinateurs virtuels au lieu de RDP et (2) le port 22 et deux autres ports de gestion sont autorisées dans la première règle de gestion hello décrite ci-dessous tooallow pour la connectivité de gestion.</span><span class="sxs-lookup"><span data-stu-id="ded98-278">An RDP service for hello Firewall is not needed for two reasons; 1) first hello firewall VM is a Linux based image so SSH would be used on port 22 for VM management instead of RDP, and 2) port 22, and two other management ports are allowed in hello first management rule described below tooallow for management connectivity.</span></span>
> 
> 

### <a name="firewall-rules-creation"></a><span data-ttu-id="ded98-279">Création de règles de pare-feu</span><span class="sxs-lookup"><span data-stu-id="ded98-279">Firewall Rules Creation</span></span>
<span data-ttu-id="ded98-280">Il existe trois types de règles de pare-feu utilisées dans cet exemple, et elles sont toutes représentées par des icônes distinctes :</span><span class="sxs-lookup"><span data-stu-id="ded98-280">There are three types of firewall rules used in this example, they all have distinct icons:</span></span>

<span data-ttu-id="ded98-281">règle de redirection de l’Application Hello : ![l’icône de redirection de l’Application][7]</span><span class="sxs-lookup"><span data-stu-id="ded98-281">hello Application Redirect rule: ![Application Redirect Icon][7]</span></span>

<span data-ttu-id="ded98-282">une règle NAT de Destination Hello : ![icône NAT de Destination][8]</span><span class="sxs-lookup"><span data-stu-id="ded98-282">hello Destination NAT rule: ![Destination NAT Icon][8]</span></span>

<span data-ttu-id="ded98-283">règle de Pass Hello : ![passer une icône][9]</span><span class="sxs-lookup"><span data-stu-id="ded98-283">hello Pass rule: ![Pass Icon][9]</span></span>

<span data-ttu-id="ded98-284">Vous trouverez plus d’informations sur ces règles sur le site web de Barracuda hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-284">More information on these rules can be found at hello Barracuda web site.</span></span>

<span data-ttu-id="ded98-285">toocreate hello suivant les règles (ou vérifiez les règles par défaut existant), à partir du tableau de bord hello Barracuda NG administrateur client, accédez d’onglet de configuration toohello, Bonjour Configuration opérationnelle de section, cliquez sur règles.</span><span class="sxs-lookup"><span data-stu-id="ded98-285">toocreate hello following rules (or verify existing default rules), starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="ded98-286">Une grille est appelée, « Règles de Main » affiche hello règles actifs et désactivés sur ce pare-feu existantes.</span><span class="sxs-lookup"><span data-stu-id="ded98-286">A grid called, “Main Rules” will show hello existing active and deactivated rules on this firewall.</span></span> <span data-ttu-id="ded98-287">Hello coin supérieur droit de cette grille est une petite, verte « + », sur cette toocreate une nouvelle règle (Remarque : votre pare-feu peut être « verrouillé » pour les modifications, si vous voyez un bouton marqué « Verrouillage » et vous toocreate impossible ou modifiez les règles, cliquez sur ce bouton trop « déverrouiller » hello se de règle t et autoriser la modification).</span><span class="sxs-lookup"><span data-stu-id="ded98-287">In hello upper right corner of this grid is a small, green “+” button, click this toocreate a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable toocreate or edit rules, click this button too“unlock” hello rule set and allow editing).</span></span> <span data-ttu-id="ded98-288">Si vous le souhaitez tooedit une règle existante, sélectionnez cette règle, avec le bouton droit et sélectionnez Modifier la règle.</span><span class="sxs-lookup"><span data-stu-id="ded98-288">If you wish tooedit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="ded98-289">Une fois vos règles sont créés ou modifiés, ils doivent être envoyées toohello pare-feu et puis activé, si cela n’est pas fait règle hello modifications ne prendront pas effet.</span><span class="sxs-lookup"><span data-stu-id="ded98-289">Once your rules are created and/or modified, they must be pushed toohello firewall and then activated, if this is not done hello rule changes will not take effect.</span></span> <span data-ttu-id="ded98-290">processus par émission de données et l’activation de Hello est décrite ci-dessous descriptions de règles de détails hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-290">hello push and activation process is described below hello details rule descriptions.</span></span>

<span data-ttu-id="ded98-291">caractéristiques de Hello de chaque règle requis toocomplete cet exemple sont décrits comme suit :</span><span class="sxs-lookup"><span data-stu-id="ded98-291">hello specifics of each rule required toocomplete this example are described as follows:</span></span>

* <span data-ttu-id="ded98-292">**Gestion des règles de pare-feu**: redirection de cette application de règle autorise le trafic toopass toohello les ports de gestion de hello network appliance virtuelle, dans cet exemple, un pare-feu de NextGen Barracuda.</span><span class="sxs-lookup"><span data-stu-id="ded98-292">**Firewall Management Rule**: This App Redirect rule allows traffic toopass toohello management ports of hello network virtual appliance, in this example a Barracuda NextGen Firewall.</span></span> <span data-ttu-id="ded98-293">les ports de gestion Hello sont 801, 807 et éventuellement 22.</span><span class="sxs-lookup"><span data-stu-id="ded98-293">hello management ports are 801, 807 and optionally 22.</span></span> <span data-ttu-id="ded98-294">les ports internes et externes Hello sont hello même (autrement dit, aucune traduction de port).</span><span class="sxs-lookup"><span data-stu-id="ded98-294">hello external and internal ports are hello same (i.e. no port translation).</span></span> <span data-ttu-id="ded98-295">Cette règle, SETUP-MGMT-ACCESS, est une règle par défaut et elle est activée par défaut (dans la version 6.1 du pare-feu Barracuda NextGen Firewall).</span><span class="sxs-lookup"><span data-stu-id="ded98-295">This rule, SETUP-MGMT-ACCESS, is a default rule and enabled by default (in Barracuda NextGen Firewall version 6.1).</span></span>
  
    <span data-ttu-id="ded98-296">![Règle de gestion de pare-feu][10]</span><span class="sxs-lookup"><span data-stu-id="ded98-296">![Firewall Management Rule][10]</span></span>

> [!TIP]
> <span data-ttu-id="ded98-297">Hello source espace d’adressage dans cette règle est un, si hello connus des plages d’adresses IP gestion, réduire cette étendue permettrait également de limiter les ports de gestion hello attaque toohello aire de conception.</span><span class="sxs-lookup"><span data-stu-id="ded98-297">hello source address space in this rule is Any, if hello management IP address ranges are known, reducing this scope would also reduce hello attack surface toohello management ports.</span></span>
> 
> 

* <span data-ttu-id="ded98-298">**Règles de RDP**: les règles NAT de Destination ces permettra gestion Hello des serveurs individuels via RDP.</span><span class="sxs-lookup"><span data-stu-id="ded98-298">**RDP Rules**:  These Destination NAT rules will allow management of hello individual servers via RDP.</span></span>
  <span data-ttu-id="ded98-299">Il existe quatre champs critiques nécessaires toocreate cette règle :</span><span class="sxs-lookup"><span data-stu-id="ded98-299">There are four critical fields needed toocreate this rule:</span></span>
  
  1. <span data-ttu-id="ded98-300">Source : tooallow RDP à partir de n’importe où, référence hello « Tout » est utilisé dans le champ de Source de hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-300">Source – tooallow RDP from anywhere, hello reference “Any” is used in hello Source field.</span></span>
  2. <span data-ttu-id="ded98-301">Service – utiliser hello objet approprié de Service créé précédemment, dans ce cas « RDP AppVM01 », des ports externes hello rediriger l’adresse IP locale toohello serveurs et tooport 3386 (hello par défaut le port RDP).</span><span class="sxs-lookup"><span data-stu-id="ded98-301">Service – use hello appropriate Service Object created earlier, in this case “AppVM01 RDP”, hello external ports redirect toohello servers local IP address and tooport 3386 (hello default RDP port).</span></span> <span data-ttu-id="ded98-302">Cette règle spécifique est pour RDP accès tooAppVM01.</span><span class="sxs-lookup"><span data-stu-id="ded98-302">This specific rule is for RDP access tooAppVM01.</span></span>
  3. <span data-ttu-id="ded98-303">Destination – doit être hello *port local sur les pare-feu hello*, « IP locale DCHP 1 » ou eth0 si vous utilisez des adresses IP statiques.</span><span class="sxs-lookup"><span data-stu-id="ded98-303">Destination – should be hello *local port on hello firewall*, “DCHP 1 Local IP” or eth0 if using static IPs.</span></span> <span data-ttu-id="ded98-304">un nombre ordinal Hello (eth0, eth1, etc.) peut être différent si votre matériel de réseau possède plusieurs interfaces de locales.</span><span class="sxs-lookup"><span data-stu-id="ded98-304">hello ordinal number (eth0, eth1, etc) may be different if your network appliance has multiple local interfaces.</span></span> <span data-ttu-id="ded98-305">Hello port envoie le pare-feu hello à partir de (peut-être même hello comme hello port de réception), destination de routage réelle hello est dans le champ de liste cible hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-305">This is hello port hello firewall is sending out from (may be hello same as hello receiving port), hello actual routed destination is in hello Target List field.</span></span>
  4. <span data-ttu-id="ded98-306">La redirection – cette section explique l’appliance virtuelle hello où tooultimately rediriger ce trafic.</span><span class="sxs-lookup"><span data-stu-id="ded98-306">Redirection – this section tells hello virtual appliance where tooultimately redirect this traffic.</span></span> <span data-ttu-id="ded98-307">redirection de la plus simple de Hello est tooplace hello IP et Port (facultatif) dans le champ de liste cible hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-307">hello simplest redirection is tooplace hello IP and Port (optional) in hello Target List field.</span></span> <span data-ttu-id="ded98-308">Si aucun port n’est le port de destination hello utilisé sur la demande entrante de hello sera utilisé (c.-à-d. aucune traduction), si un port est désigné port de hello sera également NAT, ainsi que les IP hello réponde.</span><span class="sxs-lookup"><span data-stu-id="ded98-308">If no port is used hello destination port on hello inbound request will be used (ie no translation), if a port is designated hello port will also be NAT’d along with hello IP address.</span></span>
     
     <span data-ttu-id="ded98-309">![Règle RDP de pare-feu][11]</span><span class="sxs-lookup"><span data-stu-id="ded98-309">![Firewall RDP Rule][11]</span></span>
     
     <span data-ttu-id="ded98-310">Un total de quatre règles RDP devez toobe créé :</span><span class="sxs-lookup"><span data-stu-id="ded98-310">A total of four RDP rules will need toobe created:</span></span> 
     
     | <span data-ttu-id="ded98-311">Nom de la règle</span><span class="sxs-lookup"><span data-stu-id="ded98-311">Rule Name</span></span> | <span data-ttu-id="ded98-312">Serveur</span><span class="sxs-lookup"><span data-stu-id="ded98-312">Server</span></span> | <span data-ttu-id="ded98-313">de diffusion en continu</span><span class="sxs-lookup"><span data-stu-id="ded98-313">Service</span></span> | <span data-ttu-id="ded98-314">Liste des cibles</span><span class="sxs-lookup"><span data-stu-id="ded98-314">Target List</span></span> |
     | --- | --- | --- | --- |
     | <span data-ttu-id="ded98-315">RDP-vers-IIS01</span><span class="sxs-lookup"><span data-stu-id="ded98-315">RDP-to-IIS01</span></span> |<span data-ttu-id="ded98-316">IIS01</span><span class="sxs-lookup"><span data-stu-id="ded98-316">IIS01</span></span> |<span data-ttu-id="ded98-317">IIS01 RDP</span><span class="sxs-lookup"><span data-stu-id="ded98-317">IIS01 RDP</span></span> |<span data-ttu-id="ded98-318">10.0.1.4:3389</span><span class="sxs-lookup"><span data-stu-id="ded98-318">10.0.1.4:3389</span></span> |
     | <span data-ttu-id="ded98-319">RDP-vers-DNS01</span><span class="sxs-lookup"><span data-stu-id="ded98-319">RDP-to-DNS01</span></span> |<span data-ttu-id="ded98-320">DNS01</span><span class="sxs-lookup"><span data-stu-id="ded98-320">DNS01</span></span> |<span data-ttu-id="ded98-321">DNS01 RDP</span><span class="sxs-lookup"><span data-stu-id="ded98-321">DNS01 RDP</span></span> |<span data-ttu-id="ded98-322">10.0.2.4:3389</span><span class="sxs-lookup"><span data-stu-id="ded98-322">10.0.2.4:3389</span></span> |
     | <span data-ttu-id="ded98-323">RDP 0 AppVM01</span><span class="sxs-lookup"><span data-stu-id="ded98-323">RDP-to-AppVM01</span></span> |<span data-ttu-id="ded98-324">AppVM01</span><span class="sxs-lookup"><span data-stu-id="ded98-324">AppVM01</span></span> |<span data-ttu-id="ded98-325">RDP AppVM01</span><span class="sxs-lookup"><span data-stu-id="ded98-325">AppVM01 RDP</span></span> |<span data-ttu-id="ded98-326">10.0.2.5:3389</span><span class="sxs-lookup"><span data-stu-id="ded98-326">10.0.2.5:3389</span></span> |
     | <span data-ttu-id="ded98-327">RDP-vers-AppVM02</span><span class="sxs-lookup"><span data-stu-id="ded98-327">RDP-to-AppVM02</span></span> |<span data-ttu-id="ded98-328">AppVM02</span><span class="sxs-lookup"><span data-stu-id="ded98-328">AppVM02</span></span> |<span data-ttu-id="ded98-329">AppVm02 RDP</span><span class="sxs-lookup"><span data-stu-id="ded98-329">AppVm02 RDP</span></span> |<span data-ttu-id="ded98-330">10.0.2.6:3389</span><span class="sxs-lookup"><span data-stu-id="ded98-330">10.0.2.6:3389</span></span> |

> [!TIP]
> <span data-ttu-id="ded98-331">Restreindre les résultats de portée hello Hello Source et les champs Service réduira la surface d’attaque hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-331">Narrowing down hello scope of hello Source and Service fields will reduce hello attack surface.</span></span> <span data-ttu-id="ded98-332">étendue de Hello plus limitée qui permettra de fonctionnalité doit être utilisée.</span><span class="sxs-lookup"><span data-stu-id="ded98-332">hello most limited scope that will allow functionality should be used.</span></span>
> 
> 

* <span data-ttu-id="ded98-333">**Règles de trafic d’application**: il existe deux règles de trafic d’Application, hello tout d’abord pour le trafic web de serveur frontal hello et hello seconde pour le trafic de back-end hello (par exemple, niveau serveur web toodata).</span><span class="sxs-lookup"><span data-stu-id="ded98-333">**Application Traffic Rules**: There are two Application Traffic Rules, hello first for hello front end web traffic, and hello second for hello back end traffic (eg web server toodata tier).</span></span> <span data-ttu-id="ded98-334">Ces règles dépendent de l’architecture en réseau hello (où sont placés vos serveurs) et flux de trafic (le trafic hello direction du flux, et quels ports sont utilisés).</span><span class="sxs-lookup"><span data-stu-id="ded98-334">These rules will depend on hello network architecture (where your servers are placed) and traffic flows (which direction hello traffic flows, and which ports are used).</span></span>
  
    <span data-ttu-id="ded98-335">Tout d’abord indiqué est règle de serveur frontal hello pour le trafic web :</span><span class="sxs-lookup"><span data-stu-id="ded98-335">First discussed is hello front end rule for web traffic:</span></span>
  
    <span data-ttu-id="ded98-336">![Règle web de pare-feu][12]</span><span class="sxs-lookup"><span data-stu-id="ded98-336">![Firewall Web Rule][12]</span></span>
  
    <span data-ttu-id="ded98-337">Cette règle NAT de Destination permet de serveur d’applications hello application réelle du trafic tooreach hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-337">This Destination NAT rule allows hello actual application traffic tooreach hello application server.</span></span> <span data-ttu-id="ded98-338">Alors que hello autres règles permettent de sécurité, de gestion, etc., règles d’Application sont ce qu’Autoriser tooaccess d’utilisateurs ou des services externes ou les applications hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-338">While hello other rules allow for security, management, etc., Application Rules are what allow external users or services tooaccess hello application(s).</span></span> <span data-ttu-id="ded98-339">Pour cet exemple, il existe un serveur web sur le port 80, par conséquent hello seule application règle de pare-feu redirige le trafic entrant toohello adresse IP externe, interne adresse IP des serveurs toohello web.</span><span class="sxs-lookup"><span data-stu-id="ded98-339">For this example, there is a single web server on port 80, thus hello single firewall application rule will redirect inbound traffic toohello external IP, toohello web servers internal IP address.</span></span>
  
    <span data-ttu-id="ded98-340">**Remarque**: qu’il n’existe aucun port assigné dans le champ de liste cible hello, donc hello entrants port 80 (ou 443 pour hello Service sélectionné) sera utilisé dans la redirection de hello du serveur web de hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-340">**Note**: that there is no port assigned in hello Target List field, thus hello inbound port 80 (or 443 for hello Service selected) will be used in hello redirection of hello web server.</span></span> <span data-ttu-id="ded98-341">Si le serveur web de hello est à l’écoute sur un port différent, par exemple le port 8080, champ de liste cible hello peut-être tooallow too10.0.1.4:8080 mis à jour pour la redirection de Port hello également.</span><span class="sxs-lookup"><span data-stu-id="ded98-341">If hello web server is listening on a different port, for example port 8080, hello Target List field could be updated too10.0.1.4:8080 tooallow for hello Port redirection as well.</span></span>
  
    <span data-ttu-id="ded98-342">Hello règle de trafic d’Application suivant hello règle tooallow hello Web Server tootalk toohello AppVM01 le serveur principal (mais pas AppVM02) via un service :</span><span class="sxs-lookup"><span data-stu-id="ded98-342">hello next Application Traffic Rule is hello back end rule tooallow hello Web Server tootalk toohello AppVM01 server (but not AppVM02) via Any service:</span></span>
  
    <span data-ttu-id="ded98-343">![Règle AppVM01 de pare-feu][13]</span><span class="sxs-lookup"><span data-stu-id="ded98-343">![Firewall AppVM01 Rule][13]</span></span>
  
    <span data-ttu-id="ded98-344">Cette règle passe permet de n’importe quel serveur IIS sur Bonjour frontal sous-réseau tooreach Bonjour AppVM01 (adresse IP 10.0.2.5) sur n’importe quel port, à l’aide de toutes les données de tooaccess de protocole requises par l’application web de hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-344">This Pass rule allows any IIS server on hello Frontend subnet tooreach hello AppVM01 (IP Address 10.0.2.5) on Any port, using any Protocol tooaccess data needed by hello web application.</span></span>
  
    <span data-ttu-id="ded98-345">Dans cette capture d’écran une «\<explicite-dest\>» est utilisé comme destination de hello dans hello Destination champ toosignify 10.0.2.5.</span><span class="sxs-lookup"><span data-stu-id="ded98-345">In this screen shot an "\<explicit-dest\>" is used in hello Destination field toosignify 10.0.2.5 as hello destination.</span></span> <span data-ttu-id="ded98-346">Il peut s’agir soit nommé explicite du comme illustré, ou un objet de réseau (tel qu’il a été effectuée dans les conditions préalables de hello pour le serveur DNS de hello).</span><span class="sxs-lookup"><span data-stu-id="ded98-346">This could be either explicit as shown or a named Network Object (as was done in hello prerequisites for hello DNS server).</span></span> <span data-ttu-id="ded98-347">Il est administrateur toohello du pare-feu de hello comme la méthode toowhich sera utilisée.</span><span class="sxs-lookup"><span data-stu-id="ded98-347">This is up toohello administrator of hello firewall as toowhich method will be used.</span></span> <span data-ttu-id="ded98-348">tooadd 10.0.2.5 comme un Explict Desitnation, double-cliquez sur la première ligne vide hello sous \<explicite-dest\> et entrez l’adresse de hello dans la fenêtre hello qui s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ded98-348">tooadd 10.0.2.5 as an Explict Desitnation, double-click on hello first blank row under \<explicit-dest\> and enter hello address in hello window that pops up.</span></span>
  
    <span data-ttu-id="ded98-349">Cette règle passer aucun NAT n’est nécessaire car il s’agit le trafic interne, donc hello méthode de connexion peut être défini trop « No SNAT ».</span><span class="sxs-lookup"><span data-stu-id="ded98-349">With this Pass Rule, no NAT is needed since this is internal traffic, so hello Connection Method can be set too"No SNAT".</span></span>
  
    <span data-ttu-id="ded98-350">**Remarque**: réseau Source de hello dans cette règle est n’importe quelle ressource de sous-réseau frontal hello si il sera uniquement un, ou un nombre connu spécifique de serveurs web, un objet réseau de ressource peut être créé toobe plus toothose exacte des adresses IP spécifiques à la place de tout sous-réseau du serveur frontal Hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-350">**Note**: hello Source network in this rule is any resource on hello FrontEnd subnet, if there will only be one, or a known specific number of web servers, a Network Object resource could be created toobe more specific toothose exact IP addresses instead of hello entire Frontend subnet.</span></span>

> [!TIP]
> <span data-ttu-id="ded98-351">Cette règle utilise le service hello « Any » toomake hello toosetup plus facile d’application exemple et utiliser, cela vous permet également de ICMPv4 (ping) dans une seule règle.</span><span class="sxs-lookup"><span data-stu-id="ded98-351">This rule uses hello service “Any” toomake hello sample application easier toosetup and use, this will also allow ICMPv4 (ping) in a single rule.</span></span> <span data-ttu-id="ded98-352">Toutefois, cela n’est pas recommandé.</span><span class="sxs-lookup"><span data-stu-id="ded98-352">However, this is not a recommended practice.</span></span> <span data-ttu-id="ded98-353">ports de Hello et protocoles (« Services ») doivent être filtrés toohello possible minimale qui permet la surface d’attaque application opération tooreduce hello sur cette limite.</span><span class="sxs-lookup"><span data-stu-id="ded98-353">hello ports and protocols (“Services”) should be narrowed toohello minimum possible that allows application operation tooreduce hello attack surface across this boundary.</span></span>
> 
> 

<br />

> [!TIP]
> <span data-ttu-id="ded98-354">Bien que cette règle indique une référence explicite-dest utilisée, une approche cohérente doit être utilisée dans la configuration du pare-feu hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-354">Although this rule shows an explicit-dest reference being used, a consistent approach should be used throughout hello firewall configuration.</span></span> <span data-ttu-id="ded98-355">Il est recommandé d’utiliser tout au long de ce hello nommé d’objet réseau pour faciliter la lisibilité et la prise en charge.</span><span class="sxs-lookup"><span data-stu-id="ded98-355">It is recommended that hello named Network Object be used throughout for easier readability and supportability.</span></span> <span data-ttu-id="ded98-356">Hello explicite-dest est utilisé ici tooshow d’uniquement une méthode autre référence et n’est généralement pas recommandé (en particulier pour des configurations complexes).</span><span class="sxs-lookup"><span data-stu-id="ded98-356">hello explicit-dest is used here only tooshow an alternative reference method and is not generally recommended (especially for complex configurations).</span></span>
> 
> 

* <span data-ttu-id="ded98-357">**Sortant tooInternet règle**: passer ce règle autorise le trafic à partir de n’importe quel réseau toopass toohello sélectionné Destination réseaux Source.</span><span class="sxs-lookup"><span data-stu-id="ded98-357">**Outbound tooInternet Rule**: This Pass rule will allow traffic from any Source network toopass toohello selected Destination networks.</span></span> <span data-ttu-id="ded98-358">Cette règle est une règle par défaut généralement déjà sur le pare-feu Barracuda NextGen hello, mais il est dans un état désactivé.</span><span class="sxs-lookup"><span data-stu-id="ded98-358">This rule is a default rule usually already on hello Barracuda NextGen firewall, but is in a disabled state.</span></span> <span data-ttu-id="ded98-359">Vous pouvez accéder à hello activer la règle commande en cliquant sur cette règle.</span><span class="sxs-lookup"><span data-stu-id="ded98-359">Right-clicking on this rule can access hello Activate Rule command.</span></span> <span data-ttu-id="ded98-360">règle Hello ci-après a été modifiée tooadd hello deux sous-réseaux locaux qui ont été créés en tant que références dans la section Configuration requise de hello de cet attribut de Source de document toohello de cette règle.</span><span class="sxs-lookup"><span data-stu-id="ded98-360">hello rule shown here has been modified tooadd hello two local subnets that were created as references in hello prerequisite section of this document toohello Source attribute of this rule.</span></span>
  
    <span data-ttu-id="ded98-361">![Règle de trafic sortant de pare-feu][14]</span><span class="sxs-lookup"><span data-stu-id="ded98-361">![Firewall Outbound Rule][14]</span></span>
* <span data-ttu-id="ded98-362">**Règle de DNS**: règle de passer ce permet uniquement serveur DNS de toohello de toopass DNS (port 53) le trafic.</span><span class="sxs-lookup"><span data-stu-id="ded98-362">**DNS Rule**: This Pass rule allows only DNS (port 53) traffic toopass toohello DNS server.</span></span> <span data-ttu-id="ded98-363">Pour cet environnement, la plupart du trafic à partir de hello frontal toohello back-end est bloqué, cette règle permet en particulier DNS.</span><span class="sxs-lookup"><span data-stu-id="ded98-363">For this environment most traffic from hello FrontEnd toohello BackEnd is blocked, this rule specifically allows DNS.</span></span>
  
    <span data-ttu-id="ded98-364">![Règle DNS de pare-feu][15]</span><span class="sxs-lookup"><span data-stu-id="ded98-364">![Firewall DNS Rule][15]</span></span>
  
    <span data-ttu-id="ded98-365">**Remarque**: dans cet écran hello shot méthode de connexion est inclus.</span><span class="sxs-lookup"><span data-stu-id="ded98-365">**Note**: In this screen shot hello Connection Method is included.</span></span> <span data-ttu-id="ded98-366">Étant donné que cette règle est interne toointernal IP adresse du trafic IP, aucune utilisation n’est requise, cette hello méthode de connexion est trop « No SNAT » pour cette règle de test.</span><span class="sxs-lookup"><span data-stu-id="ded98-366">Because this rule is for internal IP toointernal IP address traffic, no NATing is required, this hello Connection Method is set too“No SNAT” for this Pass rule.</span></span>
* <span data-ttu-id="ded98-367">**Sous-réseau tooSubnet règle**: passer cette règle est une règle par défaut qui a été activée et tooallow modifiée n’importe quel serveur sur hello précédent se terminent par serveur de sous-réseau tooconnect tooany hello sous-réseau du serveur frontal.</span><span class="sxs-lookup"><span data-stu-id="ded98-367">**Subnet tooSubnet Rule**: This Pass rule is a default rule that has been activated and modified tooallow any server on hello back end subnet tooconnect tooany server on hello front end subnet.</span></span> <span data-ttu-id="ded98-368">Cette règle étant le trafic interne tout hello méthode de connexion peut être définie tooNo SNAT.</span><span class="sxs-lookup"><span data-stu-id="ded98-368">This rule is all internal traffic so hello Connection Method can be set tooNo SNAT.</span></span>
  
    <span data-ttu-id="ded98-369">![Règle Intra-réseau virtuel de pare-feu][16]</span><span class="sxs-lookup"><span data-stu-id="ded98-369">![Firewall Intra-VNet Rule][16]</span></span>
  
    <span data-ttu-id="ded98-370">**Remarque**: case à cocher hello bidirectionnelle n’est pas vérifiée (et n’est pas activée dans la plupart des règles), c’est important pour cette règle, elle rend cette règle « une seule direction », une connexion peut être lancée à partir de réseau de serveur frontal hello back-end sous-réseau toohello, mais pas hello inverse.</span><span class="sxs-lookup"><span data-stu-id="ded98-370">**Note**: hello Bi-directional checkbox is not checked (nor is it checked in most rules), this is significant for this rule in that it makes this rule “one directional”, a connection can be initiated from hello back end subnet toohello front end network, but not hello reverse.</span></span> <span data-ttu-id="ded98-371">Si cette case à cocher est activée, cette règle permet le trafic bidirectionnel, ce qui n’est pas souhaitable pour notre diagramme logique.</span><span class="sxs-lookup"><span data-stu-id="ded98-371">If that checkbox was checked, this rule would enable bi-directional traffic, which from our logical diagram is not desired.</span></span>
* <span data-ttu-id="ded98-372">**Refuser toutes les règles de trafic**: cela doit toujours être règle finale de hello (en termes de priorité), et par conséquent si un trafic acheminé échoue toomatch des hello précédant les règles qu’il ne sera supprimé par cette règle.</span><span class="sxs-lookup"><span data-stu-id="ded98-372">**Deny All Traffic Rule**: This should always be hello final rule (in terms of priority), and as such if a traffic flows fails toomatch any of hello preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="ded98-373">Il s’agit d’une règle par défaut qui est en général activée, et en général, aucune modification n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ded98-373">This is a default rule and usually activated, no modifications are generally needed.</span></span> 
  
    <span data-ttu-id="ded98-374">![Règle de refus de pare-feu][17]</span><span class="sxs-lookup"><span data-stu-id="ded98-374">![Firewall Deny Rule][17]</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ded98-375">Une fois que tous les hello au-dessus de règles sont créées, il est important priorité hello tooreview chacun le trafic tooensure de règle sera autorisée ou refusée comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="ded98-375">Once all of hello above rules are created, it’s important tooreview hello priority of each rule tooensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="ded98-376">Pour cet exemple, les règles de hello sont dans l’ordre de hello qu'ils doivent apparaître dans la grille principale règles Bonjour Client de gestion Barracuda de transfert de hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-376">For this example, hello rules are in hello order they should appear in hello Main Grid of forwarding rules in hello Barracuda Management Client.</span></span>
> 
> 

## <a name="rule-activation"></a><span data-ttu-id="ded98-377">Activation d’une règle</span><span class="sxs-lookup"><span data-stu-id="ded98-377">Rule Activation</span></span>
<span data-ttu-id="ded98-378">Hello ruleset modifiée toohello spécification de diagramme logique de hello, hello ruleset doit être téléchargé toohello pare-feu et puis activé.</span><span class="sxs-lookup"><span data-stu-id="ded98-378">With hello ruleset modified toohello specification of hello logic diagram, hello ruleset must be uploaded toohello firewall and then activated.</span></span>

<span data-ttu-id="ded98-379">![Activation de règle de pare-feu][18]</span><span class="sxs-lookup"><span data-stu-id="ded98-379">![Firewall Rule Activation][18]</span></span>

<span data-ttu-id="ded98-380">Dans l’angle supérieur droit de hello du client de gestion hello sont un cluster de boutons.</span><span class="sxs-lookup"><span data-stu-id="ded98-380">In hello upper right hand corner of hello management client are a cluster of buttons.</span></span> <span data-ttu-id="ded98-381">Cliquez sur hello « envoyer des modifications » bouton toosend hello modifié règles toohello pare-feu, puis cliquez sur le bouton « Activer » de hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-381">Click hello “Send Changes” button toosend hello modified rules toohello firewall, then click hello “Activate” button.</span></span>

<span data-ttu-id="ded98-382">L’activation de l’ensemble de règles de pare-feu hello hello cette build d’environnement exemple est terminée.</span><span class="sxs-lookup"><span data-stu-id="ded98-382">With hello activation of hello firewall ruleset this example environment build is complete.</span></span>

## <a name="traffic-scenarios"></a><span data-ttu-id="ded98-383">Scénarios de trafic</span><span class="sxs-lookup"><span data-stu-id="ded98-383">Traffic Scenarios</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ded98-384">Une clé takeway est tooremember qui **tous les** trafic proviendront via le pare-feu hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-384">A key takeway is tooremember that **all** traffic will come through hello firewall.</span></span> <span data-ttu-id="ded98-385">C’est le cas toohello de bureau tooremote IIS01 server, même s’il est Bonjour Service de Cloud Front End et de sous-réseau frontal hello tooaccess ce serveur, nous devons tooRDP toohello pare-feu sur port 8014 et laissez demande RDP hello pare-feu tooroute hello en interne toohello IIS01 le Port RDP.</span><span class="sxs-lookup"><span data-stu-id="ded98-385">So tooremote desktop toohello IIS01 server, even though it's in hello Front End Cloud Service and on hello Front End subnet, tooaccess this server we will need tooRDP toohello firewall on port 8014, and then allow hello firewall tooroute hello RDP request internally toohello IIS01 RDP Port.</span></span> <span data-ttu-id="ded98-386">Hello « Se connecter » du portail Azure bouton ne fonctionne pas, car il n’existe aucun tooIIS01 de chemin d’accès RDP direct (pour autant que le portail de hello peut voir).</span><span class="sxs-lookup"><span data-stu-id="ded98-386">hello Azure portal's "Connect" button won't work because there is no direct RDP path tooIIS01 (as far as hello portal can see).</span></span> <span data-ttu-id="ded98-387">Cela signifie que toutes les connexions à partir de hello internet seront toohello Service de sécurité et un Port, par exemple, secscv001.cloudapp.net:xxxx.</span><span class="sxs-lookup"><span data-stu-id="ded98-387">This means all connections from hello internet will be toohello Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx.</span></span>
> 
> 

<span data-ttu-id="ded98-388">Pour ces scénarios, hello suivant les règles de pare-feu doit être en place :</span><span class="sxs-lookup"><span data-stu-id="ded98-388">For these scenarios, hello following firewall rules should be in place:</span></span>

1. <span data-ttu-id="ded98-389">Gestion de pare-feu</span><span class="sxs-lookup"><span data-stu-id="ded98-389">Firewall Management</span></span>
2. <span data-ttu-id="ded98-390">RDP tooIIS01</span><span class="sxs-lookup"><span data-stu-id="ded98-390">RDP tooIIS01</span></span>
3. <span data-ttu-id="ded98-391">RDP tooDNS01</span><span class="sxs-lookup"><span data-stu-id="ded98-391">RDP tooDNS01</span></span>
4. <span data-ttu-id="ded98-392">RDP tooAppVM01</span><span class="sxs-lookup"><span data-stu-id="ded98-392">RDP tooAppVM01</span></span>
5. <span data-ttu-id="ded98-393">RDP tooAppVM02</span><span class="sxs-lookup"><span data-stu-id="ded98-393">RDP tooAppVM02</span></span>
6. <span data-ttu-id="ded98-394">Toohello du trafic de l’application Web</span><span class="sxs-lookup"><span data-stu-id="ded98-394">App Traffic toohello Web</span></span>
7. <span data-ttu-id="ded98-395">Le trafic d’application tooAppVM01</span><span class="sxs-lookup"><span data-stu-id="ded98-395">App Traffic tooAppVM01</span></span>
8. <span data-ttu-id="ded98-396">Sortant toohello Internet</span><span class="sxs-lookup"><span data-stu-id="ded98-396">Outbound toohello Internet</span></span>
9. <span data-ttu-id="ded98-397">Serveur frontal tooDNS01</span><span class="sxs-lookup"><span data-stu-id="ded98-397">Frontend tooDNS01</span></span>
10. <span data-ttu-id="ded98-398">Trafic intra-sous-réseau (fin de toofront back-end uniquement)</span><span class="sxs-lookup"><span data-stu-id="ded98-398">Intra-Subnet Traffic (back end toofront end only)</span></span>
11. <span data-ttu-id="ded98-399">Refuser tout</span><span class="sxs-lookup"><span data-stu-id="ded98-399">Deny All</span></span>

<span data-ttu-id="ded98-400">groupe de règles de pare-feu Hello aura probablement bien d’autres règles dans toothese d’addition, règles hello sur n’importe quel pare-feu donné aura également les numéros de priorité différents que ceux répertoriés ici hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-400">hello actual firewall ruleset will most likely have many other rules in addition toothese, hello rules on any given firewall will also have different priority numbers than hello ones listed here.</span></span> <span data-ttu-id="ded98-401">Cette liste et les numéros associés sont pertinence tooprovide entre simplement ces onze règles et la priorité relative de hello entre elles.</span><span class="sxs-lookup"><span data-stu-id="ded98-401">This list and associated numbers are tooprovide relevance between just these eleven rules and hello relative priority amongst them.</span></span> <span data-ttu-id="ded98-402">En d’autres termes ; sur le pare-feu hello, hello « RDP tooIIS01 » peut être le numéro de la règle 5, mais à condition qu’il soit sous la règle de « Gestion de pare-feu » hello et versions ultérieures de la règle de « RDP tooDNS01 » hello qu'elle est alignée avec intention de hello de cette liste.</span><span class="sxs-lookup"><span data-stu-id="ded98-402">In other words; on hello actual firewall, hello “RDP tooIIS01” may be rule number 5, but as long as it’s below hello “Firewall Management” rule and above hello “RDP tooDNS01” rule it would align with hello intention of this list.</span></span> <span data-ttu-id="ded98-403">liste de Hello vous aide également Bonjour ci-dessous scénarios permettant le souci de concision ; par exemple « Règle de pare-feu 9 (DNS) ».</span><span class="sxs-lookup"><span data-stu-id="ded98-403">hello list will also aid in hello below scenarios allowing brevity; e.g. “FW Rule 9 (DNS)”.</span></span> <span data-ttu-id="ded98-404">Également par souci de concision, hello quatre règles RDP sera collectivement appelés, « hello règles RDP » lorsque le scénario de trafic hello est tooRDP non liée.</span><span class="sxs-lookup"><span data-stu-id="ded98-404">Also for brevity, hello four RDP rules will be collectively called, “hello RDP rules” when hello traffic scenario is unrelated tooRDP.</span></span>

<span data-ttu-id="ded98-405">Rappelez-vous également que les groupes de sécurité réseau sont sur place pour le trafic internet entrant sur hello frontal et principal des sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="ded98-405">Also recall that Network Security Groups are in-place for inbound internet traffic on hello Frontend and Backend subnets.</span></span>

#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="ded98-406">(Autorisé) Internet tooWeb Server</span><span class="sxs-lookup"><span data-stu-id="ded98-406">(Allowed) Internet tooWeb Server</span></span>
1. <span data-ttu-id="ded98-407">Un utilisateur Internet demande une page HTTP en provenance de SecSvc001.CloudApp.Net (Service cloud Internet)</span><span class="sxs-lookup"><span data-stu-id="ded98-407">Internet user requests HTTP page from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="ded98-408">Cloud service transmet le trafic via le point de terminaison ouvert sur l’interface toofirewall le port 80 sur 10.0.0.4:80</span><span class="sxs-lookup"><span data-stu-id="ded98-408">Cloud service passes traffic through open endpoint on port 80 toofirewall interface on 10.0.0.4:80</span></span>
3. <span data-ttu-id="ded98-409">Aucun groupe de sécurité réseau n’assigné tooSecurity sous-réseau, afin d’autorisent les règles du groupe de sécurité réseau système toofirewall de trafic</span><span class="sxs-lookup"><span data-stu-id="ded98-409">No NSG assigned tooSecurity subnet, so system NSG rules allow traffic toofirewall</span></span>
4. <span data-ttu-id="ded98-410">Le trafic atteint l’adresse IP interne du pare-feu de hello (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="ded98-410">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="ded98-411">Le pare-feu commence le traitement de la règle :</span><span class="sxs-lookup"><span data-stu-id="ded98-411">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="ded98-412">FW règle 1 (FW Mgmt) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-412">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="ded98-413">Règles 2 à 5 (règles RDP) ne s’appliquent, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-413">FW Rules 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="ded98-414">FW règle 6 (application : Web) s’applique, le trafic est autorisé, un pare-feu NAT il too10.0.1.4 (IIS01)</span><span class="sxs-lookup"><span data-stu-id="ded98-414">FW Rule 6 (App: Web) does apply, traffic is allowed, firewall NATs it too10.0.1.4 (IIS01)</span></span>
6. <span data-ttu-id="ded98-415">sous-réseau du serveur frontal Hello commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="ded98-415">hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="ded98-416">NSG règle 1 (bloc Internet) ne s’applique pas (ce trafic a été NAT serait par le pare-feu hello, donc hello adresse source est maintenant pare-feu hello qui se trouve sur le sous-réseau de sécurité hello et visibles par le sous-réseau du serveur frontal hello trafic de groupe de sécurité réseau toobe « local » et est donc autorisé), déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-416">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by hello firewall, thus hello source address is now hello firewall which is on hello Security subnet and seen by hello Frontend subnet NSG toobe “local” traffic and is thus allowed), move toonext rule</span></span>
   2. <span data-ttu-id="ded98-417">Règles du groupe de sécurité réseau par défaut autoriser le trafic de toosubnet de sous-réseau, le trafic est autorisé, d’arrêter le traitement des règles de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="ded98-417">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="ded98-418">IIS01 écoute pour le trafic web, reçoit la requête et démarre le traitement de demande de hello</span><span class="sxs-lookup"><span data-stu-id="ded98-418">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
8. <span data-ttu-id="ded98-419">IIS01 tente tooinitiates un tooAppVM01 de session FTP sur le sous-réseau du serveur principal</span><span class="sxs-lookup"><span data-stu-id="ded98-419">IIS01 attempts tooinitiates an FTP session tooAppVM01 on Backend subnet</span></span>
9. <span data-ttu-id="ded98-420">itinéraire UDR Hello sur le sous-réseau frontal rend le saut suivant de hello pare-feu hello</span><span class="sxs-lookup"><span data-stu-id="ded98-420">hello UDR route on Frontend subnet makes hello firewall hello next hop</span></span>
10. <span data-ttu-id="ded98-421">Aucune règle sur le trafic sortant sur le sous-réseau du serveur frontal. Le trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="ded98-421">No outbound rules on Frontend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="ded98-422">Le pare-feu commence le traitement de la règle :</span><span class="sxs-lookup"><span data-stu-id="ded98-422">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="ded98-423">FW règle 1 (FW Mgmt) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-423">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="ded98-424">FW règle 2-5 (règles RDP) ne s’appliquent pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-424">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
    3. <span data-ttu-id="ded98-425">FW règle 6 (application : Web) ne s’appliquent, déplacez la règle de toonext</span><span class="sxs-lookup"><span data-stu-id="ded98-425">FW Rule 6 (App: Web) doesn’t apply, move toonext rule</span></span>
    4. <span data-ttu-id="ded98-426">La règle 7 FW (application : back-end) s’applique, le trafic est autorisé, le pare-feu transmet le trafic too10.0.2.5 (AppVM01)</span><span class="sxs-lookup"><span data-stu-id="ded98-426">FW Rule 7 (App: Backend) does apply, traffic is allowed, firewall forwards traffic too10.0.2.5 (AppVM01)</span></span>
12. <span data-ttu-id="ded98-427">sous-réseau du serveur principal Hello commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="ded98-427">hello Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="ded98-428">Groupe de sécurité réseau règle 1 (bloc Internet) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-428">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="ded98-429">Règles du groupe de sécurité réseau par défaut autoriser le trafic de toosubnet de sous-réseau, le trafic est autorisé, d’arrêter le traitement des règles de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="ded98-429">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
13. <span data-ttu-id="ded98-430">AppVM01 reçoit la demande de hello et lance la session de hello et répond</span><span class="sxs-lookup"><span data-stu-id="ded98-430">AppVM01 receives hello request and initiates hello session and responds</span></span>
14. <span data-ttu-id="ded98-431">itinéraire UDR Hello sur le sous-réseau du serveur principal effectue le saut suivant de hello pare-feu hello</span><span class="sxs-lookup"><span data-stu-id="ded98-431">hello UDR route on Backend subnet makes hello firewall hello next hop</span></span>
15. <span data-ttu-id="ded98-432">Dans la mesure où il n’y a aucune règle de groupe de sécurité réseau sortant sur hello réponse de hello sous-réseau principal n’est autorisé.</span><span class="sxs-lookup"><span data-stu-id="ded98-432">Since there are no outbound NSG rules on hello Backend subnet hello response is allowed</span></span>
16. <span data-ttu-id="ded98-433">Car cela retourne le trafic sur un pare-feu de hello session établie passe serveur web (IIS01) de hello réponse toohello précédent</span><span class="sxs-lookup"><span data-stu-id="ded98-433">Because this is returning traffic on an established session hello firewall passes hello response back toohello web server (IIS01)</span></span>
17. <span data-ttu-id="ded98-434">Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="ded98-434">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="ded98-435">Groupe de sécurité réseau règle 1 (bloc Internet) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-435">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="ded98-436">Règles du groupe de sécurité réseau par défaut autoriser le trafic de toosubnet de sous-réseau, le trafic est autorisé, d’arrêter le traitement des règles de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="ded98-436">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
18. <span data-ttu-id="ded98-437">Hello IIS reçoit la réponse de hello, termine la transaction hello avec AppVM01 et puis termine la construction hello réponse HTTP, cette réponse HTTP est envoyée toohello demandeur</span><span class="sxs-lookup"><span data-stu-id="ded98-437">hello IIS server receives hello response, completes hello transaction with AppVM01, and then completes building hello HTTP response, this HTTP response is sent toohello requestor</span></span>
19. <span data-ttu-id="ded98-438">Dans la mesure où il n’y a aucune règle de groupe de sécurité réseau sortant sur hello réponse de hello sous-réseau frontal n’est autorisée.</span><span class="sxs-lookup"><span data-stu-id="ded98-438">Since there are no outbound NSG rules on hello Frontend subnet hello response is allowed</span></span>
20. <span data-ttu-id="ded98-439">Hello HTTP réponse accès hello pare-feu et car il s’agit de hello tooan de réponse établie session NAT est acceptée par le pare-feu hello</span><span class="sxs-lookup"><span data-stu-id="ded98-439">hello HTTP response hits hello firewall, and because this is hello response tooan established NAT session is accepted by hello firewall</span></span>
21. <span data-ttu-id="ded98-440">les pare-feu Hello redirige ensuite hello réponse toohello précédent utilisateur Internet</span><span class="sxs-lookup"><span data-stu-id="ded98-440">hello firewall then redirects hello response back toohello Internet User</span></span>
22. <span data-ttu-id="ded98-441">Dans la mesure où aucune des règles de groupe de sécurité réseau sortantes ou les sauts UDR sur le sous-réseau du serveur frontal hello réponse de hello est autorisé et hello utilisateur Internet reçoit hello web page est demandée.</span><span class="sxs-lookup"><span data-stu-id="ded98-441">Since there are no outbound NSG rules or UDR hops on hello Frontend subnet hello response is allowed, and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-internet-rdp-toobackend"></a><span data-ttu-id="ded98-442">(Autorisé) Internet RDP tooBackend</span><span class="sxs-lookup"><span data-stu-id="ded98-442">(Allowed) Internet RDP tooBackend</span></span>
1. <span data-ttu-id="ded98-443">Administrateur du serveur sur internet demande tooAppVM01 de session RDP via SecSvc001.CloudApp.Net:8025, où 8025 est numéro de port hello utilisateur affecté pour la règle de pare-feu « RDP tooAppVM01 » hello</span><span class="sxs-lookup"><span data-stu-id="ded98-443">Server Admin on internet requests RDP session tooAppVM01 via SecSvc001.CloudApp.Net:8025, where 8025 is hello user assigned port number for hello “RDP tooAppVM01” firewall rule</span></span>
2. <span data-ttu-id="ded98-444">service de cloud computing Hello transmet le trafic via le point de terminaison ouvert hello sur interface toofirewall port 8025 10.0.0.4:8025</span><span class="sxs-lookup"><span data-stu-id="ded98-444">hello cloud service passes traffic through hello open endpoint on port 8025 toofirewall interface on 10.0.0.4:8025</span></span>
3. <span data-ttu-id="ded98-445">Aucun groupe de sécurité réseau n’assigné tooSecurity sous-réseau, afin d’autorisent les règles du groupe de sécurité réseau système toofirewall de trafic</span><span class="sxs-lookup"><span data-stu-id="ded98-445">No NSG assigned tooSecurity subnet, so system NSG rules allow traffic toofirewall</span></span>
4. <span data-ttu-id="ded98-446">Le pare-feu commence le traitement de la règle :</span><span class="sxs-lookup"><span data-stu-id="ded98-446">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="ded98-447">FW règle 1 (FW Mgmt) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-447">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="ded98-448">FW règle 2 (RDP IIS) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-448">FW Rule 2 (RDP IIS) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="ded98-449">FW règle 3 (DNS01 RDP) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-449">FW Rule 3 (RDP DNS01) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="ded98-450">FW règle 4 (AppVM01 RDP) s’applique, le trafic est autorisé, un pare-feu NAT il too10.0.2.5:3386 (port RDP sur AppVM01)</span><span class="sxs-lookup"><span data-stu-id="ded98-450">FW Rule 4 (RDP AppVM01) does apply, traffic is allowed, firewall NATs it too10.0.2.5:3386 (RDP port on AppVM01)</span></span>
5. <span data-ttu-id="ded98-451">sous-réseau du serveur principal Hello commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="ded98-451">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="ded98-452">NSG règle 1 (bloc Internet) ne s’applique pas (ce trafic a été NAT serait par le pare-feu hello, donc hello adresse source est maintenant pare-feu hello qui se trouve sur le sous-réseau de sécurité hello et visibles par le sous-réseau principal de hello trafic de groupe de sécurité réseau toobe « local » et est donc autorisé), déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-452">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by hello firewall, thus hello source address is now hello firewall which is on hello Security subnet and seen by hello Backend subnet NSG toobe “local” traffic and is thus allowed), move toonext rule</span></span>
   2. <span data-ttu-id="ded98-453">Règles du groupe de sécurité réseau par défaut autoriser le trafic de toosubnet de sous-réseau, le trafic est autorisé, d’arrêter le traitement des règles de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="ded98-453">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="ded98-454">AppVM01 est à l’écoute du trafic RDP et répond</span><span class="sxs-lookup"><span data-stu-id="ded98-454">AppVM01 is listening for RDP traffic and responds</span></span>
7. <span data-ttu-id="ded98-455">En l’absence de règle NSG sur le trafic sortant, les règles par défaut s’appliquent et le retour de trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="ded98-455">With no outbound NSG rules, default rules apply and return traffic is allowed</span></span>
8. <span data-ttu-id="ded98-456">Pare-feu de toohello UDR itinéraires du trafic sortant en tant que tronçon suivant de hello</span><span class="sxs-lookup"><span data-stu-id="ded98-456">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
9. <span data-ttu-id="ded98-457">Car cela retourne le trafic sur un pare-feu de hello session établie passe utilisateur internet de hello réponse toohello précédent</span><span class="sxs-lookup"><span data-stu-id="ded98-457">Because this is returning traffic on an established session hello firewall passes hello response back toohello internet user</span></span>
10. <span data-ttu-id="ded98-458">La Session RDP est activée.</span><span class="sxs-lookup"><span data-stu-id="ded98-458">RDP session is enabled</span></span>
11. <span data-ttu-id="ded98-459">AppVM01 demande le mot de passe utilisateur</span><span class="sxs-lookup"><span data-stu-id="ded98-459">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="ded98-460">(Autorisé) recherche DNS du serveur web sur le serveur DNS</span><span class="sxs-lookup"><span data-stu-id="ded98-460">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="ded98-461">Web des besoins du serveur, IIS01, de flux de données à www.data.gov, mais doit tooresolve hello adresse.</span><span class="sxs-lookup"><span data-stu-id="ded98-461">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="ded98-462">Hello configuration réseau pour les listes de réseau virtuel hello DNS01 (10.0.2.4 sur le sous-réseau du serveur principal hello) en tant que serveur DNS principal de hello, IIS01 envoie hello DNS demande tooDNS01</span><span class="sxs-lookup"><span data-stu-id="ded98-462">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="ded98-463">Pare-feu de toohello UDR itinéraires du trafic sortant en tant que tronçon suivant de hello</span><span class="sxs-lookup"><span data-stu-id="ded98-463">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
4. <span data-ttu-id="ded98-464">Aucune règle de groupe de sécurité réseau sortantes n’est liées toohello frontal sous-réseau, le trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="ded98-464">No outbound NSG rules are bound toohello Frontend subnet, traffic is allowed</span></span>
5. <span data-ttu-id="ded98-465">Le pare-feu commence le traitement de la règle :</span><span class="sxs-lookup"><span data-stu-id="ded98-465">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="ded98-466">FW règle 1 (FW Mgmt) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-466">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="ded98-467">FW règle 2-5 (règles RDP) ne s’appliquent pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-467">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="ded98-468">FW règles 6 et 7 (règles d’application) ne s’appliquent pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-468">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="ded98-469">FW règle 8 (tooInternet) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-469">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="ded98-470">FW règle 9 (DNS) s’applique, le trafic est autorisé, le pare-feu transfère le trafic too10.0.2.4 (DNS01)</span><span class="sxs-lookup"><span data-stu-id="ded98-470">FW Rule 9 (DNS) does apply, traffic is allowed, firewall forwards traffic too10.0.2.4 (DNS01)</span></span>
6. <span data-ttu-id="ded98-471">sous-réseau du serveur principal Hello commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="ded98-471">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="ded98-472">Groupe de sécurité réseau règle 1 (bloc Internet) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-472">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="ded98-473">Règles du groupe de sécurité réseau par défaut autoriser le trafic de toosubnet de sous-réseau, le trafic est autorisé, d’arrêter le traitement des règles de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="ded98-473">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="ded98-474">Serveur DNS reçoit la demande de hello</span><span class="sxs-lookup"><span data-stu-id="ded98-474">DNS server receives hello request</span></span>
8. <span data-ttu-id="ded98-475">Serveur DNS n’a pas adresse hello mis en cache et demande à un serveur DNS racine sur hello internet</span><span class="sxs-lookup"><span data-stu-id="ded98-475">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
9. <span data-ttu-id="ded98-476">Pare-feu de toohello UDR itinéraires du trafic sortant en tant que tronçon suivant de hello</span><span class="sxs-lookup"><span data-stu-id="ded98-476">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
10. <span data-ttu-id="ded98-477">Aucune règle NSG sur le trafic sortant sur le sous-réseau du serveur principal. Le trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="ded98-477">No outbound NSG rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="ded98-478">Le pare-feu commence le traitement de la règle :</span><span class="sxs-lookup"><span data-stu-id="ded98-478">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="ded98-479">FW règle 1 (FW Mgmt) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-479">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="ded98-480">FW règle 2-5 (règles RDP) ne s’appliquent pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-480">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
    3. <span data-ttu-id="ded98-481">FW règles 6 et 7 (règles d’application) ne s’appliquent pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-481">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
    4. <span data-ttu-id="ded98-482">FW règle 8 (tooInternet) s’applique, le trafic est autorisé, la session est SNAT des serveurs DNS tooroot hello Internet</span><span class="sxs-lookup"><span data-stu-id="ded98-482">FW Rule 8 (tooInternet) does apply, traffic is allowed, session is SNAT out tooroot DNS server on hello Internet</span></span>
12. <span data-ttu-id="ded98-483">Serveur DNS Internet répond, étant donné que cette session a été lancée à partir de pare-feu de hello, réponse de hello est accepté par le pare-feu hello</span><span class="sxs-lookup"><span data-stu-id="ded98-483">Internet DNS server responds, since this session was initiated from hello firewall, hello response is accepted by hello firewall</span></span>
13. <span data-ttu-id="ded98-484">Comme il s’agit d’une session établie, les pare-feu hello transfère toohello de réponse hello lancer le serveur, DNS01</span><span class="sxs-lookup"><span data-stu-id="ded98-484">As this is an established session, hello firewall forwards hello response toohello initiating server, DNS01</span></span>
14. <span data-ttu-id="ded98-485">sous-réseau du serveur principal Hello commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="ded98-485">hello Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="ded98-486">Groupe de sécurité réseau règle 1 (bloc Internet) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-486">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="ded98-487">Règles du groupe de sécurité réseau par défaut autoriser le trafic de toosubnet de sous-réseau, le trafic est autorisé, d’arrêter le traitement des règles de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="ded98-487">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
15. <span data-ttu-id="ded98-488">serveur DNS de Hello reçoit et met en cache la réponse de hello et répond ensuite tooIIS01 arrière de demande initiale toohello</span><span class="sxs-lookup"><span data-stu-id="ded98-488">hello DNS server receives and caches hello response, and then responds toohello initial request back tooIIS01</span></span>
16. <span data-ttu-id="ded98-489">itinéraire UDR Hello sur le sous-réseau du serveur principal effectue le saut suivant de hello pare-feu hello</span><span class="sxs-lookup"><span data-stu-id="ded98-489">hello UDR route on backend subnet makes hello firewall hello next hop</span></span>
17. <span data-ttu-id="ded98-490">Il n’existe aucune règle de groupe de sécurité réseau sortant sur le sous-réseau du serveur principal hello, le trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="ded98-490">No outbound NSG rules exist on hello Backend subnet, traffic is allowed</span></span>
18. <span data-ttu-id="ded98-491">Il s’agit d’une session établie sur les pare-feu hello, réponse de hello est transmis par le serveur IIS de hello pare-feu toohello précédent</span><span class="sxs-lookup"><span data-stu-id="ded98-491">This is an established session on hello firewall, hello response is forwarded by hello firewall back toohello IIS server</span></span>
19. <span data-ttu-id="ded98-492">Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="ded98-492">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="ded98-493">Il n’existe aucune règle de groupe de sécurité réseau qui applique des tooInbound trafic de sous-réseau du serveur frontal de toohello de sous-réseau hello back-end, donc aucune des règles du groupe de sécurité réseau hello s’appliquent</span><span class="sxs-lookup"><span data-stu-id="ded98-493">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="ded98-494">règle du système par défaut Hello autorisant le trafic entre sous-réseaux permet ce trafic donc hello le trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="ded98-494">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
20. <span data-ttu-id="ded98-495">IIS01 reçoit hello réponse DNS01</span><span class="sxs-lookup"><span data-stu-id="ded98-495">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-backend-server-toofrontend-server"></a><span data-ttu-id="ded98-496">(Autorisé) Serveur tooFrontend de serveur principal</span><span class="sxs-lookup"><span data-stu-id="ded98-496">(Allowed) Backend server tooFrontend server</span></span>
1. <span data-ttu-id="ded98-497">Un administrateur connecté tooAppVM02 via RDP demande un fichier directement hello IIS01 serveur via l’Explorateur de fichiers windows</span><span class="sxs-lookup"><span data-stu-id="ded98-497">An administrator logged on tooAppVM02 via RDP requests a file directly from hello IIS01 server via windows file explorer</span></span>
2. <span data-ttu-id="ded98-498">itinéraire UDR Hello sur le sous-réseau du serveur principal effectue le saut suivant de hello pare-feu hello</span><span class="sxs-lookup"><span data-stu-id="ded98-498">hello UDR route on Backend subnet makes hello firewall hello next hop</span></span>
3. <span data-ttu-id="ded98-499">Dans la mesure où il n’y a aucune règle de groupe de sécurité réseau sortant sur hello réponse de hello sous-réseau principal n’est autorisé.</span><span class="sxs-lookup"><span data-stu-id="ded98-499">Since there are no outbound NSG rules on hello Backend subnet hello response is allowed</span></span>
4. <span data-ttu-id="ded98-500">Le pare-feu commence le traitement de la règle :</span><span class="sxs-lookup"><span data-stu-id="ded98-500">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="ded98-501">FW règle 1 (FW Mgmt) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-501">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="ded98-502">FW règle 2-5 (règles RDP) ne s’appliquent pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-502">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="ded98-503">FW règles 6 et 7 (règles d’application) ne s’appliquent pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-503">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="ded98-504">FW règle 8 (tooInternet) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-504">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="ded98-505">Règle de pare-feu 9 (DNS) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-505">FW Rule 9 (DNS) doesn’t apply, move toonext rule</span></span>
   6. <span data-ttu-id="ded98-506">10 de règle FW (Intra-sous-réseau) s’applique, le trafic est autorisé, le pare-feu transmet le trafic too10.0.1.4 (IIS01)</span><span class="sxs-lookup"><span data-stu-id="ded98-506">FW Rule 10 (Intra-Subnet) does apply, traffic is allowed, firewall passes traffic too10.0.1.4 (IIS01)</span></span>
5. <span data-ttu-id="ded98-507">Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="ded98-507">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="ded98-508">Groupe de sécurité réseau règle 1 (bloc Internet) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-508">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="ded98-509">Règles du groupe de sécurité réseau par défaut autoriser le trafic de toosubnet de sous-réseau, le trafic est autorisé, d’arrêter le traitement des règles de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="ded98-509">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="ded98-510">En supposant que d’autorisation et authentification appropriée, IIS01 hello accepte et répond</span><span class="sxs-lookup"><span data-stu-id="ded98-510">Assuming proper authentication and authorization, IIS01 accepts hello request and responds</span></span>
7. <span data-ttu-id="ded98-511">itinéraire UDR Hello sur le sous-réseau frontal rend le saut suivant de hello pare-feu hello</span><span class="sxs-lookup"><span data-stu-id="ded98-511">hello UDR route on Frontend subnet makes hello firewall hello next hop</span></span>
8. <span data-ttu-id="ded98-512">Dans la mesure où il n’y a aucune règle de groupe de sécurité réseau sortant sur hello réponse de hello sous-réseau frontal n’est autorisée.</span><span class="sxs-lookup"><span data-stu-id="ded98-512">Since there are no outbound NSG rules on hello Frontend subnet hello response is allowed</span></span>
9. <span data-ttu-id="ded98-513">Comme il s’agit d’une session existante sur le pare-feu hello cette réponse est autorisée et les pare-feu hello retourne hello réponse tooAppVM02</span><span class="sxs-lookup"><span data-stu-id="ded98-513">As this is an existing session on hello firewall this response is allowed and hello firewall returns hello response tooAppVM02</span></span>
10. <span data-ttu-id="ded98-514">Le sous-réseau du serveur principal entame le traitement du réseau entrant :</span><span class="sxs-lookup"><span data-stu-id="ded98-514">Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="ded98-515">Groupe de sécurité réseau règle 1 (bloc Internet) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-515">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="ded98-516">Règles du groupe de sécurité réseau par défaut autoriser le trafic de toosubnet de sous-réseau, le trafic est autorisé, d’arrêter le traitement des règles de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="ded98-516">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
11. <span data-ttu-id="ded98-517">AppVM02 reçoit la réponse de hello</span><span class="sxs-lookup"><span data-stu-id="ded98-517">AppVM02 receives hello response</span></span>

#### <a name="denied-internet-direct-tooweb-server"></a><span data-ttu-id="ded98-518">(Refusé) Internet, tooWeb directe serveur</span><span class="sxs-lookup"><span data-stu-id="ded98-518">(Denied) Internet direct tooWeb Server</span></span>
1. <span data-ttu-id="ded98-519">Utilisateur Internet tente tooaccess hello serveur web, IIS01, via hello FrontEnd001.CloudApp.Net service</span><span class="sxs-lookup"><span data-stu-id="ded98-519">Internet user tries tooaccess hello web server, IIS01, through hello FrontEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="ded98-520">Étant donné qu’aucun point de terminaison ouvert pour le trafic HTTP, cela ne peut pas passer via hello Service Cloud et ne pas de joindre le serveur de hello</span><span class="sxs-lookup"><span data-stu-id="ded98-520">Since there are no endpoints open for HTTP traffic, this would not pass through hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="ded98-521">Si les points de terminaison hello étaient ouverts pour une raison quelconque, hello NSG (bloc Internet) sur le sous-réseau du serveur frontal hello susceptibles de bloquer ce trafic</span><span class="sxs-lookup"><span data-stu-id="ded98-521">If hello endpoints were open for some reason, hello NSG (Block Internet) on hello Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="ded98-522">Enfin, itinéraire UDR sous-réseau hello frontal envoie tout le trafic sortant à partir de pare-feu de toohello IIS01 en tant que tronçon suivant de hello, les pare-feu hello seraient et consultez ce trafic asymétrique déposez hello de réponse sortants ainsi il y a au moins trois couches indépendantes de défense entre hello internet et IIS01 via son service de cloud empêche l’accès non autorisé/inappropriés.</span><span class="sxs-lookup"><span data-stu-id="ded98-522">Finally, hello Frontend subnet UDR route would send any outbound traffic from IIS01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and IIS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-toobackend-server"></a><span data-ttu-id="ded98-523">(Refusé) Internet tooBackend Server</span><span class="sxs-lookup"><span data-stu-id="ded98-523">(Denied) Internet tooBackend Server</span></span>
1. <span data-ttu-id="ded98-524">Utilisateur Internet tente tooaccess un fichier sur AppVM01 via hello BackEnd001.CloudApp.Net service</span><span class="sxs-lookup"><span data-stu-id="ded98-524">Internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="ded98-525">Étant donné qu’aucun point de terminaison ouvert pour le partage de fichiers, cela ne peut pas passer hello Service Cloud et ne pas de joindre le serveur de hello</span><span class="sxs-lookup"><span data-stu-id="ded98-525">Since there are no endpoints open for file share, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="ded98-526">Si les points de terminaison hello étaient ouverts pour une raison quelconque, hello NSG (bloc Internet) susceptibles de bloquer ce trafic</span><span class="sxs-lookup"><span data-stu-id="ded98-526">If hello endpoints were open for some reason, hello NSG (Block Internet) would block this traffic</span></span>
4. <span data-ttu-id="ded98-527">Enfin, itinéraire UDR hello envoie tout le trafic sortant à partir de pare-feu de toohello AppVM01 en tant que tronçon suivant de hello, les pare-feu hello seraient et consultez ce trafic asymétrique déposez hello de réponse sortants ainsi il y a au moins trois couches indépendantes de défense entre Bonjour internet et AppVM01 via son service de cloud empêche l’accès non autorisé/inappropriés.</span><span class="sxs-lookup"><span data-stu-id="ded98-527">Finally, hello UDR route would send any outbound traffic from AppVM01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and AppVM01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-frontend-server-toobackend-server"></a><span data-ttu-id="ded98-528">(Refusé) Serveur frontal serveur tooBackend serveur</span><span class="sxs-lookup"><span data-stu-id="ded98-528">(Denied) Frontend server tooBackend Server</span></span>
1. <span data-ttu-id="ded98-529">Supposez IIS01 a été compromis et que la tentative de serveurs de sous-réseau tooscan hello principaux programmes malveillants est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="ded98-529">Assume IIS01 was compromised and is running malicious code trying tooscan hello Backend subnet servers.</span></span>
2. <span data-ttu-id="ded98-530">itinéraire UDR sous-réseau Hello frontal envoie tout le trafic sortant IIS01 toohello pare-feu en tant que tronçon suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="ded98-530">hello Frontend subnet UDR route would send any outbound traffic from IIS01 toohello firewall as hello next hop.</span></span> <span data-ttu-id="ded98-531">Ce n’est pas un élément qui peut être modifiée par hello compromis de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ded98-531">This is not something that can be altered by hello compromised VM.</span></span>
3. <span data-ttu-id="ded98-532">les pare-feu Hello seraient traiter le trafic hello, si la demande de hello a été tooAppVM01 ou serveur DNS de toohello pour les recherches DNS, que le trafic peut potentiellement par pare-feu hello (échéance tooFW règles 7 et 9).</span><span class="sxs-lookup"><span data-stu-id="ded98-532">hello firewall would process hello traffic, if hello request was tooAppVM01, or toohello DNS server for DNS lookups that traffic could potentially be allowed by hello firewall (due tooFW Rules 7 and 9).</span></span> <span data-ttu-id="ded98-533">Tout autre trafic est bloqué par la règle de pare-feu 11 (Refuser tout).</span><span class="sxs-lookup"><span data-stu-id="ded98-533">All other traffic would be blocked by FW Rule 11 (Deny All).</span></span>
4. <span data-ttu-id="ded98-534">Si la détection des menaces a été activée sur le pare-feu hello (qui n’est pas abordé dans ce document, consultez la documentation du fournisseur hello pour votre solution de réseau spécifique des fonctionnalités de menaces avancées), même le trafic qui serait autorisé par hello base de règles de transfert abordés dans ce document ne soient pas si le trafic de hello contenait des signatures connus ou des modèles que l’indicateur d’une règle avancée.</span><span class="sxs-lookup"><span data-stu-id="ded98-534">If advanced threat detection was enabled on hello firewall (which is not covered in this document, see hello vendor documentation for your specific network appliance advanced threat capabilities), even traffic that would be allowed by hello basic forwarding rules discussed in this document could be prevented if hello traffic contained known signatures or patterns that flag an advanced threat rule.</span></span>

#### <a name="denied-internet-dns-lookup-on-dns-server"></a><span data-ttu-id="ded98-535">(Refusé) Recherche Internet DNS sur le serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="ded98-535">(Denied) Internet DNS lookup on DNS server</span></span>
1. <span data-ttu-id="ded98-536">Utilisateur Internet tente toolookup un enregistrement DNS interne sur DNS01 via BackEnd001.CloudApp.Net service</span><span class="sxs-lookup"><span data-stu-id="ded98-536">Internet user tries toolookup an internal DNS record on DNS01 through BackEnd001.CloudApp.Net service</span></span> 
2. <span data-ttu-id="ded98-537">Étant donné qu’aucun point de terminaison ouvert pour le trafic DNS, cela ne peut pas passer via hello Service Cloud et ne pas de joindre le serveur de hello</span><span class="sxs-lookup"><span data-stu-id="ded98-537">Since there are no endpoints open for DNS traffic, this would not pass through hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="ded98-538">Si les points de terminaison hello étaient ouverts pour une raison quelconque, règle de groupe de sécurité réseau hello (bloc Internet) sur le sous-réseau du serveur frontal hello susceptibles de bloquer ce trafic</span><span class="sxs-lookup"><span data-stu-id="ded98-538">If hello endpoints were open for some reason, hello NSG rule (Block Internet) on hello Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="ded98-539">Enfin, itinéraire UDR sous-réseau hello principal envoie tout le trafic sortant à partir de pare-feu de toohello DNS01 en tant que tronçon suivant de hello, les pare-feu hello seraient et consultez ce trafic asymétrique déposez hello de réponse sortants ainsi il y a au moins trois couches indépendantes de défense entre hello internet et DNS01 via son service de cloud empêche l’accès non autorisé/inappropriés.</span><span class="sxs-lookup"><span data-stu-id="ded98-539">Finally, hello Backend subnet UDR route would send any outbound traffic from DNS01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and DNS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-toosql-access-through-firewall"></a><span data-ttu-id="ded98-540">(Refusé) Accès à Internet tooSQL via le pare-feu</span><span class="sxs-lookup"><span data-stu-id="ded98-540">(Denied) Internet tooSQL access through Firewall</span></span>
1. <span data-ttu-id="ded98-541">Un utilisateur Internet demande des données SQL de SecSvc001.CloudApp.Net (Service cloud Internet)</span><span class="sxs-lookup"><span data-stu-id="ded98-541">Internet user requests SQL data from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="ded98-542">Étant donné qu’aucun point de terminaison ouvert pour SQL, cela ne peut pas passer hello Service Cloud et ne pas atteindre le pare-feu hello</span><span class="sxs-lookup"><span data-stu-id="ded98-542">Since there are no endpoints open for SQL, this would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="ded98-543">Si les points de terminaison SQL a été ouvertes pour une raison quelconque, les pare-feu hello seraient commencer le traitement de la règle :</span><span class="sxs-lookup"><span data-stu-id="ded98-543">If SQL endpoints were open for some reason, hello firewall would begin rule processing:</span></span>
   1. <span data-ttu-id="ded98-544">FW règle 1 (FW Mgmt) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-544">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="ded98-545">Règles 2 à 5 (règles RDP) ne s’appliquent, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-545">FW Rules 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="ded98-546">FW règle 6 et 7 (règles d’Application) ne s’appliquent pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-546">FW Rule 6 & 7 (Application Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="ded98-547">FW règle 8 (tooInternet) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-547">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="ded98-548">Règle de pare-feu 9 (DNS) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-548">FW Rule 9 (DNS) doesn’t apply, move toonext rule</span></span>
   6. <span data-ttu-id="ded98-549">Règle de pare-feu 10 (Intra-sous-réseau) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="ded98-549">FW Rule 10 (Intra-Subnet) doesn’t apply, move toonext rule</span></span>
   7. <span data-ttu-id="ded98-550">La règle de pare-feu 11 (Refuser tout) s’applique, le trafic est autorisé, arrêter le traitement des règles.</span><span class="sxs-lookup"><span data-stu-id="ded98-550">FW Rule 11 (Deny All) does apply, traffic is blocked, stop rule processing</span></span>

## <a name="references"></a><span data-ttu-id="ded98-551">Références</span><span class="sxs-lookup"><span data-stu-id="ded98-551">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="ded98-552">Script principal et configuration réseau</span><span class="sxs-lookup"><span data-stu-id="ded98-552">Main Script and Network Config</span></span>
<span data-ttu-id="ded98-553">Enregistrez hello Script complet dans un fichier de script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ded98-553">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="ded98-554">Enregistrez hello configuration réseau dans un fichier nommé « NetworkConf2.xml ».</span><span class="sxs-lookup"><span data-stu-id="ded98-554">Save hello Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="ded98-555">Modifier les variables de défini par l’utilisateur de hello en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="ded98-555">Modify hello user defined variables as needed.</span></span> <span data-ttu-id="ded98-556">Exécuter le script de hello, puis suivez le programme d’installation hello pare-feu règle instructions ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="ded98-556">Run hello script, then follow hello Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="ded98-557">Script complet</span><span class="sxs-lookup"><span data-stu-id="ded98-557">Full Script</span></span>
<span data-ttu-id="ded98-558">Ce script sera, en fonction des variables définies par l’utilisateur de hello :</span><span class="sxs-lookup"><span data-stu-id="ded98-558">This script will, based on hello user defined variables:</span></span>

1. <span data-ttu-id="ded98-559">Se connecter tooan abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="ded98-559">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="ded98-560">Création d’un nouveau compte de stockage</span><span class="sxs-lookup"><span data-stu-id="ded98-560">Create a new storage account</span></span>
3. <span data-ttu-id="ded98-561">Créer un nouveau réseau virtuel et trois sous-réseaux tel que défini dans le fichier de configuration de réseau de hello</span><span class="sxs-lookup"><span data-stu-id="ded98-561">Create a new VNet and three subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="ded98-562">Créer cinq machines virtuelles, 1 pare-feu et 4 machines virtuelles Windows Server </span><span class="sxs-lookup"><span data-stu-id="ded98-562">Build five virtual machines; 1 firewall and 4 windows server VMs</span></span>
5. <span data-ttu-id="ded98-563">Configurer UDR, notamment :</span><span class="sxs-lookup"><span data-stu-id="ded98-563">Configure UDR including:</span></span>
   1. <span data-ttu-id="ded98-564">Création de deux nouvelles tables d’itinéraire</span><span class="sxs-lookup"><span data-stu-id="ded98-564">Creating two new route tables</span></span>
   2. <span data-ttu-id="ded98-565">Ajouter des itinéraires toohello tables</span><span class="sxs-lookup"><span data-stu-id="ded98-565">Add routes toohello tables</span></span>
   3. <span data-ttu-id="ded98-566">Lier les sous-réseaux tooappropriate de tables</span><span class="sxs-lookup"><span data-stu-id="ded98-566">Bind tables tooappropriate subnets</span></span>
6. <span data-ttu-id="ded98-567">Activer le transfert IP hello NVA</span><span class="sxs-lookup"><span data-stu-id="ded98-567">Enable IP Forwarding on hello NVA</span></span>
7. <span data-ttu-id="ded98-568">Configurez un groupe de sécurité réseau, notamment :</span><span class="sxs-lookup"><span data-stu-id="ded98-568">Configure NSG including:</span></span>
   1. <span data-ttu-id="ded98-569">Création d’un groupe de protection réseau</span><span class="sxs-lookup"><span data-stu-id="ded98-569">Creating a NSG</span></span>
   2. <span data-ttu-id="ded98-570">Ajout d’une règle</span><span class="sxs-lookup"><span data-stu-id="ded98-570">Adding a rule</span></span>
   3. <span data-ttu-id="ded98-571">Sous-réseaux appropriés de liaison hello NSG toohello</span><span class="sxs-lookup"><span data-stu-id="ded98-571">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="ded98-572">Ce script PowerShell doit être exécuté localement sur un PC ou un serveur connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="ded98-572">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ded98-573">Lorsque ce script est exécuté, des avertissements ou autres messages d’information peuvent s’afficher dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ded98-573">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="ded98-574">Seuls les messages d’erreur affichés en rouge sont source de préoccupation.</span><span class="sxs-lookup"><span data-stu-id="ded98-574">Only error messages in red are cause for concern.</span></span>
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and User Defined Routing in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Three new cloud services
       - Three Subnets (SecNet, FrontEnd, and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet
       - Three Servers on hello BackEnd Subnet
       - IP Forwading from hello FireWall out toohello internet
       - User Defined Routing FrontEnd and BackEnd Subnets toohello NVA

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Everyone's security requirements are different and can be addressed in a myriad of ways.
      Please be sure that any sensitive data or applications are behind hello appropriate
      layer(s) of protection. This script serves as an example of some of hello techniques
      that can be used, but should not be used for all scenarios. You are responsible to
      assess your security needs and hello appropriate protections needed, and then effectively
      implement those protections.

      Security Service (SecNet subnet 10.0.0.0/24)
       myFirewall - 10.0.0.4

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       IIS01      - 10.0.1.4

      BackEnd Service (BackEnd subnet 10.0.2.0/24)
       DNS01      - 10.0.2.4
       AppVM01    - 10.0.2.5
       AppVM02    - 10.0.2.6

    #>

    # Fixed Variables
        $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password toobe used for all VMs"
        $VMName = @()
        $ServiceName = @()
        $VMFamily = @()
        $img = @()
        $size = @()
        $SubnetName = @()
        $VMIP = @()

    # User Defined Global Variables
      # These should be changes tooreflect your subscription and services
      # Invalid options will fail in hello validation section

      # Subscription Access Details
        $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

      # VM Account, Location, and Storage Details
        $LocalAdmin = "theAdmin"
        $DeploymentLocation = "Central US"
        $StorageAccountName = "vmstore02"

      # Service Details
        $SecureService = "SecSvc001"
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $VNetPrefix = "10.0.0.0/16"
        $SecNet = "SecNet"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf3.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # UDR Details
        $FERouteTableName = "FrontEndSubnetRouteTable"
        $BERouteTableName = "BackEndSubnetRouteTable"

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure UDR and IP forwarding is setup
        # properly this script requires VM 0 be hello NVA.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $SecureService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $SecNet
          $VMIP += "10.0.0.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 2 - hello First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - hello Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - hello DNS Server
          $VMName += "DNS01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.4"

    # ----------------------------- #
    # No User Defined Varibles or   #
    # Configuration past this point #
    # ----------------------------- #

      # Get your Azure accounts
        Add-AzureAccount
        Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
        Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

      # Create Storage Account
        If (Test-AzureName -Storage -Name $StorageAccountName) { 
            Write-Host "Fatal Error: This storage account name is already in use, please pick a diffrent name." -ForegroundColor Red
            Return}
        Else {Write-Host "Creating Storage Account" -ForegroundColor Cyan 
              New-AzureStorageAccount -Location $DeploymentLocation -StorageAccountName $StorageAccountName}

      # Update Subscription Pointer tooNew Storage Account
        Write-Host "Updating Subscription Pointer tooNew Storage Account" -ForegroundColor Cyan 
        Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

    # Validation
    $FatalError = $false

    If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
         Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
         $FatalError = $true}

    If (Test-AzureName -Service -Name $SecureService) { 
        Write-Host "hello SecureService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use" -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation varible is correct and hello netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see hello above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

    # Create VNET
        Write-Host "Creating VNET" -ForegroundColor Cyan 
        Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

    # Create Services
        Write-Host "Creating Services" -ForegroundColor Cyan
        New-AzureService -Location $DeploymentLocation -ServiceName $SecureService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

    # Build VMs
        $i=0
        $VMName | Foreach {
            Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
            If ($VMFamily[$i] -eq "Firewall") 
                { 
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Linux -LinuxUser $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                # Set up all hello EndPoints we'll need once we're up and running
                # Note: All traffic goes through hello firewall, so we'll need tooset up all ports here.
                #       Also, hello firewall will be redirecting traffic tooa new IP and Port in a forwarding
                #       rule, so all of these endpoint have hello same public and local port and hello firewall
                #       will do hello mapping, NATing, and/or redirection as declared in hello firewall rules.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPWeb"    -Protocol tcp -PublicPort 8014 -LocalPort 8014 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp1"   -Protocol tcp -PublicPort 8025 -LocalPort 8025 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp2"   -Protocol tcp -PublicPort 8026 -LocalPort 8026 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPDNS01"  -Protocol tcp -PublicPort 8024 -LocalPort 8024 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "RemoteDesktop" | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                }
            $i++
        }

    # Configure UDR and IP Forwarding
        Write-Host "Configuring UDR" -ForegroundColor Cyan

      # Create hello Route Tables
        Write-Host "Creating hello Route Tables" -ForegroundColor Cyan 
        New-AzureRouteTable -Name $BERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $BESubnet subnet"
        New-AzureRouteTable -Name $FERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $FESubnet subnet"

      # Add Routes tooRoute Tables
        Write-Host "Adding Routes toohello Route Tables" -ForegroundColor Cyan 
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $FEPrefix `
            -NextHopType VNETLocal

      # Assoicate hello Route Tables with hello Subnets
        Write-Host "Binding Route Tables toohello Subnets" -ForegroundColor Cyan 
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $BESubnet `
            -RouteTableName $BERouteTableName
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $FESubnet `
            -RouteTableName $FERouteTableName

     # Enable IP Forwarding on hello Virtual Appliance
        Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] `
            |Set-AzureIPForwarding -Enable

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rule
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 100 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

      # Assign hello NSG tootwo Subnets
        # hello NSG is *not* bound toohello Security Subnet. hello result
        # is that internet traffic flows only toohello Security subnet
        # since hello NSG bound toohello Frontend and Backback subnets
        # will Deny internet traffic toothose subnets.
        Write-Host "Binding hello NSG tootwo subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on hello IIS Server)
      # Install Backend resource (Run Post-Build Script on hello AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a><span data-ttu-id="ded98-575">Fichier de configuration réseau</span><span class="sxs-lookup"><span data-stu-id="ded98-575">Network Config File</span></span>
<span data-ttu-id="ded98-576">Enregistrez ce fichier xml avec l’emplacement mis à jour et ajouter hello lien toothis fichier toohello $NetworkConfigFile variable dans le script hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="ded98-576">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello script above.</span></span>

    <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
      <VirtualNetworkConfiguration>
        <Dns>
          <DnsServers>
            <DnsServer name="DNS01" IPAddress="10.0.2.4" />
            <DnsServer name="Level3" IPAddress="209.244.0.3" />
          </DnsServers>
        </Dns>
        <VirtualNetworkSites>
          <VirtualNetworkSite name="CorpNetwork" Location="Central US">
            <AddressSpace>
              <AddressPrefix>10.0.0.0/16</AddressPrefix>
            </AddressSpace>
            <Subnets>
              <Subnet name="SecNet">
                <AddressPrefix>10.0.0.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="FrontEnd">
                <AddressPrefix>10.0.1.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="BackEnd">
                <AddressPrefix>10.0.2.0/24</AddressPrefix>
              </Subnet>
            </Subnets>
            <DnsServersRef>
              <DnsServerRef name="DNS01" />
              <DnsServerRef name="Level3" />
            </DnsServersRef>
          </VirtualNetworkSite>
        </VirtualNetworkSites>
      </VirtualNetworkConfiguration>
    </NetworkConfiguration>

#### <a name="sample-application-scripts"></a><span data-ttu-id="ded98-577">Exemples de scripts d’application</span><span class="sxs-lookup"><span data-stu-id="ded98-577">Sample Application Scripts</span></span>
<span data-ttu-id="ded98-578">Si vous le souhaitez tooinstall un exemple d’application pour ce, ainsi que d’autres exemples de réseau de périmètre, un a été fourni au lien de hello : [Application exemple de Script][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="ded98-578">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "Zone DMZ bidirectionnelle avec NVA, NSG et UDR"
[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Affichage logique de règles de pare-feu de hello"
[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "Créer un objet réseau FrontEnd"
[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "Créer un objet de serveur DNS"
[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "Copie de la règle RDP par défaut"
[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "Règle AppVM01"
[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "Icône de redirection d’application"
[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "Icône NAT de destination"
[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "Icône de réussite"
[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "Règle de gestion de pare-feu"
[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "Règle RDP de pare-feu"
[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "Règle web de pare-feu "
[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "Règle AppVM01 de pare-feu "
[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "Règle de trafic sortant de pare-feu"
[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "Règle DNS de pare-feu"
[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "Règle Intra-réseau virtuel de pare-feu"
[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "Règle de refus de pare-feu"
[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "Activation de règle de pare-feu"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
