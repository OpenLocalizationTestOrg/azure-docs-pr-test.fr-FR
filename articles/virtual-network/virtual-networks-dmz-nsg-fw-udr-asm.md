---
title: "Exemple DMZ : créer une zone DMZ pour protéger les réseaux avec un pare-feu, un itinéraire défini par l’utilisateur et un groupe de sécurité réseau | Microsoft Docs"
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
ms.openlocfilehash: fdb3c5cbd3acee90386352c6f180a71aa81f54fe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="example-3--build-a-dmz-to-protect-networks-with-a-firewall-udr-and-nsg"></a><span data-ttu-id="ea2ea-103">Exemple 3 : créer un réseau de périmètre DMZ pour protéger les réseaux avec un pare-feu, un réseau défini sur l’utilisateur et un groupe de réseau</span><span class="sxs-lookup"><span data-stu-id="ea2ea-103">Example 3 – Build a DMZ to Protect Networks with a Firewall, UDR, and NSG</span></span>
<span data-ttu-id="ea2ea-104">[Revenir à la page Meilleures pratiques relatives aux frontières de sécurité][HOME]</span><span class="sxs-lookup"><span data-stu-id="ea2ea-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="ea2ea-105">Cet exemple va créer un réseau de périmètre avec un pare-feu, quatre serveurs Windows, Routage défini par l’utilisateur (UDR), Transfert IP et groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-105">This example will create a DMZ with a firewall, four windows servers, User Defined Routing, IP Forwarding, and Network Security Groups.</span></span> <span data-ttu-id="ea2ea-106">Vous y découvrirez également comment chacune des commandes concernées fournit une meilleure connaissance de chaque opération.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-106">It will also walk through each of the relevant commands to provide a deeper understanding of each step.</span></span> <span data-ttu-id="ea2ea-107">Il comporte également une section Scénario de trafic (Traffic Scenario) qui explique en détail et étape par étape l’évolution du trafic à travers les couches de défense dans la zone DMZ.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-107">There is also a Traffic Scenario section to provide an in-depth step-by-step how traffic proceeds through the layers of defense in the DMZ.</span></span> <span data-ttu-id="ea2ea-108">Enfin, dans la section de référence se trouve l’intégralité du code et des instructions permettant d’élaborer l’environnement destiné à tester et à expérimenter différents scénarios.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-108">Finally, in the references section is the complete code and instruction to build this environment to test and experiment with various scenarios.</span></span> 

<span data-ttu-id="ea2ea-109">![Zone DMZ bidirectionnelle avec NVA, NSG et UDR][1]</span><span class="sxs-lookup"><span data-stu-id="ea2ea-109">![Bi-directional DMZ with NVA, NSG, and UDR][1]</span></span>

## <a name="environment-setup"></a><span data-ttu-id="ea2ea-110">Configuration de l’environnement</span><span class="sxs-lookup"><span data-stu-id="ea2ea-110">Environment Setup</span></span>
<span data-ttu-id="ea2ea-111">Dans cet exemple, il existe un abonnement qui contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-111">In this example there is a subscription that contains the following:</span></span>

* <span data-ttu-id="ea2ea-112">Trois services cloud : « SecSvc001 », « FrontEnd001 » et « BackEnd001 »</span><span class="sxs-lookup"><span data-stu-id="ea2ea-112">Three cloud services: “SecSvc001”, “FrontEnd001”, and “BackEnd001”</span></span>
* <span data-ttu-id="ea2ea-113">Un réseau virtuel « CorpNetwork », avec trois sous-réseaux : « SecNet », « FrontEnd » et « BackEnd »</span><span class="sxs-lookup"><span data-stu-id="ea2ea-113">A Virtual Network “CorpNetwork”, with three subnets: “SecNet”, “FrontEnd”, and “BackEnd”</span></span>
* <span data-ttu-id="ea2ea-114">Une appliance virtuelle du réseau, dans cet exemple un pare-feu, connecté au sous-réseau SecNet</span><span class="sxs-lookup"><span data-stu-id="ea2ea-114">A network virtual appliance, in this example a firewall, connected to the SecNet subnet</span></span>
* <span data-ttu-id="ea2ea-115">un serveur Windows Server représentant un serveur web d’application (« IIS01 »),</span><span class="sxs-lookup"><span data-stu-id="ea2ea-115">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="ea2ea-116">Deux serveurs Windows Server qui représentent les serveurs principaux d’applications (« AppVM01 », « AppVM02 »)</span><span class="sxs-lookup"><span data-stu-id="ea2ea-116">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="ea2ea-117">Un serveur Windows Server qui représente un serveur DNS (« DNS01 »),</span><span class="sxs-lookup"><span data-stu-id="ea2ea-117">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="ea2ea-118">Dans la section Références ci-dessous figure un script PowerShell qui générera une grande partie l’environnement décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-118">In the references section below there is a PowerShell script that will build most of the environment described above.</span></span> <span data-ttu-id="ea2ea-119">La création de machines virtuelles et de réseaux virtuels, bien qu’effectuée par l’exemple de script, ne figure pas en détail dans ce document.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-119">Building the VMs and Virtual Networks, although are done by the example script, are not described in detail in this document.</span></span>

<span data-ttu-id="ea2ea-120">Pour créer l’environnement :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-120">To build the environment:</span></span>

1. <span data-ttu-id="ea2ea-121">Enregistrer le fichier XML de configuration réseau contenu dans la section Références (mis à jour avec les noms, l’emplacement et les adresses IP correspondant à un scénario donné)</span><span class="sxs-lookup"><span data-stu-id="ea2ea-121">Save the network config xml file included in the references section (updated with names, location, and IP addresses to match the given scenario)</span></span>
2. <span data-ttu-id="ea2ea-122">Mettre à jour les variables de l’utilisateur dans le script pour qu’elles correspondent à l’environnement dans lequel le script est exécuté (abonnements, noms de service, etc.)</span><span class="sxs-lookup"><span data-stu-id="ea2ea-122">Update the user variables in the script to match the environment the script is to be run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="ea2ea-123">Exécuter le script dans PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea2ea-123">Execute the script in PowerShell</span></span>

<span data-ttu-id="ea2ea-124">**Remarque**: la région indiquée dans le script PowerShell doit correspondre à la région indiquée dans le fichier xml de configuration réseau.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-124">**Note**: The region signified in the PowerShell script must match the region signified in the network configuration xml file.</span></span>

<span data-ttu-id="ea2ea-125">Une fois que le script s’exécute correctement, les opérations de post-script qui suivent doivent être exécutées :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-125">Once the script runs successfully the following post-script steps may be taken:</span></span>

1. <span data-ttu-id="ea2ea-126">Configurer les règles de pare-feu. Ce sujet est traité dans la section ci-dessous intitulée Description de règles de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-126">Set up the firewall rules, this is covered in the section below titled: Firewall Rule Description.</span></span>
2. <span data-ttu-id="ea2ea-127">Dans la section Références, il existe deux scripts pour configurer le serveur web et le serveur d’application avec une application web simple permettant le test avec cette configuration réseau de périmètre.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-127">Optionally in the references section are two scripts to set up the web server and app server with a simple web application to allow testing with this DMZ configuration.</span></span>

<span data-ttu-id="ea2ea-128">Une fois que le script s’exécute correctement, il faut terminer les règles de pare-feu. Ce sujet est traité dans la section intitulée : Règles de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-128">Once the script runs successfully the firewall rules will need to be completed, this is covered in the section titled: Firewall Rules.</span></span>

## <a name="user-defined-routing-udr"></a><span data-ttu-id="ea2ea-129">Itinéraire défini par l’utilisateur (UDR)</span><span class="sxs-lookup"><span data-stu-id="ea2ea-129">User Defined Routing (UDR)</span></span>
<span data-ttu-id="ea2ea-130">Par défaut, les itinéraires système suivants sont définis en tant que :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-130">By default, the following system routes are defined as:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

<span data-ttu-id="ea2ea-131">Le VNETLocal constitue toujours le ou les préfixes d’adresse de réseau virtuel défini(s) du réseau virtuel correspondant à ce réseau spécifique (il passera de VNet à VNet en fonction de la manière dont chaque réseau virtuel spécifique est défini.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-131">The VNETLocal is always the defined address prefix(es) of the VNet for that specific network (ie it will change from VNet to VNet depending on how each specific VNet is defined).</span></span> <span data-ttu-id="ea2ea-132">Les itinéraires système restants sont statiques et par défaut, ils prennent la valeur indiquée ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-132">The remaining system routes are static and default as above.</span></span>

<span data-ttu-id="ea2ea-133">En matière de priorité, les itinéraires sont traités via la méthode de correspondance du plus long préfixe (LPM) et l’itinéraire le lus spécifique de la table est appliqué à une adresse de destination donnée.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-133">As for priority, routes are processed via the Longest Prefix Match (LPM) method, thus the most specific route in the table would apply to a given destination address.</span></span>

<span data-ttu-id="ea2ea-134">Par conséquent, le trafic (par exemple pour le serveur DNS01, 10.0.2.4) pour le réseau local (10.0.0.0/16) serait acheminé via VNet vers sa destination par le biais de l’itinéraire 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-134">Therefore, traffic (for example to the DNS01 server, 10.0.2.4) intended for the local network (10.0.0.0/16) would be routed across the VNet to its destination due to the 10.0.0.0/16 route.</span></span> <span data-ttu-id="ea2ea-135">En d’autres termes, pour 10.0.2.4, l’itinéraire 10.0.0.0/16 est l’itinéraire le plus spécifique, et ce, même si 10.0.0.0/8 et 0.0.0.0/0 pourraient s’appliquer également. Comme ils sont moins spécifiques, ils n’affectent pas ce trafic.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-135">In other words, for 10.0.2.4, the 10.0.0.0/16 route is the most specific route, even though the 10.0.0.0/8 and 0.0.0.0/0 also could apply, but since they are less specific they don’t affect this traffic.</span></span> <span data-ttu-id="ea2ea-136">Par conséquent, le trafic vers 10.0.2.4 emprunterait un tronçon suivant du réseau virtuel et serait simplement acheminé vers la destination.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-136">Thus the traffic to 10.0.2.4 would have a next hop of the local VNet and simply route to the destination.</span></span>

<span data-ttu-id="ea2ea-137">Si le trafic a été conçu pour 10.1.1.1 par exemple, l’itinéraire 10.0.0.0/16 ne s’applique pas, mais 10.0.0.0/8 serait le plus spécifique, et le trafic serait supprimé (« placé dans le trou noir ») dans la mesure où le tronçon suivant est Null.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-137">If traffic was intended for 10.1.1.1 for example, the 10.0.0.0/16 route wouldn’t apply, but the 10.0.0.0/8 would be the most specific, and this the traffic would be dropped (“black holed”) since the next hop is Null.</span></span> 

<span data-ttu-id="ea2ea-138">Si la destination ne s’applique à aucun des préfixes Null ou aux préfixes de réseaux virtuels locaux, le trafic suivra l’itinéraire spécifique, 0.0.0.0/0 et sera acheminé en externe via Internet, le tronçon suivant et donc, hors du secteur Internet d’Azure.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-138">If the destination didn’t apply to any of the Null prefixes or the VNETLocal prefixes, then it would follow the least specific route, 0.0.0.0/0 and be routed out to the Internet as the next hop and thus out Azure’s internet edge.</span></span>

<span data-ttu-id="ea2ea-139">S’il existe deux préfixes identiques dans la table d’itinéraires, voici l’ordre de préférence basé sur l’attribut « source » de routes :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-139">If there are two identical prefixes in the route table, the following is the order of preference based on the routes “source” attribute:</span></span>

1. <span data-ttu-id="ea2ea-140">"VirtualAppliance" = Un itinéraire défini par l’utilisateur ajouté manuellement à la table</span><span class="sxs-lookup"><span data-stu-id="ea2ea-140">"VirtualAppliance" = A User Defined Route manually added to the table</span></span>
2. <span data-ttu-id="ea2ea-141">« VPNGateway » = un itinéraire dynamique ( BGP en cas d’utilisation avec des réseaux hybrides), ajouté par un protocole réseau dynamique. Ces itinéraires peuvent changer au fil du temps, le protocole dynamique reflétant automatiquement les modifications intervenues dans le réseau associé</span><span class="sxs-lookup"><span data-stu-id="ea2ea-141">“VPNGateway” = A Dynamic Route (BGP when used with hybrid networks), added by a dynamic network protocol, these routes may change over time as the dynamic protocol automatically reflects changes in peered network</span></span>
3. <span data-ttu-id="ea2ea-142">« Default » = les itinéraires du système, le réseau local virtuel et les entrées statiques, comme indiqué dans la table d’itinéraires.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-142">“Default” = The System Routes, the local VNet and the static entries as shown in the route table above.</span></span>

> [!NOTE]
> <span data-ttu-id="ea2ea-143">Vous pouvez maintenant utiliser le routage défini par l’utilisateur (UDR) avec ExpressRoute et les passerelles VPN pour forcer l’acheminement du trafic intersite entrant et sortant vers une appliance virtuelle de réseau (NVA).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-143">You can now use User Defined Routing (UDR) with ExpressRoute and VPN Gateways to force outbound and inbound cross-premises traffic to be routed to a network virtual appliance (NVA).</span></span>
> 
> 

#### <a name="creating-the-local-routes"></a><span data-ttu-id="ea2ea-144">Création d’itinéraires locaux</span><span class="sxs-lookup"><span data-stu-id="ea2ea-144">Creating the local routes</span></span>
<span data-ttu-id="ea2ea-145">Dans cet exemple, deux tables d’itinéraires sont nécessaires, une pour chacun des sous-réseaux principal et frontal.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-145">In this example, two routing tables are needed, one each for the Frontend and Backend subnets.</span></span> <span data-ttu-id="ea2ea-146">Chaque table est chargée d’itinéraires statiques appropriés au sous-réseau donné.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-146">Each table is loaded with static routes appropriate for the given subnet.</span></span> <span data-ttu-id="ea2ea-147">Dans cet exemple, chaque table possède trois routes :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-147">For the purpose of this example, each table has three routes:</span></span>

1. <span data-ttu-id="ea2ea-148">Trafic de sous-réseau local avec Tronçon suivant défini pour permettre le trafic du sous-réseau local pour contourner le pare-feu</span><span class="sxs-lookup"><span data-stu-id="ea2ea-148">Local subnet traffic with no Next Hop defined to allow local subnet traffic to bypass the firewall</span></span>
2. <span data-ttu-id="ea2ea-149">Trafic du réseau virtuel avec un tronçon suivant défini comme pare-feu. Cela remplace la règle par défaut qui autorise un acheminement direct du trafic de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="ea2ea-149">Virtual Network traffic with a Next Hop defined as firewall, this overrides the default rule that allows local VNet traffic to route directly</span></span>
3. <span data-ttu-id="ea2ea-150">Ensemble du trafic restant (0/0) avec le tronçon suivant défini comme pare-feu</span><span class="sxs-lookup"><span data-stu-id="ea2ea-150">All remaining traffic (0/0) with a Next Hop defined as the firewall</span></span>

<span data-ttu-id="ea2ea-151">Une fois que les tables de routage sont créées, ils sont liés à leurs sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-151">Once the routing tables are created they are bound to their subnets.</span></span> <span data-ttu-id="ea2ea-152">La table d’itinéraire de sous-réseau du serveur frontal, une fois créée et liée au sous-réseau, doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-152">For the Frontend subnet routing table, once created and bound to the subnet should look like this:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active 
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active


<span data-ttu-id="ea2ea-153">Dans cet exemple, les commandes suivantes sont utilisées pour générer la table d’itinéraires, ajouter un itinéraire défini par l’utilisateur, puis lier la table d’itinéraire à un sous-réseau (Remarque : tous les éléments ci-dessous commençant par un signe dollar (par ex.: $BESubnet) sont des variables définies par l’utilisateur à partir du script de la section Références de ce document) :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-153">For this example, the following commands are used to build the route table, add a user defined route, and then bind the route table to a subnet (Note; any items below beginning with a dollar sign (e.g.: $BESubnet) are user defined variables from the script in the reference section of this document):</span></span>

1. <span data-ttu-id="ea2ea-154">Tout d’abord, il faut créer la table d’itinéraires de base.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-154">First the base routing table must be created.</span></span> <span data-ttu-id="ea2ea-155">Cet extrait de code illustre la création de la table du sous-réseau du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-155">This snippet shows the creation of the table for the Backend subnet.</span></span> <span data-ttu-id="ea2ea-156">Dans le script, une table correspondante est également créée pour le sous-réseau du serveur frontal.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-156">In the script, a corresponding table is also created for the Frontend subnet.</span></span>
   
     <span data-ttu-id="ea2ea-157">New-AzureRouteTable -Name $BERouteTableName \`</span><span class="sxs-lookup"><span data-stu-id="ea2ea-157">New-AzureRouteTable -Name $BERouteTableName \`</span></span>
   
         -Location $DeploymentLocation `
         -Label "Route table for $BESubnet subnet"
2. <span data-ttu-id="ea2ea-158">Une fois la table de routage créée, les itinéraires définis par l’utilisateur spécifiques peuvent être ajoutés.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-158">Once the route table is created, specific user defined routes can be added.</span></span> <span data-ttu-id="ea2ea-159">Dans cet extrait, tout le trafic (0.0.0.0/0) est acheminé via l’appliance virtuelle (une variable, $VMIP [0], est utilisée pour transmettre l’adresse IP affectée au moment de la création de l’équipement dans le script).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-159">In this snipped, all traffic (0.0.0.0/0) will be routed through the virtual appliance (a variable, $VMIP[0], is used to pass in the IP address assigned when the virtual appliance was created earlier in the script).</span></span> <span data-ttu-id="ea2ea-160">Dans le script, une table correspondante est également créée dans la table frontale.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-160">In the script, a corresponding rule is also created in the Frontend table.</span></span>
   
     <span data-ttu-id="ea2ea-161">Get-AzureRouteTable $BERouteTableName | \`</span><span class="sxs-lookup"><span data-stu-id="ea2ea-161">Get-AzureRouteTable $BERouteTableName | \`</span></span>
   
         Set-AzureRoute -RouteName "All traffic to FW" -AddressPrefix 0.0.0.0/0 `
         -NextHopType VirtualAppliance `
         -NextHopIpAddress $VMIP[0]
3. <span data-ttu-id="ea2ea-162">La saisie d’itinéraire ci-dessus remplace l’itinéraire par défaut « 0.0.0.0/0 », mais la règle de 10.0.0.0/16 par défaut existante autoriserait le trafic au sein du réseau virtuel acheminer les éléments directement vers leur destination, et non vers l’équipement de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-162">The above route entry will override the default "0.0.0.0/0" route, but the default 10.0.0.0/16 rule still existing which would allow traffic within the VNet to route directly to the destination and not to the Network Virtual Appliance.</span></span> <span data-ttu-id="ea2ea-163">Pour corriger ce comportement, vous devez ajouter la règle suivante.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-163">To correct this behavior the follow rule must be added.</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Internal traffic to FW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
4. <span data-ttu-id="ea2ea-164">À ce stade, vous devez faire un choix.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-164">At this point there is a choice to be made.</span></span> <span data-ttu-id="ea2ea-165">Les deux itinéraires ci-dessus acheminent tout le trafic vers le pare-feu pour évaluation, même le trafic au sein d’un sous-réseau unique.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-165">With the above two routes all traffic will route to the firewall for assessment, even traffic within a single subnet.</span></span> <span data-ttu-id="ea2ea-166">Cela peut être souhaitable, cependant, pour autoriser le trafic au sein d’un sous-réseau pour acheminer localement sans intervention du pare-feu, une troisième règle très spécifique peut être ajoutée.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-166">This may be desired, however to allow traffic within a subnet to route locally without involvement from the firewall a third, very specific rule can be added.</span></span> <span data-ttu-id="ea2ea-167">Cet itinéraire États déclare que n’importe quelle adresse de destination du sous-réseau local peut être acheminée directement (NextHopType = VNETLocal).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-167">This route states that any address destine for the local subnet can just route there directly (NextHopType = VNETLocal).</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
5. <span data-ttu-id="ea2ea-168">Enfin, avec la table d’itinéraires créée et renseignée à l’aide d’itinéraires définis par l’utilisateur, le tableau doit être associé à un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-168">Finally, with the routing table created and populated with a user defined routes, the table must now be bound to a subnet.</span></span> <span data-ttu-id="ea2ea-169">Dans le script, la table d’itinéraires du serveur principal est également liée au sous-réseau du serveur frontal.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-169">In the script, the front end route table is also bound to the Frontend subnet.</span></span> <span data-ttu-id="ea2ea-170">Voici le script de liaison pour le sous-réseau du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-170">Here is the binding script for the back end subnet.</span></span>
   
     <span data-ttu-id="ea2ea-171">Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName \`</span><span class="sxs-lookup"><span data-stu-id="ea2ea-171">Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName \`</span></span>
   
        -SubnetName $BESubnet `
        -RouteTableName $BERouteTableName

## <a name="ip-forwarding"></a><span data-ttu-id="ea2ea-172">transfert IP</span><span class="sxs-lookup"><span data-stu-id="ea2ea-172">IP Forwarding</span></span>
<span data-ttu-id="ea2ea-173">Le transfert IP est associé à UDR.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-173">A companion feature to UDR, is IP Forwarding.</span></span> <span data-ttu-id="ea2ea-174">Il s’agit d’un paramètre d’appliance virtuelle qui permet de recevoir du trafic pas spécialement adressé à l’équipement, puis de transférer ce trafic vers sa destination finale.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-174">This is a setting on a Virtual Appliance that allows it to receive traffic not specifically addressed to the appliance and then forward that traffic to its ultimate destination.</span></span>

<span data-ttu-id="ea2ea-175">Par exemple, si le trafic à partir d’AppVM01 fait une demande au serveur DNS01, l’UDR l’achemine vers le pare-feu.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-175">As an example, if traffic from AppVM01 makes a request to the DNS01 server, UDR would route this to the firewall.</span></span> <span data-ttu-id="ea2ea-176">Lorsque le transfert IP est activé, le trafic de la destination de DNS01 (10.0.2.4) est accepté par l’appliance (10.0.0.4), puis transféré vers sa destination finale (10.0.2.4).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-176">With IP Forwarding enabled, the traffic for the DNS01 destination (10.0.2.4) will be accepted by the appliance (10.0.0.4) and then forwarded to its ultimate destination (10.0.2.4).</span></span> <span data-ttu-id="ea2ea-177">Si le routage IP n’est pas activé sur le pare-feu, le trafic ne sera pas accepté par l’équipement, même si le tronçon suivant de la table d’itinéraires est le pare-feu.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-177">Without IP Forwarding enabled on the Firewall, traffic would not be accepted by the appliance even though the route table has the firewall as the next hop.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ea2ea-178">Il est essentiel de ne pas oublier d’activer le transfert IP en conjonction avec l’utilisateur défini.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-178">It’s critical to remember to enable IP Forwarding in conjunction with User Defined Routing.</span></span>
> 
> 

<span data-ttu-id="ea2ea-179">La configuration du transfert IP est une commande unique et peut être exécutée au moment de la création d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-179">Setting up IP Forwarding is a single command and can be done at VM creation time.</span></span> <span data-ttu-id="ea2ea-180">Pour le flux de cet exemple, l’extrait de code se trouve vers la fin du script et regroupé avec les commandes UDR :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-180">For the flow of this example the code snippet is towards the end of the script and grouped with the UDR commands:</span></span>

1. <span data-ttu-id="ea2ea-181">Appelez l’instance de machine virtuelle qui est votre équipement virtuel, dans ce cas, le pare-feu, et activez le transfert IP (Remarque : tout élément en rouge contenant un signe dollar (par exemple : $VMName[0]) est une variable définie par l’utilisateur issue du script dans la section de référence de ce document.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-181">Call the VM instance that is your virtual appliance, the firewall in this case, and enable IP Forwarding (Note; any item in red beginning with a dollar sign (e.g.: $VMName[0]) is a user defined variable from the script in the reference section of this document.</span></span> <span data-ttu-id="ea2ea-182">Le zéro entre crochets, [0], représente la première machine virtuelle du tableau des machines virtuelles, pour que l’exemple de script fonctionne sans modification, la première machine virtuelle (VM 0) doit être le pare-feu) :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-182">The zero in brackets, [0], represents the first VM in the array of VMs, for the example script to work without modification, the first VM (VM 0) must be the firewall):</span></span>
   
     <span data-ttu-id="ea2ea-183">Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | \`</span><span class="sxs-lookup"><span data-stu-id="ea2ea-183">Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | \`</span></span>
   
        Set-AzureIPForwarding -Enable

## <a name="network-security-groups-nsg"></a><span data-ttu-id="ea2ea-184">Groupes de sécurité réseau (NSG)</span><span class="sxs-lookup"><span data-stu-id="ea2ea-184">Network Security Groups (NSG)</span></span>
<span data-ttu-id="ea2ea-185">Dans cet exemple, un groupe NSG est créé, puis chargé avec une seule règle.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-185">In this example, a NSG group is built and then loaded with a single rule.</span></span> <span data-ttu-id="ea2ea-186">Ce groupe est ensuite lié uniquement aux sous-réseaux frontaux et principaux (et pas au SecNet).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-186">This group is then bound only to the Frontend and Backend subnets (not the SecNet).</span></span> <span data-ttu-id="ea2ea-187">La règle suivante est générée de manière déclarative :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-187">Declaratively the following rule is being built:</span></span>

1. <span data-ttu-id="ea2ea-188">Tout le trafic (tous les ports) depuis Internet vers l’ensemble du réseau virtuel entier (tous les sous-réseaux) est refusé.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-188">Any traffic (all ports) from the Internet to the entire VNet (all subnets) is Denied</span></span>

<span data-ttu-id="ea2ea-189">Bien que dans cet exemple, on utilise des NSG, son principal objectif est celui d’une couche secondaire de défense contre les erreurs de configuration manuelle.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-189">Although NSGs are used in this example, it’s main purpose is as a secondary layer of defense against manual misconfiguration.</span></span> <span data-ttu-id="ea2ea-190">Nous voulons bloquer tout trafic entrant en provenance d’Internet vers les sous-réseaux frontal ou principal des sous-réseaux, le trafic doit circuler uniquement via le sous-réseau SecNet vers le pare-feu (puis, le cas échéant, sur les sous-réseaux frontal ou principal).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-190">We want to block all inbound traffic from the internet to either the Frontend or Backend subnets, traffic should only flow through the SecNet subnet to the firewall (and then if appropriate on to the Frontend or Backend subnets).</span></span> <span data-ttu-id="ea2ea-191">En outre, avec les règles UDR en place, tout trafic ayant atteint les sous-réseaux principal ou frontal est dirigé vers le pare-feu (grâce à l’UDR).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-191">Plus, with the UDR rules in place, any traffic that did make it into the Frontend or Backend subnets would be directed out to the firewall (thanks to UDR).</span></span> <span data-ttu-id="ea2ea-192">Le pare-feu serait considéré comme un flux asymétrique et abandonnerait le trafic sortant.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-192">The firewall would see this as an asymmetric flow and would drop the outbound traffic.</span></span> <span data-ttu-id="ea2ea-193">Par conséquent, il existe trois couches de sécurité protégeant les sous-réseaux frontaux et principaux ; (1) aucun point de terminaison n’est ouvert sur les services cloud FrontEnd001 et BackEnd001, (2) NSGs empêche le trafic provenant d’Internet, (3) le pare-feu abandonne le trafic asymétrique.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-193">Thus there are three layers of security protecting the Frontend and Backend subnets; 1) no open endpoints on the FrontEnd001 and BackEnd001 cloud services, 2) NSGs denying traffic from the Internet, 3) the firewall dropping asymmetric traffic.</span></span>

<span data-ttu-id="ea2ea-194">Point intéressant concernant le groupe de sécurité réseau dans cet exemple : il contient une seule règle, illustrée ci-dessous, qui consiste à refuser le trafic Internet de l’ensemble du réseau virtuel qui inclut le sous-réseau de sécurité.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-194">One interesting point regarding the Network Security Group in this example is that it contains only one rule, shown below, which is to deny internet traffic to the entire virtual network which would include the Security subnet.</span></span> 

    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Isolate the $VNetName VNet `
        from the Internet" `
        -Type Inbound -Priority 100 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *

<span data-ttu-id="ea2ea-195">Toutefois, étant donné que le NSG est associé uniquement aux sous-réseaux frontaux et principaux, la règle n’est pas exécutée sur le trafic entrant du sous-réseau de sécurité.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-195">However, since the NSG is only bound to the Frontend and Backend subnets, the rule isn’t processed on traffic inbound to the Security subnet.</span></span> <span data-ttu-id="ea2ea-196">Par conséquent, même si la règle NSG n’indique aucun trafic Internet sur une adresse de réseau virtuel, le NSG n’est jamais lié au sous-réseau de sécurité, le trafic passe au sous-réseau de sécurité.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-196">As a result, even though the NSG rule says no Internet traffic to any address on the VNet, because the NSG was never bound to the Security subnet, traffic will flow to the Security subnet.</span></span>

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $FESubnet -VirtualNetworkName $VNetName

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $BESubnet -VirtualNetworkName $VNetName

## <a name="firewall-rules"></a><span data-ttu-id="ea2ea-197">Règles de pare-feu</span><span class="sxs-lookup"><span data-stu-id="ea2ea-197">Firewall Rules</span></span>
<span data-ttu-id="ea2ea-198">Sur le pare-feu, vous devrez créer les règles de transfert.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-198">On the firewall, forwarding rules will need to be created.</span></span> <span data-ttu-id="ea2ea-199">Étant donné que le pare-feu bloque ou transfère le trafic entrant, sortant ou intra-réseau virtuel, de nombreuses règles de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-199">Since the firewall is blocking or forwarding all inbound, outbound, and intra-VNet traffic many firewall rules are needed.</span></span> <span data-ttu-id="ea2ea-200">Tout trafic entrant atteindra l’adresse IP publique de service de sécurité (sur différents ports), pour être traité par le pare-feu.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-200">Also, all inbound traffic will hit the Security Service public IP address (on different ports), to be processed by the firewall.</span></span> <span data-ttu-id="ea2ea-201">L’une des meilleures pratiques consiste à faire un schéma des flux logiques avant de configurer les règles de sous-réseau et de pare-feu afin d’éviter la reprise du travail par la suite.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-201">A best practice is to diagram the logical flows before setting up the subnets and firewall rules to avoid rework later.</span></span> <span data-ttu-id="ea2ea-202">La figure qui suit est une vue logique des règles de pare-feu de cet exemple :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-202">The following figure is a logical view of the firewall rules for this example:</span></span>

<span data-ttu-id="ea2ea-203">![Affichage logique des règles de pare-feu][2]</span><span class="sxs-lookup"><span data-stu-id="ea2ea-203">![Logical View of the Firewall Rules][2]</span></span>

> [!NOTE]
> <span data-ttu-id="ea2ea-204">Selon l’appliance virtuelle réseau utilisée, les ports de gestion peuvent varier.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-204">Based on the Network Virtual Appliance used, the management ports will vary.</span></span> <span data-ttu-id="ea2ea-205">Dans cet exemple, il est fait référence à un pare-feu Barracuda NextGen Firewall utilisant les ports 22, 801 et 807.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-205">In this example a Barracuda NextGen Firewall is referenced which uses ports 22, 801, and 807.</span></span> <span data-ttu-id="ea2ea-206">Veuillez consulter la documentation du fournisseur d’appliance pour rechercher les ports exacts utilisés pour la gestion de l’appareil utilisé.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-206">Please consult the appliance vendor documentation to find the exact ports used for management of the device being used.</span></span>
> 
> 

### <a name="logical-rule-description"></a><span data-ttu-id="ea2ea-207">Description de la logique de règle</span><span class="sxs-lookup"><span data-stu-id="ea2ea-207">Logical Rule Description</span></span>
<span data-ttu-id="ea2ea-208">Dans le diagramme logique ci-dessus, le sous-réseau de sécurité n’est pas affiché car le pare-feu est la seule ressource de ce sous-réseau, et ce diagramme présente les règles de pare-feu et la façon dont elles autorisent ou refusent les flux et non les itinéraires réels.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-208">In the logical diagram above, the security subnet is not shown since the firewall is the only resource on that subnet, and this diagram is showing the firewall rules and how they logically allow or deny traffic flows and not the actual routed path.</span></span> <span data-ttu-id="ea2ea-209">En outre, les ports externes sélectionnés pour le trafic RDP appartiennent à la plage supérieure de ports (8014 – 8026) et ont été sélectionnés pour s’aligner à peu près sur les deux derniers octets de l’adresse IP locale, pour faciliter la lecture (par exemple, l’adresse du serveur local 10.0.1.4 est associée à un port externe 8014), cependant, tous les ports supérieurs non conflictuels peuvent être utilisés.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-209">Also, the external ports selected for the RDP traffic are higher ranged ports (8014 – 8026) and were selected to somewhat align with the last two octets of the local IP address for easier readability (e.g. local server address 10.0.1.4 is associated with external port 8014), however any higher non-conflicting ports could be used.</span></span>

<span data-ttu-id="ea2ea-210">Dans cet exemple, nous avons besoin de 7 types de règles, qui se présentent comme suit :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-210">For this example, we need 7 types of rules, these rule types are described as follows:</span></span>

* <span data-ttu-id="ea2ea-211">Règles externes (pour le trafic entrant) :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-211">External Rules (for inbound traffic):</span></span>
  1. <span data-ttu-id="ea2ea-212">Règle de gestion de pare-feu : cette règle de redirection de l’application autorise le trafic à traverser les ports de gestion de l’appliance virtuelle du réseau.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-212">Firewall Management Rule: This App Redirect rule allows traffic to pass to the management ports of the network virtual appliance.</span></span>
  2. <span data-ttu-id="ea2ea-213">Règles de RDP (pour chaque serveur Windows) : ces quatre réseaux (une pour chaque serveur) permettront la gestion des serveurs individuels via RDP.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-213">RDP Rules (for each windows server): These four rules (one for each server) will allow management of the individual servers via RDP.</span></span> <span data-ttu-id="ea2ea-214">Ces éléments pourraient être regroupés en une règle, en fonction de la capacité de l’appliance virtuelle réseau utilisée.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-214">This could also be bundled into one rule depending on the capabilities of the Network Virtual Appliance being used.</span></span>
  3. <span data-ttu-id="ea2ea-215">Règles de trafic d’application : elles sont au nombre de deux, la première correspondant au trafic web frontal, et la seconde, pour le trafic de l’ordinateur principal (par exemple, serveur web vers couche de données).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-215">Application Traffic Rules: There are two Application Traffic Rules, the first for the front end web traffic, and the second for the back end traffic (eg web server to data tier).</span></span> <span data-ttu-id="ea2ea-216">La configuration de ces règles dépend de l’architecture réseau (sur lequel sont placés vos serveurs) et les flux de trafic (direction du flux de trafic et ports utilisés).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-216">The configuration of these rules will depend on the network architecture (where your servers are placed) and traffic flows (which direction the traffic flows, and which ports are used).</span></span>
     * <span data-ttu-id="ea2ea-217">La première règle permet au trafic d’application réel de parvenir au serveur d’applications.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-217">The first rule will allow the actual application traffic to reach the application server.</span></span> <span data-ttu-id="ea2ea-218">Les autres règles concernent la sécurité, la gestion, etc., les règles d’application sont celles qui permettent aux utilisateurs externes ou aux services d’accéder aux applications.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-218">While the other rules allow for security, management, etc., Application Rules are what allow external users or services to access the application(s).</span></span> <span data-ttu-id="ea2ea-219">Pour cet exemple, il existe un serveur web sur le port 80, et donc une seule règle d’application redirige le trafic entrant vers l’adresse IP externe, vers l’adresse IP interne des serveurs web.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-219">For this example, there is a single web server on port 80, thus a single firewall application rule will redirect inbound traffic to the external IP, to the web servers internal IP address.</span></span> <span data-ttu-id="ea2ea-220">L’adresse réseau de la session de trafic redirigée sera traduite vers le serveur interne.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-220">The redirected traffic session would be NAT’d to the internal server.</span></span>
     * <span data-ttu-id="ea2ea-221">La seconde règle de trafic d’application est la règle du serveur principal qui permet au serveur web de communiquer avec le serveur AppVM01 (et non AppVM02) via n’importe quel port.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-221">The second Application Traffic Rule is the back end rule to allow the Web Server to talk to the AppVM01 server (but not AppVM02) via any port.</span></span>
* <span data-ttu-id="ea2ea-222">Règles internes (pour le trafic réseau virtuel interne)</span><span class="sxs-lookup"><span data-stu-id="ea2ea-222">Internal Rules (for intra-VNet traffic)</span></span>
  1. <span data-ttu-id="ea2ea-223">Sortie vers règle Internet : cette règle autorise le transfert du trafic en provenance de n’importe quel réseau vers les réseaux sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-223">Outbound to Internet Rule: This rule will allow traffic from any network to pass to the selected networks.</span></span> <span data-ttu-id="ea2ea-224">Cette règle est généralement une règle par défaut déjà présente sur le pare-feu, mais à l’état désactivé.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-224">This rule is usually a default rule already on the firewall, but in a disabled state.</span></span> <span data-ttu-id="ea2ea-225">Pour cet exemple, cette règle doit être activée.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-225">This rule should be enabled for this example.</span></span>
  2. <span data-ttu-id="ea2ea-226">Règle DNS : cette règle autorise uniquement le trafic DNS (port 53) vers le serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-226">DNS Rule: This rule allows only DNS (port 53) traffic to pass to the DNS server.</span></span> <span data-ttu-id="ea2ea-227">Pour cet environnement, la majeure partie du trafic du serveur frontal vers le serveur principal est bloquée. Cette règle autorise spécifiquement DNS à partir de n’importe quel sous-réseau local.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-227">For this environment most traffic from the Frontend to the Backend is blocked, this rule specifically allows DNS from any local subnet.</span></span>
  3. <span data-ttu-id="ea2ea-228">Règle sous-réseau à sous-réseau : cette règle permet à n’importe quel serveur principal du sous-réseau de se connecter à n’importe quel serveur du sous-réseau du serveur frontal (mais pas l’inverse).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-228">Subnet to Subnet Rule: This rule is to allow any server on the back end subnet to connect to any server on the front end subnet (but not the reverse).</span></span>
* <span data-ttu-id="ea2ea-229">Règle de prévention de défaillance (pour le trafic ne répondant à aucun des éléments ci-dessus) :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-229">Fail-safe Rule (for traffic that doesn’t meet any of the above):</span></span>
  1. <span data-ttu-id="ea2ea-230">Refuser toutes les règles de trafic : il doit toujours s’agir de la dernière règle (en termes de priorité) et par conséquent, si un trafic ne correspond à aucune des règles qui précèdent, il sera abandonné par cette règle.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-230">Deny All Traffic Rule: This should always be the final rule (in terms of priority), and as such if a traffic flows fails to match any of the preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="ea2ea-231">Il s’agit d’une règle par défaut qui est en général activée, et en général, aucune modification n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-231">This is a default rule and usually activated, no modifications are generally needed.</span></span>

> [!TIP]
> <span data-ttu-id="ea2ea-232">Sur la deuxième règle de trafic de l’application, n’importe quel port est autorisé pour simplifier cet exemple. Dans un scénario réel, le port le plus spécifique et les plages d’adresses doivent être utilisés pour réduire la surface d’attaque de cette règle.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-232">On the second application traffic rule, any port is allowed for easy of this example, in a real scenario the most specific port and address ranges should be used to reduce the attack surface of this rule.</span></span>
> 
> 

<br />

> [!IMPORTANT]
> <span data-ttu-id="ea2ea-233">Une fois que toutes les règles ci-dessus sont créées, il est important de revoir la priorité de chaque règle pour s’assurer que le trafic sera autorisé ou rejeté comme souhaité.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-233">Once all of the above rules are created, it’s important to review the priority of each rule to ensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="ea2ea-234">Pour cet exemple, les règles sont classées par ordre de priorité.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-234">For this example, the rules are in priority order.</span></span> <span data-ttu-id="ea2ea-235">Il est facile d’être bloqué hors du pare-feu si les règles ne sont pas dans l’ordre.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-235">It's easy to be locked out of the firewall due to mis-ordered rules.</span></span> <span data-ttu-id="ea2ea-236">Vous devez au minimum vous assurer que la gestion du pare-feu lui-même est la priorité absolue.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-236">At a minimum, ensure the management for the firewall itself is always the absolute highest priority rule.</span></span>
> 
> 

### <a name="rule-prerequisites"></a><span data-ttu-id="ea2ea-237">Préalable en matière de règles</span><span class="sxs-lookup"><span data-stu-id="ea2ea-237">Rule Prerequisites</span></span>
<span data-ttu-id="ea2ea-238">Condition préalable pour que la machine virtuelle exécute le pare-feu : les points de terminaison publics.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-238">One prerequisite for the Virtual Machine running the firewall are public endpoints.</span></span> <span data-ttu-id="ea2ea-239">Pour que le pare-feu traite le trafic, les points de terminaison publics appropriés doivent être ouverts.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-239">For the firewall to process traffic the appropriate public endpoints must be open.</span></span> <span data-ttu-id="ea2ea-240">Cet exemple comporte trois types de trafic : 1) Trafic de gestion pour contrôler le pare-feu et les règles de pare-feu, 2)Trafic RDP pour contrôler les serveurs Windows et 3) Trafic d’application.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-240">There are three types of traffic in this example; 1) Management traffic to control the firewall and firewall rules, 2) RDP traffic to control the windows servers, and 3) Application Traffic.</span></span> <span data-ttu-id="ea2ea-241">Voici les trois colonnes de types de trafic situées dans la partie supérieure des règles de la vue logique des règles de pare-feu ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-241">These are the three columns of traffic types in the upper half of logical view of the firewall rules above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ea2ea-242">Il ne faut surtout pas oublier que **tout** le trafic passe par le pare-feu.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-242">A key takeway here is to remember that **all** traffic will come through the firewall.</span></span> <span data-ttu-id="ea2ea-243">Donc, depuis le bureau du serveur IIS01, même s’il se trouve dans le Service cloud du serveur frontal et sur le sous- réseau frontal, pour accéder à ce serveur, nous aurons besoin d’établir une connexion RDP vers le pare-feu sur le port 8014, puis nous devrons autoriser le pare-feu à acheminer la requête RDP en interne vers le port RDP IIS01.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-243">So to remote desktop to the IIS01 server, even though it's in the Front End Cloud Service and on the Front End subnet, to access this server we will need to RDP to the firewall on port 8014, and then allow the firewall to route the RDP request internally to the IIS01 RDP Port.</span></span> <span data-ttu-id="ea2ea-244">Le bouton « Se connecter » du portail Azure ne fonctionne pas car il n’existe pas d’itinéraire RDP vers IIS01 (du point de vue du portail).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-244">The Azure portal's "Connect" button won't work because there is no direct RDP path to IIS01 (as far as the portal can see).</span></span> <span data-ttu-id="ea2ea-245">En d’autres termes, toutes les connexions à partir d’Internet seront établies avec le service de sécurité et un Port, par exemple, secscv001.cloudapp.net:xxxx (se reporter au schéma ci-dessus mapper le port externe et l’adresse et le port IP interne).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-245">This means all connections from the internet will be to the Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx (reference the above diagram for the mapping of External Port and Internal IP and Port).</span></span>
> 
> 

<span data-ttu-id="ea2ea-246">Un point de terminaison peut être ouvert au moment de la création de la machine virtuelle ou après sa création (comme dans le script d’exemple), et affiché ci-dessous dans cet extrait de code (Remarque : tout élément qui est précédé du signe dollar (par exemple, $VMName[$i]), est une variable définie par l’utilisateur à partir du script de la section Références de ce document.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-246">An endpoint can be opened either at the time of VM creation or post build as is done in the example script and shown below in this code snippet (Note; any item beginning with a dollar sign (e.g.: $VMName[$i]) is a user defined variable from the script in the reference section of this document.</span></span> <span data-ttu-id="ea2ea-247">Le « $I » entre crochets, [$i], représente le nombre de tableaux d’une machine virtuelle dans un tableau de machines virtuelles) :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-247">The “$i” in brackets, [$i], represents the array number of a specific VM in an array of VMs):</span></span>

    Add-AzureEndpoint -Name "HTTP" -Protocol tcp -PublicPort 80 -LocalPort 80 `
        -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | `
        Update-AzureVM

<span data-ttu-id="ea2ea-248">Bien que ce ne soit pas clairement indiqué ici en raison de l’utilisation de variables, les points de terminaison sont **uniquement** ouverts sur le Service de sécurité cloud.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-248">Although not clearly shown here due to the use of variables, but endpoints are **only** opened on the Security Cloud Service.</span></span> <span data-ttu-id="ea2ea-249">Ainsi, on est sûr que la totalité du trafic entrant est gérée (acheminé, les adresses traduites, annulé) par le pare-feu.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-249">This is to ensure that all inbound traffic is handled (routed, NAT'd, dropped) by the firewall.</span></span>

<span data-ttu-id="ea2ea-250">Un client de gestion devra être installé sur un ordinateur pour gérer le pare-feu et créer les configurations nécessaires.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-250">A management client will need to be installed on a PC to manage the firewall and create the configurations needed.</span></span> <span data-ttu-id="ea2ea-251">Consultez la documentation du fournisseur de votre pare-feu (ou autre NVA) sur la façon de gérer l’appareil.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-251">See the documentation from your firewall (or other NVA) vendor on how to manage the device.</span></span> <span data-ttu-id="ea2ea-252">Le reste de cette section et la section suivante, Création de règles de pare-feu, décrivent la configuration du pare-feu lui-même par le biais du client de gestion des fournisseurs (et non par le portail Azure ou PowerShell).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-252">The remainder of this section and the next section, Firewall Rules Creation, will describe the configuration of the firewall itself, through the vendors management client (i.e. not the Azure portal or PowerShell).</span></span>

<span data-ttu-id="ea2ea-253">Les instructions pour le téléchargement client et la connexion à Barracuda utilisé dans cet exemple se trouvent ici : [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="ea2ea-253">Instructions for client download and connecting to the Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="ea2ea-254">Une fois connecté au pare-feu, mais avant la création des règles de pare-feu, il existe deux classes d’objets pré-requises qui peuvent faciliter la création des règles, Réseau et objets service.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-254">Once logged onto the firewall but before creating firewall rules, there are two prerequisite object classes that can make creating the rules easier; Network & Service objects.</span></span>

<span data-ttu-id="ea2ea-255">Pour cet exemple, trois objets réseaux nommés doivent être définis (un pour le sous-réseau du serveur frontal et le sous-réseau principal, et un objet réseau pour l’adresse IP du serveur DNS).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-255">For this example, three named network objects should be defined (one for the Frontend subnet and the Backend subnet, also a network object for the IP address of the DNS server).</span></span> <span data-ttu-id="ea2ea-256">Pour créer un réseau nommé, à partir du tableau de bord client admin Barracuda NG, accédez à l’onglet Configuration. Dans la section de Configuration opérationnelle, cliquez sur Ensemble de règles, puis, dans le menu Objets de pare-feu, cliquez sur « Réseaux ». Ensuite, dans le menu Édition de réseau, cliquez sur Nouveau.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-256">To create a named network; starting from the Barracuda NG Admin client dashboard, navigate to the configuration tab, in the Operational Configuration section click Ruleset, then click “Networks” under the Firewall Objects menu, then click New in the Edit Networks menu.</span></span> <span data-ttu-id="ea2ea-257">L’objet réseau peut désormais être créé, en ajoutant le nom et le préfixe :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-257">The network object can now be created, by adding the name and the prefix:</span></span>

<span data-ttu-id="ea2ea-258">![Créer un objet réseau de serveur frontal][3]</span><span class="sxs-lookup"><span data-stu-id="ea2ea-258">![Create a FrontEnd Network Object][3]</span></span>

<span data-ttu-id="ea2ea-259">Cette opération crée un réseau nommé correspondant au sous-réseau du serveur frontal. Un objet similaire doit être créé pour le sous-réseau du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-259">This will create a named network for the FrontEnd subnet, a similar object should be created for the BackEnd subnet as well.</span></span> <span data-ttu-id="ea2ea-260">Désormais les sous-réseaux peuvent être référencés plus facilement par nom dans les règles de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-260">Now the subnets can be more easily referenced by name in the firewall rules.</span></span>

<span data-ttu-id="ea2ea-261">Créer un objet de serveur DNS :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-261">For the DNS Server Object:</span></span>

<span data-ttu-id="ea2ea-262">![Créer un objet de serveur DNS][4]</span><span class="sxs-lookup"><span data-stu-id="ea2ea-262">![Create a DNS Server Object][4]</span></span>

<span data-ttu-id="ea2ea-263">La référence d’adresse IP unique sera utilisée comme règle DNS plus tard dans le document.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-263">This single IP address reference will be utilized in a DNS rule later in the document.</span></span>

<span data-ttu-id="ea2ea-264">Le deuxième objet requis sont les Services.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-264">The second prerequisite objects are Services objects.</span></span> <span data-ttu-id="ea2ea-265">Il représente les ports de connexion RDP de chaque serveur.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-265">These will represent the RDP connection ports for each server.</span></span> <span data-ttu-id="ea2ea-266">Étant donné que l’objet de service RDP existant est lié au port RDP par défaut, 3389, de nouveaux services peuvent être créés pour autoriser le trafic à partir des ports externes (8014-8026).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-266">Since the existing RDP service object is bound to the default RDP port, 3389, new Services can be created to allow traffic from the external ports (8014-8026).</span></span> <span data-ttu-id="ea2ea-267">Les nouveaux ports peuvent également être ajoutés au service RDP existant, mais pour faciliter la démonstration, une règle individuelle doit être créée pour chaque serveur.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-267">The new ports could also be added to the existing RDP service, but for ease of demonstration, an individual rule for each server can be created.</span></span> <span data-ttu-id="ea2ea-268">Pour créer une nouvelle règle RDP pour un serveur, à partir du tableau de bord client administrateur Barracuda NG, accédez à l’onglet configuration. Dans la section Configuration opérationnelle, cliquez sur l’ensemble de règles, puis, dans le menu Objets de pare-feu, cliquez sur « Services », faites défiler la liste des services, puis sélectionnez le service « RDP ».</span><span class="sxs-lookup"><span data-stu-id="ea2ea-268">To create a new RDP rule for a server; starting from the Barracuda NG Admin client dashboard, navigate to the configuration tab, in the Operational Configuration section click Ruleset, then click “Services” under the Firewall Objects menu, scroll down the list of services and select the “RDP” service.</span></span> <span data-ttu-id="ea2ea-269">Effectuez un clic droit et sélectionnez Copier, puis avec le bouton droit, cliquez et sélectionnez Coller.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-269">Right-click and select copy, then right-click and select Paste.</span></span> <span data-ttu-id="ea2ea-270">Il existe désormais un objet de Service RDP-Copie1 qui peut être modifié.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-270">There is now a RDP-Copy1 Service Object that can be edited.</span></span> <span data-ttu-id="ea2ea-271">Cliquez avec le bouton droit sur RDP-Coy1, sélectionnez Modifier. La fenêtre Modifier l’objet de service s’affiche s’affiche comme indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-271">Right-click RDP-Copy1 and select Edit, the Edit Service Object window will pop up as shown here:</span></span>

<span data-ttu-id="ea2ea-272">![Copie de la règle RDP par défaut][5]</span><span class="sxs-lookup"><span data-stu-id="ea2ea-272">![Copy of Default RDP Rule][5]</span></span>

<span data-ttu-id="ea2ea-273">Les valeurs peuvent ensuite être modifiées pour représenter le service RDP d’un serveur spécifique.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-273">The values can then be edited to represent the RDP service for a specific server.</span></span> <span data-ttu-id="ea2ea-274">Pour AppVM01, la règle RDP par défaut doit être modifiée pour intégrer de nouveaux nom de service, description, et port RDP externe utilisé dans le schéma de la Figure 8 (Remarque : les ports passent du port RDP par défaut 3389 au port externe utilisé pour ce serveur spécifique, dans le cas où AppVM01, le port externe, est le 8025). Le service modifié est illustré ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-274">For AppVM01 the above default RDP rule should be modified to reflect a new Service Name, Description, and external RDP Port used in the Figure 8 diagram (Note: the ports are changed from the RDP default of 3389 to the external port being used for this specific server, in the case of AppVM01 the external Port is 8025) the modified service is shown below:</span></span>

<span data-ttu-id="ea2ea-275">![Règle AppVM01][6]</span><span class="sxs-lookup"><span data-stu-id="ea2ea-275">![AppVM01 Rule][6]</span></span>

<span data-ttu-id="ea2ea-276">Ce processus doit être répété pour créer des Services RDP pour les serveurs restants (AppVM02, DNS01 et IIS01).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-276">This process must be repeated to create RDP Services for the remaining servers; AppVM02, DNS01, and IIS01.</span></span> <span data-ttu-id="ea2ea-277">La création de ces services facilite la création de règles et la rend plus évidente dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-277">The creation of these Services will make the Rule creation simpler and more obvious in the next section.</span></span>

> [!NOTE]
> <span data-ttu-id="ea2ea-278">Un service de protocole RDP pour le pare-feu est inutile pour deux raisons. 1) tout d’abord, la machine virtuelle pare-feu est une image Linux, et SSH sera utilisé sur le port 22 de gestion de machine virtuelle et non sur RDP et 2) port 22 et deux autres ports de gestion sont autorisés dans la première règle de gestion décrite ci-dessous. Ils permettent de gérer la connectivité de gestion.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-278">An RDP service for the Firewall is not needed for two reasons; 1) first the firewall VM is a Linux based image so SSH would be used on port 22 for VM management instead of RDP, and 2) port 22, and two other management ports are allowed in the first management rule described below to allow for management connectivity.</span></span>
> 
> 

### <a name="firewall-rules-creation"></a><span data-ttu-id="ea2ea-279">Création de règles de pare-feu</span><span class="sxs-lookup"><span data-stu-id="ea2ea-279">Firewall Rules Creation</span></span>
<span data-ttu-id="ea2ea-280">Il existe trois types de règles de pare-feu utilisées dans cet exemple, et elles sont toutes représentées par des icônes distinctes :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-280">There are three types of firewall rules used in this example, they all have distinct icons:</span></span>

<span data-ttu-id="ea2ea-281">La règle de redirection d’application : ![Icône de redirection d’application][7]</span><span class="sxs-lookup"><span data-stu-id="ea2ea-281">The Application Redirect rule: ![Application Redirect Icon][7]</span></span>

<span data-ttu-id="ea2ea-282">La règle NAT de destination : ![Icône NAT de destination][8]</span><span class="sxs-lookup"><span data-stu-id="ea2ea-282">The Destination NAT rule: ![Destination NAT Icon][8]</span></span>

<span data-ttu-id="ea2ea-283">La règle Pass : ![Icône de réussite][9]</span><span class="sxs-lookup"><span data-stu-id="ea2ea-283">The Pass rule: ![Pass Icon][9]</span></span>

<span data-ttu-id="ea2ea-284">Vous trouverez d’autres informations sur ces règles sur le site web de Barracuda.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-284">More information on these rules can be found at the Barracuda web site.</span></span>

<span data-ttu-id="ea2ea-285">Pour créer les règles suivantes (ou consulter les règles par défaut existantes), sur le tableau de bord du client administrateur de Barracuda NG, accédez à l’onglet configuration. Dans la section Configuration opérationnelle, cliquez sur Ensemble de règles.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-285">To create the following rules (or verify existing default rules), starting from the Barracuda NG Admin client dashboard, navigate to the configuration tab, in the Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="ea2ea-286">Une grille nommée « Règles principales » affiche des règles actives et désactivées sur ce pare-feu.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-286">A grid called, “Main Rules” will show the existing active and deactivated rules on this firewall.</span></span> <span data-ttu-id="ea2ea-287">Dans le coin supérieur droit de cette grille se trouve un petit bouton « + » vert. Cliquez dessus pour créer une nouvelle règle (Remarque : votre pare-feu peut être « verrouillé » pour les modifications. Si vous voyez un bouton marqué « Verrouiller » et que vous êtes incapable de créer ou d’éditer des règles, cliquez dessus pour « déverrouiller » l’ensemble de règles et autoriser la modification).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-287">In the upper right corner of this grid is a small, green “+” button, click this to create a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable to create or edit rules, click this button to “unlock” the rule set and allow editing).</span></span> <span data-ttu-id="ea2ea-288">Si vous souhaitez modifier une règle existante, sélectionnez cette règle, cliquez avec le bouton droit et sélectionnez Modifier la règle.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-288">If you wish to edit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="ea2ea-289">Une fois que vos règles sont créées et/ou modifiées, elles doivent être transférées vers le pare-feu et activées. Si cette opération n’est pas effectuée, les modifications de règles ne prendront pas effet.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-289">Once your rules are created and/or modified, they must be pushed to the firewall and then activated, if this is not done the rule changes will not take effect.</span></span> <span data-ttu-id="ea2ea-290">Le processus d’activation et de transfert est décrit en dessous des descriptions de règles de détails.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-290">The push and activation process is described below the details rule descriptions.</span></span>

<span data-ttu-id="ea2ea-291">Les caractéristiques de chaque règle nécessaire pour compléter cet exemple sont décrites comme suit :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-291">The specifics of each rule required to complete this example are described as follows:</span></span>

* <span data-ttu-id="ea2ea-292">**Règle de gestion de pare-feu**: cette règle de redirection de l’application autorise le trafic à franchir les ports de gestion de l’appliance virtuelle du réseau (dans cet exemple, un pare-feu Barracuda NextGen).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-292">**Firewall Management Rule**: This App Redirect rule allows traffic to pass to the management ports of the network virtual appliance, in this example a Barracuda NextGen Firewall.</span></span> <span data-ttu-id="ea2ea-293">Les ports de gestion sont 801, 807 et éventuellement, 22.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-293">The management ports are 801, 807 and optionally 22.</span></span> <span data-ttu-id="ea2ea-294">Les ports interne et externe sont identiques (pas de transfert de port).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-294">The external and internal ports are the same (i.e. no port translation).</span></span> <span data-ttu-id="ea2ea-295">Cette règle, SETUP-MGMT-ACCESS, est une règle par défaut et elle est activée par défaut (dans la version 6.1 du pare-feu Barracuda NextGen Firewall).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-295">This rule, SETUP-MGMT-ACCESS, is a default rule and enabled by default (in Barracuda NextGen Firewall version 6.1).</span></span>
  
    <span data-ttu-id="ea2ea-296">![Règle de gestion de pare-feu][10]</span><span class="sxs-lookup"><span data-stu-id="ea2ea-296">![Firewall Management Rule][10]</span></span>

> [!TIP]
> <span data-ttu-id="ea2ea-297">L’espace d’adresse de cette règle est « Tout » si les plages d’adresses IP de gestion sont connues. La réduction de la portée se traduit par la réduction de la surface d’attaque des ports de gestion.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-297">The source address space in this rule is Any, if the management IP address ranges are known, reducing this scope would also reduce the attack surface to the management ports.</span></span>
> 
> 

* <span data-ttu-id="ea2ea-298">**Règles RDP** : ces règles NAT de destination permettent la gestion des serveurs individuels via RDP.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-298">**RDP Rules**:  These Destination NAT rules will allow management of the individual servers via RDP.</span></span>
  <span data-ttu-id="ea2ea-299">Il existe quatre champs critiques nécessaires à la création de cette règle :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-299">There are four critical fields needed to create this rule:</span></span>
  
  1. <span data-ttu-id="ea2ea-300">Source : pour permettre l’exécution de RDP depuis n’importe quel endroit, la référence « Tout » est utilisée dans le champ Source.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-300">Source – to allow RDP from anywhere, the reference “Any” is used in the Source field.</span></span>
  2. <span data-ttu-id="ea2ea-301">Service : utilise l’objet de Service approprié créé précédemment, dans ce cas « AppVM01 RDP ». Les ports externes redirigent le trafic vers l’adresse IP locale des serveurs et vers le port 3386 (port RDP par défaut).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-301">Service – use the appropriate Service Object created earlier, in this case “AppVM01 RDP”, the external ports redirect to the servers local IP address and to port 3386 (the default RDP port).</span></span> <span data-ttu-id="ea2ea-302">Cette règle spécifique sert à l’accès RDP à AppVM01.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-302">This specific rule is for RDP access to AppVM01.</span></span>
  3. <span data-ttu-id="ea2ea-303">Destination : doit être le *port local sur le pare-feu*, « DCHP IP Local 1 » ou eth0 si vous utilisez des adresses IP statiques.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-303">Destination – should be the *local port on the firewall*, “DCHP 1 Local IP” or eth0 if using static IPs.</span></span> <span data-ttu-id="ea2ea-304">Le nombre ordinal (eth0, eth1, etc.) peut être différent si votre équipement réseau dispose de plusieurs interfaces locales.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-304">The ordinal number (eth0, eth1, etc) may be different if your network appliance has multiple local interfaces.</span></span> <span data-ttu-id="ea2ea-305">C’est le port à partir duquel le port fait ses envois (il peut s’agir du même port que le port de réception), la destination réellement acheminée est celle qui se trouve dans le champ Liste cible.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-305">This is the port the firewall is sending out from (may be the same as the receiving port), the actual routed destination is in the Target List field.</span></span>
  4. <span data-ttu-id="ea2ea-306">Redirection : cette section indique l’appliance virtuelle vers lequel rediriger finalement ce trafic.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-306">Redirection – this section tells the virtual appliance where to ultimately redirect this traffic.</span></span> <span data-ttu-id="ea2ea-307">La redirection la plus simple consiste à placer l’adresse IP et le Port (facultatif) dans le champ Liste des cibles.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-307">The simplest redirection is to place the IP and Port (optional) in the Target List field.</span></span> <span data-ttu-id="ea2ea-308">Si aucun port n’est utilisé, c’est le port de destination de la demande entrante qui est utilisé (c’est-à-dire aucune traduction), si un port est désigné, le port est également traduit avec l’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-308">If no port is used the destination port on the inbound request will be used (ie no translation), if a port is designated the port will also be NAT’d along with the IP address.</span></span>
     
     <span data-ttu-id="ea2ea-309">![Règle RDP de pare-feu][11]</span><span class="sxs-lookup"><span data-stu-id="ea2ea-309">![Firewall RDP Rule][11]</span></span>
     
     <span data-ttu-id="ea2ea-310">Un total de quatre règles RDP doit être créé :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-310">A total of four RDP rules will need to be created:</span></span> 
     
     | <span data-ttu-id="ea2ea-311">Nom de la règle</span><span class="sxs-lookup"><span data-stu-id="ea2ea-311">Rule Name</span></span> | <span data-ttu-id="ea2ea-312">Serveur</span><span class="sxs-lookup"><span data-stu-id="ea2ea-312">Server</span></span> | <span data-ttu-id="ea2ea-313">de diffusion en continu</span><span class="sxs-lookup"><span data-stu-id="ea2ea-313">Service</span></span> | <span data-ttu-id="ea2ea-314">Liste des cibles</span><span class="sxs-lookup"><span data-stu-id="ea2ea-314">Target List</span></span> |
     | --- | --- | --- | --- |
     | <span data-ttu-id="ea2ea-315">RDP-vers-IIS01</span><span class="sxs-lookup"><span data-stu-id="ea2ea-315">RDP-to-IIS01</span></span> |<span data-ttu-id="ea2ea-316">IIS01</span><span class="sxs-lookup"><span data-stu-id="ea2ea-316">IIS01</span></span> |<span data-ttu-id="ea2ea-317">IIS01 RDP</span><span class="sxs-lookup"><span data-stu-id="ea2ea-317">IIS01 RDP</span></span> |<span data-ttu-id="ea2ea-318">10.0.1.4:3389</span><span class="sxs-lookup"><span data-stu-id="ea2ea-318">10.0.1.4:3389</span></span> |
     | <span data-ttu-id="ea2ea-319">RDP-vers-DNS01</span><span class="sxs-lookup"><span data-stu-id="ea2ea-319">RDP-to-DNS01</span></span> |<span data-ttu-id="ea2ea-320">DNS01</span><span class="sxs-lookup"><span data-stu-id="ea2ea-320">DNS01</span></span> |<span data-ttu-id="ea2ea-321">DNS01 RDP</span><span class="sxs-lookup"><span data-stu-id="ea2ea-321">DNS01 RDP</span></span> |<span data-ttu-id="ea2ea-322">10.0.2.4:3389</span><span class="sxs-lookup"><span data-stu-id="ea2ea-322">10.0.2.4:3389</span></span> |
     | <span data-ttu-id="ea2ea-323">RDP 0 AppVM01</span><span class="sxs-lookup"><span data-stu-id="ea2ea-323">RDP-to-AppVM01</span></span> |<span data-ttu-id="ea2ea-324">AppVM01</span><span class="sxs-lookup"><span data-stu-id="ea2ea-324">AppVM01</span></span> |<span data-ttu-id="ea2ea-325">RDP AppVM01</span><span class="sxs-lookup"><span data-stu-id="ea2ea-325">AppVM01 RDP</span></span> |<span data-ttu-id="ea2ea-326">10.0.2.5:3389</span><span class="sxs-lookup"><span data-stu-id="ea2ea-326">10.0.2.5:3389</span></span> |
     | <span data-ttu-id="ea2ea-327">RDP-vers-AppVM02</span><span class="sxs-lookup"><span data-stu-id="ea2ea-327">RDP-to-AppVM02</span></span> |<span data-ttu-id="ea2ea-328">AppVM02</span><span class="sxs-lookup"><span data-stu-id="ea2ea-328">AppVM02</span></span> |<span data-ttu-id="ea2ea-329">AppVm02 RDP</span><span class="sxs-lookup"><span data-stu-id="ea2ea-329">AppVm02 RDP</span></span> |<span data-ttu-id="ea2ea-330">10.0.2.6:3389</span><span class="sxs-lookup"><span data-stu-id="ea2ea-330">10.0.2.6:3389</span></span> |

> [!TIP]
> <span data-ttu-id="ea2ea-331">Affiner la portée des champs Source et Service réduira la surface d’attaque.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-331">Narrowing down the scope of the Source and Service fields will reduce the attack surface.</span></span> <span data-ttu-id="ea2ea-332">Vous devez utiliser la portée la plus limitée possible, qui permet toutefois d’utiliser la fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-332">The most limited scope that will allow functionality should be used.</span></span>
> 
> 

* <span data-ttu-id="ea2ea-333">**Règles de trafic d’application**: elles sont au nombre de deux, la première correspondant au trafic web frontal, et la seconde, pour le trafic de l’ordinateur principal (par exemple, serveur web vers couche de données).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-333">**Application Traffic Rules**: There are two Application Traffic Rules, the first for the front end web traffic, and the second for the back end traffic (eg web server to data tier).</span></span> <span data-ttu-id="ea2ea-334">La configuration de ces règles dépend de l’architecture du réseau sur lequel sont placés vos serveurs et des flux de trafic (sens du flux de trafic et les ports utilisés).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-334">These rules will depend on the network architecture (where your servers are placed) and traffic flows (which direction the traffic flows, and which ports are used).</span></span>
  
    <span data-ttu-id="ea2ea-335">Le premier concerne la règle frontale de trafic web :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-335">First discussed is the front end rule for web traffic:</span></span>
  
    <span data-ttu-id="ea2ea-336">![Règle web de pare-feu][12]</span><span class="sxs-lookup"><span data-stu-id="ea2ea-336">![Firewall Web Rule][12]</span></span>
  
    <span data-ttu-id="ea2ea-337">La règle Destination NAT permet au trafic de l’application d’atteindre le serveur d’applications.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-337">This Destination NAT rule allows the actual application traffic to reach the application server.</span></span> <span data-ttu-id="ea2ea-338">Les autres règles concernent la sécurité, la gestion, etc., les règles d’application sont celles qui permettent aux utilisateurs externes ou aux services d’accéder aux applications.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-338">While the other rules allow for security, management, etc., Application Rules are what allow external users or services to access the application(s).</span></span> <span data-ttu-id="ea2ea-339">Pour cet exemple, il existe un seul serveur web sur le port 80, et donc, la règle d’application du pare-feu unique redirigera le trafic entrant vers l’adresse IP externe, vers l’adresse IP interne des serveurs web.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-339">For this example, there is a single web server on port 80, thus the single firewall application rule will redirect inbound traffic to the external IP, to the web servers internal IP address.</span></span>
  
    <span data-ttu-id="ea2ea-340">**Remarque**: aucun port n’est affecté dans le champ de la liste cible est, et par conséquent le port entrant 80 (ou 443 pour le Service sélectionné) sera utilisé pour la redirection du serveur web.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-340">**Note**: that there is no port assigned in the Target List field, thus the inbound port 80 (or 443 for the Service selected) will be used in the redirection of the web server.</span></span> <span data-ttu-id="ea2ea-341">Si le serveur web est à l’écoute sur un autre port, par exemple, le port 8080, le champ de liste cible peut être mis à jour vers 10.0.1.4:8080 pour permettre aussi de rediriger le port.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-341">If the web server is listening on a different port, for example port 8080, the Target List field could be updated to 10.0.1.4:8080 to allow for the Port redirection as well.</span></span>
  
    <span data-ttu-id="ea2ea-342">La seconde règle de trafic d’application est la règle principale qui permet au serveur web de communiquer avec le serveur AppVM01 (et non AppVM02) via le service Any.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-342">The next Application Traffic Rule is the back end rule to allow the Web Server to talk to the AppVM01 server (but not AppVM02) via Any service:</span></span>
  
    <span data-ttu-id="ea2ea-343">![Règle AppVM01 de pare-feu][13]</span><span class="sxs-lookup"><span data-stu-id="ea2ea-343">![Firewall AppVM01 Rule][13]</span></span>
  
    <span data-ttu-id="ea2ea-344">Cette règle passe permet à n’importe quel serveur IIS sur le sous-réseau du serveur frontal d’atteindre AppVM01 (adresse IP 10.0.2.5) sur le port Any, en utilisant n’importe quel protocole nécessaire à l’application web.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-344">This Pass rule allows any IIS server on the Frontend subnet to reach the AppVM01 (IP Address 10.0.2.5) on Any port, using any Protocol to access data needed by the web application.</span></span>
  
    <span data-ttu-id="ea2ea-345">Dans cette capture d’écran, l’élément « \<explicite-dest\> » est utilisé dans le champ Destination pour désigner 10.0.2.5 comme destination.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-345">In this screen shot an "\<explicit-dest\>" is used in the Destination field to signify 10.0.2.5 as the destination.</span></span> <span data-ttu-id="ea2ea-346">Il peut être soit explicite, comme indiqué, ou il peut s’agir d’un objet réseau nommé (comme dans les conditions préalables requises pour le serveur DNS).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-346">This could be either explicit as shown or a named Network Object (as was done in the prerequisites for the DNS server).</span></span> <span data-ttu-id="ea2ea-347">C’est à l’administrateur du pare-feu qu’il appartient de choisir la méthode qui sera utilisée.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-347">This is up to the administrator of the firewall as to which method will be used.</span></span> <span data-ttu-id="ea2ea-348">Pour ajouter 10.0.2.5 comme destination explicite, double-cliquez sur la première ligne vide sous \<explicite dest\>, puis entrez l’adresse dans la fenêtre qui s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-348">To add 10.0.2.5 as an Explict Desitnation, double-click on the first blank row under \<explicit-dest\> and enter the address in the window that pops up.</span></span>
  
    <span data-ttu-id="ea2ea-349">Avec cette règle Pass, aucune traduction n’est nécessaire, car il s’agit de trafic interne et donc, la méthode de connexion peut être définie sur « Non SNAT ».</span><span class="sxs-lookup"><span data-stu-id="ea2ea-349">With this Pass Rule, no NAT is needed since this is internal traffic, so the Connection Method can be set to "No SNAT".</span></span>
  
    <span data-ttu-id="ea2ea-350">**Remarque**: le réseau Source de cette règle correspond à n’importe quelle ressource du sous-réseau du serveur frontal s’il n’y en a qu’un, ou s’il s’agit d’un nombre spécifique de serveurs web, une ressource d’objet réseau peut être créée pour préciser ces adresses IP exactes et non l’ensemble du sous-réseau du serveur frontal.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-350">**Note**: The Source network in this rule is any resource on the FrontEnd subnet, if there will only be one, or a known specific number of web servers, a Network Object resource could be created to be more specific to those exact IP addresses instead of the entire Frontend subnet.</span></span>

> [!TIP]
> <span data-ttu-id="ea2ea-351">Cette règle utilise le service « Any » pour faciliter l’installation et l’utilisation. Cela permet d’exécuter une commande ICMPv4 (ping) dans une seule règle.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-351">This rule uses the service “Any” to make the sample application easier to setup and use, this will also allow ICMPv4 (ping) in a single rule.</span></span> <span data-ttu-id="ea2ea-352">Toutefois, cela n’est pas recommandé.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-352">However, this is not a recommended practice.</span></span> <span data-ttu-id="ea2ea-353">Les ports et protocoles (« Services ») doivent être réduits au minimum, tout en permettant le fonctionnement de l’application, et ce, afin de réduire la surface d’attaque au-delà de cette limite.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-353">The ports and protocols (“Services”) should be narrowed to the minimum possible that allows application operation to reduce the attack surface across this boundary.</span></span>
> 
> 

<br />

> [!TIP]
> <span data-ttu-id="ea2ea-354">Bien que cette règle indique une référence explicite-dest utilisée, une approche cohérente doit être utilisée tout au long de la configuration du pare-feu.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-354">Although this rule shows an explicit-dest reference being used, a consistent approach should be used throughout the firewall configuration.</span></span> <span data-ttu-id="ea2ea-355">Il est recommandé d’utiliser l’objet réseau nommé tout au long de la prise en charge pour faciliter la lisibilité et la prise en charge.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-355">It is recommended that the named Network Object be used throughout for easier readability and supportability.</span></span> <span data-ttu-id="ea2ea-356">L’élément explicit-dest est utilisé ici uniquement pour montrer une méthode de référence alternative et est en général déconseillé (en particulier pour des configurations complexes).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-356">The explicit-dest is used here only to show an alternative reference method and is not generally recommended (especially for complex configurations).</span></span>
> 
> 

* <span data-ttu-id="ea2ea-357">**Règle de sortie vers Internet**: cette règle Pass autorise le transfert du trafic en provenance de n’importe quel réseau vers les réseaux de destination sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-357">**Outbound to Internet Rule**: This Pass rule will allow traffic from any Source network to pass to the selected Destination networks.</span></span> <span data-ttu-id="ea2ea-358">Cette règle est généralement une règle par défaut déjà présente sur le pare-feu Barracuda NextGen Firewall, mais à l’état désactivé.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-358">This rule is a default rule usually already on the Barracuda NextGen firewall, but is in a disabled state.</span></span> <span data-ttu-id="ea2ea-359">Un clic droit sur cette règle peut permettre d’accéder à la commande Activer la règle.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-359">Right-clicking on this rule can access the Activate Rule command.</span></span> <span data-ttu-id="ea2ea-360">La règle affichée ici a été modifiée pour y ajouter les deux sous-réseaux locaux créés en tant que références dans la section Configuration requise de ce document à l’attribut Source de cette règle.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-360">The rule shown here has been modified to add the two local subnets that were created as references in the prerequisite section of this document to the Source attribute of this rule.</span></span>
  
    <span data-ttu-id="ea2ea-361">![Règle de trafic sortant de pare-feu][14]</span><span class="sxs-lookup"><span data-stu-id="ea2ea-361">![Firewall Outbound Rule][14]</span></span>
* <span data-ttu-id="ea2ea-362">**Règle DNS** : cette règle autorise uniquement le transfert du trafic DNS (port 53) vers le serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-362">**DNS Rule**: This Pass rule allows only DNS (port 53) traffic to pass to the DNS server.</span></span> <span data-ttu-id="ea2ea-363">Pour cet environnement, la majeure partie du trafic du serveur frontal vers le serveur principal est bloquée. Cette règle autorise spécifiquement DNS.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-363">For this environment most traffic from the FrontEnd to the BackEnd is blocked, this rule specifically allows DNS.</span></span>
  
    <span data-ttu-id="ea2ea-364">![Règle DNS de pare-feu][15]</span><span class="sxs-lookup"><span data-stu-id="ea2ea-364">![Firewall DNS Rule][15]</span></span>
  
    <span data-ttu-id="ea2ea-365">**Remarque** : dans cette capture d’écran, la méthode de connexion est incluse.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-365">**Note**: In this screen shot the Connection Method is included.</span></span> <span data-ttu-id="ea2ea-366">Cette règle concernant le trafic d’adresse IP pour le trafic des adresses IP interne, aucune traduction n’est requise. La méthode de connexion est définie sur « No SNAT » pour cette règle de test.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-366">Because this rule is for internal IP to internal IP address traffic, no NATing is required, this the Connection Method is set to “No SNAT” for this Pass rule.</span></span>
* <span data-ttu-id="ea2ea-367">**Règle sous-réseau à sous-réseau**: la règle Pass est une règle par défaut qui a été activée et modifiée pour permettre à n’importe quel serveur du sous-réseau du serveur principal de se connecter à n’importe quel sous-réseau du serveur frontal.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-367">**Subnet to Subnet Rule**: This Pass rule is a default rule that has been activated and modified to allow any server on the back end subnet to connect to any server on the front end subnet.</span></span> <span data-ttu-id="ea2ea-368">Cette règle concerne l’ensemble du trafic interne, et la méthode de connexion peut être définie sur No SNAT.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-368">This rule is all internal traffic so the Connection Method can be set to No SNAT.</span></span>
  
    <span data-ttu-id="ea2ea-369">![Règle Intra-réseau virtuel de pare-feu][16]</span><span class="sxs-lookup"><span data-stu-id="ea2ea-369">![Firewall Intra-VNet Rule][16]</span></span>
  
    <span data-ttu-id="ea2ea-370">**Remarque** : la case bidirectionnelle n’est pas cochée (et ne l’est pas dans la plupart des règles). Ceci est important dans le sens où cette règle est alors « unidirectionnelle ». Une connexion peut donc être initiée du sous-réseau principal vers le réseau frontal, mais l’opération inverse est impossible.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-370">**Note**: The Bi-directional checkbox is not checked (nor is it checked in most rules), this is significant for this rule in that it makes this rule “one directional”, a connection can be initiated from the back end subnet to the front end network, but not the reverse.</span></span> <span data-ttu-id="ea2ea-371">Si cette case à cocher est activée, cette règle permet le trafic bidirectionnel, ce qui n’est pas souhaitable pour notre diagramme logique.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-371">If that checkbox was checked, this rule would enable bi-directional traffic, which from our logical diagram is not desired.</span></span>
* <span data-ttu-id="ea2ea-372">**Refuser toutes les règles de trafic**: il doit toujours s’agir de la dernière règle (en termes de priorité) et par conséquent si un trafic ne correspond à aucune des règles qui précèdent, il sera abandonné par cette règle.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-372">**Deny All Traffic Rule**: This should always be the final rule (in terms of priority), and as such if a traffic flows fails to match any of the preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="ea2ea-373">Il s’agit d’une règle par défaut qui est en général activée, et en général, aucune modification n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-373">This is a default rule and usually activated, no modifications are generally needed.</span></span> 
  
    <span data-ttu-id="ea2ea-374">![Règle de refus de pare-feu][17]</span><span class="sxs-lookup"><span data-stu-id="ea2ea-374">![Firewall Deny Rule][17]</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ea2ea-375">Une fois que toutes les règles ci-dessus sont créées, il est important de revoir la priorité de chaque règle pour s’assurer que le trafic sera autorisé ou rejeté comme souhaité.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-375">Once all of the above rules are created, it’s important to review the priority of each rule to ensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="ea2ea-376">Pour cet exemple, les règles sont dans l’ordre, dans lequel elles doivent apparaître dans la grille principale des règles de transfert du Client de gestion Barracuda.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-376">For this example, the rules are in the order they should appear in the Main Grid of forwarding rules in the Barracuda Management Client.</span></span>
> 
> 

## <a name="rule-activation"></a><span data-ttu-id="ea2ea-377">Activation d’une règle</span><span class="sxs-lookup"><span data-stu-id="ea2ea-377">Rule Activation</span></span>
<span data-ttu-id="ea2ea-378">Une fois l’ensemble de règles modifié en fonction de la spécification du schéma logique, il doit être téléchargé sur le pare-feu et ensuite activé.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-378">With the ruleset modified to the specification of the logic diagram, the ruleset must be uploaded to the firewall and then activated.</span></span>

<span data-ttu-id="ea2ea-379">![Activation de règle de pare-feu][18]</span><span class="sxs-lookup"><span data-stu-id="ea2ea-379">![Firewall Rule Activation][18]</span></span>

<span data-ttu-id="ea2ea-380">Dans le coin supérieur droit du client de gestion se trouve un ensemble de boutons.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-380">In the upper right hand corner of the management client are a cluster of buttons.</span></span> <span data-ttu-id="ea2ea-381">Cliquez sur le bouton « Envoyer les modifications » pour envoyer les règles modifiées au pare-feu, puis cliquez sur le bouton « Activer ».</span><span class="sxs-lookup"><span data-stu-id="ea2ea-381">Click the “Send Changes” button to send the modified rules to the firewall, then click the “Activate” button.</span></span>

<span data-ttu-id="ea2ea-382">Avec l’activation de l’ensemble de règles de pare-feu, la création de l’environnement de cet exemple est terminée.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-382">With the activation of the firewall ruleset this example environment build is complete.</span></span>

## <a name="traffic-scenarios"></a><span data-ttu-id="ea2ea-383">Scénarios de trafic</span><span class="sxs-lookup"><span data-stu-id="ea2ea-383">Traffic Scenarios</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ea2ea-384">Il ne faut pas oublier que **tout** le trafic passe par le pare-feu.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-384">A key takeway is to remember that **all** traffic will come through the firewall.</span></span> <span data-ttu-id="ea2ea-385">Donc, depuis le bureau du serveur IIS01, même s’il se trouve dans le Service cloud du serveur frontal et sur le sous- réseau frontal, pour accéder à ce serveur, nous aurons besoin d’établir une connexion RDP vers le pare-feu sur le port 8014, puis nous devrons autoriser le pare-feu à acheminer la requête RDP en interne vers le port RDP IIS01.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-385">So to remote desktop to the IIS01 server, even though it's in the Front End Cloud Service and on the Front End subnet, to access this server we will need to RDP to the firewall on port 8014, and then allow the firewall to route the RDP request internally to the IIS01 RDP Port.</span></span> <span data-ttu-id="ea2ea-386">Le bouton « Se connecter » du portail Azure ne fonctionne pas car il n’existe pas d’itinéraire RDP vers IIS01 (du point de vue du portail).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-386">The Azure portal's "Connect" button won't work because there is no direct RDP path to IIS01 (as far as the portal can see).</span></span> <span data-ttu-id="ea2ea-387">Cela signifie que toutes les connexions à partir d’Internet seront orientées vers le Service Sécurité et un port, par exemple, secscv001.cloudapp.net:xxxx.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-387">This means all connections from the internet will be to the Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx.</span></span>
> 
> 

<span data-ttu-id="ea2ea-388">Pour ces scénarios, les règles de pare-feu suivantes doivent être en place :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-388">For these scenarios, the following firewall rules should be in place:</span></span>

1. <span data-ttu-id="ea2ea-389">Gestion de pare-feu</span><span class="sxs-lookup"><span data-stu-id="ea2ea-389">Firewall Management</span></span>
2. <span data-ttu-id="ea2ea-390">RDP vers IIS01</span><span class="sxs-lookup"><span data-stu-id="ea2ea-390">RDP to IIS01</span></span>
3. <span data-ttu-id="ea2ea-391">RDP vers DNS01</span><span class="sxs-lookup"><span data-stu-id="ea2ea-391">RDP to DNS01</span></span>
4. <span data-ttu-id="ea2ea-392">RDP vers AppVM01</span><span class="sxs-lookup"><span data-stu-id="ea2ea-392">RDP to AppVM01</span></span>
5. <span data-ttu-id="ea2ea-393">RDP vers AppVM02</span><span class="sxs-lookup"><span data-stu-id="ea2ea-393">RDP to AppVM02</span></span>
6. <span data-ttu-id="ea2ea-394">Trafic d’application vers le web</span><span class="sxs-lookup"><span data-stu-id="ea2ea-394">App Traffic to the Web</span></span>
7. <span data-ttu-id="ea2ea-395">Trafic d’application vers AppVM01</span><span class="sxs-lookup"><span data-stu-id="ea2ea-395">App Traffic to AppVM01</span></span>
8. <span data-ttu-id="ea2ea-396">Sortant vers Internet</span><span class="sxs-lookup"><span data-stu-id="ea2ea-396">Outbound to the Internet</span></span>
9. <span data-ttu-id="ea2ea-397">Serveur frontal vers DNS01</span><span class="sxs-lookup"><span data-stu-id="ea2ea-397">Frontend to DNS01</span></span>
10. <span data-ttu-id="ea2ea-398">Trafic intra-sous-réseau (principal vers frontal uniquement)</span><span class="sxs-lookup"><span data-stu-id="ea2ea-398">Intra-Subnet Traffic (back end to front end only)</span></span>
11. <span data-ttu-id="ea2ea-399">Refuser tout</span><span class="sxs-lookup"><span data-stu-id="ea2ea-399">Deny All</span></span>

<span data-ttu-id="ea2ea-400">L’ensemble de règles de pare-feu comporte probablement bien d’autres règles. Les règles de n’importe quel pare-feu donné peuvent comporter d’autres numéros de priorité que ceux qui apparaissent ici.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-400">The actual firewall ruleset will most likely have many other rules in addition to these, the rules on any given firewall will also have different priority numbers than the ones listed here.</span></span> <span data-ttu-id="ea2ea-401">Cette liste et les numéros associés représentent une pertinence entre les onze règles et la priorité à laquelle elles obéissent.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-401">This list and associated numbers are to provide relevance between just these eleven rules and the relative priority amongst them.</span></span> <span data-ttu-id="ea2ea-402">En d’autres termes, sur le pare-feu, la règle « RDP vers IIS01 » peut être le la règle numéro 5, mais aussi longtemps qu’elle se trouve en dessous de la règle « Gestion du pare-feu » au-dessus de la règle « RDP DNS01 » elle respecte l’esprit général de la liste.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-402">In other words; on the actual firewall, the “RDP to IIS01” may be rule number 5, but as long as it’s below the “Firewall Management” rule and above the “RDP to DNS01” rule it would align with the intention of this list.</span></span> <span data-ttu-id="ea2ea-403">Cette liste favorise également les scénarios ci-dessous et leur rapidité, par exemple, « Règle de pare-feu 9 (DNS) ».</span><span class="sxs-lookup"><span data-stu-id="ea2ea-403">The list will also aid in the below scenarios allowing brevity; e.g. “FW Rule 9 (DNS)”.</span></span> <span data-ttu-id="ea2ea-404">Par souci de concision, quatre règles de RDP sont collectivement appelées « règles RDP » lorsque le scénario de trafic n’a aucun rapport avec RDP.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-404">Also for brevity, the four RDP rules will be collectively called, “the RDP rules” when the traffic scenario is unrelated to RDP.</span></span>

<span data-ttu-id="ea2ea-405">Rappelez-vous également que les groupes de sécurité réseau sont en place pour le trafic Internet entrant sur les sous-réseaux serveurs frontal et principal.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-405">Also recall that Network Security Groups are in-place for inbound internet traffic on the Frontend and Backend subnets.</span></span>

#### <a name="allowed-internet-to-web-server"></a><span data-ttu-id="ea2ea-406">(Autorisé) Internet vers le serveur web</span><span class="sxs-lookup"><span data-stu-id="ea2ea-406">(Allowed) Internet to Web Server</span></span>
1. <span data-ttu-id="ea2ea-407">Un utilisateur Internet demande une page HTTP en provenance de SecSvc001.CloudApp.Net (Service cloud Internet)</span><span class="sxs-lookup"><span data-stu-id="ea2ea-407">Internet user requests HTTP page from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="ea2ea-408">Le service Cloud transfère le trafic via un point de terminaison ouvert sur le port 80 vers l’interface de pare-feu sur 10.0.0.4:80 (serveur web)</span><span class="sxs-lookup"><span data-stu-id="ea2ea-408">Cloud service passes traffic through open endpoint on port 80 to firewall interface on 10.0.0.4:80</span></span>
3. <span data-ttu-id="ea2ea-409">Aucun groupe de sécurité réseau n’est affecté au sous-réseau de sécurité, ce qui permet le trafic vers le pare-feu</span><span class="sxs-lookup"><span data-stu-id="ea2ea-409">No NSG assigned to Security subnet, so system NSG rules allow traffic to firewall</span></span>
4. <span data-ttu-id="ea2ea-410">Le trafic parvient à l’adresse IP du pare-feu (10.0.1.4).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-410">Traffic hits internal IP address of the firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="ea2ea-411">Le pare-feu commence le traitement de la règle :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-411">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="ea2ea-412">La règle de pare-feu 1 (Gestion de pare-feu) ne s’applique pas. Passer à la règle suivante.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-412">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="ea2ea-413">Les règles de pare-feu 2 à 5 (règles RDP) ne s’appliquent pas, passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="ea2ea-413">FW Rules 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
   3. <span data-ttu-id="ea2ea-414">La règle de pare-feu 6 (application: web) s’applique. Le trafic est autorisé, le pare-feu exécute la traduction NAT sur 10.0.1.4 (IIS01)</span><span class="sxs-lookup"><span data-stu-id="ea2ea-414">FW Rule 6 (App: Web) does apply, traffic is allowed, firewall NATs it to 10.0.1.4 (IIS01)</span></span>
6. <span data-ttu-id="ea2ea-415">Le sous-réseau du serveur frontal commence le traitement des règles du trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-415">The Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="ea2ea-416">La règle NSG 1 (blocage Internet) ne s’applique pas (le pare-feu a exécuté la traduction d’adresse NAT sur le pare-feu, donc l’adresse source se trouve désormais le pare-feu du sous-réseau de sécurité et est considérée par le sous-réseau du serveur frontal NSG comme « locale » et est donc autorisée). Passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="ea2ea-416">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by the firewall, thus the source address is now the firewall which is on the Security subnet and seen by the Frontend subnet NSG to be “local” traffic and is thus allowed), move to next rule</span></span>
   2. <span data-ttu-id="ea2ea-417">Les règles par défaut NSG autorisent le trafic de sous-réseau vers sous-réseau. Le trafic est autorisé, arrête le traitement des règles NSG</span><span class="sxs-lookup"><span data-stu-id="ea2ea-417">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="ea2ea-418">IIS01 écoute le trafic web, reçoit cette requête et commence à traiter la demande.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-418">IIS01 is listening for web traffic, receives this request and starts processing the request</span></span>
8. <span data-ttu-id="ea2ea-419">IIS01 tente de lancer une session FTP vers AppVM01 sur le sous-réseau du serveur principal</span><span class="sxs-lookup"><span data-stu-id="ea2ea-419">IIS01 attempts to initiates an FTP session to AppVM01 on Backend subnet</span></span>
9. <span data-ttu-id="ea2ea-420">L’itinéraire UDR sur le sous-réseau du serveur frontal définit le pare-feu comme le tronçon suivant</span><span class="sxs-lookup"><span data-stu-id="ea2ea-420">The UDR route on Frontend subnet makes the firewall the next hop</span></span>
10. <span data-ttu-id="ea2ea-421">Aucune règle sur le trafic sortant sur le sous-réseau du serveur frontal. Le trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-421">No outbound rules on Frontend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="ea2ea-422">Le pare-feu commence le traitement de la règle :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-422">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="ea2ea-423">La règle de pare-feu 1 (Gestion de pare-feu) ne s’applique pas. Passer à la règle suivante.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-423">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="ea2ea-424">Les règles de pare-feu 2 à 5 (règles RDP) ne s’appliquent pas. Passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="ea2ea-424">FW Rule 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
    3. <span data-ttu-id="ea2ea-425">La règle de pare-feu 6 (Aplication:Web) ne s’applique pas. Passer à la règle suivante.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-425">FW Rule 6 (App: Web) doesn’t apply, move to next rule</span></span>
    4. <span data-ttu-id="ea2ea-426">La règle de pare-feu 7 (application: principal) s’applique, le trafic est autorisé, le pare-feu transfère le trafic vers 10.0.2.5 (AppVM01)</span><span class="sxs-lookup"><span data-stu-id="ea2ea-426">FW Rule 7 (App: Backend) does apply, traffic is allowed, firewall forwards traffic to 10.0.2.5 (AppVM01)</span></span>
12. <span data-ttu-id="ea2ea-427">Le sous-réseau du serveur principal commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-427">The Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="ea2ea-428">La règle NSG 1 (Blocage Internet) ne s’applique pas. Passer à la règle suivante.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-428">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="ea2ea-429">Les règles par défaut NSG autorisent le trafic de sous-réseau vers sous-réseau. Le trafic est autorisé, arrête le traitement des règles NSG</span><span class="sxs-lookup"><span data-stu-id="ea2ea-429">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
13. <span data-ttu-id="ea2ea-430">AppVM01 reçoit la demande et lance la session et répond</span><span class="sxs-lookup"><span data-stu-id="ea2ea-430">AppVM01 receives the request and initiates the session and responds</span></span>
14. <span data-ttu-id="ea2ea-431">L’itinéraire défini par l’utilisateur (UDR) du sous-réseau du serveur principal fait du pare-feu le tronçon suivant</span><span class="sxs-lookup"><span data-stu-id="ea2ea-431">The UDR route on Backend subnet makes the firewall the next hop</span></span>
15. <span data-ttu-id="ea2ea-432">Comme il n’existe aucune règle NSG sortante sur le sous-réseau du serveur principal, la réponse est autorisée.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-432">Since there are no outbound NSG rules on the Backend subnet the response is allowed</span></span>
16. <span data-ttu-id="ea2ea-433">Comme il s’agit d’un trafic de retour sur une session établie, le pare-feu retransfère la réponse au serveur web (IIS01)</span><span class="sxs-lookup"><span data-stu-id="ea2ea-433">Because this is returning traffic on an established session the firewall passes the response back to the web server (IIS01)</span></span>
17. <span data-ttu-id="ea2ea-434">Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-434">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="ea2ea-435">La règle NSG 1 (Blocage Internet) ne s’applique pas. Passer à la règle suivante.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-435">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="ea2ea-436">Les règles par défaut NSG autorisent le trafic de sous-réseau vers sous-réseau. Le trafic est autorisé, arrête le traitement des règles NSG</span><span class="sxs-lookup"><span data-stu-id="ea2ea-436">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
18. <span data-ttu-id="ea2ea-437">Le serveur IIS reçoit la réponse, effectue la transaction avec AppVM01, puis termine la réalisation de la réponse HTT. Cette réponse HTTP est envoyée au demandeur</span><span class="sxs-lookup"><span data-stu-id="ea2ea-437">The IIS server receives the response, completes the transaction with AppVM01, and then completes building the HTTP response, this HTTP response is sent to the requestor</span></span>
19. <span data-ttu-id="ea2ea-438">Comme il n’existe pas de règle NSG pour le trafic sortant sur le sous-réseau du serveur frontal, la réponse est autorisée</span><span class="sxs-lookup"><span data-stu-id="ea2ea-438">Since there are no outbound NSG rules on the Frontend subnet the response is allowed</span></span>
20. <span data-ttu-id="ea2ea-439">La réponse HTTP atteint le pare-feu et, comme il s’agit de la réponse à une session NAT établie, elle est acceptée par le pare-feu</span><span class="sxs-lookup"><span data-stu-id="ea2ea-439">The HTTP response hits the firewall, and because this is the response to an established NAT session is accepted by the firewall</span></span>
21. <span data-ttu-id="ea2ea-440">Le pare-feu redirige ensuite la réponse vers l’utilisateur Internet</span><span class="sxs-lookup"><span data-stu-id="ea2ea-440">The firewall then redirects the response back to the Internet User</span></span>
22. <span data-ttu-id="ea2ea-441">Comme il n’existe aucune règle NSR sortante ou tronçon UDR sur le sous-réseau frontal, la réponse est autorisée, et l’utilisateur Internet reçoit la page web demandée.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-441">Since there are no outbound NSG rules or UDR hops on the Frontend subnet the response is allowed, and the Internet User receives the web page requested.</span></span>

#### <a name="allowed-internet-rdp-to-backend"></a><span data-ttu-id="ea2ea-442">(Autorisé) Internet RDP vers le serveur principal</span><span class="sxs-lookup"><span data-stu-id="ea2ea-442">(Allowed) Internet RDP to Backend</span></span>
1. <span data-ttu-id="ea2ea-443">Un Administrateur serveur sur Internet demande une session RDP AppVM01 via SecSvc001.CloudApp.Net:8025, 8025 étant le numéro de port utilisateur affecté à la règle de pare-feu « RDP vers AppVM01 »</span><span class="sxs-lookup"><span data-stu-id="ea2ea-443">Server Admin on internet requests RDP session to AppVM01 via SecSvc001.CloudApp.Net:8025, where 8025 is the user assigned port number for the “RDP to AppVM01” firewall rule</span></span>
2. <span data-ttu-id="ea2ea-444">Le service de cloud transmet le trafic via le point de terminaison ouvert sur le port 8025 vers l’interface de pare-feu sur 10.0.0.4:8025</span><span class="sxs-lookup"><span data-stu-id="ea2ea-444">The cloud service passes traffic through the open endpoint on port 8025 to firewall interface on 10.0.0.4:8025</span></span>
3. <span data-ttu-id="ea2ea-445">Aucun groupe de sécurité réseau n’est affecté au sous-réseau de sécurité, ce qui permet le trafic vers le pare-feu</span><span class="sxs-lookup"><span data-stu-id="ea2ea-445">No NSG assigned to Security subnet, so system NSG rules allow traffic to firewall</span></span>
4. <span data-ttu-id="ea2ea-446">Le pare-feu commence le traitement de la règle :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-446">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="ea2ea-447">La règle de pare-feu 1 (Gestion de pare-feu) ne s’applique pas. Passer à la règle suivante.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-447">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="ea2ea-448">La règle de pare-feu NSG 2 (RDP IIS) ne s’applique pas. Passer à la règle suivante.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-448">FW Rule 2 (RDP IIS) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="ea2ea-449">La règle de pare-feu NSG 3 (RDP DNS01) ne s’applique pas. Passer à la règle suivante.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-449">FW Rule 3 (RDP DNS01) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="ea2ea-450">La règle de pare-feu 4 (AppVM01 RDP) s’applique, le trafic est autorisé, le pare-feu exécute une traduction d’adresse NAT vers 10.0.2.5:3386 (port RDP sur AppVM01)</span><span class="sxs-lookup"><span data-stu-id="ea2ea-450">FW Rule 4 (RDP AppVM01) does apply, traffic is allowed, firewall NATs it to 10.0.2.5:3386 (RDP port on AppVM01)</span></span>
5. <span data-ttu-id="ea2ea-451">Le sous-réseau du serveur principal commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-451">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="ea2ea-452">La règle NSG 1 (blocage Internet) ne s’applique pas (le pare-feu a exécuté la traduction d’adresse NAT sur le pare-feu, donc l’adresse source se trouve désormais le pare-feu du sous-réseau de sécurité et est considéré par le sous-réseau NSG principal comme « locale » et est donc autorisée). Passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="ea2ea-452">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by the firewall, thus the source address is now the firewall which is on the Security subnet and seen by the Backend subnet NSG to be “local” traffic and is thus allowed), move to next rule</span></span>
   2. <span data-ttu-id="ea2ea-453">Les règles par défaut NSG autorisent le trafic de sous-réseau vers sous-réseau. Le trafic est autorisé, arrête le traitement des règles NSG</span><span class="sxs-lookup"><span data-stu-id="ea2ea-453">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="ea2ea-454">AppVM01 est à l’écoute du trafic RDP et répond</span><span class="sxs-lookup"><span data-stu-id="ea2ea-454">AppVM01 is listening for RDP traffic and responds</span></span>
7. <span data-ttu-id="ea2ea-455">En l’absence de règle NSG sur le trafic sortant, les règles par défaut s’appliquent et le retour de trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-455">With no outbound NSG rules, default rules apply and return traffic is allowed</span></span>
8. <span data-ttu-id="ea2ea-456">UDR achemine le trafic sortant vers le pare-feu qui représente le tronçon suivant</span><span class="sxs-lookup"><span data-stu-id="ea2ea-456">UDR routes outbound traffic to the firewall as the next hop</span></span>
9. <span data-ttu-id="ea2ea-457">Comme il s’agit d’un trafic de retour sur une session établie, le pare-feu retransfère la réponse au serveur Internet</span><span class="sxs-lookup"><span data-stu-id="ea2ea-457">Because this is returning traffic on an established session the firewall passes the response back to the internet user</span></span>
10. <span data-ttu-id="ea2ea-458">La Session RDP est activée.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-458">RDP session is enabled</span></span>
11. <span data-ttu-id="ea2ea-459">AppVM01 demande le mot de passe utilisateur</span><span class="sxs-lookup"><span data-stu-id="ea2ea-459">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="ea2ea-460">(Autorisé) recherche DNS du serveur web sur le serveur DNS</span><span class="sxs-lookup"><span data-stu-id="ea2ea-460">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="ea2ea-461">Le serveur Web Server IIS01 a besoin d’un flux de données sur www.data.gov, mais doit résoudre l’adresse.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-461">Web Server, IIS01, needs a data feed at www.data.gov, but needs to resolve the address.</span></span>
2. <span data-ttu-id="ea2ea-462">La configuration réseau du réseau virtuel DNS01 définit (10.0.2.4 sur le sous-réseau du serveur principal) comme serveur DNS principal, IIS01 envoie la requête DNS pour DNS01.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-462">The network configuration for the VNet lists DNS01 (10.0.2.4 on the Backend subnet) as the primary DNS server, IIS01 sends the DNS request to DNS01</span></span>
3. <span data-ttu-id="ea2ea-463">UDR achemine le trafic sortant vers le pare-feu qui représente le tronçon suivant</span><span class="sxs-lookup"><span data-stu-id="ea2ea-463">UDR routes outbound traffic to the firewall as the next hop</span></span>
4. <span data-ttu-id="ea2ea-464">Aucune règle NSG sortante n’est signalée sur le sous-réseau du serveur principal. Le trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-464">No outbound NSG rules are bound to the Frontend subnet, traffic is allowed</span></span>
5. <span data-ttu-id="ea2ea-465">Le pare-feu commence le traitement de la règle :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-465">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="ea2ea-466">La règle de pare-feu 1 (Gestion de pare-feu) ne s’applique pas. Passer à la règle suivante.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-466">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="ea2ea-467">Les règles de pare-feu 2 à 5 (règles RDP) ne s’appliquent pas. Passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="ea2ea-467">FW Rule 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
   3. <span data-ttu-id="ea2ea-468">Les règles de pare-feu 6 à 7 (règles Application) ne s’appliquent pas. Passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="ea2ea-468">FW Rules 6 & 7 (App Rules) don’t apply, move to next rule</span></span>
   4. <span data-ttu-id="ea2ea-469">La règle de pare-feu 8 (vers Internet) ne s’applique pas. Passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="ea2ea-469">FW Rule 8 (To Internet) doesn’t apply, move to next rule</span></span>
   5. <span data-ttu-id="ea2ea-470">La règle de pare-feu 9 (DNS) s’applique, le trafic est autorisé, le pare-feu transfère le trafic vers 10.0.2.4 (DNS01)</span><span class="sxs-lookup"><span data-stu-id="ea2ea-470">FW Rule 9 (DNS) does apply, traffic is allowed, firewall forwards traffic to 10.0.2.4 (DNS01)</span></span>
6. <span data-ttu-id="ea2ea-471">Le sous-réseau du serveur principal commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-471">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="ea2ea-472">La règle NSG 1 (Blocage Internet) ne s’applique pas. Passer à la règle suivante.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-472">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="ea2ea-473">Les règles par défaut NSG autorisent le trafic de sous-réseau vers sous-réseau. Le trafic est autorisé, arrête le traitement des règles NSG</span><span class="sxs-lookup"><span data-stu-id="ea2ea-473">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="ea2ea-474">Le serveur DNS reçoit la demande.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-474">DNS server receives the request</span></span>
8. <span data-ttu-id="ea2ea-475">Le serveur DNS n’a pas d’adresse en cache et demande à un serveur DNS racine sur Internet.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-475">DNS server doesn’t have the address cached and asks a root DNS server on the internet</span></span>
9. <span data-ttu-id="ea2ea-476">UDR achemine le trafic sortant vers le pare-feu qui représente le tronçon suivant</span><span class="sxs-lookup"><span data-stu-id="ea2ea-476">UDR routes outbound traffic to the firewall as the next hop</span></span>
10. <span data-ttu-id="ea2ea-477">Aucune règle NSG sur le trafic sortant sur le sous-réseau du serveur principal. Le trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-477">No outbound NSG rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="ea2ea-478">Le pare-feu commence le traitement de la règle :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-478">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="ea2ea-479">La règle de pare-feu 1 (Gestion de pare-feu) ne s’applique pas. Passer à la règle suivante.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-479">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="ea2ea-480">Les règles de pare-feu 2 à 5 (règles RDP) ne s’appliquent pas. Passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="ea2ea-480">FW Rule 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
    3. <span data-ttu-id="ea2ea-481">Les règles de pare-feu 6 à 7 (règles Application) ne s’appliquent pas. Passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="ea2ea-481">FW Rules 6 & 7 (App Rules) don’t apply, move to next rule</span></span>
    4. <span data-ttu-id="ea2ea-482">La règle de pare-feu 8 (vers Internet) s’applique, le trafic est autorisé, une opération SNAT est exécutée sur la session vers le serveur DNS racine sur Internet</span><span class="sxs-lookup"><span data-stu-id="ea2ea-482">FW Rule 8 (To Internet) does apply, traffic is allowed, session is SNAT out to root DNS server on the Internet</span></span>
12. <span data-ttu-id="ea2ea-483">Le serveur Internet DNS répond, car cette session a été initialisée en interne, la réponse est acceptée par le pare-feu.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-483">Internet DNS server responds, since this session was initiated from the firewall, the response is accepted by the firewall</span></span>
13. <span data-ttu-id="ea2ea-484">Comme il s’agit d’une session établie, le pare-feu transmet la réponse au serveur initiateur, DNS01</span><span class="sxs-lookup"><span data-stu-id="ea2ea-484">As this is an established session, the firewall forwards the response to the initiating server, DNS01</span></span>
14. <span data-ttu-id="ea2ea-485">Le sous-réseau du serveur principal commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-485">The Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="ea2ea-486">La règle NSG 1 (Blocage Internet) ne s’applique pas. Passer à la règle suivante.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-486">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="ea2ea-487">Les règles par défaut NSG autorisent le trafic de sous-réseau vers sous-réseau. Le trafic est autorisé, arrête le traitement des règles NSG</span><span class="sxs-lookup"><span data-stu-id="ea2ea-487">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
15. <span data-ttu-id="ea2ea-488">Le serveur DNS reçoit la réponse et la met en mémoire cache, puis il répond à la demande initiale de IIS01</span><span class="sxs-lookup"><span data-stu-id="ea2ea-488">The DNS server receives and caches the response, and then responds to the initial request back to IIS01</span></span>
16. <span data-ttu-id="ea2ea-489">L’itinéraire défini par l’utilisateur (UDR) du sous-réseau du serveur principal fait du pare-feu le tronçon suivant </span><span class="sxs-lookup"><span data-stu-id="ea2ea-489">The UDR route on backend subnet makes the firewall the next hop</span></span>
17. <span data-ttu-id="ea2ea-490">Aucune règle NSG sortante sur le sous-réseau du serveur principal. Le trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-490">No outbound NSG rules exist on the Backend subnet, traffic is allowed</span></span>
18. <span data-ttu-id="ea2ea-491">Il s’agit d’une session établie sur le pare-feu. La réponse est transmise par le pare-feu sur le serveur IIS</span><span class="sxs-lookup"><span data-stu-id="ea2ea-491">This is an established session on the firewall, the response is forwarded by the firewall back to the IIS server</span></span>
19. <span data-ttu-id="ea2ea-492">Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-492">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="ea2ea-493">Aucune règle NSG ne s’applique au trafic entrant en provenance du sous-réseau du serveur principal vers le sous-réseau du serveur frontal, par conséquent aucune des règles NSG ne s’applique</span><span class="sxs-lookup"><span data-stu-id="ea2ea-493">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="ea2ea-494">La règle système par défaut autorisant le trafic entre sous-réseaux autorise le trafic, le trafic est donc autorisé</span><span class="sxs-lookup"><span data-stu-id="ea2ea-494">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed</span></span>
20. <span data-ttu-id="ea2ea-495">IIS01 reçoit la réponse de la part de DNS01</span><span class="sxs-lookup"><span data-stu-id="ea2ea-495">IIS01 receives the response from DNS01</span></span>

#### <a name="allowed-backend-server-to-frontend-server"></a><span data-ttu-id="ea2ea-496">(Autorisé) Serveur principal vers Serveur frontal</span><span class="sxs-lookup"><span data-stu-id="ea2ea-496">(Allowed) Backend server to Frontend server</span></span>
1. <span data-ttu-id="ea2ea-497">Un administrateur connecté à AppVM02 via RDP demande un fichier directement depuis le serveur IIS01 via l’explorateur Windows</span><span class="sxs-lookup"><span data-stu-id="ea2ea-497">An administrator logged on to AppVM02 via RDP requests a file directly from the IIS01 server via windows file explorer</span></span>
2. <span data-ttu-id="ea2ea-498">L’itinéraire défini par l’utilisateur (UDR) du sous-réseau du serveur principal fait du pare-feu le tronçon suivant</span><span class="sxs-lookup"><span data-stu-id="ea2ea-498">The UDR route on Backend subnet makes the firewall the next hop</span></span>
3. <span data-ttu-id="ea2ea-499">Comme il n’existe aucune règle NSG sortante sur le sous-réseau du serveur principal, la réponse est autorisée.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-499">Since there are no outbound NSG rules on the Backend subnet the response is allowed</span></span>
4. <span data-ttu-id="ea2ea-500">Le pare-feu commence le traitement de la règle :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-500">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="ea2ea-501">La règle de pare-feu 1 (Gestion de pare-feu) ne s’applique pas. Passer à la règle suivante.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-501">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="ea2ea-502">Les règles de pare-feu 2 à 5 (règles RDP) ne s’appliquent pas. Passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="ea2ea-502">FW Rule 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
   3. <span data-ttu-id="ea2ea-503">Les règles de pare-feu 6 à 7 (règles Application) ne s’appliquent pas. Passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="ea2ea-503">FW Rules 6 & 7 (App Rules) don’t apply, move to next rule</span></span>
   4. <span data-ttu-id="ea2ea-504">La règle de pare-feu 8 (vers Internet) ne s’applique pas. Passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="ea2ea-504">FW Rule 8 (To Internet) doesn’t apply, move to next rule</span></span>
   5. <span data-ttu-id="ea2ea-505">La règle de pare-feu 9 (DNS) ne s’applique pas. Passer à la règle suivante.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-505">FW Rule 9 (DNS) doesn’t apply, move to next rule</span></span>
   6. <span data-ttu-id="ea2ea-506">La règle de pare-feu 10 (Intra-sous-réseau) s’applique, le trafic est autorisé. Le pare-feu transmet le trafic à 10.0.1.4 (IIS01)</span><span class="sxs-lookup"><span data-stu-id="ea2ea-506">FW Rule 10 (Intra-Subnet) does apply, traffic is allowed, firewall passes traffic to 10.0.1.4 (IIS01)</span></span>
5. <span data-ttu-id="ea2ea-507">Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-507">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="ea2ea-508">La règle NSG 1 (Blocage Internet) ne s’applique pas. Passer à la règle suivante.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-508">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="ea2ea-509">Les règles par défaut NSG autorisent le trafic de sous-réseau vers sous-réseau. Le trafic est autorisé, arrête le traitement des règles NSG</span><span class="sxs-lookup"><span data-stu-id="ea2ea-509">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="ea2ea-510">En supposant que l’autorisation et l’authentification sont correctes, IIS01 accepte la demande et répond</span><span class="sxs-lookup"><span data-stu-id="ea2ea-510">Assuming proper authentication and authorization, IIS01 accepts the request and responds</span></span>
7. <span data-ttu-id="ea2ea-511">L’itinéraire UDR sur le sous-réseau du serveur frontal définit le pare-feu comme le tronçon suivant</span><span class="sxs-lookup"><span data-stu-id="ea2ea-511">The UDR route on Frontend subnet makes the firewall the next hop</span></span>
8. <span data-ttu-id="ea2ea-512">Comme il n’existe pas de règle NSG pour le trafic sortant sur le sous-réseau du serveur frontal, la réponse est autorisée</span><span class="sxs-lookup"><span data-stu-id="ea2ea-512">Since there are no outbound NSG rules on the Frontend subnet the response is allowed</span></span>
9. <span data-ttu-id="ea2ea-513">Comme il s’agit d’une session existante sur le pare-feu, cette réponse est autorisée et le pare-feu renvoie la réponse à AppVM02</span><span class="sxs-lookup"><span data-stu-id="ea2ea-513">As this is an existing session on the firewall this response is allowed and the firewall returns the response to AppVM02</span></span>
10. <span data-ttu-id="ea2ea-514">Le sous-réseau du serveur principal entame le traitement du réseau entrant :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-514">Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="ea2ea-515">La règle NSG 1 (Blocage Internet) ne s’applique pas. Passer à la règle suivante.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-515">NSG Rule 1 (Block Internet) doesn’t apply, move to next rule</span></span>
    2. <span data-ttu-id="ea2ea-516">Les règles par défaut NSG autorisent le trafic de sous-réseau vers sous-réseau. Le trafic est autorisé, arrête le traitement des règles NSG</span><span class="sxs-lookup"><span data-stu-id="ea2ea-516">Default NSG Rules allow subnet to subnet traffic, traffic is allowed, stop NSG rule processing</span></span>
11. <span data-ttu-id="ea2ea-517">AppVM02 reçoit la réponse</span><span class="sxs-lookup"><span data-stu-id="ea2ea-517">AppVM02 receives the response</span></span>

#### <a name="denied-internet-direct-to-web-server"></a><span data-ttu-id="ea2ea-518">(Refusé) Internet direct vers le serveur web</span><span class="sxs-lookup"><span data-stu-id="ea2ea-518">(Denied) Internet direct to Web Server</span></span>
1. <span data-ttu-id="ea2ea-519">L’utilisateur Internet tente d’accéder à un fichier sur IIS01 via le service FrontEnd001.CloudApp.Net.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-519">Internet user tries to access the web server, IIS01, through the FrontEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="ea2ea-520">Comme aucun point de terminaison n’est ouvert pour le trafic HTTP, il ne franchit pas le service Cloud et n’atteint pas le serveur.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-520">Since there are no endpoints open for HTTP traffic, this would not pass through the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="ea2ea-521">Si, pour une raison quelconque, les points de terminaison étaient ouverts, la règle NSG 5 (Bloquer Internet) bloquerait ce trafic.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-521">If the endpoints were open for some reason, the NSG (Block Internet) on the Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="ea2ea-522">Enfin, l’itinéraire UDR du réseau frontal envoie tout le trafic sortant à partir de IIS01 vers le pare-feu (le tronçon suivant) et le pare-feu est considéré comme un trafic asymétrique et supprime la réponse sortante. Par conséquent, il existe au moins trois couches indépendantes de défense entre Internet et IIS01 via son service de cloud empêchant l’accès non autorisé/inapproprié.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-522">Finally, the Frontend subnet UDR route would send any outbound traffic from IIS01 to the firewall as the next hop, and the firewall would see this as asymmetric traffic and drop the outbound response Thus there are at least three independent layers of defense between the internet and IIS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-to-backend-server"></a><span data-ttu-id="ea2ea-523">(Refusé) Internet vers le serveur principal</span><span class="sxs-lookup"><span data-stu-id="ea2ea-523">(Denied) Internet to Backend Server</span></span>
1. <span data-ttu-id="ea2ea-524">L’utilisateur Internet tente d’accéder à un fichier sur AppVM01 via le service BackEnd001.CloudApp.Net.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-524">Internet user tries to access a file on AppVM01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="ea2ea-525">Comme il n’y a aucun point de terminaison ouvert pour le partage de fichiers, il ne passe pas le Service Cloud et n’atteint pas le serveur.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-525">Since there are no endpoints open for file share, this would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="ea2ea-526">Si les points de terminaison ont été ouverts pour une raison quelconque, la règle NSG 5 (Bloquer Internet) bloquerait le trafic.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-526">If the endpoints were open for some reason, the NSG (Block Internet) would block this traffic</span></span>
4. <span data-ttu-id="ea2ea-527">Enfin, l’itinéraire UDR envoie tout le trafic sortant à partir de AppVM01 vers le pare-feu (le tronçon suivant), et le pare-feu est considéré comme un trafic asymétrique et supprime la réponse sortante. Par conséquent, il existe au moins trois couches indépendantes de défense entre Internet et AppVM01 via son service de cloud empêchant l’accès non autorisé/inapproprié.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-527">Finally, the UDR route would send any outbound traffic from AppVM01 to the firewall as the next hop, and the firewall would see this as asymmetric traffic and drop the outbound response Thus there are at least three independent layers of defense between the internet and AppVM01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-frontend-server-to-backend-server"></a><span data-ttu-id="ea2ea-528">(Autorisé) Serveur frontal vers Serveur principal</span><span class="sxs-lookup"><span data-stu-id="ea2ea-528">(Denied) Frontend server to Backend Server</span></span>
1. <span data-ttu-id="ea2ea-529">Supposons que IIS01 est compromis et qu’un code malveillant essaie d’analyser les serveurs du sous-réseau du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-529">Assume IIS01 was compromised and is running malicious code trying to scan the Backend subnet servers.</span></span>
2. <span data-ttu-id="ea2ea-530">L’itinéraire UDR de sous-réseau du serveur frontal envoie tout le trafic sortant à partir de IIS01 vers le pare-feu (le tronçon suivant).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-530">The Frontend subnet UDR route would send any outbound traffic from IIS01 to the firewall as the next hop.</span></span> <span data-ttu-id="ea2ea-531">Cette opération ne peut pas être affectée par la machine virtuelle compromise.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-531">This is not something that can be altered by the compromised VM.</span></span>
3. <span data-ttu-id="ea2ea-532">Le pare-feu traite le trafic si la demande est faite à AppVM01, ou au serveur DNS dans le cadre de recherches DNS. Le trafic peut potentiellement être autorisé par le pare-feu (en raison des règles de pare-feu 7 et 9).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-532">The firewall would process the traffic, if the request was to AppVM01, or to the DNS server for DNS lookups that traffic could potentially be allowed by the firewall (due to FW Rules 7 and 9).</span></span> <span data-ttu-id="ea2ea-533">Tout autre trafic est bloqué par la règle de pare-feu 11 (Refuser tout).</span><span class="sxs-lookup"><span data-stu-id="ea2ea-533">All other traffic would be blocked by FW Rule 11 (Deny All).</span></span>
4. <span data-ttu-id="ea2ea-534">Si une détection de menaces avancée a été activée sur le pare-feu (sujet qui n’est pas abordé dans ce document, consultez la documentation du fournisseur de fonctionnalités avancées de votre équipement réseau). Même le trafic autorisé par les règles de transfert de base abordées dans ce document pourrait être bloqué s’il contient des signatures ou des modèles connus signalant une règle de menace avancée.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-534">If advanced threat detection was enabled on the firewall (which is not covered in this document, see the vendor documentation for your specific network appliance advanced threat capabilities), even traffic that would be allowed by the basic forwarding rules discussed in this document could be prevented if the traffic contained known signatures or patterns that flag an advanced threat rule.</span></span>

#### <a name="denied-internet-dns-lookup-on-dns-server"></a><span data-ttu-id="ea2ea-535">(Refusé) Recherche Internet DNS sur le serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-535">(Denied) Internet DNS lookup on DNS server</span></span>
1. <span data-ttu-id="ea2ea-536">L’utilisateur Internet tente de rechercher un enregistrement DNS interne sur DNS01 via le service BackEnd001.CloudApp.Net</span><span class="sxs-lookup"><span data-stu-id="ea2ea-536">Internet user tries to lookup an internal DNS record on DNS01 through BackEnd001.CloudApp.Net service</span></span> 
2. <span data-ttu-id="ea2ea-537">Comme aucun point de terminaison n’est ouvert pour le trafic DNS, il ne franchit pas le service Cloud et n’atteint pas le serveur.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-537">Since there are no endpoints open for DNS traffic, this would not pass through the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="ea2ea-538">Si, pour une raison quelconque, les points de terminaison étaient ouverts, la règle NSG (Bloquer Internet) bloquerait ce trafic.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-538">If the endpoints were open for some reason, the NSG rule (Block Internet) on the Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="ea2ea-539">Enfin, l’itinéraire UDR du réseau principal envoie tout le trafic sortant à partir de DNS01 au pare-feu (le tronçon suivant), et le pare-feu le considère comme un trafic asymétrique et supprime la réponse sortante. Par conséquent, il existe au moins trois couches indépendantes de défense entre Internet et DNS01 via son service de cloud empêchant l’accès non autorisé/inapproprié.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-539">Finally, the Backend subnet UDR route would send any outbound traffic from DNS01 to the firewall as the next hop, and the firewall would see this as asymmetric traffic and drop the outbound response Thus there are at least three independent layers of defense between the internet and DNS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-to-sql-access-through-firewall"></a><span data-ttu-id="ea2ea-540">(Refusé) Accès Internet vers SQL via le pare-feu</span><span class="sxs-lookup"><span data-stu-id="ea2ea-540">(Denied) Internet to SQL access through Firewall</span></span>
1. <span data-ttu-id="ea2ea-541">Un utilisateur Internet demande des données SQL de SecSvc001.CloudApp.Net (Service cloud Internet)</span><span class="sxs-lookup"><span data-stu-id="ea2ea-541">Internet user requests SQL data from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="ea2ea-542">Comme aucun point de terminaison n’est ouvert pour SQL, la demande ne franchit pas le service cloud et n’atteint pas le pare-feu.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-542">Since there are no endpoints open for SQL, this would not pass the Cloud Service and wouldn’t reach the firewall</span></span>
3. <span data-ttu-id="ea2ea-543">Si , pour une raison quelconque, les points de terminaison SQL étaient ouverts, le pare-feu serait commencerait le traitement de la règle :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-543">If SQL endpoints were open for some reason, the firewall would begin rule processing:</span></span>
   1. <span data-ttu-id="ea2ea-544">La règle de pare-feu 1 (Gestion de pare-feu) ne s’applique pas. Passer à la règle suivante.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-544">FW Rule 1 (FW Mgmt) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="ea2ea-545">Les règles de pare-feu 2 à 5 (règles RDP) ne s’appliquent pas, passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="ea2ea-545">FW Rules 2 - 5 (RDP Rules) don’t apply, move to next rule</span></span>
   3. <span data-ttu-id="ea2ea-546">Les règles de pare-feu 6 à 7 (règles d’application) ne s’appliquent pas. Passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="ea2ea-546">FW Rule 6 & 7 (Application Rules) don’t apply, move to next rule</span></span>
   4. <span data-ttu-id="ea2ea-547">La règle de pare-feu 8 (vers Internet) ne s’applique pas. Passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="ea2ea-547">FW Rule 8 (To Internet) doesn’t apply, move to next rule</span></span>
   5. <span data-ttu-id="ea2ea-548">La règle de pare-feu 9 (DNS) ne s’applique pas. Passer à la règle suivante.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-548">FW Rule 9 (DNS) doesn’t apply, move to next rule</span></span>
   6. <span data-ttu-id="ea2ea-549">La règle de pare-feu 10 (vers Internet) ne s’applique pas. Passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="ea2ea-549">FW Rule 10 (Intra-Subnet) doesn’t apply, move to next rule</span></span>
   7. <span data-ttu-id="ea2ea-550">La règle de pare-feu 11 (Refuser tout) s’applique, le trafic est autorisé, arrêter le traitement des règles.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-550">FW Rule 11 (Deny All) does apply, traffic is blocked, stop rule processing</span></span>

## <a name="references"></a><span data-ttu-id="ea2ea-551">Références</span><span class="sxs-lookup"><span data-stu-id="ea2ea-551">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="ea2ea-552">Script principal et configuration réseau</span><span class="sxs-lookup"><span data-stu-id="ea2ea-552">Main Script and Network Config</span></span>
<span data-ttu-id="ea2ea-553">Enregistrez le script complet dans un fichier de script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-553">Save the Full Script in a PowerShell script file.</span></span> <span data-ttu-id="ea2ea-554">Enregistrez la configuration réseau dans un fichier nommé « NetworkConf2.xml ».</span><span class="sxs-lookup"><span data-stu-id="ea2ea-554">Save the Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="ea2ea-555">Modifiez les variables définies par l’utilisateur selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-555">Modify the user defined variables as needed.</span></span> <span data-ttu-id="ea2ea-556">Exécutez le script, puis suivez les instructions d’installation de règle de pare-feu ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-556">Run the script, then follow the Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="ea2ea-557">Script complet</span><span class="sxs-lookup"><span data-stu-id="ea2ea-557">Full Script</span></span>
<span data-ttu-id="ea2ea-558">Ce script exécutera les actions suivantes en fonction des variables définies par l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-558">This script will, based on the user defined variables:</span></span>

1. <span data-ttu-id="ea2ea-559">Connexion à un abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="ea2ea-559">Connect to an Azure subscription</span></span>
2. <span data-ttu-id="ea2ea-560">Création d’un nouveau compte de stockage</span><span class="sxs-lookup"><span data-stu-id="ea2ea-560">Create a new storage account</span></span>
3. <span data-ttu-id="ea2ea-561">Créer un nouveau réseau virtuel et trois sous-réseaux, comme indiqué dans le fichier de configuration du réseau</span><span class="sxs-lookup"><span data-stu-id="ea2ea-561">Create a new VNet and three subnets as defined in the Network Config file</span></span>
4. <span data-ttu-id="ea2ea-562">Créer cinq machines virtuelles, 1 pare-feu et 4 machines virtuelles Windows Server </span><span class="sxs-lookup"><span data-stu-id="ea2ea-562">Build five virtual machines; 1 firewall and 4 windows server VMs</span></span>
5. <span data-ttu-id="ea2ea-563">Configurer UDR, notamment :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-563">Configure UDR including:</span></span>
   1. <span data-ttu-id="ea2ea-564">Création de deux nouvelles tables d’itinéraire</span><span class="sxs-lookup"><span data-stu-id="ea2ea-564">Creating two new route tables</span></span>
   2. <span data-ttu-id="ea2ea-565">Ajouter des itinéraires aux tables</span><span class="sxs-lookup"><span data-stu-id="ea2ea-565">Add routes to the tables</span></span>
   3. <span data-ttu-id="ea2ea-566">Lier des tables aux sous-réseaux appropriés</span><span class="sxs-lookup"><span data-stu-id="ea2ea-566">Bind tables to appropriate subnets</span></span>
6. <span data-ttu-id="ea2ea-567">Activer le transfert IP sur le NVA</span><span class="sxs-lookup"><span data-stu-id="ea2ea-567">Enable IP Forwarding on the NVA</span></span>
7. <span data-ttu-id="ea2ea-568">Configurez un groupe de sécurité réseau, notamment :</span><span class="sxs-lookup"><span data-stu-id="ea2ea-568">Configure NSG including:</span></span>
   1. <span data-ttu-id="ea2ea-569">Création d’un groupe de protection réseau</span><span class="sxs-lookup"><span data-stu-id="ea2ea-569">Creating a NSG</span></span>
   2. <span data-ttu-id="ea2ea-570">Ajout d’une règle</span><span class="sxs-lookup"><span data-stu-id="ea2ea-570">Adding a rule</span></span>
   3. <span data-ttu-id="ea2ea-571">La liaison du groupe de sécurité réseaux au sous-réseaux appropriés</span><span class="sxs-lookup"><span data-stu-id="ea2ea-571">Binding the NSG to the appropriate subnets</span></span>

<span data-ttu-id="ea2ea-572">Ce script PowerShell doit être exécuté localement sur un PC ou un serveur connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-572">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ea2ea-573">Lorsque ce script est exécuté, des avertissements ou autres messages d’information peuvent s’afficher dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-573">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="ea2ea-574">Seuls les messages d’erreur affichés en rouge sont source de préoccupation.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-574">Only error messages in red are cause for concern.</span></span>
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
       - One server on the FrontEnd Subnet
       - Three Servers on the BackEnd Subnet
       - IP Forwading from the FireWall out to the internet
       - User Defined Routing FrontEnd and BackEnd Subnets to the NVA

      Before running script, ensure the network configuration file is created in
      the directory referenced by $NetworkConfigFile variable (or update the
      variable to reflect the path and file name of the config file being used).

     .Notes
      Everyone's security requirements are different and can be addressed in a myriad of ways.
      Please be sure that any sensitive data or applications are behind the appropriate
      layer(s) of protection. This script serves as an example of some of the techniques
      that can be used, but should not be used for all scenarios. You are responsible to
      assess your security needs and the appropriate protections needed, and then effectively
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
        $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password to be used for all VMs"
        $VMName = @()
        $ServiceName = @()
        $VMFamily = @()
        $img = @()
        $size = @()
        $SubnetName = @()
        $VMIP = @()

    # User Defined Global Variables
      # These should be changes to reflect your subscription and services
      # Invalid options will fail in the validation section

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
        # Note: To ensure UDR and IP forwarding is setup
        # properly this script requires VM 0 be the NVA.

        # VM 0 - The Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $SecureService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $SecNet
          $VMIP += "10.0.0.4"

        # VM 1 - The Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 2 - The First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - The Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - The DNS Server
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

      # Update Subscription Pointer to New Storage Account
        Write-Host "Updating Subscription Pointer to New Storage Account" -ForegroundColor Cyan 
        Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

    # Validation
    $FatalError = $false

    If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
         Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
         $FatalError = $true}

    If (Test-AzureName -Service -Name $SecureService) { 
        Write-Host "The SecureService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "The FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "The FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "The FrontEndService service name is valid for use" -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "The BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "The BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'The network config file was not found, please update the $NetworkConfigFile variable to point to the network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "The network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'The deployment location was not found in the network config file, please check the network config file to ensure the $DeploymentLocation varible is correct and the netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "The deployment location was found in the network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see the above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building the environment." -ForegroundColor Green}

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
                # Set up all the EndPoints we'll need once we're up and running
                # Note: All traffic goes through the firewall, so we'll need to set up all ports here.
                #       Also, the firewall will be redirecting traffic to a new IP and Port in a forwarding
                #       rule, so all of these endpoint have the same public and local port and the firewall
                #       will do the mapping, NATing, and/or redirection as declared in the firewall rules.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPWeb"    -Protocol tcp -PublicPort 8014 -LocalPort 8014 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp1"   -Protocol tcp -PublicPort 8025 -LocalPort 8025 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp2"   -Protocol tcp -PublicPort 8026 -LocalPort 8026 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPDNS01"  -Protocol tcp -PublicPort 8024 -LocalPort 8024 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when the appliance is created.
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

      # Create the Route Tables
        Write-Host "Creating the Route Tables" -ForegroundColor Cyan 
        New-AzureRouteTable -Name $BERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $BESubnet subnet"
        New-AzureRouteTable -Name $FERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $FESubnet subnet"

      # Add Routes to Route Tables
        Write-Host "Adding Routes to the Route Tables" -ForegroundColor Cyan 
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "All traffic to FW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic to FW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "All traffic to FW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic to FW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $FEPrefix `
            -NextHopType VNETLocal

      # Assoicate the Route Tables with the Subnets
        Write-Host "Binding Route Tables to the Subnets" -ForegroundColor Cyan 
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $BESubnet `
            -RouteTableName $BERouteTableName
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $FESubnet `
            -RouteTableName $FERouteTableName

     # Enable IP Forwarding on the Virtual Appliance
        Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] `
            |Set-AzureIPForwarding -Enable

    # Configure NSG
        Write-Host "Configuring the Network Security Group (NSG)" -ForegroundColor Cyan

      # Build the NSG
        Write-Host "Building the NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rule
        Write-Host "Writing rules into the NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate the $VNetName VNet from the Internet" -Type Inbound -Priority 100 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

      # Assign the NSG to two Subnets
        # The NSG is *not* bound to the Security Subnet. The result
        # is that internet traffic flows only to the Security subnet
        # since the NSG bound to the Frontend and Backback subnets
        # will Deny internet traffic to those subnets.
        Write-Host "Binding the NSG to two subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on the IIS Server)
      # Install Backend resource (Run Post-Build Script on the AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on the IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on the AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a><span data-ttu-id="ea2ea-575">Fichier de configuration réseau</span><span class="sxs-lookup"><span data-stu-id="ea2ea-575">Network Config File</span></span>
<span data-ttu-id="ea2ea-576">Enregistrer ce fichier XML avec l’emplacement mis à jour et ajouter le lien vers ce fichier à la variable $NetworkConfigFile dans le script ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="ea2ea-576">Save this xml file with updated location and add the link to this file to the $NetworkConfigFile variable in the script above.</span></span>

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

#### <a name="sample-application-scripts"></a><span data-ttu-id="ea2ea-577">Exemples de scripts d’application</span><span class="sxs-lookup"><span data-stu-id="ea2ea-577">Sample Application Scripts</span></span>
<span data-ttu-id="ea2ea-578">Si vous souhaitez installer un exemple d’application et d’autres exemples de zone DMZ, vous en trouverez à l’adresse suivante : [Exemple de script d’application][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="ea2ea-578">If you wish to install a sample application for this, and other DMZ Examples, one has been provided at the following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
<span data-ttu-id="ea2ea-579">[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "Zone DMZ bidirectionnelle avec NVA, NSG et UDR"</span><span class="sxs-lookup"><span data-stu-id="ea2ea-579">[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "Bi-directional DMZ with NVA, NSG, and UDR"</span></span>
<span data-ttu-id="ea2ea-580">[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Affichage logique des règles de pare-feu"</span><span class="sxs-lookup"><span data-stu-id="ea2ea-580">[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Logical View of the Firewall Rules"</span></span>
<span data-ttu-id="ea2ea-581">[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "Créer un objet réseau FrontEnd"</span><span class="sxs-lookup"><span data-stu-id="ea2ea-581">[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "Create a FrontEnd Network Object"</span></span>
<span data-ttu-id="ea2ea-582">[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "Créer un objet de serveur DNS"</span><span class="sxs-lookup"><span data-stu-id="ea2ea-582">[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "Create a DNS Server Object"</span></span>
<span data-ttu-id="ea2ea-583">[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "Copie de la règle RDP par défaut"</span><span class="sxs-lookup"><span data-stu-id="ea2ea-583">[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "Copy of Default RDP Rule"</span></span>
<span data-ttu-id="ea2ea-584">[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "Règle AppVM01"</span><span class="sxs-lookup"><span data-stu-id="ea2ea-584">[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "AppVM01 Rule"</span></span>
<span data-ttu-id="ea2ea-585">[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "Icône de redirection d’application"</span><span class="sxs-lookup"><span data-stu-id="ea2ea-585">[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "Application Redirect Icon"</span></span>
<span data-ttu-id="ea2ea-586">[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "Icône NAT de destination"</span><span class="sxs-lookup"><span data-stu-id="ea2ea-586">[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "Destination NAT Icon"</span></span>
<span data-ttu-id="ea2ea-587">[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "Icône de réussite"</span><span class="sxs-lookup"><span data-stu-id="ea2ea-587">[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "Pass Icon"</span></span>
<span data-ttu-id="ea2ea-588">[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "Règle de gestion de pare-feu"</span><span class="sxs-lookup"><span data-stu-id="ea2ea-588">[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "Firewall Management Rule"</span></span>
<span data-ttu-id="ea2ea-589">[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "Règle RDP de pare-feu"</span><span class="sxs-lookup"><span data-stu-id="ea2ea-589">[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "Firewall RDP Rule"</span></span>
<span data-ttu-id="ea2ea-590">[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "Règle web de pare-feu "</span><span class="sxs-lookup"><span data-stu-id="ea2ea-590">[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "Firewall Web Rule"</span></span>
<span data-ttu-id="ea2ea-591">[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "Règle AppVM01 de pare-feu "</span><span class="sxs-lookup"><span data-stu-id="ea2ea-591">[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "Firewall AppVM01 Rule"</span></span>
<span data-ttu-id="ea2ea-592">[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "Règle de trafic sortant de pare-feu"</span><span class="sxs-lookup"><span data-stu-id="ea2ea-592">[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "Firewall Outbound Rule"</span></span>
<span data-ttu-id="ea2ea-593">[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "Règle DNS de pare-feu"</span><span class="sxs-lookup"><span data-stu-id="ea2ea-593">[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "Firewall DNS Rule"</span></span>
<span data-ttu-id="ea2ea-594">[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "Règle Intra-réseau virtuel de pare-feu"</span><span class="sxs-lookup"><span data-stu-id="ea2ea-594">[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "Firewall Intra-VNet Rule"</span></span>
<span data-ttu-id="ea2ea-595">[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "Règle de refus de pare-feu"</span><span class="sxs-lookup"><span data-stu-id="ea2ea-595">[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "Firewall Deny Rule"</span></span>
<span data-ttu-id="ea2ea-596">[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "Activation de règle de pare-feu"</span><span class="sxs-lookup"><span data-stu-id="ea2ea-596">[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "Firewall Rule Activation"</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
