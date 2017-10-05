---
title: "Exemple de zone Azure DMZ – Créer une zone DMZ simple avec des groupes de sécurité réseau | Microsoft Docs"
description: "Générer une zone DMZ avec des groupes de sécurité réseau (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: f8622b1d-c07d-4ea6-b41c-4ae98d998fff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: ed172d552e1e4c9ee27c58abcd7ad2d98df21579
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a><span data-ttu-id="9d884-103">Exemple 1 : Générer une zone DMZ simple en utilisant des groupes de sécurité réseau (NSG) avec Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d884-103">Example 1 – Build a simple DMZ using NSGs with classic PowerShell</span></span>
<span data-ttu-id="9d884-104">[Revenir à la page Meilleures pratiques relatives aux frontières de sécurité][HOME]</span><span class="sxs-lookup"><span data-stu-id="9d884-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9d884-105">Modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9d884-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="9d884-106">Classic - PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d884-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="9d884-107">Cet exemple crée une zone DMZ primitive avec quatre serveurs Windows et des groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="9d884-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="9d884-108">Cet exemple décrit chacune des commandes PowerShell correspondantes pour vous aider à mieux comprendre chaque étape.</span><span class="sxs-lookup"><span data-stu-id="9d884-108">This example describes each of the relevant PowerShell commands to provide a deeper understanding of each step.</span></span> <span data-ttu-id="9d884-109">Il comporte également une section Scénario de trafic (Traffic Scenario) qui explique en détail et étape par étape l’évolution du trafic à travers les couches de défense dans la zone DMZ.</span><span class="sxs-lookup"><span data-stu-id="9d884-109">There is also a Traffic Scenario section to provide an in-depth step-by-step how traffic proceeds through the layers of defense in the DMZ.</span></span> <span data-ttu-id="9d884-110">Enfin, dans la section de référence se trouve l’intégralité du code et des instructions permettant d’élaborer l’environnement destiné à tester et à expérimenter différents scénarios.</span><span class="sxs-lookup"><span data-stu-id="9d884-110">Finally, in the references section is the complete code and instruction to build this environment to test and experiment with various scenarios.</span></span> 

<span data-ttu-id="9d884-111">![Réseau de périmètre entrant avec groupe de sécurité réseau][1]</span><span class="sxs-lookup"><span data-stu-id="9d884-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="9d884-112">Description de l’environnement</span><span class="sxs-lookup"><span data-stu-id="9d884-112">Environment description</span></span>
<span data-ttu-id="9d884-113">Dans cet exemple, un abonnement contient les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="9d884-113">In this example a subscription contains the following resources:</span></span>

* <span data-ttu-id="9d884-114">deux services cloud : « FrontEnd001 », « BackEnd001 »,</span><span class="sxs-lookup"><span data-stu-id="9d884-114">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="9d884-115">Un réseau virtuel « CorpNetwork » avec deux sous-réseaux « FrontEnd » et « BackEnd »</span><span class="sxs-lookup"><span data-stu-id="9d884-115">A Virtual Network, “CorpNetwork”, with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="9d884-116">un groupe de sécurité réseau est appliqué aux deux sous-réseaux,</span><span class="sxs-lookup"><span data-stu-id="9d884-116">A Network Security Group that is applied to both subnets</span></span>
* <span data-ttu-id="9d884-117">un serveur Windows Server représentant un serveur web d’application (« IIS01 »),</span><span class="sxs-lookup"><span data-stu-id="9d884-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="9d884-118">Deux serveurs Windows Server qui représentent les serveurs principaux d’applications (« AppVM01 », « AppVM02 »)</span><span class="sxs-lookup"><span data-stu-id="9d884-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="9d884-119">Un serveur Windows Server qui représente un serveur DNS (« DNS01 »)</span><span class="sxs-lookup"><span data-stu-id="9d884-119">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="9d884-120">Dans la section Références figure un script PowerShell qui génère une grande partie l’environnement décrit dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="9d884-120">In the references section, there is a PowerShell script that builds most of the environment described in this example.</span></span> <span data-ttu-id="9d884-121">La création de machines virtuelles et de réseaux virtuels, bien qu’effectuée par l’exemple de script, ne figure pas en détail dans ce document.</span><span class="sxs-lookup"><span data-stu-id="9d884-121">Building the VMs and Virtual Networks, although are done by the example script, are not described in detail in this document.</span></span> 

<span data-ttu-id="9d884-122">Pour créer l’environnement :</span><span class="sxs-lookup"><span data-stu-id="9d884-122">To build the environment;</span></span>

1. <span data-ttu-id="9d884-123">Enregistrer le fichier XML de configuration réseau contenu dans la section Références (mis à jour avec les noms, l’emplacement et les adresses IP correspondant à un scénario donné)</span><span class="sxs-lookup"><span data-stu-id="9d884-123">Save the network config xml file included in the references section (updated with names, location, and IP addresses to match the given scenario)</span></span>
2. <span data-ttu-id="9d884-124">Mettre à jour les variables de l’utilisateur dans le script pour qu’elles correspondent à l’environnement dans lequel le script est exécuté (abonnements, noms de service, etc.)</span><span class="sxs-lookup"><span data-stu-id="9d884-124">Update the user variables in the script to match the environment the script is to be run against (subscriptions, service names, etc.)</span></span>
3. <span data-ttu-id="9d884-125">Exécuter le script dans PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d884-125">Execute the script in PowerShell</span></span>

>[!Note]
><span data-ttu-id="9d884-126">La région indiquée dans le script PowerShell doit correspondre à la région indiquée dans le fichier xml de configuration réseau.</span><span class="sxs-lookup"><span data-stu-id="9d884-126">The region signified in the PowerShell script must match the region signified in the network configuration xml file.</span></span>
>
>

<span data-ttu-id="9d884-127">Une fois que le script s’exécute correctement, d’autres opérations peuvent être effectuées. Dans la section Références, il existe deux scripts servant à configurer le serveur web et le serveur d’application avec une application web simple permettant le test avec cette configuration réseau de périmètre DMZ.</span><span class="sxs-lookup"><span data-stu-id="9d884-127">Once the script runs successfully additional optional steps may be taken, in the references section are two scripts to set up the web server and app server with a simple web application to allow testing with this DMZ configuration.</span></span>

<span data-ttu-id="9d884-128">Les sections suivantes fournissent une description détaillée des groupes de sécurité réseau et de leur fonctionnement pour cet exemple, grâce à l’examen des lignes clés du script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9d884-128">The following sections provide a detailed description of Network Security Groups and how they function for this example by walking through key lines of the PowerShell script.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="9d884-129">Groupes de sécurité réseau (NSG)</span><span class="sxs-lookup"><span data-stu-id="9d884-129">Network Security Groups (NSG)</span></span>
<span data-ttu-id="9d884-130">Pour cet exemple, un groupe NSG est créé, puis chargé avec six règles.</span><span class="sxs-lookup"><span data-stu-id="9d884-130">For this example, an NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="9d884-131">En règle générale, vous devez d’abord créer les règles d’« autorisation » spécifiques, puis les règles de « refus » plus générales.</span><span class="sxs-lookup"><span data-stu-id="9d884-131">Generally speaking, you should create your specific “Allow” rules first and then the more generic “Deny” rules last.</span></span> <span data-ttu-id="9d884-132">La priorité établit les règles évaluées en premier.</span><span class="sxs-lookup"><span data-stu-id="9d884-132">The assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="9d884-133">Une fois qu’il a été déterminé que le trafic répond à une règle spécifique, aucune autre règle n’est évaluée.</span><span class="sxs-lookup"><span data-stu-id="9d884-133">Once traffic is found to apply to a specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="9d884-134">Les règles du groupe de sécurité réseau peuvent s’appliquer dans le sens entrant ou sortant (du point de vue du sous-réseau).</span><span class="sxs-lookup"><span data-stu-id="9d884-134">NSG rules can apply in either in the inbound or outbound direction (from the perspective of the subnet).</span></span>
> 
> 

<span data-ttu-id="9d884-135">Les règles qui suivent sont générées de façon déclarative pour le trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="9d884-135">Declaratively, the following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="9d884-136">Le trafic DNS interne (port 53) est autorisé</span><span class="sxs-lookup"><span data-stu-id="9d884-136">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="9d884-137">Le trafic RDP (port 3389) à partir d’Internet vers n’importe quelle machine virtuelle est autorisé.</span><span class="sxs-lookup"><span data-stu-id="9d884-137">RDP traffic (port 3389) from the Internet to any VM is allowed</span></span>
3. <span data-ttu-id="9d884-138">Le trafic HTTP (port 80) à partir d’Internet vers le serveur web (IIS01) est autorisé.</span><span class="sxs-lookup"><span data-stu-id="9d884-138">HTTP traffic (port 80) from the Internet to web server (IIS01) is allowed</span></span>
4. <span data-ttu-id="9d884-139">Tout trafic (tous les ports) en provenance d’IIS01 vers AppVM1 est autorisé.</span><span class="sxs-lookup"><span data-stu-id="9d884-139">Any traffic (all ports) from IIS01 to AppVM1 is allowed</span></span>
5. <span data-ttu-id="9d884-140">Tout trafic (tous les ports) en provenance d’Internet vers l’ensemble du réseau virtuel (les deux sous-réseaux) est refusé.</span><span class="sxs-lookup"><span data-stu-id="9d884-140">Any traffic (all ports) from the Internet to the entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="9d884-141">Tout trafic (tous les ports) en provenance du sous-réseau frontal vers le sous-réseau principal est refusé.</span><span class="sxs-lookup"><span data-stu-id="9d884-141">Any traffic (all ports) from the Frontend subnet to the Backend subnet is Denied</span></span>

<span data-ttu-id="9d884-142">Lorsque ces règles sont associées à chacun des sous-réseaux, si une requête HTTP entrante en provenance d’HTTP arrive d’Internet à destination du serveur web, les 3 règles (autorisation) et les 5 règles (refus) s’appliquent. Cependant, comme la règle 3 a une priorité plus élevée, elle seule s’applique, et la règle 5 n’entre pas en jeu.</span><span class="sxs-lookup"><span data-stu-id="9d884-142">With these rules bound to each subnet, if an HTTP request was inbound from the Internet to the web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="9d884-143">La requête HTTP est donc autorisée à accéder au serveur web.</span><span class="sxs-lookup"><span data-stu-id="9d884-143">Thus the HTTP request would be allowed to the web server.</span></span> <span data-ttu-id="9d884-144">Si le même trafic tentait d’atteindre le serveur DNS01, la règle 5 (Refus) serait la première à s’appliquer et le trafic ne serait pas autorisé à accéder au serveur.</span><span class="sxs-lookup"><span data-stu-id="9d884-144">If that same traffic was trying to reach the DNS01 server, rule 5 (Deny) would be the first to apply and the traffic would not be allowed to pass to the server.</span></span> <span data-ttu-id="9d884-145">La règle 6 (Refus) bloque la communication du sous-réseau frontal vers le sous-réseau principal (excepté le trafic autorisé dans les règles 1 et 4), ce qui protège le réseau principal en cas d’attaque d’une personne mal intentionnée sur l’application web sur le serveur frontal. Cette personne aurait alors un accès limité au réseau principal « protégé » (uniquement les ressources exposées sur le serveur AppVM01).</span><span class="sxs-lookup"><span data-stu-id="9d884-145">Rule 6 (Deny) blocks the Frontend subnet from talking to the Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects the Backend network in case an attacker compromises the web application on the Frontend, the attacker would have limited access to the Backend “protected” network (only to resources exposed on the AppVM01 server).</span></span>

<span data-ttu-id="9d884-146">Il existe une règle par défaut qui autorise le trafic sortant vers Internet.</span><span class="sxs-lookup"><span data-stu-id="9d884-146">There is a default outbound rule that allows traffic out to the internet.</span></span> <span data-ttu-id="9d884-147">Pour cet exemple, nous allons autoriser le trafic sortant sans modifier les règles de trafic sortant.</span><span class="sxs-lookup"><span data-stu-id="9d884-147">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="9d884-148">Pour verrouiller le trafic dans les deux sens, l’itinéraire défini par l’utilisateur est requis et cette opération est expliquée dans l’exemple 3 ci-dessous à la [page Meilleures pratiques relatives aux frontières de sécurité][HOME].</span><span class="sxs-lookup"><span data-stu-id="9d884-148">To lock down traffic in both directions, User Defined Routing is required and is explored in “Example 3” on the [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="9d884-149">Chaque règle est abordée plus en détail par la suite (**Remarque**: tous les éléments de la liste ci-dessous commençant par un signe dollar (par exemple : $NSGName) sont des variables définies par l’utilisateur à partir du script de la section Références de ce document) :</span><span class="sxs-lookup"><span data-stu-id="9d884-149">Each rule is discussed in more detail as follows (**Note**: any item in the following list beginning with a dollar sign (for example: $NSGName) is a user-defined variable from the script in the reference section of this document):</span></span>

1. <span data-ttu-id="9d884-150">Tout d’abord, un groupe de sécurité réseau doit être généré. Il contiendra les règles :</span><span class="sxs-lookup"><span data-stu-id="9d884-150">First a Network Security Group must be built to hold the rules:</span></span>

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. <span data-ttu-id="9d884-151">La première règle de cet exemple autorise le trafic DNS entre tous les réseaux internes au serveur DNS sur le sous-réseau du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="9d884-151">The first rule in this example allows DNS traffic between all internal networks to the DNS server on the backend subnet.</span></span> <span data-ttu-id="9d884-152">La règle comporte certains paramètres importants :</span><span class="sxs-lookup"><span data-stu-id="9d884-152">The rule has some important parameters:</span></span>
   
   * <span data-ttu-id="9d884-153">« Type » indique le sens du trafic qui sera appliqué à cette règle.</span><span class="sxs-lookup"><span data-stu-id="9d884-153">“Type” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="9d884-154">La direction est déterminée du point de vue du sous-réseau ou de la machine virtuelle (selon l'élément auquel ce groupe de sécurité réseau est lié).</span><span class="sxs-lookup"><span data-stu-id="9d884-154">The direction is from the perspective of the subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="9d884-155">Donc si le Type est « Entrant » et si le trafic entre dans le sous-réseau, la règle s’applique et le trafic quittant le sous-réseau n’est pas concerné.</span><span class="sxs-lookup"><span data-stu-id="9d884-155">Thus if Type is “Inbound” and traffic is entering the subnet, the rule would apply and traffic leaving the subnet would not be affected by this rule.</span></span>
   * <span data-ttu-id="9d884-156">« Priorité » définit l’ordre dans lequel le flux de trafic est évalué.</span><span class="sxs-lookup"><span data-stu-id="9d884-156">“Priority” sets the order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="9d884-157">Plus le numéro de priorité est faible, plus la priorité de la règle est élevée.</span><span class="sxs-lookup"><span data-stu-id="9d884-157">The lower the number the higher the priority.</span></span> <span data-ttu-id="9d884-158">Lorsqu’une règle s’applique à un flux de trafic spécifique, aucune autre règle n’est traitée.</span><span class="sxs-lookup"><span data-stu-id="9d884-158">When a rule applies to a specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="9d884-159">Donc si une règle de priorité 1 autorise le trafic et une règle de priorité 2 le refuse, si les deux règles s’appliquent, alors le trafic est autorisé à circuler (dans la mesure où la règle 1 a une priorité plus élevée et est appliquée, aucune autre règle n’est prise en compte).</span><span class="sxs-lookup"><span data-stu-id="9d884-159">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply to traffic then the traffic would be allowed to flow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
   * <span data-ttu-id="9d884-160">« Action » indique si le trafic concerné par cette règle est bloqué ou autorisé.</span><span class="sxs-lookup"><span data-stu-id="9d884-160">“Action” signifies if traffic affected by this rule is blocked or allowed.</span></span>

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. <span data-ttu-id="9d884-161">Cette règle autorise le trafic RDP à circuler depuis Internet vers le port RDP de n’importe quel serveur du sous-réseau lié.</span><span class="sxs-lookup"><span data-stu-id="9d884-161">This rule allows RDP traffic to flow from the internet to the RDP port on any server on the bound subnet.</span></span> <span data-ttu-id="9d884-162">Cette règle utilise deux types spéciaux de préfixes d’adresses ; « VIRTUAL_NETWORK » et « INTERNET ».</span><span class="sxs-lookup"><span data-stu-id="9d884-162">This rule uses two special types of address prefixes; “VIRTUAL_NETWORK” and “INTERNET.”</span></span> <span data-ttu-id="9d884-163">Ces balises constituent un moyen simple de traiter une catégorie plus importante de préfixes d’adresses.</span><span class="sxs-lookup"><span data-stu-id="9d884-163">These tags are an easy way to address a larger category of address prefixes.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP to $VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. <span data-ttu-id="9d884-164">Cette règle autorise le trafic Internet entrant à accéder au serveur web.</span><span class="sxs-lookup"><span data-stu-id="9d884-164">This rule allows inbound internet traffic to hit the web server.</span></span> <span data-ttu-id="9d884-165">Cette règle ne modifie pas le comportement du routage.</span><span class="sxs-lookup"><span data-stu-id="9d884-165">This rule does not change the routing behavior.</span></span> <span data-ttu-id="9d884-166">La règle n’autorise que le trafic destiné à IIS01.</span><span class="sxs-lookup"><span data-stu-id="9d884-166">The rule only allows traffic destined for IIS01 to pass.</span></span> <span data-ttu-id="9d884-167">Donc, si le trafic en provenance d’Internet a pour destination le serveur web, cette règle l’autorise et arrête le traitement des règles suivantes.</span><span class="sxs-lookup"><span data-stu-id="9d884-167">Thus if traffic from the Internet had the web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="9d884-168">(Dans la règle de priorité 140, tout autre trafic Internet entrant est bloqué).</span><span class="sxs-lookup"><span data-stu-id="9d884-168">(In the rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="9d884-169">Si vous traitez uniquement le trafic HTTP, cette règle peut encore être restreinte pour autoriser uniquement le trafic à destination du Port 80.</span><span class="sxs-lookup"><span data-stu-id="9d884-169">If you're only processing HTTP traffic, this rule could be further restricted to only allow Destination Port 80.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet to $VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. <span data-ttu-id="9d884-170">Cette règle autorise le trafic à passer du serveur IIS01 au serveur AppVM01. Une autre règle bloque tout autre trafic du serveur frontal vers le serveur principal.</span><span class="sxs-lookup"><span data-stu-id="9d884-170">This rule allows traffic to pass from the IIS01 server to the AppVM01 server, a later rule blocks all other Frontend to Backend traffic.</span></span> <span data-ttu-id="9d884-171">Pour améliorer cette règle, si le port est connu, il doit être ajouté.</span><span class="sxs-lookup"><span data-stu-id="9d884-171">To improve this rule, if the port is known that should be added.</span></span> <span data-ttu-id="9d884-172">Par exemple, si le serveur IIS accède uniquement au serveur SQL Server sur AppVM01, la plage de ports de destination doit passer de « * » (tout) à 1433 (le port SQL), ce qui réduit la surface vulnérable sur AppVM01 au cas où l’application web serait compromise.</span><span class="sxs-lookup"><span data-stu-id="9d884-172">For example, if the IIS server is hitting only SQL Server on AppVM01, the Destination Port Range should be changed from “*” (Any) to 1433 (the SQL port) thus allowing a smaller inbound attack surface on AppVM01 should the web application ever be compromised.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] to $VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. <span data-ttu-id="9d884-173">Cette règle refuse le trafic en provenance d’Internet vers des serveurs sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="9d884-173">This rule denies traffic from the internet to any servers on the network.</span></span> <span data-ttu-id="9d884-174">Avec les règles de priorité 110 et 120, elle permet uniquement au trafic Internet entrant d’accéder au pare-feu et aux ports RDP d’autres serveurs et bloque tout le reste.</span><span class="sxs-lookup"><span data-stu-id="9d884-174">With the rules at priority 110 and 120, the effect is to allow only inbound internet traffic to the firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="9d884-175">Cette règle est une règle de « prévention de défaillance » qui bloque tous les flux inattendus.</span><span class="sxs-lookup"><span data-stu-id="9d884-175">This rule is a "fail-safe" rule to block all unexpected flows.</span></span>
    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate the $VNetName VNet from the Internet" `
        -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *
    ```
7. <span data-ttu-id="9d884-176">La règle finale refuse le trafic du sous-réseau du serveur frontal vers le sous-réseau du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="9d884-176">The final rule denies traffic from the Frontend subnet to the Backend subnet.</span></span> <span data-ttu-id="9d884-177">Dans la mesure où il s’agit d’une règle entrante uniquement, le trafic en sens inverse est autorisé (du serveur principal vers le serveur frontal).</span><span class="sxs-lookup"><span data-stu-id="9d884-177">Since this rule is an Inbound only rule, reverse traffic is allowed (from the Backend to the Frontend).</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate the $FESubnet subnet from the $BESubnet subnet" `
        -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix `
        -DestinationPortRange '*' `
        -Protocol * 
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="9d884-178">Scénarios de trafic</span><span class="sxs-lookup"><span data-stu-id="9d884-178">Traffic scenarios</span></span>
#### <a name="allowed-internet-to-web-server"></a><span data-ttu-id="9d884-179">(*Autorisé*) Internet vers le serveur web</span><span class="sxs-lookup"><span data-stu-id="9d884-179">(*Allowed*) Internet to web server</span></span>
1. <span data-ttu-id="9d884-180">Un utilisateur Internet demande une page HTTP en provenance de FrontEnd001.CloudApp.Net (service cloud face à Internet)</span><span class="sxs-lookup"><span data-stu-id="9d884-180">An internet user requests an HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="9d884-181">Le service Cloud transfère le trafic via un point de terminaison ouvert sur le port 80 vers IIS01 (serveur web)</span><span class="sxs-lookup"><span data-stu-id="9d884-181">Cloud service passes traffic through open endpoint on port 80 towards IIS01 (the web server)</span></span>
3. <span data-ttu-id="9d884-182">Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="9d884-182">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="9d884-183">La règle NSG 1 (DNS) ne s’applique pas, passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="9d884-183">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="9d884-184">La règle NSG 2 (RDP) ne s’applique pas, passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="9d884-184">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="9d884-185">La règle NSG 3 (Internet pour IIS01) s’applique, le trafic est autorisé, arrêter le traitement.</span><span class="sxs-lookup"><span data-stu-id="9d884-185">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="9d884-186">Le trafic parvient à l’adresse IP interne du serveur web IIS01 (10.0.1.5).</span><span class="sxs-lookup"><span data-stu-id="9d884-186">Traffic hits internal IP address of the web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="9d884-187">IIS01 écoute le trafic web, reçoit cette requête et commence à traiter la demande.</span><span class="sxs-lookup"><span data-stu-id="9d884-187">IIS01 is listening for web traffic, receives this request and starts processing the request</span></span>
6. <span data-ttu-id="9d884-188">IIS01 demande des informations au serveur SQL Server sur AppVM01</span><span class="sxs-lookup"><span data-stu-id="9d884-188">IIS01 asks the SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="9d884-189">Comme il n'existe aucune règle sortante sur le sous-réseau du serveur frontal, le trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="9d884-189">Since there are no outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="9d884-190">Le sous-réseau du serveur principal commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="9d884-190">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="9d884-191">La règle NSG 1 (DNS) ne s’applique pas, passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="9d884-191">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="9d884-192">La règle NSG 2 (RDP) ne s’applique pas, passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="9d884-192">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="9d884-193">La règle NSG 3 (Internet vers le pare-feu) ne s’applique pas, passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="9d884-193">NSG Rule 3 (Internet to Firewall) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="9d884-194">La règle NSG 4 (IIS01 vers AppVM01) s’applique, le trafic est autorisé, arrêter le traitement des règles</span><span class="sxs-lookup"><span data-stu-id="9d884-194">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="9d884-195">AppVM01 reçoit la requête SQL et répond</span><span class="sxs-lookup"><span data-stu-id="9d884-195">AppVM01 receives the SQL Query and responds</span></span>
10. <span data-ttu-id="9d884-196">Comme il n’existe aucune règle sur le trafic sortant sur le sous-réseau du serveur principal, la réponse est autorisée</span><span class="sxs-lookup"><span data-stu-id="9d884-196">Since there are no outbound rules on the Backend subnet, the response is allowed</span></span>
11. <span data-ttu-id="9d884-197">Le sous-réseau du serveur frontal commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="9d884-197">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="9d884-198">Aucune règle NSG ne s’applique au trafic entrant en provenance du sous-réseau du serveur principal vers le sous-réseau du serveur frontal, par conséquent aucune des règles NSG ne s’applique</span><span class="sxs-lookup"><span data-stu-id="9d884-198">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="9d884-199">La règle du système par défaut autorisant le trafic entre sous-réseaux autorise le trafic, le trafic est donc autorisé.</span><span class="sxs-lookup"><span data-stu-id="9d884-199">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
12. <span data-ttu-id="9d884-200">Le serveur IIS reçoit la réponse SQL, complète la réponse HTTP et l’envoie au demandeur</span><span class="sxs-lookup"><span data-stu-id="9d884-200">The IIS server receives the SQL response and completes the HTTP response and sends to the requestor</span></span>
13. <span data-ttu-id="9d884-201">Comme il n’existe aucune règle sortante sur le sous-réseau du serveur frontal, la réponse est autorisée, et l’utilisateur Internet reçoit la page web demandée.</span><span class="sxs-lookup"><span data-stu-id="9d884-201">Since there are no outbound rules on the Frontend subnet the response is allowed, and the internet User receives the web page requested.</span></span>

#### <a name="allowed-rdp-to-backend"></a><span data-ttu-id="9d884-202">(*Autorisé*) RDP vers le serveur principal</span><span class="sxs-lookup"><span data-stu-id="9d884-202">(*Allowed*) RDP to backend</span></span>
1. <span data-ttu-id="9d884-203">L’administrateur du serveur sur Internet demande une session RDP AppVM01 sur BackEnd001.CloudApp.Net:xxxxx, où xxxxx est le numéro de port attribué de façon aléatoire au trafic RDP vers AppVM01 (le port attribué se trouve sur le portail Azure ou via PowerShell)</span><span class="sxs-lookup"><span data-stu-id="9d884-203">Server Admin on internet requests RDP session to AppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is the randomly assigned port number for RDP to AppVM01 (the assigned port can be found on the Azure portal or via PowerShell)</span></span>
2. <span data-ttu-id="9d884-204">Le sous-réseau du serveur principal entame le traitement du réseau entrant :</span><span class="sxs-lookup"><span data-stu-id="9d884-204">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="9d884-205">La règle NSG 1 (DNS) ne s’applique pas, passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="9d884-205">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="9d884-206">La règle NSG 2 (RDP) s’applique, le trafic est autorisé, arrêter le traitement des règles</span><span class="sxs-lookup"><span data-stu-id="9d884-206">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
3. <span data-ttu-id="9d884-207">En l’absence de réseau sortant, les règles par défaut s’appliquent et le retour de trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="9d884-207">With no outbound rules, default rules apply and return traffic is allowed</span></span>
4. <span data-ttu-id="9d884-208">La session RDP est activée</span><span class="sxs-lookup"><span data-stu-id="9d884-208">RDP session is enabled</span></span>
5. <span data-ttu-id="9d884-209">AppVM01 demande le nom et le mot de passe de l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="9d884-209">AppVM01 prompts for the user name and password</span></span>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="9d884-210">(*Autorisé*) recherche DNS du serveur web sur le serveur DNS</span><span class="sxs-lookup"><span data-stu-id="9d884-210">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="9d884-211">Le serveur Web Server IIS01 a besoin d’un flux de données sur www.data.gov, mais doit résoudre l’adresse.</span><span class="sxs-lookup"><span data-stu-id="9d884-211">Web Server, IIS01, needs a data feed at www.data.gov, but needs to resolve the address.</span></span>
2. <span data-ttu-id="9d884-212">La configuration réseau du réseau virtuel définit DNS01 (10.0.2.4 sur le sous-réseau du serveur principal) comme serveur DNS principal, IIS01 envoie la requête DNS à DNS01</span><span class="sxs-lookup"><span data-stu-id="9d884-212">The network configuration for the VNet lists DNS01 (10.0.2.4 on the Backend subnet) as the primary DNS server, IIS01 sends the DNS request to DNS01</span></span>
3. <span data-ttu-id="9d884-213">Aucune règle sortante sur le sous-réseau du serveur frontal, le trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="9d884-213">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="9d884-214">Le sous-réseau du serveur principal entame le traitement du réseau entrant :</span><span class="sxs-lookup"><span data-stu-id="9d884-214">Backend subnet begins inbound rule processing:</span></span>
   * <span data-ttu-id="9d884-215">La règle NSG 1 (DNS) s’applique, le trafic est autorisé, arrêter le traitement des règles</span><span class="sxs-lookup"><span data-stu-id="9d884-215">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="9d884-216">Le serveur DNS reçoit la demande</span><span class="sxs-lookup"><span data-stu-id="9d884-216">DNS server receives the request</span></span>
6. <span data-ttu-id="9d884-217">Le serveur DNS n’a pas d’adresse en cache et demande à un serveur DNS racine sur Internet.</span><span class="sxs-lookup"><span data-stu-id="9d884-217">DNS server doesn’t have the address cached and asks a root DNS server on the internet</span></span>
7. <span data-ttu-id="9d884-218">Aucune règle sortante sur le sous-réseau du serveur principal, le trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="9d884-218">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="9d884-219">Un serveur Internet DNS répond, car cette session a été initialisée en interne, la réponse est autorisée</span><span class="sxs-lookup"><span data-stu-id="9d884-219">Internet DNS server responds, since this session was initiated internally, the response is allowed</span></span>
9. <span data-ttu-id="9d884-220">Le serveur DNS met en cache la réponse et répond à la demande initiale à IIS01</span><span class="sxs-lookup"><span data-stu-id="9d884-220">DNS server caches the response, and responds to the initial request back to IIS01</span></span>
10. <span data-ttu-id="9d884-221">Aucune règle sortante sur le sous-réseau du serveur principal, le trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="9d884-221">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="9d884-222">Le sous-réseau du serveur frontal commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="9d884-222">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="9d884-223">Aucune règle NSG ne s’applique au trafic entrant en provenance du sous-réseau du serveur principal vers le sous-réseau du serveur frontal, par conséquent aucune des règles NSG ne s’applique</span><span class="sxs-lookup"><span data-stu-id="9d884-223">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="9d884-224">La règle système par défaut autorisant le trafic entre sous-réseaux autorise le trafic, le trafic est donc autorisé</span><span class="sxs-lookup"><span data-stu-id="9d884-224">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed</span></span>
12. <span data-ttu-id="9d884-225">IIS01 reçoit la réponse de la part de DNS01</span><span class="sxs-lookup"><span data-stu-id="9d884-225">IIS01 receives the response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="9d884-226">(*Autorisé*) fichier d’accès de serveur Web sur AppVM01</span><span class="sxs-lookup"><span data-stu-id="9d884-226">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="9d884-227">IIS01 demande un fichier sur AppVM01</span><span class="sxs-lookup"><span data-stu-id="9d884-227">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="9d884-228">Aucune règle sortante sur le sous-réseau du serveur frontal, le trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="9d884-228">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="9d884-229">Le sous-réseau du serveur principal commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="9d884-229">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="9d884-230">La règle NSG 1 (DNS) ne s’applique pas, passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="9d884-230">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="9d884-231">La règle NSG 2 (RDP) ne s’applique pas. Passer à la règle suivante.</span><span class="sxs-lookup"><span data-stu-id="9d884-231">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="9d884-232">La règle NSG 3 (Internet vers le IIS01) ne s’applique pas. Passer à la règle suivante.</span><span class="sxs-lookup"><span data-stu-id="9d884-232">NSG Rule 3 (Internet to IIS01) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="9d884-233">La règle NSG 4 (IIS01 vers AppVM01) s’applique, le trafic est autorisé, arrêter le traitement des règles.</span><span class="sxs-lookup"><span data-stu-id="9d884-233">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="9d884-234">AppVM01 reçoit la demande et répond avec un fichier (en supposant que l’accès est autorisé)</span><span class="sxs-lookup"><span data-stu-id="9d884-234">AppVM01 receives the request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="9d884-235">Comme il n’existe aucune règle sur le trafic sortant sur le sous-réseau du serveur principal, la réponse est autorisée</span><span class="sxs-lookup"><span data-stu-id="9d884-235">Since there are no outbound rules on the Backend subnet, the response is allowed</span></span>
6. <span data-ttu-id="9d884-236">Le sous-réseau du serveur frontal commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="9d884-236">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="9d884-237">Aucune règle NSG ne s’applique au trafic entrant en provenance du sous-réseau du serveur principal vers le sous-réseau du serveur frontal, par conséquent aucune des règles NSG ne s’applique</span><span class="sxs-lookup"><span data-stu-id="9d884-237">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
   2. <span data-ttu-id="9d884-238">La règle du système par défaut autorisant le trafic entre sous-réseaux autorise le trafic, le trafic est donc autorisé.</span><span class="sxs-lookup"><span data-stu-id="9d884-238">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
7. <span data-ttu-id="9d884-239">Le serveur IIS reçoit le fichier</span><span class="sxs-lookup"><span data-stu-id="9d884-239">The IIS server receives the file</span></span>

#### <a name="denied-web-to-backend-server"></a><span data-ttu-id="9d884-240">(*Refusé*) Web vers le serveur principal</span><span class="sxs-lookup"><span data-stu-id="9d884-240">(*Denied*) Web to backend server</span></span>
1. <span data-ttu-id="9d884-241">Un utilisateur Internet tente d’accéder à un fichier sur AppVM01 via le service BackEnd001.CloudApp.Net</span><span class="sxs-lookup"><span data-stu-id="9d884-241">An internet user tries to access a file on AppVM01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="9d884-242">Comme il n’y a aucun point de terminaison ouvert pour le partage de fichiers, ce trafic ne passe pas le service cloud et n’atteint pas le serveur</span><span class="sxs-lookup"><span data-stu-id="9d884-242">Since there are no endpoints open for file share, this traffic would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="9d884-243">Si les points de terminaison ont été ouverts pour une raison quelconque, la règle NSG 5 (Internet vers le réseau virtuel) bloque ce trafic</span><span class="sxs-lookup"><span data-stu-id="9d884-243">If the endpoints were open for some reason, NSG rule 5 (Internet to VNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="9d884-244">(*Refusé*) recherche DNS web sur le serveur DNS</span><span class="sxs-lookup"><span data-stu-id="9d884-244">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="9d884-245">Un utilisateur Internet tente de rechercher un enregistrement DNS interne sur DNS01 par le biais du service BackEnd001.CloudApp.Net</span><span class="sxs-lookup"><span data-stu-id="9d884-245">An internet user tries to look up an internal DNS record on DNS01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="9d884-246">Comme aucun point de terminaison n’est ouvert pour DNS, ce trafic ne passe pas le service Cloud et n’atteint pas le serveur</span><span class="sxs-lookup"><span data-stu-id="9d884-246">Since there are no endpoints open for DNS, this traffic would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="9d884-247">Si les points de terminaison ont été ouverts pour une raison quelconque, la règle NSG 5 (Internet vers réseau virtuel) bloque ce trafic (Remarque : cette règle 1 (DNS) ne s’applique pas pour deux raisons : tout d’abord l’adresse source est sur Internet, et cette règle s’applique uniquement lorsque la source locale est le réseau virtuel local ; de plus, s’il s’agit d’une règle d’autorisation, le trafic n’est jamais refusé)</span><span class="sxs-lookup"><span data-stu-id="9d884-247">If the endpoints were open for some reason, NSG rule 5 (Internet to VNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first the source address is the internet, this rule only applies to the local VNet as the source, also this rule is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-to-sql-access-through-firewall"></a><span data-ttu-id="9d884-248">(*Refusé*) Accès web vers SQL via le pare-feu</span><span class="sxs-lookup"><span data-stu-id="9d884-248">(*Denied*) Web to SQL access through firewall</span></span>
1. <span data-ttu-id="9d884-249">Un utilisateur Internet demande des données SQL de FrontEnd001.CloudApp.Net (Service cloud face à Internet)</span><span class="sxs-lookup"><span data-stu-id="9d884-249">An internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="9d884-250">Comme aucun point de terminaison n’est ouvert pour SQL, ce trafic ne franchit pas le service cloud et n’atteint pas le pare-feu</span><span class="sxs-lookup"><span data-stu-id="9d884-250">Since there are no endpoints open for SQL, this traffic would not pass the Cloud Service and wouldn’t reach the firewall</span></span>
3. <span data-ttu-id="9d884-251">Si des points de terminaison étaient ouverts pour une raison quelconque, le sous-réseau frontal commence le traitement des règles entrantes :</span><span class="sxs-lookup"><span data-stu-id="9d884-251">If endpoints were open for some reason, the Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="9d884-252">La règle NSG 1 (DNS) ne s’applique pas, passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="9d884-252">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="9d884-253">La règle NSG 2 (RDP) ne s’applique pas, passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="9d884-253">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="9d884-254">La règle NSG 3 (Internet pour IIS01) s’applique, le trafic est autorisé, arrêter le traitement.</span><span class="sxs-lookup"><span data-stu-id="9d884-254">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="9d884-255">Le trafic parvient à l’adresse IP de IIS01 (10.0.1.5).</span><span class="sxs-lookup"><span data-stu-id="9d884-255">Traffic hits internal IP address of the IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="9d884-256">IIS01 n’est pas à l’écoute sur le port 1433, donc aucune réponse à la demande</span><span class="sxs-lookup"><span data-stu-id="9d884-256">IIS01 isn't listening on port 1433, so no response to the request</span></span>

## <a name="conclusion"></a><span data-ttu-id="9d884-257">Conclusion</span><span class="sxs-lookup"><span data-stu-id="9d884-257">Conclusion</span></span>
<span data-ttu-id="9d884-258">Cet exemple est un moyen relativement simple et direct d’isoler le sous-réseau du serveur principal du trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="9d884-258">This example is a relatively simple and straight forward way of isolating the back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="9d884-259">Vous trouverez d’autres exemples et une vue d’ensemble des frontières de sécurité réseau [ici][HOME].</span><span class="sxs-lookup"><span data-stu-id="9d884-259">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="9d884-260">Références</span><span class="sxs-lookup"><span data-stu-id="9d884-260">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="9d884-261">Script principal et configuration réseau</span><span class="sxs-lookup"><span data-stu-id="9d884-261">Main script and network config</span></span>
<span data-ttu-id="9d884-262">Enregistrez le script complet dans un fichier de script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9d884-262">Save the Full Script in a PowerShell script file.</span></span> <span data-ttu-id="9d884-263">Enregistrez la configuration réseau dans un fichier nommé « NetworkConf1.xml ».</span><span class="sxs-lookup"><span data-stu-id="9d884-263">Save the Network Config into a file named “NetworkConf1.xml.”</span></span>
<span data-ttu-id="9d884-264">Modifiez les variables définies par l’utilisateur selon vos besoins puis exécutez le script.</span><span class="sxs-lookup"><span data-stu-id="9d884-264">Modify the user-defined variables as needed and run the script.</span></span>

#### <a name="full-script"></a><span data-ttu-id="9d884-265">Script complet</span><span class="sxs-lookup"><span data-stu-id="9d884-265">Full script</span></span>
<span data-ttu-id="9d884-266">Ce script exécutera les actions suivantes en fonction des variables définies par l’utilisateur ;</span><span class="sxs-lookup"><span data-stu-id="9d884-266">This script will, based on the user-defined variables;</span></span>

1. <span data-ttu-id="9d884-267">Connexion à un abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="9d884-267">Connect to an Azure subscription</span></span>
2. <span data-ttu-id="9d884-268">Créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="9d884-268">Create a storage account</span></span>
3. <span data-ttu-id="9d884-269">Création d’un réseau virtuel et de deux sous-réseaux, comme indiqué dans le fichier de configuration du réseau</span><span class="sxs-lookup"><span data-stu-id="9d884-269">Create a VNet and two subnets as defined in the Network Config file</span></span>
4. <span data-ttu-id="9d884-270">Génération de quatre machines virtuelles Windows Server</span><span class="sxs-lookup"><span data-stu-id="9d884-270">Build four windows server VMs</span></span>
5. <span data-ttu-id="9d884-271">Configurez un groupe de sécurité réseau, notamment :</span><span class="sxs-lookup"><span data-stu-id="9d884-271">Configure NSG including:</span></span>
   * <span data-ttu-id="9d884-272">Création d’un groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="9d884-272">Creating an NSG</span></span>
   * <span data-ttu-id="9d884-273">Ajout de règles à ce dernier</span><span class="sxs-lookup"><span data-stu-id="9d884-273">Populating it with rules</span></span>
   * <span data-ttu-id="9d884-274">La liaison du groupe de sécurité réseaux au sous-réseaux appropriés</span><span class="sxs-lookup"><span data-stu-id="9d884-274">Binding the NSG to the appropriate subnets</span></span>

<span data-ttu-id="9d884-275">Ce script PowerShell doit être exécuté localement sur un PC ou un serveur connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="9d884-275">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9d884-276">Lorsque ce script est exécuté, des avertissements ou autres messages d’information peuvent s’afficher dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9d884-276">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="9d884-277">Seuls les messages d’erreur affichés en rouge sont source de préoccupation.</span><span class="sxs-lookup"><span data-stu-id="9d884-277">Only error messages in red are cause for concern.</span></span>
> 
>

```PowerShell
<# 
 .SYNOPSIS
  Example of Network Security Groups in an isolated network (Azure only, no hybrid connections)

 .DESCRIPTION
  This script will build out a sample DMZ setup containing:
   - A default storage account for VM disks
   - Two new cloud services
   - Two Subnets (FrontEnd and BackEnd subnets)
   - One server on the FrontEnd Subnet
   - Three Servers on the BackEnd Subnet
   - Network Security Groups to allow/deny traffic patterns as declared

  Before running script, ensure the network configuration file is created in
  the directory referenced by $NetworkConfigFile variable (or update the
  variable to reflect the path and file name of the config file being used).

 .Notes
  Security requirements are different for each use case and can be addressed in a
  myriad of ways. Please be sure that any sensitive data or applications are behind
  the appropriate layer(s) of protection. This script serves as an example of some
  of the techniques that can be used, but should not be used for all scenarios. You
  are responsible to assess your security needs and the appropriate protections
  needed, and then effectively implement those protections.

  FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
   IIS01      - 10.0.1.5

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

# User-Defined Global Variables
  # These should be changes to reflect your subscription and services
  # Invalid options will fail in the validation section

  # Subscription Access Details
    $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

  # VM Account, Location, and Storage Details
    $LocalAdmin = "theAdmin"
    $DeploymentLocation = "Central US"
    $StorageAccountName = "vmstore02"

  # Service Details
    $FrontEndService = "FrontEnd001"
    $BackEndService = "BackEnd001"

  # Network Details
    $VNetName = "CorpNetwork"
    $FESubnet = "FrontEnd"
    $FEPrefix = "10.0.1.0/24"
    $BESubnet = "BackEnd"
    $BEPrefix = "10.0.2.0/24"
    $NetworkConfigFile = "C:\Scripts\NetworkConf1.xml"

  # VM Base Disk Image Details
    $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

  # NSG Details
    $NSGName = "MyVNetSG"

# User-Defined VM Specific Configuration
    # Note: To ensure proper NSG Rule creation later in this script:
    #       - The Web Server must be VM 0
    #       - The AppVM1 Server must be VM 1
    #       - The DNS server must be VM 3
    #
    #       Otherwise the NSG rules in the last section of this
    #       script will need to be changed to match the modified
    #       VM array numbers ($i) so the NSG Rule IP addresses
    #       are aligned to the associated VM IP addresses.

    # VM 0 - The Web Server
      $VMName += "IIS01"
      $ServiceName += $FrontEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $FESubnet
      $VMIP += "10.0.1.5"

    # VM 1 - The First Application Server
      $VMName += "AppVM01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.5"

    # VM 2 - The Second Application Server
      $VMName += "AppVM02"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.6"

    # VM 3 - The DNS Server
      $VMName += "DNS01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.4"

# ----------------------------- #
# No User-Defined Variables or  #
# Configuration past this point #
# ----------------------------- #    

  # Get your Azure accounts
    Add-AzureAccount
    Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
    Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

  # Create Storage Account
    If (Test-AzureName -Storage -Name $StorageAccountName) { 
        Write-Host "Fatal Error: This storage account name is already in use, please pick a different name." -ForegroundColor Red
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

If (Test-AzureName -Service -Name $FrontEndService) { 
    Write-Host "The FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "The FrontEndService service name is valid for use." -ForegroundColor Green}

If (Test-AzureName -Service -Name $BackEndService) { 
    Write-Host "The BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "The BackEndService service name is valid for use." -ForegroundColor Green}

If (-Not (Test-Path $NetworkConfigFile)) { 
    Write-Host 'The network config file was not found, please update the $NetworkConfigFile variable to point to the network config xml file.' -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "The network configuration file was found" -ForegroundColor Green
        If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
            Write-Host 'The deployment location was not found in the network config file, please check the network config file to ensure the $DeploymentLocation variable is correct and the network config file matches.' -ForegroundColor Yellow
            $FatalError = $true}
        Else { Write-Host "The deployment location was found in the network config file." -ForegroundColor Green}}

If ($FatalError) {
    Write-Host "A fatal error has occurred, please see the above messages for more information." -ForegroundColor Red
    Return}
Else { Write-Host "Validation passed, now building the environment." -ForegroundColor Green}

# Create VNET
    Write-Host "Creating VNET" -ForegroundColor Cyan 
    Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

# Create Services
    Write-Host "Creating Services" -ForegroundColor Cyan
    New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
    New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

# Build VMs
    $i=0
    $VMName | Foreach {
        Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
        New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
            Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
            Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
            Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
            Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
            Remove-AzureEndpoint -Name "PowerShell" | `
            New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
            # Note: A Remote Desktop endpoint is automatically created when each VM is created.
        $i++
    }
    # Add HTTP Endpoint for IIS01
    Get-AzureVM -ServiceName $ServiceName[0] -Name $VMName[0] | Add-AzureEndpoint -Name HTTP -Protocol tcp -LocalPort 80 -PublicPort 80 | Update-AzureVM

# Configure NSG
    Write-Host "Configuring the Network Security Group (NSG)" -ForegroundColor Cyan

  # Build the NSG
    Write-Host "Building the NSG" -ForegroundColor Cyan
    New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

  # Add NSG Rules
    Write-Host "Writing rules into the NSG" -ForegroundColor Cyan
    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[3] -DestinationPortRange '53' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP to $VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet to $($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
        -SourceAddressPrefix Internet -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[0]) to $($VMName[1])" -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[0] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[1] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate the $VNetName VNet from the Internet" -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate the $FESubnet subnet from the $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
        -Protocol *

    # Assign the NSG to the Subnets
        Write-Host "Binding the NSG to both subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

# Optional Post-script Manual Configuration
  # Install Test Web App (Run Post-Build Script on the IIS Server)
  # Install Backend resource (Run Post-Build Script on the AppVM01)
  Write-Host
  Write-Host "Build Complete!" -ForegroundColor Green
  Write-Host
  Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
  Write-Host " - Install Test Web App (Run Post-Build Script on the IIS Server)" -ForegroundColor Gray
  Write-Host " - Install Backend resource (Run Post-Build Script on the AppVM01)" -ForegroundColor Gray
  Write-Host
```

#### <a name="network-config-file"></a><span data-ttu-id="9d884-278">Fichier de configuration réseau</span><span class="sxs-lookup"><span data-stu-id="9d884-278">Network config file</span></span>
<span data-ttu-id="9d884-279">Enregistrez ce fichier XML avec l’emplacement mis à jour et ajoutez le lien vers ce fichier à la variable $NetworkConfigFile dans le script précédent.</span><span class="sxs-lookup"><span data-stu-id="9d884-279">Save this xml file with updated location and add the link to this file to the $NetworkConfigFile variable in the preceding script.</span></span>

```XML
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
```

#### <a name="sample-application-scripts"></a><span data-ttu-id="9d884-280">Exemples de scripts d’application</span><span class="sxs-lookup"><span data-stu-id="9d884-280">Sample application scripts</span></span>
<span data-ttu-id="9d884-281">Si vous souhaitez installer un exemple d’application et d’autres exemples de zone DMZ, vous en trouverez à l’adresse suivante : [Exemple de script d’application][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="9d884-281">If you wish to install a sample application for this, and other DMZ Examples, one has been provided at the following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d884-282">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9d884-282">Next steps</span></span>
* <span data-ttu-id="9d884-283">Mise à jour et enregistrement du fichier XML</span><span class="sxs-lookup"><span data-stu-id="9d884-283">Update and save XML file</span></span>
* <span data-ttu-id="9d884-284">Exécution du script PowerShell pour générer l’environnement</span><span class="sxs-lookup"><span data-stu-id="9d884-284">Run the PowerShell script to build the environment</span></span>
* <span data-ttu-id="9d884-285">Installation de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="9d884-285">Install the sample application</span></span>
* <span data-ttu-id="9d884-286">Tester différents flux de trafic via cette zone DMZ</span><span class="sxs-lookup"><span data-stu-id="9d884-286">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
<span data-ttu-id="9d884-287">[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "Zone DMZ avec groupe de sécurité réseau (NSG)"</span><span class="sxs-lookup"><span data-stu-id="9d884-287">[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "Inbound DMZ with NSG"</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

