---
title: "aaaAzure DMZ, exemple : créer un réseau de périmètre Simple avec des groupes de sécurité réseau | Documents Microsoft"
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
ms.openlocfilehash: 32a40a8dc7539c4c7293988e6c36e5e32ef11045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a><span data-ttu-id="50aac-103">Exemple 1 : Générer une zone DMZ simple en utilisant des groupes de sécurité réseau (NSG) avec Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="50aac-103">Example 1 – Build a simple DMZ using NSGs with classic PowerShell</span></span>
<span data-ttu-id="50aac-104">[Retour toohello Page meilleures pratiques de sécurité limite][HOME]</span><span class="sxs-lookup"><span data-stu-id="50aac-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="50aac-105">Modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="50aac-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="50aac-106">Classic - PowerShell</span><span class="sxs-lookup"><span data-stu-id="50aac-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="50aac-107">Cet exemple crée une zone DMZ primitive avec quatre serveurs Windows et des groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="50aac-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="50aac-108">Cet exemple décrit chacun des hello pertinentes PowerShell commandes tooprovide une meilleure compréhension de chaque étape.</span><span class="sxs-lookup"><span data-stu-id="50aac-108">This example describes each of hello relevant PowerShell commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="50aac-109">Il existe également un scénario de trafic section tooprovide un détaillées étape par étape comment le trafic passe par le biais des couches de défense dans hello hello réseau de périmètre.</span><span class="sxs-lookup"><span data-stu-id="50aac-109">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="50aac-110">Enfin, dans la section des références hello est code complet de hello et instruction toobuild cette tootest d’environnement et de faire des essais avec différents scénarios.</span><span class="sxs-lookup"><span data-stu-id="50aac-110">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="50aac-111">![Réseau de périmètre entrant avec groupe de sécurité réseau][1]</span><span class="sxs-lookup"><span data-stu-id="50aac-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="50aac-112">Description de l’environnement</span><span class="sxs-lookup"><span data-stu-id="50aac-112">Environment description</span></span>
<span data-ttu-id="50aac-113">Dans cet exemple, un abonnement contient hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="50aac-113">In this example a subscription contains hello following resources:</span></span>

* <span data-ttu-id="50aac-114">deux services cloud : « FrontEnd001 », « BackEnd001 »,</span><span class="sxs-lookup"><span data-stu-id="50aac-114">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="50aac-115">Un réseau virtuel « CorpNetwork » avec deux sous-réseaux « FrontEnd » et « BackEnd »</span><span class="sxs-lookup"><span data-stu-id="50aac-115">A Virtual Network, “CorpNetwork”, with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="50aac-116">Un groupe de sécurité réseau qui est appliquée tooboth sous-réseaux</span><span class="sxs-lookup"><span data-stu-id="50aac-116">A Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="50aac-117">un serveur Windows Server représentant un serveur web d’application (« IIS01 »),</span><span class="sxs-lookup"><span data-stu-id="50aac-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="50aac-118">Deux serveurs Windows Server qui représentent les serveurs principaux d’applications (« AppVM01 », « AppVM02 »)</span><span class="sxs-lookup"><span data-stu-id="50aac-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="50aac-119">Un serveur Windows Server qui représente un serveur DNS (« DNS01 »),</span><span class="sxs-lookup"><span data-stu-id="50aac-119">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="50aac-120">Dans la section des références de hello, il existe un script PowerShell qui génère la plupart des environnement hello décrite dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="50aac-120">In hello references section, there is a PowerShell script that builds most of hello environment described in this example.</span></span> <span data-ttu-id="50aac-121">Machines virtuelles de génération hello et réseaux virtuels, bien que s’effectuent par le script d’exemple hello, ne sont pas décrits en détail dans ce document.</span><span class="sxs-lookup"><span data-stu-id="50aac-121">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span> 

<span data-ttu-id="50aac-122">environnement de hello toobuild ;</span><span class="sxs-lookup"><span data-stu-id="50aac-122">toobuild hello environment;</span></span>

1. <span data-ttu-id="50aac-123">Fichier hello réseau config xml figurant dans la section de références hello (mis à jour avec les noms, l’emplacement et scénario de hello donné toomatch IP adresses)</span><span class="sxs-lookup"><span data-stu-id="50aac-123">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="50aac-124">Variables utilisateur hello script toomatch hello environnement hello de script de mise à jour hello est toobe exécutée (abonnements, les noms de service, etc.).</span><span class="sxs-lookup"><span data-stu-id="50aac-124">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc.)</span></span>
3. <span data-ttu-id="50aac-125">Exécutez le script de hello dans PowerShell</span><span class="sxs-lookup"><span data-stu-id="50aac-125">Execute hello script in PowerShell</span></span>

>[!Note]
><span data-ttu-id="50aac-126">région Hello signifiée Bonjour script PowerShell doit correspondre à la région hello signifiée dans le fichier xml de configuration de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="50aac-126">hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>
>
>

<span data-ttu-id="50aac-127">Une fois que hello script s’exécute correctement supplémentaire étapes facultatives peuvent être prises, dans la section des références de hello sont deux tooset de scripts de serveur web de hello et le serveur d’applications à un tooallow d’application web simple test avec cette configuration de réseau de périmètre.</span><span class="sxs-lookup"><span data-stu-id="50aac-127">Once hello script runs successfully additional optional steps may be taken, in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="50aac-128">Hello sections suivantes fournissent une description détaillée des groupes de sécurité réseau et leur fonctionnement pour cet exemple en parcourant des lignes de clés de script PowerShell de hello.</span><span class="sxs-lookup"><span data-stu-id="50aac-128">hello following sections provide a detailed description of Network Security Groups and how they function for this example by walking through key lines of hello PowerShell script.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="50aac-129">Groupes de sécurité réseau (NSG)</span><span class="sxs-lookup"><span data-stu-id="50aac-129">Network Security Groups (NSG)</span></span>
<span data-ttu-id="50aac-130">Pour cet exemple, un groupe NSG est créé, puis chargé avec six règles.</span><span class="sxs-lookup"><span data-stu-id="50aac-130">For this example, an NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="50aac-131">En règle générale, vous devez créer vos règles « Autoriser » spécifiques tout d’abord et puis hello dernière plus générique « Refuser » règles.</span><span class="sxs-lookup"><span data-stu-id="50aac-131">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="50aac-132">Hello priorité détermine les règles sont évaluées en premier.</span><span class="sxs-lookup"><span data-stu-id="50aac-132">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="50aac-133">Une fois que le trafic est trouvé règle spécifique de tooapply tooa, aucune autre règle n’est évaluées.</span><span class="sxs-lookup"><span data-stu-id="50aac-133">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="50aac-134">Les règles de groupe de sécurité réseau peuvent être appliquées, que ce soit dans hello direction entrante ou sortante (du point de vue hello du sous-réseau de hello).</span><span class="sxs-lookup"><span data-stu-id="50aac-134">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
> 
> 

<span data-ttu-id="50aac-135">De façon déclarative, hello suivant les règles est généré pour le trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="50aac-135">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="50aac-136">Le trafic DNS interne (port 53) est autorisé</span><span class="sxs-lookup"><span data-stu-id="50aac-136">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="50aac-137">Le trafic RDP (port 3389) à partir d’Internet de hello tooany machine virtuelle est autorisé.</span><span class="sxs-lookup"><span data-stu-id="50aac-137">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="50aac-138">Le trafic HTTP (port 80) à partir du serveur de tooweb hello Internet (IIS01) est autorisé.</span><span class="sxs-lookup"><span data-stu-id="50aac-138">HTTP traffic (port 80) from hello Internet tooweb server (IIS01) is allowed</span></span>
4. <span data-ttu-id="50aac-139">Tout trafic (tous les ports) à partir de IIS01 tooAppVM1 est autorisée.</span><span class="sxs-lookup"><span data-stu-id="50aac-139">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="50aac-140">Tout trafic (tous les ports) à partir de hello Internet toohello réseau virtuel entier (les deux sous-réseaux) est refusé.</span><span class="sxs-lookup"><span data-stu-id="50aac-140">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="50aac-141">Tout trafic (tous les ports) à partir du sous-réseau principal toohello hello frontal sous-réseau est refusé.</span><span class="sxs-lookup"><span data-stu-id="50aac-141">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="50aac-142">Avec ces sous-réseau tooeach dépendant de règles, si une requête HTTP a été entrante à partir de hello toohello le serveur web Internet, les deux règles 3 (autoriser) et 5 (refuser) s’appliquent, mais étant donné que la règle 3 a une priorité plus élevée s’appliquerait et règle 5 ne serait pas entrent en jeu.</span><span class="sxs-lookup"><span data-stu-id="50aac-142">With these rules bound tooeach subnet, if an HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="50aac-143">Par conséquent, demande HTTP de hello serait autorisée serveur web de toohello.</span><span class="sxs-lookup"><span data-stu-id="50aac-143">Thus hello HTTP request would be allowed toohello web server.</span></span> <span data-ttu-id="50aac-144">Si ce trafic même a essayé de serveur de DNS01 tooreach hello, règle 5 (Deny) serait hello premier tooapply hello le trafic et ne serait pas autorisé toopass toohello serveur.</span><span class="sxs-lookup"><span data-stu-id="50aac-144">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="50aac-145">Règle 6 (Deny) bloque le sous-réseau frontal hello communique avec le sous-réseau du serveur principal toohello (à l’exception du trafic autorisé dans les règles 1 et 4), cet ensemble de règles protège le réseau principal de hello au cas où une personne malveillante compromet hello application web sur hello serveur frontal, serait de personne malveillante de hello limitée toohello d’accès réseau (uniquement tooresources exposée sur le serveur de AppVM01 hello) principal « protégé ».</span><span class="sxs-lookup"><span data-stu-id="50aac-145">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="50aac-146">Il existe une règle sortante par défaut qui autorise le trafic sortant toohello internet.</span><span class="sxs-lookup"><span data-stu-id="50aac-146">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="50aac-147">Pour cet exemple, nous allons autoriser le trafic sortant sans modifier les règles de trafic sortant.</span><span class="sxs-lookup"><span data-stu-id="50aac-147">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="50aac-148">toolock vers le bas le trafic dans les deux directions, utilisateur défini par routage est obligatoire et est exploré dans « Exemple 3 » sur hello [Page meilleures pratiques de sécurité limite][HOME].</span><span class="sxs-lookup"><span data-stu-id="50aac-148">toolock down traffic in both directions, User Defined Routing is required and is explored in “Example 3” on hello [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="50aac-149">Chaque règle est décrite plus en détail comme suit (**Remarque**: n’importe quel élément Bonjour suivant le début de liste avec un signe dollar (par exemple : $NSGName) est une variable définie par l’utilisateur à partir du script hello dans la section de référence hello de ce document) :</span><span class="sxs-lookup"><span data-stu-id="50aac-149">Each rule is discussed in more detail as follows (**Note**: any item in hello following list beginning with a dollar sign (for example: $NSGName) is a user-defined variable from hello script in hello reference section of this document):</span></span>

1. <span data-ttu-id="50aac-150">Tout d’abord un groupe de sécurité réseau doivent être généré des règles toohold hello :</span><span class="sxs-lookup"><span data-stu-id="50aac-150">First a Network Security Group must be built toohold hello rules:</span></span>

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. <span data-ttu-id="50aac-151">Hello première règle de cet exemple autorise le trafic DNS entre tous les réseaux internes toohello serveur DNS hello principal sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="50aac-151">hello first rule in this example allows DNS traffic between all internal networks toohello DNS server on hello backend subnet.</span></span> <span data-ttu-id="50aac-152">règle de Hello a certains paramètres importants :</span><span class="sxs-lookup"><span data-stu-id="50aac-152">hello rule has some important parameters:</span></span>
   
   * <span data-ttu-id="50aac-153">« Type » indique le sens du trafic qui sera appliqué à cette règle.</span><span class="sxs-lookup"><span data-stu-id="50aac-153">“Type” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="50aac-154">direction de Hello est hello du point de vue de l’ordinateur virtuel ou le sous-réseau de hello (selon où ce groupe de sécurité réseau est lié).</span><span class="sxs-lookup"><span data-stu-id="50aac-154">hello direction is from hello perspective of hello subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="50aac-155">Par conséquent, si le Type est « Entrant » et le trafic est entrant sous-réseau de hello, hello règle s’applique et le trafic en laissant le sous-réseau de hello ne serait pas affecté par cette règle.</span><span class="sxs-lookup"><span data-stu-id="50aac-155">Thus if Type is “Inbound” and traffic is entering hello subnet, hello rule would apply and traffic leaving hello subnet would not be affected by this rule.</span></span>
   * <span data-ttu-id="50aac-156">« Priority » définit la commande hello dans lequel un flux de trafic est évalué.</span><span class="sxs-lookup"><span data-stu-id="50aac-156">“Priority” sets hello order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="50aac-157">Hello inférieur hello numéro hello hello prioritaires.</span><span class="sxs-lookup"><span data-stu-id="50aac-157">hello lower hello number hello higher hello priority.</span></span> <span data-ttu-id="50aac-158">Lorsqu’une règle s’applique le flux de trafic spécifique tooa, aucune autre règle n’est traitées.</span><span class="sxs-lookup"><span data-stu-id="50aac-158">When a rule applies tooa specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="50aac-159">Par conséquent, si une règle avec la priorité 1 autorise le trafic et une règle de priorité 2 refuse le trafic et les deux règles s’appliquent tootraffic alors le trafic de hello serait autorisé tooflow (étant donné que la règle 1 a une priorité plus élevée qu’il a pris effet et aucune autre règle n’ont été appliquées).</span><span class="sxs-lookup"><span data-stu-id="50aac-159">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply tootraffic then hello traffic would be allowed tooflow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
   * <span data-ttu-id="50aac-160">« Action » indique si le trafic concerné par cette règle est bloqué ou autorisé.</span><span class="sxs-lookup"><span data-stu-id="50aac-160">“Action” signifies if traffic affected by this rule is blocked or allowed.</span></span>

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. <span data-ttu-id="50aac-161">Cette règle permet de tooflow de trafic RDP à partir de port RDP hello internet toohello sur n’importe quel serveur hello lié sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="50aac-161">This rule allows RDP traffic tooflow from hello internet toohello RDP port on any server on hello bound subnet.</span></span> <span data-ttu-id="50aac-162">Cette règle utilise deux types spéciaux de préfixes d’adresses ; « VIRTUAL_NETWORK » et « INTERNET ».</span><span class="sxs-lookup"><span data-stu-id="50aac-162">This rule uses two special types of address prefixes; “VIRTUAL_NETWORK” and “INTERNET.”</span></span> <span data-ttu-id="50aac-163">Ces balises sont un tooaddress facilement une catégorie supérieure de préfixes d’adresses.</span><span class="sxs-lookup"><span data-stu-id="50aac-163">These tags are an easy way tooaddress a larger category of address prefixes.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. <span data-ttu-id="50aac-164">Cette règle permet de trafic entrant du trafic toohit hello le serveur web internet.</span><span class="sxs-lookup"><span data-stu-id="50aac-164">This rule allows inbound internet traffic toohit hello web server.</span></span> <span data-ttu-id="50aac-165">Cette règle ne modifie pas le comportement de routage hello.</span><span class="sxs-lookup"><span data-stu-id="50aac-165">This rule does not change hello routing behavior.</span></span> <span data-ttu-id="50aac-166">règle de Hello autorise uniquement le trafic destiné à IIS01 toopass.</span><span class="sxs-lookup"><span data-stu-id="50aac-166">hello rule only allows traffic destined for IIS01 toopass.</span></span> <span data-ttu-id="50aac-167">Par conséquent, si le trafic à partir de hello Internet avait le serveur web de hello comme destination cette règle est autoriser et arrêter le traitement des règles.</span><span class="sxs-lookup"><span data-stu-id="50aac-167">Thus if traffic from hello Internet had hello web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="50aac-168">(Dans la règle hello avec une priorité de 140 tous les autres trafic internet entrant est bloqué).</span><span class="sxs-lookup"><span data-stu-id="50aac-168">(In hello rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="50aac-169">Si vous traitez uniquement le trafic HTTP, cette règle pourrait être plue restreint tooonly autoriser Destination Port 80.</span><span class="sxs-lookup"><span data-stu-id="50aac-169">If you're only processing HTTP traffic, this rule could be further restricted tooonly allow Destination Port 80.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet too$VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. <span data-ttu-id="50aac-170">Cette règle permet toopass le trafic à partir du serveur de IIS01 hello toohello AppVM01 serveur, une règle ultérieure bloque tout autre trafic tooBackend de serveur frontal.</span><span class="sxs-lookup"><span data-stu-id="50aac-170">This rule allows traffic toopass from hello IIS01 server toohello AppVM01 server, a later rule blocks all other Frontend tooBackend traffic.</span></span> <span data-ttu-id="50aac-171">tooimprove cette règle, si le port de hello est connu, qui doit être ajoutée.</span><span class="sxs-lookup"><span data-stu-id="50aac-171">tooimprove this rule, if hello port is known that should be added.</span></span> <span data-ttu-id="50aac-172">Par exemple, si le serveur IIS hello accède uniquement à SQL Server sur AppVM01, plage de ports de Destination hello doit être changé de « * » (tout) too1433 (hello port SQL), permettant ainsi une surface d’attaque entrante réduite sur AppVM01 doit hello web application jamais être compromise.</span><span class="sxs-lookup"><span data-stu-id="50aac-172">For example, if hello IIS server is hitting only SQL Server on AppVM01, hello Destination Port Range should be changed from “*” (Any) too1433 (hello SQL port) thus allowing a smaller inbound attack surface on AppVM01 should hello web application ever be compromised.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] too$VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. <span data-ttu-id="50aac-173">Cette règle refuse le trafic à partir des serveurs de tooany hello internet sur le réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="50aac-173">This rule denies traffic from hello internet tooany servers on hello network.</span></span> <span data-ttu-id="50aac-174">Les règles hello avec une priorité de 110 et 120, effet de hello est tooallow uniquement internet trafic toohello pare-feu entrantes et ports RDP sur les serveurs et bloque tout le reste.</span><span class="sxs-lookup"><span data-stu-id="50aac-174">With hello rules at priority 110 and 120, hello effect is tooallow only inbound internet traffic toohello firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="50aac-175">Cette règle est une « sécurité intégrée » règle tooblock tous les flux inattendues.</span><span class="sxs-lookup"><span data-stu-id="50aac-175">This rule is a "fail-safe" rule tooblock all unexpected flows.</span></span>
    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $VNetName VNet from hello Internet" `
        -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *
    ```
7. <span data-ttu-id="50aac-176">règle finale de Hello refuse le trafic du sous-réseau de hello frontal sous-réseau toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="50aac-176">hello final rule denies traffic from hello Frontend subnet toohello Backend subnet.</span></span> <span data-ttu-id="50aac-177">Étant donné que cette règle est la seule règle de trafic entrant, le trafic inverse est autorisé (à partir de toohello de back-end hello frontal).</span><span class="sxs-lookup"><span data-stu-id="50aac-177">Since this rule is an Inbound only rule, reverse traffic is allowed (from hello Backend toohello Frontend).</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" `
        -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix `
        -DestinationPortRange '*' `
        -Protocol * 
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="50aac-178">Scénarios de trafic</span><span class="sxs-lookup"><span data-stu-id="50aac-178">Traffic scenarios</span></span>
#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="50aac-179">(*Autorisées*) Internet tooweb server</span><span class="sxs-lookup"><span data-stu-id="50aac-179">(*Allowed*) Internet tooweb server</span></span>
1. <span data-ttu-id="50aac-180">Un utilisateur Internet demande une page HTTP en provenance de FrontEnd001.CloudApp.Net (service cloud face à Internet)</span><span class="sxs-lookup"><span data-stu-id="50aac-180">An internet user requests an HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="50aac-181">Le trafic via le point de terminaison ouvert sur le port 80 vers IIS01 passe du service de cloud computing (serveur web de hello)</span><span class="sxs-lookup"><span data-stu-id="50aac-181">Cloud service passes traffic through open endpoint on port 80 towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="50aac-182">Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="50aac-182">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="50aac-183">Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="50aac-183">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="50aac-184">Règle de groupe de sécurité réseau 2 (RDP) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="50aac-184">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="50aac-185">Règle de groupe de sécurité réseau 3 (tooIIS01 Internet) s’applique, le trafic est le traitement des règles autorisées, arrêter</span><span class="sxs-lookup"><span data-stu-id="50aac-185">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="50aac-186">Le trafic atteint l’adresse IP interne du serveur web de hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="50aac-186">Traffic hits internal IP address of hello web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="50aac-187">IIS01 écoute pour le trafic web, reçoit la requête et démarre le traitement de demande de hello</span><span class="sxs-lookup"><span data-stu-id="50aac-187">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
6. <span data-ttu-id="50aac-188">IIS01 demande hello SQL Server sur AppVM01 pour plus d’informations</span><span class="sxs-lookup"><span data-stu-id="50aac-188">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="50aac-189">Comme il n'existe aucune règle sortante sur le sous-réseau du serveur frontal, le trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="50aac-189">Since there are no outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="50aac-190">sous-réseau du serveur principal Hello commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="50aac-190">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="50aac-191">Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="50aac-191">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="50aac-192">Règle de groupe de sécurité réseau 2 (RDP) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="50aac-192">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="50aac-193">Règle de groupe de sécurité réseau 3 (tooFirewall Internet) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="50aac-193">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="50aac-194">Règle de groupe de sécurité réseau 4 (IIS01 tooAppVM01) s’applique, le trafic est le traitement des règles autorisées, arrêter</span><span class="sxs-lookup"><span data-stu-id="50aac-194">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="50aac-195">AppVM01 reçoit hello requête SQL et répond</span><span class="sxs-lookup"><span data-stu-id="50aac-195">AppVM01 receives hello SQL Query and responds</span></span>
10. <span data-ttu-id="50aac-196">Dans la mesure où il n’y a aucune règles de trafic sortant sur le sous-réseau du serveur principal hello, réponse de hello est autorisée.</span><span class="sxs-lookup"><span data-stu-id="50aac-196">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
11. <span data-ttu-id="50aac-197">Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="50aac-197">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="50aac-198">Il n’existe aucune règle de groupe de sécurité réseau qui applique des tooInbound trafic de sous-réseau du serveur frontal de toohello de sous-réseau hello back-end, donc aucune des règles du groupe de sécurité réseau hello s’appliquent</span><span class="sxs-lookup"><span data-stu-id="50aac-198">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="50aac-199">règle du système par défaut Hello autorisant le trafic entre sous-réseaux permettrait ce trafic donc hello le trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="50aac-199">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
12. <span data-ttu-id="50aac-200">le serveur IIS Hello reçoit la réponse SQL hello et termine la réponse HTTP de hello et envoie toohello demandeur</span><span class="sxs-lookup"><span data-stu-id="50aac-200">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requestor</span></span>
13. <span data-ttu-id="50aac-201">Étant donné qu’aucune règle sortante sur le sous-réseau du serveur frontal hello hello réponse soit autorisée, et hello internet utilisateur reçoit hello web page est demandée.</span><span class="sxs-lookup"><span data-stu-id="50aac-201">Since there are no outbound rules on hello Frontend subnet hello response is allowed, and hello internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-toobackend"></a><span data-ttu-id="50aac-202">(*Autorisées*) RDP toobackend</span><span class="sxs-lookup"><span data-stu-id="50aac-202">(*Allowed*) RDP toobackend</span></span>
1. <span data-ttu-id="50aac-203">Administrateur du serveur sur internet demande tooAppVM01 de session RDP sur BackEnd001.CloudApp.Net:xxxxx où xxxxx représente le numéro de port hello affecté de façon aléatoire pour RDP tooAppVM01 (port de hello affecté sont accessibles sur hello portail Azure ou via PowerShell)</span><span class="sxs-lookup"><span data-stu-id="50aac-203">Server Admin on internet requests RDP session tooAppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is hello randomly assigned port number for RDP tooAppVM01 (hello assigned port can be found on hello Azure portal or via PowerShell)</span></span>
2. <span data-ttu-id="50aac-204">Le sous-réseau du serveur principal entame le traitement du réseau entrant :</span><span class="sxs-lookup"><span data-stu-id="50aac-204">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="50aac-205">Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="50aac-205">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="50aac-206">La règle NSG 2 (RDP) s’applique, le trafic est autorisé, arrêter le traitement des règles</span><span class="sxs-lookup"><span data-stu-id="50aac-206">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
3. <span data-ttu-id="50aac-207">En l’absence de réseau sortant, les règles par défaut s’appliquent et le retour de trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="50aac-207">With no outbound rules, default rules apply and return traffic is allowed</span></span>
4. <span data-ttu-id="50aac-208">La Session RDP est activée.</span><span class="sxs-lookup"><span data-stu-id="50aac-208">RDP session is enabled</span></span>
5. <span data-ttu-id="50aac-209">Invites AppVM01 hello nom d’utilisateur et mot de passe</span><span class="sxs-lookup"><span data-stu-id="50aac-209">AppVM01 prompts for hello user name and password</span></span>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="50aac-210">(*Autorisé*) recherche DNS du serveur web sur le serveur DNS</span><span class="sxs-lookup"><span data-stu-id="50aac-210">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="50aac-211">Web des besoins du serveur, IIS01, de flux de données à www.data.gov, mais doit tooresolve hello adresse.</span><span class="sxs-lookup"><span data-stu-id="50aac-211">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="50aac-212">Hello configuration réseau pour les listes de réseau virtuel hello DNS01 (10.0.2.4 sur le sous-réseau du serveur principal hello) en tant que serveur DNS principal de hello, IIS01 envoie hello DNS demande tooDNS01</span><span class="sxs-lookup"><span data-stu-id="50aac-212">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="50aac-213">Aucune règle sur le trafic sortant sur le sous-réseau du serveur frontal. Le trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="50aac-213">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="50aac-214">Le sous-réseau du serveur principal entame le traitement du réseau entrant :</span><span class="sxs-lookup"><span data-stu-id="50aac-214">Backend subnet begins inbound rule processing:</span></span>
   * <span data-ttu-id="50aac-215">La règle NSG 1 (DNS) s’applique, le trafic est autorisé, arrêter le traitement des règles</span><span class="sxs-lookup"><span data-stu-id="50aac-215">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="50aac-216">Serveur DNS reçoit la demande de hello</span><span class="sxs-lookup"><span data-stu-id="50aac-216">DNS server receives hello request</span></span>
6. <span data-ttu-id="50aac-217">Serveur DNS n’a pas adresse hello mis en cache et demande à un serveur DNS racine sur hello internet</span><span class="sxs-lookup"><span data-stu-id="50aac-217">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="50aac-218">Aucune règle sortante sur le sous-réseau du serveur principal, le trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="50aac-218">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="50aac-219">Serveur DNS Internet répond, étant donné que cette session a été lancée en interne, réponse de hello est autorisée.</span><span class="sxs-lookup"><span data-stu-id="50aac-219">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="50aac-220">Le serveur DNS met en cache la réponse de hello et répond tooIIS01 arrière de demande initiale toohello</span><span class="sxs-lookup"><span data-stu-id="50aac-220">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="50aac-221">Aucune règle sortante sur le sous-réseau du serveur principal, le trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="50aac-221">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="50aac-222">Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="50aac-222">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="50aac-223">Il n’existe aucune règle de groupe de sécurité réseau qui applique des tooInbound trafic de sous-réseau du serveur frontal de toohello de sous-réseau hello back-end, donc aucune des règles du groupe de sécurité réseau hello s’appliquent</span><span class="sxs-lookup"><span data-stu-id="50aac-223">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="50aac-224">règle du système par défaut Hello autorisant le trafic entre sous-réseaux permet ce trafic donc hello le trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="50aac-224">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="50aac-225">IIS01 reçoit hello réponse DNS01</span><span class="sxs-lookup"><span data-stu-id="50aac-225">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="50aac-226">(*Autorisé*) fichier d’accès de serveur Web sur AppVM01</span><span class="sxs-lookup"><span data-stu-id="50aac-226">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="50aac-227">IIS01 demande un fichier sur AppVM01</span><span class="sxs-lookup"><span data-stu-id="50aac-227">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="50aac-228">Aucune règle sur le trafic sortant sur le sous-réseau du serveur frontal. Le trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="50aac-228">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="50aac-229">sous-réseau du serveur principal Hello commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="50aac-229">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="50aac-230">Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="50aac-230">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="50aac-231">Règle de groupe de sécurité réseau 2 (RDP) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="50aac-231">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="50aac-232">Règle de groupe de sécurité réseau 3 (tooIIS01 Internet) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="50aac-232">NSG Rule 3 (Internet tooIIS01) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="50aac-233">Règle de groupe de sécurité réseau 4 (IIS01 tooAppVM01) s’applique, le trafic est le traitement des règles autorisées, arrêter</span><span class="sxs-lookup"><span data-stu-id="50aac-233">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="50aac-234">AppVM01 reçoit la demande de hello et répond avec le fichier (en supposant que l’accès est autorisé)</span><span class="sxs-lookup"><span data-stu-id="50aac-234">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="50aac-235">Dans la mesure où il n’y a aucune règles de trafic sortant sur le sous-réseau du serveur principal hello, réponse de hello est autorisée.</span><span class="sxs-lookup"><span data-stu-id="50aac-235">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
6. <span data-ttu-id="50aac-236">Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="50aac-236">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="50aac-237">Il n’existe aucune règle de groupe de sécurité réseau qui applique des tooInbound trafic de sous-réseau du serveur frontal de toohello de sous-réseau hello back-end, donc aucune des règles du groupe de sécurité réseau hello s’appliquent</span><span class="sxs-lookup"><span data-stu-id="50aac-237">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
   2. <span data-ttu-id="50aac-238">règle du système par défaut Hello autorisant le trafic entre sous-réseaux permettrait ce trafic donc hello le trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="50aac-238">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="50aac-239">le serveur IIS Hello reçoit le fichier de hello</span><span class="sxs-lookup"><span data-stu-id="50aac-239">hello IIS server receives hello file</span></span>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="50aac-240">(*Refusé*) serveur de toobackend Web</span><span class="sxs-lookup"><span data-stu-id="50aac-240">(*Denied*) Web toobackend server</span></span>
1. <span data-ttu-id="50aac-241">Un utilisateur internet tente de tooaccess un fichier sur AppVM01 via hello BackEnd001.CloudApp.Net service</span><span class="sxs-lookup"><span data-stu-id="50aac-241">An internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="50aac-242">Étant donné qu’aucun point de terminaison ouvert pour le partage de fichiers, ce trafic ne peut pas passer hello Service Cloud et ne pas de joindre le serveur de hello</span><span class="sxs-lookup"><span data-stu-id="50aac-242">Since there are no endpoints open for file share, this traffic would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="50aac-243">Si les points de terminaison hello étaient ouverts pour une raison quelconque, la règle de groupe de sécurité réseau 5 (tooVNet Internet) susceptibles de bloquer ce trafic</span><span class="sxs-lookup"><span data-stu-id="50aac-243">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="50aac-244">(*Refusé*) recherche DNS web sur le serveur DNS</span><span class="sxs-lookup"><span data-stu-id="50aac-244">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="50aac-245">Un utilisateur internet tente de toolook d’un enregistrement DNS interne sur DNS01 via hello BackEnd001.CloudApp.Net service</span><span class="sxs-lookup"><span data-stu-id="50aac-245">An internet user tries toolook up an internal DNS record on DNS01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="50aac-246">Étant donné qu’aucun point de terminaison ouvert pour un serveur DNS, ce trafic ne peut pas passer hello Service Cloud et ne pas de joindre le serveur de hello</span><span class="sxs-lookup"><span data-stu-id="50aac-246">Since there are no endpoints open for DNS, this traffic would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="50aac-247">Si les points de terminaison hello étaient ouverts pour une raison quelconque, la règle de groupe de sécurité réseau 5 (tooVNet Internet) susceptibles de bloquer ce trafic (Remarque : cette règle 1 (DNS) ne peuvent pas s’appliquer pour deux raisons, première adresse de la source hello est hello internet, cette règle s’applique uniquement toohello réseau local en tant que hello source, Cette règle est une règle d’autorisation, donc il n’est jamais refuser le trafic)</span><span class="sxs-lookup"><span data-stu-id="50aac-247">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first hello source address is hello internet, this rule only applies toohello local VNet as hello source, also this rule is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-toosql-access-through-firewall"></a><span data-ttu-id="50aac-248">(*Refusé*) Web tooSQL l’accès via le pare-feu</span><span class="sxs-lookup"><span data-stu-id="50aac-248">(*Denied*) Web tooSQL access through firewall</span></span>
1. <span data-ttu-id="50aac-249">Un utilisateur Internet demande des données SQL de FrontEnd001.CloudApp.Net (Service cloud face à Internet)</span><span class="sxs-lookup"><span data-stu-id="50aac-249">An internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="50aac-250">Étant donné qu’aucun point de terminaison ouvert pour SQL, ce trafic ne peut pas passer hello Service Cloud et ne pas atteindre le pare-feu hello</span><span class="sxs-lookup"><span data-stu-id="50aac-250">Since there are no endpoints open for SQL, this traffic would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="50aac-251">Si les points de terminaison ont été ouverts pour une raison quelconque, sous-réseau du serveur frontal hello commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="50aac-251">If endpoints were open for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="50aac-252">Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="50aac-252">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="50aac-253">Règle de groupe de sécurité réseau 2 (RDP) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="50aac-253">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="50aac-254">Règle de groupe de sécurité réseau 3 (tooIIS01 Internet) s’applique, le trafic est le traitement des règles autorisées, arrêter</span><span class="sxs-lookup"><span data-stu-id="50aac-254">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="50aac-255">Le trafic atteint l’adresse IP interne de hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="50aac-255">Traffic hits internal IP address of hello IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="50aac-256">IIS01 n’est pas à l’écoute sur le port 1433, par conséquent, aucune demande toohello de réponse</span><span class="sxs-lookup"><span data-stu-id="50aac-256">IIS01 isn't listening on port 1433, so no response toohello request</span></span>

## <a name="conclusion"></a><span data-ttu-id="50aac-257">Conclusion</span><span class="sxs-lookup"><span data-stu-id="50aac-257">Conclusion</span></span>
<span data-ttu-id="50aac-258">Cet exemple est un moyen relativement simple et direct d’isoler le sous-réseau principal hello le trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="50aac-258">This example is a relatively simple and straight forward way of isolating hello back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="50aac-259">Vous trouverez d’autres exemples et une vue d’ensemble des frontières de sécurité réseau [ici][HOME].</span><span class="sxs-lookup"><span data-stu-id="50aac-259">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="50aac-260">Références</span><span class="sxs-lookup"><span data-stu-id="50aac-260">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="50aac-261">Script principal et configuration réseau</span><span class="sxs-lookup"><span data-stu-id="50aac-261">Main script and network config</span></span>
<span data-ttu-id="50aac-262">Enregistrez hello Script complet dans un fichier de script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="50aac-262">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="50aac-263">Enregistrer hello configuration réseau dans un fichier nommé « NetworkConf1.xml ».</span><span class="sxs-lookup"><span data-stu-id="50aac-263">Save hello Network Config into a file named “NetworkConf1.xml.”</span></span>
<span data-ttu-id="50aac-264">Modifier les variables de défini par l’utilisateur de hello en tant que script de hello nécessaires et les exécuter.</span><span class="sxs-lookup"><span data-stu-id="50aac-264">Modify hello user-defined variables as needed and run hello script.</span></span>

#### <a name="full-script"></a><span data-ttu-id="50aac-265">Script complet</span><span class="sxs-lookup"><span data-stu-id="50aac-265">Full script</span></span>
<span data-ttu-id="50aac-266">Ce script sera, en fonction des variables définies par l’utilisateur de hello ;</span><span class="sxs-lookup"><span data-stu-id="50aac-266">This script will, based on hello user-defined variables;</span></span>

1. <span data-ttu-id="50aac-267">Se connecter tooan abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="50aac-267">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="50aac-268">Créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="50aac-268">Create a storage account</span></span>
3. <span data-ttu-id="50aac-269">Créer un réseau virtuel et deux sous-réseaux, tel que défini dans le fichier de configuration de réseau de hello</span><span class="sxs-lookup"><span data-stu-id="50aac-269">Create a VNet and two subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="50aac-270">Génération de quatre machines virtuelles Windows Server</span><span class="sxs-lookup"><span data-stu-id="50aac-270">Build four windows server VMs</span></span>
5. <span data-ttu-id="50aac-271">Configurez un groupe de sécurité réseau, notamment :</span><span class="sxs-lookup"><span data-stu-id="50aac-271">Configure NSG including:</span></span>
   * <span data-ttu-id="50aac-272">Création d’un groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="50aac-272">Creating an NSG</span></span>
   * <span data-ttu-id="50aac-273">Ajout de règles à ce dernier</span><span class="sxs-lookup"><span data-stu-id="50aac-273">Populating it with rules</span></span>
   * <span data-ttu-id="50aac-274">Sous-réseaux appropriés de liaison hello NSG toohello</span><span class="sxs-lookup"><span data-stu-id="50aac-274">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="50aac-275">Ce script PowerShell doit être exécuté localement sur un PC ou un serveur connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="50aac-275">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="50aac-276">Lorsque ce script est exécuté, des avertissements ou autres messages d’information peuvent s’afficher dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="50aac-276">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="50aac-277">Seuls les messages d’erreur affichés en rouge sont source de préoccupation.</span><span class="sxs-lookup"><span data-stu-id="50aac-277">Only error messages in red are cause for concern.</span></span>
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
   - One server on hello FrontEnd Subnet
   - Three Servers on hello BackEnd Subnet
   - Network Security Groups tooallow/deny traffic patterns as declared

  Before running script, ensure hello network configuration file is created in
  hello directory referenced by $NetworkConfigFile variable (or update the
  variable tooreflect hello path and file name of hello config file being used).

 .Notes
  Security requirements are different for each use case and can be addressed in a
  myriad of ways. Please be sure that any sensitive data or applications are behind
  hello appropriate layer(s) of protection. This script serves as an example of some
  of hello techniques that can be used, but should not be used for all scenarios. You
  are responsible tooassess your security needs and hello appropriate protections
  needed, and then effectively implement those protections.

  FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
   IIS01      - 10.0.1.5

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

# User-Defined Global Variables
  # These should be changes tooreflect your subscription and services
  # Invalid options will fail in hello validation section

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
    # Note: tooensure proper NSG Rule creation later in this script:
    #       - hello Web Server must be VM 0
    #       - hello AppVM1 Server must be VM 1
    #       - hello DNS server must be VM 3
    #
    #       Otherwise hello NSG rules in hello last section of this
    #       script will need toobe changed toomatch hello modified
    #       VM array numbers ($i) so hello NSG Rule IP addresses
    #       are aligned toohello associated VM IP addresses.

    # VM 0 - hello Web Server
      $VMName += "IIS01"
      $ServiceName += $FrontEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $FESubnet
      $VMIP += "10.0.1.5"

    # VM 1 - hello First Application Server
      $VMName += "AppVM01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.5"

    # VM 2 - hello Second Application Server
      $VMName += "AppVM02"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.6"

    # VM 3 - hello DNS Server
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

  # Update Subscription Pointer tooNew Storage Account
    Write-Host "Updating Subscription Pointer tooNew Storage Account" -ForegroundColor Cyan 
    Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

# Validation
$FatalError = $false

If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
     Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
     $FatalError = $true}

If (Test-AzureName -Service -Name $FrontEndService) { 
    Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

If (Test-AzureName -Service -Name $BackEndService) { 
    Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

If (-Not (Test-Path $NetworkConfigFile)) { 
    Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello network configuration file was found" -ForegroundColor Green
        If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
            Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation variable is correct and hello network config file matches.' -ForegroundColor Yellow
            $FatalError = $true}
        Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

If ($FatalError) {
    Write-Host "A fatal error has occurred, please see hello above messages for more information." -ForegroundColor Red
    Return}
Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

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
    Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

  # Build hello NSG
    Write-Host "Building hello NSG" -ForegroundColor Cyan
    New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

  # Add NSG Rules
    Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[3] -DestinationPortRange '53' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
        -SourceAddressPrefix Internet -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[0]) too$($VMName[1])" -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[0] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[1] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
        -Protocol *

    # Assign hello NSG toohello Subnets
        Write-Host "Binding hello NSG tooboth subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

# Optional Post-script Manual Configuration
  # Install Test Web App (Run Post-Build Script on hello IIS Server)
  # Install Backend resource (Run Post-Build Script on hello AppVM01)
  Write-Host
  Write-Host "Build Complete!" -ForegroundColor Green
  Write-Host
  Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
  Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
  Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
  Write-Host
```

#### <a name="network-config-file"></a><span data-ttu-id="50aac-278">Fichier de configuration réseau</span><span class="sxs-lookup"><span data-stu-id="50aac-278">Network config file</span></span>
<span data-ttu-id="50aac-279">Enregistrez ce fichier xml avec l’emplacement mis à jour et du fichier toohello $NetworkConfigFile variable hello lien toothis dans hello précédant le script.</span><span class="sxs-lookup"><span data-stu-id="50aac-279">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello preceding script.</span></span>

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

#### <a name="sample-application-scripts"></a><span data-ttu-id="50aac-280">Exemples de scripts d’application</span><span class="sxs-lookup"><span data-stu-id="50aac-280">Sample application scripts</span></span>
<span data-ttu-id="50aac-281">Si vous le souhaitez tooinstall un exemple d’application pour ce, ainsi que d’autres exemples de réseau de périmètre, un a été fourni au lien de hello : [Application exemple de Script][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="50aac-281">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="50aac-282">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="50aac-282">Next steps</span></span>
* <span data-ttu-id="50aac-283">Mise à jour et enregistrement du fichier XML</span><span class="sxs-lookup"><span data-stu-id="50aac-283">Update and save XML file</span></span>
* <span data-ttu-id="50aac-284">Exécuter hello PowerShell script toobuild hello environnement</span><span class="sxs-lookup"><span data-stu-id="50aac-284">Run hello PowerShell script toobuild hello environment</span></span>
* <span data-ttu-id="50aac-285">Installer l’application d’exemple hello</span><span class="sxs-lookup"><span data-stu-id="50aac-285">Install hello sample application</span></span>
* <span data-ttu-id="50aac-286">Tester différents flux de trafic via cette zone DMZ</span><span class="sxs-lookup"><span data-stu-id="50aac-286">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "Zone DMZ avec groupe de sécurité réseau (NSG)"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

