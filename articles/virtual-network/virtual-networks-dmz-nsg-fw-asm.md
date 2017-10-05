---
title: "Exemple DMZ : créer une zone démilitarisée (DMZ) pour protéger les applications avec un pare-feu et des groupes de sécurité réseau | Microsoft Docs"
description: "Créer une zone DMZ avec un pare-feu et des groupes de sécurité réseau (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: c78491c7-54ac-4469-851c-b35bfed0f528
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: cc0e8a3fa749eb2e6f65ef92c2d3cb404cfc8bc0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="example-2--build-a-dmz-to-protect-applications-with-a-firewall-and-nsgs"></a><span data-ttu-id="4fdea-103">Exemple 2 : Créer une zone démilitarisée (DMZ) pour protéger les applications avec un pare-feu et des groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="4fdea-103">Example 2 – Build a DMZ to protect applications with a Firewall and NSGs</span></span>
<span data-ttu-id="4fdea-104">[Revenir à la page Meilleures pratiques relatives aux frontières de sécurité][HOME]</span><span class="sxs-lookup"><span data-stu-id="4fdea-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="4fdea-105">Cet exemple crée une zone DMZ avec un pare-feu, quatre serveurs Windows et des groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="4fdea-105">This example will create a DMZ with a firewall, four windows servers, and Network Security Groups.</span></span> <span data-ttu-id="4fdea-106">Vous y découvrirez également comment chacune des commandes concernées fournit une meilleure connaissance de chaque opération.</span><span class="sxs-lookup"><span data-stu-id="4fdea-106">It will also walk through each of the relevant commands to provide a deeper understanding of each step.</span></span> <span data-ttu-id="4fdea-107">Il comporte également une section Scénario de trafic (Traffic Scenario) qui explique en détail et étape par étape l’évolution du trafic à travers les couches de défense dans la zone DMZ.</span><span class="sxs-lookup"><span data-stu-id="4fdea-107">There is also a Traffic Scenario section to provide an in-depth step-by-step how traffic proceeds through the layers of defense in the DMZ.</span></span> <span data-ttu-id="4fdea-108">Enfin, dans la section de référence se trouve l’intégralité du code et des instructions permettant d’élaborer l’environnement destiné à tester et à expérimenter différents scénarios.</span><span class="sxs-lookup"><span data-stu-id="4fdea-108">Finally, in the references section is the complete code and instruction to build this environment to test and experiment with various scenarios.</span></span> 

<span data-ttu-id="4fdea-109">![Zone DMZ entrante avec NVA et NSG][1]</span><span class="sxs-lookup"><span data-stu-id="4fdea-109">![Inbound DMZ with NVA and NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="4fdea-110">Description de l’environnement</span><span class="sxs-lookup"><span data-stu-id="4fdea-110">Environment Description</span></span>
<span data-ttu-id="4fdea-111">Dans cet exemple, il existe un abonnement qui contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4fdea-111">In this example there is a subscription that contains the following:</span></span>

* <span data-ttu-id="4fdea-112">deux services cloud : « FrontEnd001 », « BackEnd001 »,</span><span class="sxs-lookup"><span data-stu-id="4fdea-112">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="4fdea-113">Un réseau virtuel « CorpNetwork » avec deux sous-réseaux : « FrontEnd » et « BackEnd »</span><span class="sxs-lookup"><span data-stu-id="4fdea-113">A Virtual Network “CorpNetwork”, with two subnets: “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="4fdea-114">Un groupe de sécurité réseau unique qui est appliqué aux deux sous-réseaux</span><span class="sxs-lookup"><span data-stu-id="4fdea-114">A single Network Security Group that is applied to both subnets</span></span>
* <span data-ttu-id="4fdea-115">Une appliance virtuelle du réseau, dans cet exemple un pare-feu Barracuda NextGen Firewall, connectée au sous-réseau Frontend</span><span class="sxs-lookup"><span data-stu-id="4fdea-115">A network virtual appliance, in this example a Barracuda NextGen Firewall, connected to the Frontend subnet</span></span>
* <span data-ttu-id="4fdea-116">un serveur Windows Server représentant un serveur web d’application (« IIS01 »),</span><span class="sxs-lookup"><span data-stu-id="4fdea-116">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="4fdea-117">Deux serveurs Windows Server qui représentent les serveurs principaux d’applications (« AppVM01 », « AppVM02 »)</span><span class="sxs-lookup"><span data-stu-id="4fdea-117">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="4fdea-118">Un serveur Windows Server qui représente un serveur DNS (« DNS01 »)</span><span class="sxs-lookup"><span data-stu-id="4fdea-118">A Windows server that represents a DNS server (“DNS01”)</span></span>

> [!NOTE]
> <span data-ttu-id="4fdea-119">Bien que cet exemple utilise un pare-feu Barracuda NextGen Firewall, différentes appliances virtuelles du réseau peuvent être utilisées pour cet exemple.</span><span class="sxs-lookup"><span data-stu-id="4fdea-119">Although this example uses a Barracuda NextGen Firewall, many of the different Network Virtual Appliances could be used for this example.</span></span>
> 
> 

<span data-ttu-id="4fdea-120">Dans la section Références ci-dessous figure un script PowerShell qui générera une grande partie l’environnement décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="4fdea-120">In the references section below there is a PowerShell script that will build most of the environment described above.</span></span> <span data-ttu-id="4fdea-121">La création de machines virtuelles et de réseaux virtuels, bien qu’effectuée par l’exemple de script, ne figure pas en détail dans ce document.</span><span class="sxs-lookup"><span data-stu-id="4fdea-121">Building the VMs and Virtual Networks, although are done by the example script, are not described in detail in this document.</span></span>

<span data-ttu-id="4fdea-122">Pour créer l’environnement :</span><span class="sxs-lookup"><span data-stu-id="4fdea-122">To build the environment:</span></span>

1. <span data-ttu-id="4fdea-123">Enregistrer le fichier XML de configuration réseau contenu dans la section Références (mis à jour avec les noms, l’emplacement et les adresses IP correspondant à un scénario donné)</span><span class="sxs-lookup"><span data-stu-id="4fdea-123">Save the network config xml file included in the references section (updated with names, location, and IP addresses to match the given scenario)</span></span>
2. <span data-ttu-id="4fdea-124">Mettre à jour les variables de l’utilisateur dans le script pour qu’elles correspondent à l’environnement dans lequel le script est exécuté (abonnements, noms de service, etc.)</span><span class="sxs-lookup"><span data-stu-id="4fdea-124">Update the user variables in the script to match the environment the script is to be run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="4fdea-125">Exécuter le script dans PowerShell</span><span class="sxs-lookup"><span data-stu-id="4fdea-125">Execute the script in PowerShell</span></span>

<span data-ttu-id="4fdea-126">**Remarque**: la région indiquée dans le script PowerShell doit correspondre à la région indiquée dans le fichier xml de configuration réseau.</span><span class="sxs-lookup"><span data-stu-id="4fdea-126">**Note**: The region signified in the PowerShell script must match the region signified in the network configuration xml file.</span></span>

<span data-ttu-id="4fdea-127">Une fois que le script s’exécute correctement, les opérations de post-script qui suivent doivent être exécutées :</span><span class="sxs-lookup"><span data-stu-id="4fdea-127">Once the script runs successfully the following post-script steps may be taken:</span></span>

1. <span data-ttu-id="4fdea-128">Configurer les règles de pare-feu. Ce sujet est traité dans la section ci-dessous, intitulée Règles de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="4fdea-128">Set up the firewall rules, this is covered in the section below titled: Firewall Rules.</span></span>
2. <span data-ttu-id="4fdea-129">Dans la section Références, il existe deux scripts pour configurer le serveur web et le serveur d’application avec une application web simple permettant le test avec cette configuration DMZ.</span><span class="sxs-lookup"><span data-stu-id="4fdea-129">Optionally in the references section are two scripts to set up the web server and app server with a simple web application to allow testing with this DMZ configuration.</span></span>

<span data-ttu-id="4fdea-130">La section suivante explique la plupart des instructions de scripts relatives aux groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="4fdea-130">The next section explains most of the scripts statements relative to Network Security Groups.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="4fdea-131">Groupes de sécurité réseau (NSG)</span><span class="sxs-lookup"><span data-stu-id="4fdea-131">Network Security Groups (NSG)</span></span>
<span data-ttu-id="4fdea-132">Dans cet exemple, un groupe NSG est créé, puis chargé avec six règles.</span><span class="sxs-lookup"><span data-stu-id="4fdea-132">For this example, a NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="4fdea-133">En règle générale, vous devez d’abord créer les règles d’« autorisation » spécifiques, puis les règles de « refus » plus générales.</span><span class="sxs-lookup"><span data-stu-id="4fdea-133">Generally speaking, you should create your specific “Allow” rules first and then the more generic “Deny” rules last.</span></span> <span data-ttu-id="4fdea-134">La priorité établit les règles évaluées en premier.</span><span class="sxs-lookup"><span data-stu-id="4fdea-134">The assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="4fdea-135">Une fois qu’il a été déterminé que le trafic répond à une règle spécifique, aucune autre règle n’est évaluée.</span><span class="sxs-lookup"><span data-stu-id="4fdea-135">Once traffic is found to apply to a specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="4fdea-136">Les règles du groupe de sécurité réseau peuvent s’appliquer dans le sens entrant ou sortant (du point de vue du sous-réseau).</span><span class="sxs-lookup"><span data-stu-id="4fdea-136">NSG rules can apply in either in the inbound or outbound direction (from the perspective of the subnet).</span></span>
> 
> 

<span data-ttu-id="4fdea-137">Les règles qui suivent sont générées de façon déclarative pour le trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="4fdea-137">Declaratively, the following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="4fdea-138">Le trafic DNS interne (port 53) est autorisé</span><span class="sxs-lookup"><span data-stu-id="4fdea-138">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="4fdea-139">Le trafic RDP (port 3389) à partir d’Internet vers n’importe quelle machine virtuelle est autorisé</span><span class="sxs-lookup"><span data-stu-id="4fdea-139">RDP traffic (port 3389) from the Internet to any VM is allowed</span></span>
3. <span data-ttu-id="4fdea-140">Le trafic HTTP (port 80) à partir d’Internet vers l’appliance virtuelle réseau (pare-feu) est autorisé</span><span class="sxs-lookup"><span data-stu-id="4fdea-140">HTTP traffic (port 80) from the Internet to the NVA (firewall) is allowed</span></span>
4. <span data-ttu-id="4fdea-141">Tout le trafic (tous les ports) IIS01 vers AppVM1 est autorisé</span><span class="sxs-lookup"><span data-stu-id="4fdea-141">Any traffic (all ports) from IIS01 to AppVM1 is allowed</span></span>
5. <span data-ttu-id="4fdea-142">Tout trafic (tous les ports) en provenance d’Internet vers l’ensemble du réseau virtuel (les deux sous-réseaux) est refusé.</span><span class="sxs-lookup"><span data-stu-id="4fdea-142">Any traffic (all ports) from the Internet to the entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="4fdea-143">Tout trafic (tous les ports) en provenance du sous-réseau frontal vers le sous-réseau principal est refusé.</span><span class="sxs-lookup"><span data-stu-id="4fdea-143">Any traffic (all ports) from the Frontend subnet to the Backend subnet is Denied</span></span>

<span data-ttu-id="4fdea-144">Lorsque ces règles sont associées à chacun des sous-réseaux, si une requête HTTP entrante en provenance d’HTTP arrive d’Internet à destination du serveur web, les 3 règles (autorisation) et les 5 règles (refus) s’appliquent. Cependant, comme la règle 3 a une priorité plus élevée, elle seule s’applique, et la règle 5 n’entre pas en jeu.</span><span class="sxs-lookup"><span data-stu-id="4fdea-144">With these rules bound to each subnet, if a HTTP request was inbound from the Internet to the web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="4fdea-145">La requête HTTP est donc autorisée à accéder au pare-feu.</span><span class="sxs-lookup"><span data-stu-id="4fdea-145">Thus the HTTP request would be allowed to the firewall.</span></span> <span data-ttu-id="4fdea-146">Si le même trafic tentait d’atteindre le serveur DNS01, la règle 5 (Refus) serait la première à s’appliquer et le trafic ne serait pas autorisé à accéder au serveur.</span><span class="sxs-lookup"><span data-stu-id="4fdea-146">If that same traffic was trying to reach the DNS01 server, rule 5 (Deny) would be the first to apply and the traffic would not be allowed to pass to the server.</span></span> <span data-ttu-id="4fdea-147">La règle 6 (Refus) bloque la communication du sous-réseau frontal vers le sous-réseau principal (excepté le trafic autorisé dans les règles 1 et 4), ce qui protège le réseau principal en cas d’attaque d’une personne mal intentionnée sur l’application web sur le serveur frontal. Cette personne aurait alors un accès limité au réseau principal « protégé » (uniquement les ressources exposées sur le serveur AppVM01).</span><span class="sxs-lookup"><span data-stu-id="4fdea-147">Rule 6 (Deny) blocks the Frontend subnet from talking to the Backend subnet (except for allowed traffic in rules 1 and 4), this protects the Backend network in case an attacker compromises the web application on the Frontend, the attacker would have limited access to the Backend “protected” network (only to resources exposed on the AppVM01 server).</span></span>

<span data-ttu-id="4fdea-148">Il existe une règle par défaut qui autorise le trafic sortant vers Internet.</span><span class="sxs-lookup"><span data-stu-id="4fdea-148">There is a default outbound rule that allows traffic out to the internet.</span></span> <span data-ttu-id="4fdea-149">Pour cet exemple, nous allons autoriser le trafic sortant sans modifier les règles de trafic sortant.</span><span class="sxs-lookup"><span data-stu-id="4fdea-149">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="4fdea-150">Pour verrouiller le trafic dans les deux directions, le routage défini par l’utilisateur est requis. Cette opération est expliquée dans un autre exemple qui figure dans le [document de frontière de sécurité principal][HOME].</span><span class="sxs-lookup"><span data-stu-id="4fdea-150">To lock down traffic in both directions, User Defined Routing is required, this is explored in a different example that can found in the [main security boundary document][HOME].</span></span>

<span data-ttu-id="4fdea-151">Les règles NSG abordées ci-dessus sont très similaires aux règles NSG décrites dans [Exemple 1 : créer une zone DMZ simple à l’aide de groupes de sécurité réseau][Example1].</span><span class="sxs-lookup"><span data-stu-id="4fdea-151">The above discussed NSG rules are very similar to the NSG rules in [Example 1 - Build a Simple DMZ with NSGs][Example1].</span></span> <span data-ttu-id="4fdea-152">Veuillez consulter la description NSG dans ce document pour obtenir une description détaillée de chaque règle NSG et de ses attributs.</span><span class="sxs-lookup"><span data-stu-id="4fdea-152">Please review the NSG Description in that document for a detailed look at each NSG rule and it's attributes.</span></span>

## <a name="firewall-rules"></a><span data-ttu-id="4fdea-153">Règles de pare-feu</span><span class="sxs-lookup"><span data-stu-id="4fdea-153">Firewall Rules</span></span>
<span data-ttu-id="4fdea-154">Un client de gestion devra être installé sur un ordinateur pour gérer le pare-feu et créer les configurations nécessaires.</span><span class="sxs-lookup"><span data-stu-id="4fdea-154">A management client will need to be installed on a PC to manage the firewall and create the configurations needed.</span></span> <span data-ttu-id="4fdea-155">Consultez la documentation du fournisseur de votre pare-feu (ou autre NVA) sur la façon de gérer l’appareil.</span><span class="sxs-lookup"><span data-stu-id="4fdea-155">See the documentation from your firewall (or other NVA) vendor on how to manage the device.</span></span> <span data-ttu-id="4fdea-156">Le reste de cette section décrit la configuration du pare-feu lui-même par le biais du client de gestion des fournisseurs (et non par le portail Azure ou PowerShell).</span><span class="sxs-lookup"><span data-stu-id="4fdea-156">The remainder of this section will describe the configuration of the firewall itself, through the vendors management client (i.e. not the Azure portal or PowerShell).</span></span>

<span data-ttu-id="4fdea-157">Les instructions de téléchargement client et de connexion à Barracuda utilisées dans cet exemple se trouvent ici : [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="4fdea-157">Instructions for client download and connecting to the Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="4fdea-158">Sur le pare-feu, vous devrez créer des règles de transfert.</span><span class="sxs-lookup"><span data-stu-id="4fdea-158">On the firewall, forwarding rules will need to be created.</span></span> <span data-ttu-id="4fdea-159">Étant donné que cet exemple achemine uniquement le trafic Internet entrant vers le pare-feu, puis vers le serveur web, seule une règle NAT de transfert est requise.</span><span class="sxs-lookup"><span data-stu-id="4fdea-159">Since this example only routes internet traffic in-bound to the firewall and then to the web server, only one forwarding NAT rule is needed.</span></span> <span data-ttu-id="4fdea-160">Sur le pare-feu Barracuda NextGen Firewall utilisé dans cet exemple, la règle serait une règle NAT de destination (« Dst NAT ») pour autoriser ce trafic.</span><span class="sxs-lookup"><span data-stu-id="4fdea-160">On the Barracuda NextGen Firewall used in this example the rule would be a Destination NAT rule (“Dst NAT”) to pass this traffic.</span></span>

<span data-ttu-id="4fdea-161">Pour créer la règle suivante (ou vérifier les règles par défaut existantes), sur le tableau de bord du client administrateur de Barracuda NG, accédez à l’onglet Configuration. Dans la section Configuration opérationnelle, cliquez sur Ensemble de règles.</span><span class="sxs-lookup"><span data-stu-id="4fdea-161">To create the following rule (or verify existing default rules), starting from the Barracuda NG Admin client dashboard, navigate to the configuration tab, in the Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="4fdea-162">Une grille nommée « Règles principales » affiche les règles actives et désactivées sur le pare-feu.</span><span class="sxs-lookup"><span data-stu-id="4fdea-162">A grid called, “Main Rules” will show the existing active and deactivated rules on the firewall.</span></span> <span data-ttu-id="4fdea-163">Dans le coin supérieur droit de cette grille se trouve un petit bouton « + » vert. Cliquez dessus pour créer une nouvelle règle (Remarque : votre pare-feu peut être « verrouillé » contre les modifications. Si vous voyez un bouton marqué « Verrouiller » et que vous ne pouvez pas créer ou modifier les règles, cliquez dessus pour « déverrouiller » l’ensemble de règles et autoriser la modification).</span><span class="sxs-lookup"><span data-stu-id="4fdea-163">In the upper right corner of this grid is a small, green “+” button, click this to create a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable to create or edit rules, click this button to “unlock” the ruleset and allow editing).</span></span> <span data-ttu-id="4fdea-164">Si vous souhaitez modifier une règle existante, sélectionnez cette règle, cliquez avec le bouton droit et sélectionnez Modifier la règle.</span><span class="sxs-lookup"><span data-stu-id="4fdea-164">If you wish to edit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="4fdea-165">Créez une nouvelle règle et indiquez un nom, par exemple « WebTraffic ».</span><span class="sxs-lookup"><span data-stu-id="4fdea-165">Create a new rule and provide a name, such as "WebTraffic".</span></span> 

<span data-ttu-id="4fdea-166">L'icône de la règle NAT de destination se présente ainsi : ![Icône NAT de destination][2]</span><span class="sxs-lookup"><span data-stu-id="4fdea-166">The Destination NAT rule icon looks like this: ![Destination NAT Icon][2]</span></span>

<span data-ttu-id="4fdea-167">La règle proprement dite se présente ainsi :</span><span class="sxs-lookup"><span data-stu-id="4fdea-167">The rule itself would look something like this:</span></span>

<span data-ttu-id="4fdea-168">![Règle de pare-feu][3]</span><span class="sxs-lookup"><span data-stu-id="4fdea-168">![Firewall Rule][3]</span></span>

<span data-ttu-id="4fdea-169">Ici, toute adresse entrante qui atteint le pare-feu en essayant d'atteindre HTTP (port 80 ou 443 pour HTTPS) est envoyée à l'interface « DHCP1 Local IP » du pare-feu et redirigée vers le serveur web avec l'adresse IP 10.0.1.5.</span><span class="sxs-lookup"><span data-stu-id="4fdea-169">Here any inbound address that hits the Firewall trying to reach HTTP (port 80 or 443 for HTTPS) will be sent out the Firewall’s “DHCP1 Local IP” interface and redirected to the Web Server with the IP Address of 10.0.1.5.</span></span> <span data-ttu-id="4fdea-170">Dans la mesure où le trafic entrant utilise le port 80 et le trafic sortant à destination du serveur web utilise le port 80, aucun changement de port n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4fdea-170">Since the traffic is coming in on port 80 and going to the web server on port 80 no port change was needed.</span></span> <span data-ttu-id="4fdea-171">Toutefois, la liste des cibles aurait pu être 10.0.1.5:8080 si notre serveur Web avait été à l'écoute sur le port 8080 et avait par conséquent traduit le port 80 entrant sur le pare-feu en port 8080 entrant sur le serveur web.</span><span class="sxs-lookup"><span data-stu-id="4fdea-171">However, the Target List could have been 10.0.1.5:8080 if our Web Server listened on port 8080 thus translating the inbound port 80 on the firewall to inbound port 8080 on the web server.</span></span>

<span data-ttu-id="4fdea-172">Une méthode de connexion doit également être indiquée. Pour la règle de destination à partir d'Internet, « SNAT dynamique » est la plus appropriée.</span><span class="sxs-lookup"><span data-stu-id="4fdea-172">A Connection Method should also be signified, for the Destination Rule from the Internet, "Dynamic SNAT" is most appropriate.</span></span> 

<span data-ttu-id="4fdea-173">Bien qu'une seule règle soit créée, il est important de définir correctement sa priorité.</span><span class="sxs-lookup"><span data-stu-id="4fdea-173">Although only one rule has been created it's important that its priority is set correctly.</span></span> <span data-ttu-id="4fdea-174">Si, dans la grille de toutes les règles du pare-feu, cette nouvelle règle se trouve en bas (sous la règle « BLOCKALL »), elle n’entrera jamais en jeu.</span><span class="sxs-lookup"><span data-stu-id="4fdea-174">If in the grid of all rules on the firewall this new rule is on the bottom (below the "BLOCKALL" rule) it will never come into play.</span></span> <span data-ttu-id="4fdea-175">Assurez-vous que la règle nouvellement créée pour le trafic web soit au-dessus de la règle BLOCKALL.</span><span class="sxs-lookup"><span data-stu-id="4fdea-175">Ensure the newly created rule for web traffic is above the BLOCKALL rule.</span></span>

<span data-ttu-id="4fdea-176">Une fois la règle créée, elle doit être transférée vers le pare-feu et activée. Si cette opération n’est pas effectuée, la modification de règle ne prendra pas effet.</span><span class="sxs-lookup"><span data-stu-id="4fdea-176">Once the rule is created, it must be pushed to the firewall and then activated, if this is not done the rule change will not take effect.</span></span> <span data-ttu-id="4fdea-177">Le processus de push et d’activation est décrit dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="4fdea-177">The push and activation process is described in the next section.</span></span>

## <a name="rule-activation"></a><span data-ttu-id="4fdea-178">Activation d’une règle</span><span class="sxs-lookup"><span data-stu-id="4fdea-178">Rule Activation</span></span>
<span data-ttu-id="4fdea-179">Une fois l'ensemble de règles modifié par l’ajout de cette règle, l’ensemble de règles doit être chargé sur le pare-feu et activé.</span><span class="sxs-lookup"><span data-stu-id="4fdea-179">With the ruleset modified to add this rule, the ruleset must be uploaded to the firewall and activated.</span></span>

<span data-ttu-id="4fdea-180">![Activation de règle de pare-feu][4]</span><span class="sxs-lookup"><span data-stu-id="4fdea-180">![Firewall Rule Activation][4]</span></span>

<span data-ttu-id="4fdea-181">Dans le coin supérieur droit du client de gestion se trouve un ensemble de boutons.</span><span class="sxs-lookup"><span data-stu-id="4fdea-181">In the upper right hand corner of the management client are a cluster of buttons.</span></span> <span data-ttu-id="4fdea-182">Cliquez sur le bouton « Envoyer les modifications » pour envoyer les règles modifiées au pare-feu, puis cliquez sur le bouton « Activer ».</span><span class="sxs-lookup"><span data-stu-id="4fdea-182">Click the “Send Changes” button to send the modified rules to the firewall, then click the “Activate” button.</span></span>

<span data-ttu-id="4fdea-183">Avec l’activation de l’ensemble de règles de pare-feu, la création de l’environnement de cet exemple est terminée.</span><span class="sxs-lookup"><span data-stu-id="4fdea-183">With the activation of the firewall ruleset this example environment build is complete.</span></span> <span data-ttu-id="4fdea-184">Les scripts post-build de la section Références peuvent si nécessaire être exécutés pour ajouter une application à cet environnement afin de tester les scénarios de trafic ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4fdea-184">Optionally, the post build scripts in the References section can be run to add an application to this environment to test the below traffic scenarios.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4fdea-185">Il est essentiel de comprendre que vous n’atteindrez pas le serveur web directement.</span><span class="sxs-lookup"><span data-stu-id="4fdea-185">It is critical to realize that you will not hit the web server directly.</span></span> <span data-ttu-id="4fdea-186">Lorsqu'un navigateur demande une page HTTP à FrontEnd001.CloudApp.Net, le point de terminaison HTTP (port 80) transmet ce trafic au pare-feu et non au serveur web.</span><span class="sxs-lookup"><span data-stu-id="4fdea-186">When a browser requests an HTTP page from FrontEnd001.CloudApp.Net, the HTTP endpoint (port 80) passes this traffic to the firewall not the web server.</span></span> <span data-ttu-id="4fdea-187">Ensuite, le pare-feu, en fonction de la règle créée ci-dessus, exécute la traduction NAT de cette demande sur le serveur Web.</span><span class="sxs-lookup"><span data-stu-id="4fdea-187">The firewall then, according to the rule created above, NATs that request to the Web Server.</span></span>
> 
> 

## <a name="traffic-scenarios"></a><span data-ttu-id="4fdea-188">Scénarios de trafic</span><span class="sxs-lookup"><span data-stu-id="4fdea-188">Traffic Scenarios</span></span>
#### <a name="allowed-web-to-web-server-through-firewall"></a><span data-ttu-id="4fdea-189">(Autorisé) web vers serveur web via le pare-feu</span><span class="sxs-lookup"><span data-stu-id="4fdea-189">(Allowed) Web to Web Server through Firewall</span></span>
1. <span data-ttu-id="4fdea-190">Un utilisateur Internet demande une page HTTP en provenance de FrontEnd001.CloudApp.Net (service cloud face à Internet)</span><span class="sxs-lookup"><span data-stu-id="4fdea-190">Internet user requests HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="4fdea-191">Le service cloud transfère le trafic via un point de terminaison ouvert sur le port 80 vers l’interface locale de pare-feu sur 10.0.1.4:80 (serveur web)</span><span class="sxs-lookup"><span data-stu-id="4fdea-191">Cloud service passes traffic through open endpoint on port 80 to firewall local interface on 10.0.1.4:80</span></span>
3. <span data-ttu-id="4fdea-192">Le sous-réseau du serveur frontal commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="4fdea-192">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="4fdea-193">La règle NSG 1 (DNS) ne s’applique pas, passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="4fdea-193">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="4fdea-194">La règle NSG 2 (RDP) ne s’applique pas, passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="4fdea-194">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="4fdea-195">La règle NSG 3 (Internet vers pare-feu) s’applique, le trafic est autorisé, arrêter le traitement</span><span class="sxs-lookup"><span data-stu-id="4fdea-195">NSG Rule 3 (Internet to Firewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="4fdea-196">Le trafic parvient à l’adresse IP du pare-feu (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="4fdea-196">Traffic hits internal IP address of the firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="4fdea-197">La règle de transfert du pare-feu constate que le trafic utilise le port 80, elle redirige vers le serveur web IIS01</span><span class="sxs-lookup"><span data-stu-id="4fdea-197">Firewall forwarding rule see this is port 80 traffic, redirects it to the web server IIS01</span></span>
6. <span data-ttu-id="4fdea-198">IIS01 écoute le trafic web, reçoit cette requête et commence à traiter la demande</span><span class="sxs-lookup"><span data-stu-id="4fdea-198">IIS01 is listening for web traffic, receives this request and starts processing the request</span></span>
7. <span data-ttu-id="4fdea-199">IIS01 demande des informations au serveur SQL Server sur AppVM01</span><span class="sxs-lookup"><span data-stu-id="4fdea-199">IIS01 asks the SQL Server on AppVM01 for information</span></span>
8. <span data-ttu-id="4fdea-200">Aucune règle sortante sur le sous-réseau du serveur frontal, le trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="4fdea-200">No outbound rules on Frontend subnet, traffic is allowed</span></span>
9. <span data-ttu-id="4fdea-201">Le sous-réseau du serveur principal commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="4fdea-201">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="4fdea-202">La règle NSG 1 (DNS) ne s’applique pas, passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="4fdea-202">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="4fdea-203">La règle NSG 2 (RDP) ne s’applique pas, passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="4fdea-203">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="4fdea-204">La règle NSG 3 (Internet vers le pare-feu) ne s’applique pas, passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="4fdea-204">NSG Rule 3 (Internet to Firewall) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="4fdea-205">La règle NSG 4 (IIS01 vers AppVM01) s’applique, le trafic est autorisé, arrêter le traitement des règles</span><span class="sxs-lookup"><span data-stu-id="4fdea-205">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
10. <span data-ttu-id="4fdea-206">AppVM01 reçoit la requête SQL et répond</span><span class="sxs-lookup"><span data-stu-id="4fdea-206">AppVM01 receives the SQL Query and responds</span></span>
11. <span data-ttu-id="4fdea-207">Comme il n’existe aucune règle sur le trafic sortant sur le sous-réseau du serveur principal, la réponse est autorisée.</span><span class="sxs-lookup"><span data-stu-id="4fdea-207">Since there are no outbound rules on the Backend subnet the response is allowed</span></span>
12. <span data-ttu-id="4fdea-208">Le sous-réseau du serveur frontal commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="4fdea-208">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="4fdea-209">Aucune règle NSG ne s’applique au trafic entrant en provenance du sous-réseau du serveur principal vers le sous-réseau du serveur frontal, par conséquent aucune des règles NSG ne s’applique</span><span class="sxs-lookup"><span data-stu-id="4fdea-209">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="4fdea-210">La règle du système par défaut autorisant le trafic entre sous-réseaux autorise le trafic, le trafic est donc autorisé.</span><span class="sxs-lookup"><span data-stu-id="4fdea-210">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
13. <span data-ttu-id="4fdea-211">Le serveur IIS reçoit la réponse SQL, complète la réponse HTTP et l’envoie au demandeur</span><span class="sxs-lookup"><span data-stu-id="4fdea-211">The IIS server receives the SQL response and completes the HTTP response and sends to the requestor</span></span>
14. <span data-ttu-id="4fdea-212">Dans la mesure où il s'agit d'une session NAT provenant du pare-feu, la destination de la réponse est (initialement) le pare-feu</span><span class="sxs-lookup"><span data-stu-id="4fdea-212">Since this is a NAT session from the firewall, the response destination (initially) is for the Firewall</span></span>
15. <span data-ttu-id="4fdea-213">Le pare-feu reçoit la réponse du serveur Web et le transfère à l'utilisateur Internet</span><span class="sxs-lookup"><span data-stu-id="4fdea-213">The firewall receives the response from the Web Server and forwards back to the Internet User</span></span>
16. <span data-ttu-id="4fdea-214">Comme il n’existe aucune règle sortante sur le sous-réseau du serveur frontal, la réponse est autorisée, et l’utilisateur Internet reçoit la page web demandée.</span><span class="sxs-lookup"><span data-stu-id="4fdea-214">Since there are no outbound rules on the Frontend subnet the response is allowed, and the Internet User receives the web page requested.</span></span>

#### <a name="allowed-rdp-to-backend"></a><span data-ttu-id="4fdea-215">(Autorisé) RDP vers le serveur principal</span><span class="sxs-lookup"><span data-stu-id="4fdea-215">(Allowed) RDP to Backend</span></span>
1. <span data-ttu-id="4fdea-216">L’administrateur du serveur sur Internet demande une session RDP AppVM01 sur BackEnd001.CloudApp.Net:xxxxx, où xxxxx est le numéro de port attribué de façon aléatoire au trafic RDP vers AppVM01 (le port attribué se trouve sur le portail Azure ou via PowerShell)</span><span class="sxs-lookup"><span data-stu-id="4fdea-216">Server Admin on internet requests RDP session to AppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is the randomly assigned port number for RDP to AppVM01 (the assigned port can be found on the Azure Portal or via PowerShell)</span></span>
2. <span data-ttu-id="4fdea-217">Étant donné que le pare-feu n'écoute que sur l'adresse FrontEnd001.CloudApp.Net, il n'est pas impliqué dans ce flux de trafic</span><span class="sxs-lookup"><span data-stu-id="4fdea-217">Since the Firewall is only listening on the FrontEnd001.CloudApp.Net address, it is not involved with this traffic flow</span></span>
3. <span data-ttu-id="4fdea-218">Le sous-réseau du serveur principal entame le traitement du réseau entrant :</span><span class="sxs-lookup"><span data-stu-id="4fdea-218">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="4fdea-219">La règle NSG 1 (DNS) ne s’applique pas, passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="4fdea-219">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="4fdea-220">La règle NSG 2 (RDP) s’applique, le trafic est autorisé, arrêter le traitement des règles</span><span class="sxs-lookup"><span data-stu-id="4fdea-220">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="4fdea-221">En l’absence de réseau sortant, les règles par défaut s’appliquent et le retour de trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="4fdea-221">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="4fdea-222">La session RDP est activée</span><span class="sxs-lookup"><span data-stu-id="4fdea-222">RDP session is enabled</span></span>
6. <span data-ttu-id="4fdea-223">AppVM01 demande le mot de passe utilisateur</span><span class="sxs-lookup"><span data-stu-id="4fdea-223">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="4fdea-224">(Autorisé) recherche DNS du serveur web sur le serveur DNS</span><span class="sxs-lookup"><span data-stu-id="4fdea-224">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="4fdea-225">Le serveur Web Server IIS01 a besoin d’un flux de données sur www.data.gov, mais doit résoudre l’adresse.</span><span class="sxs-lookup"><span data-stu-id="4fdea-225">Web Server, IIS01, needs a data feed at www.data.gov, but needs to resolve the address.</span></span>
2. <span data-ttu-id="4fdea-226">La configuration réseau du réseau virtuel définit DNS01 (10.0.2.4 sur le sous-réseau du serveur principal) comme serveur DNS principal, IIS01 envoie la requête DNS à DNS01</span><span class="sxs-lookup"><span data-stu-id="4fdea-226">The network configuration for the VNet lists DNS01 (10.0.2.4 on the Backend subnet) as the primary DNS server, IIS01 sends the DNS request to DNS01</span></span>
3. <span data-ttu-id="4fdea-227">Aucune règle sortante sur le sous-réseau du serveur frontal, le trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="4fdea-227">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="4fdea-228">Le sous-réseau du serveur principal entame le traitement du réseau entrant :</span><span class="sxs-lookup"><span data-stu-id="4fdea-228">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="4fdea-229">La règle NSG 1 (DNS) s’applique, le trafic est autorisé, arrêter le traitement des règles</span><span class="sxs-lookup"><span data-stu-id="4fdea-229">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="4fdea-230">Le serveur DNS reçoit la demande</span><span class="sxs-lookup"><span data-stu-id="4fdea-230">DNS server receives the request</span></span>
6. <span data-ttu-id="4fdea-231">Le serveur DNS n’a pas d’adresse en cache et demande à un serveur DNS racine sur Internet.</span><span class="sxs-lookup"><span data-stu-id="4fdea-231">DNS server doesn’t have the address cached and asks a root DNS server on the internet</span></span>
7. <span data-ttu-id="4fdea-232">Aucune règle sortante sur le sous-réseau du serveur principal, le trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="4fdea-232">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="4fdea-233">Un serveur Internet DNS répond, car cette session a été initialisée en interne, la réponse est autorisée</span><span class="sxs-lookup"><span data-stu-id="4fdea-233">Internet DNS server responds, since this session was initiated internally, the response is allowed</span></span>
9. <span data-ttu-id="4fdea-234">Le serveur DNS met en cache la réponse et répond à la demande initiale à IIS01</span><span class="sxs-lookup"><span data-stu-id="4fdea-234">DNS server caches the response, and responds to the initial request back to IIS01</span></span>
10. <span data-ttu-id="4fdea-235">Aucune règle sortante sur le sous-réseau du serveur principal, le trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="4fdea-235">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="4fdea-236">Le sous-réseau du serveur frontal commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="4fdea-236">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="4fdea-237">Aucune règle NSG ne s’applique au trafic entrant en provenance du sous-réseau du serveur principal vers le sous-réseau du serveur frontal, par conséquent aucune des règles NSG ne s’applique</span><span class="sxs-lookup"><span data-stu-id="4fdea-237">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="4fdea-238">La règle système par défaut autorisant le trafic entre sous-réseaux autorise le trafic, le trafic est donc autorisé</span><span class="sxs-lookup"><span data-stu-id="4fdea-238">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed</span></span>
12. <span data-ttu-id="4fdea-239">IIS01 reçoit la réponse de la part de DNS01</span><span class="sxs-lookup"><span data-stu-id="4fdea-239">IIS01 receives the response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="4fdea-240">(Autorisé) fichier d’accès de serveur Web sur AppVM01</span><span class="sxs-lookup"><span data-stu-id="4fdea-240">(Allowed) Web Server access file on AppVM01</span></span>
1. <span data-ttu-id="4fdea-241">IIS01 demande un fichier sur AppVM01</span><span class="sxs-lookup"><span data-stu-id="4fdea-241">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="4fdea-242">Aucune règle sortante sur le sous-réseau du serveur frontal, le trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="4fdea-242">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="4fdea-243">Le sous-réseau du serveur principal commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="4fdea-243">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="4fdea-244">La règle NSG 1 (DNS) ne s’applique pas, passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="4fdea-244">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="4fdea-245">La règle NSG 2 (RDP) ne s’applique pas, passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="4fdea-245">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="4fdea-246">La règle NSG 3 (Internet vers le pare-feu) ne s’applique pas, passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="4fdea-246">NSG Rule 3 (Internet to Firewall) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="4fdea-247">La règle NSG 4 (IIS01 vers AppVM01) s’applique, le trafic est autorisé, arrêter le traitement des règles</span><span class="sxs-lookup"><span data-stu-id="4fdea-247">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="4fdea-248">AppVM01 reçoit la demande et répond avec un fichier (en supposant que l’accès est autorisé)</span><span class="sxs-lookup"><span data-stu-id="4fdea-248">AppVM01 receives the request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="4fdea-249">Comme il n’existe aucune règle sur le trafic sortant sur le sous-réseau du serveur principal, la réponse est autorisée.</span><span class="sxs-lookup"><span data-stu-id="4fdea-249">Since there are no outbound rules on the Backend subnet the response is allowed</span></span>
6. <span data-ttu-id="4fdea-250">Le sous-réseau du serveur frontal commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="4fdea-250">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="4fdea-251">Aucune règle NSG ne s’applique au trafic entrant en provenance du sous-réseau du serveur principal vers le sous-réseau du serveur frontal, par conséquent aucune des règles NSG ne s’applique</span><span class="sxs-lookup"><span data-stu-id="4fdea-251">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
   2. <span data-ttu-id="4fdea-252">La règle du système par défaut autorisant le trafic entre sous-réseaux autorise le trafic, le trafic est donc autorisé.</span><span class="sxs-lookup"><span data-stu-id="4fdea-252">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
7. <span data-ttu-id="4fdea-253">Le serveur IIS reçoit le fichier</span><span class="sxs-lookup"><span data-stu-id="4fdea-253">The IIS server receives the file</span></span>

#### <a name="denied-web-direct-to-web-server"></a><span data-ttu-id="4fdea-254">(Refusé) Web direct vers le serveur Web</span><span class="sxs-lookup"><span data-stu-id="4fdea-254">(Denied) Web direct to Web Server</span></span>
<span data-ttu-id="4fdea-255">Étant donné que le serveur Web, IIS01 et le pare-feu sont dans le même service cloud, ils partagent la même adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="4fdea-255">Since the Web Server, IIS01, and the Firewall are in the same Cloud Service they share the same public facing IP address.</span></span> <span data-ttu-id="4fdea-256">Par conséquent, tout le trafic HTTP est dirigé vers le pare-feu.</span><span class="sxs-lookup"><span data-stu-id="4fdea-256">Thus any HTTP traffic would be directed to the firewall.</span></span> <span data-ttu-id="4fdea-257">Alors que la demande est servie avec succès, elle ne peut pas accéder directement au serveur Web. Elle est d’abord transmise, comme prévu, via le pare-feu.</span><span class="sxs-lookup"><span data-stu-id="4fdea-257">While the request would be successfully served, it cannot go directly to the Web Server, it passed, as designed, through the Firewall first.</span></span> <span data-ttu-id="4fdea-258">Consultez le premier scénario de cette section sur le flux de trafic.</span><span class="sxs-lookup"><span data-stu-id="4fdea-258">See the first Scenario in this section for the traffic flow.</span></span>

#### <a name="denied-web-to-backend-server"></a><span data-ttu-id="4fdea-259">(Refusé) Web vers le serveur principal</span><span class="sxs-lookup"><span data-stu-id="4fdea-259">(Denied) Web to Backend Server</span></span>
1. <span data-ttu-id="4fdea-260">L’utilisateur Internet tente d’accéder à un fichier sur AppVM01 via le service BackEnd001.CloudApp.Net</span><span class="sxs-lookup"><span data-stu-id="4fdea-260">Internet user tries to access a file on AppVM01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="4fdea-261">Comme il n’y a aucun point de terminaison ouvert pour le partage de fichiers, il ne passe pas le service cloud et n’atteint pas le serveur</span><span class="sxs-lookup"><span data-stu-id="4fdea-261">Since there are no endpoints open for file share, this would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="4fdea-262">Si les points de terminaison ont été ouverts pour une raison quelconque, la règle NSG 5 (Internet vers le réseau virtuel) bloque ce trafic</span><span class="sxs-lookup"><span data-stu-id="4fdea-262">If the endpoints were open for some reason, NSG rule 5 (Internet to VNet) would block this traffic</span></span>

#### <a name="denied-web-dns-lookup-on-dns-server"></a><span data-ttu-id="4fdea-263">(Refusé) recherche DNS web sur le serveur DNS</span><span class="sxs-lookup"><span data-stu-id="4fdea-263">(Denied) Web DNS lookup on DNS server</span></span>
1. <span data-ttu-id="4fdea-264">L’utilisateur Internet tente de rechercher un enregistrement DNS interne sur DNS01 par le biais du service BackEnd001.CloudApp.Net</span><span class="sxs-lookup"><span data-stu-id="4fdea-264">Internet user tries to lookup an internal DNS record on DNS01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="4fdea-265">Comme aucun point de terminaison n’est ouvert pour DNS, il ne passe pas le service Cloud et n’atteint pas le serveur</span><span class="sxs-lookup"><span data-stu-id="4fdea-265">Since there are no endpoints open for DNS, this would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="4fdea-266">Si les points de terminaison ont été ouverts pour une raison quelconque, la règle NSG 5 (Internet vers réseau virtuel) bloque ce trafic (Remarque : cette règle 1 (DNS) ne s’applique pas pour deux raisons : tout d’abord l’adresse source est sur Internet, et cette règle s’applique uniquement lorsque la source locale est le réseau virtuel local ; de plus, s’il s’agit d’une règle d’autorisation, le trafic n’est jamais refusé)</span><span class="sxs-lookup"><span data-stu-id="4fdea-266">If the endpoints were open for some reason, NSG rule 5 (Internet to VNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first the source address is the internet, this rule only applies to the local VNet as the source, also this is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-to-sql-access-through-firewall"></a><span data-ttu-id="4fdea-267">(Refusé) Accès web vers SQL via le pare-feu</span><span class="sxs-lookup"><span data-stu-id="4fdea-267">(Denied) Web to SQL access through Firewall</span></span>
1. <span data-ttu-id="4fdea-268">Un utilisateur Internet demande des données SQL de FrontEnd001.CloudApp.Net (Service cloud face à Internet)</span><span class="sxs-lookup"><span data-stu-id="4fdea-268">Internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="4fdea-269">Comme aucun point de terminaison n’est ouvert pour SQL, la demande ne franchit pas le service cloud et n’atteint pas le pare-feu</span><span class="sxs-lookup"><span data-stu-id="4fdea-269">Since there are no endpoints open for SQL, this would not pass the Cloud Service and wouldn’t reach the firewall</span></span>
3. <span data-ttu-id="4fdea-270">Si des points de terminaison étaient ouverts pour une raison quelconque, le sous-réseau frontal commence le traitement des règles entrantes :</span><span class="sxs-lookup"><span data-stu-id="4fdea-270">If endpoints were open for some reason, the Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="4fdea-271">La règle NSG 1 (DNS) ne s’applique pas, passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="4fdea-271">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="4fdea-272">La règle NSG 2 (RDP) ne s’applique pas, passer à la règle suivante</span><span class="sxs-lookup"><span data-stu-id="4fdea-272">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="4fdea-273">La règle NSG 2 (Internet vers pare-feu) s’applique, le trafic est autorisé, arrêter le traitement</span><span class="sxs-lookup"><span data-stu-id="4fdea-273">NSG Rule 2 (Internet to Firewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="4fdea-274">Le trafic parvient à l’adresse IP du pare-feu (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="4fdea-274">Traffic hits internal IP address of the firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="4fdea-275">Le pare-feu n'a aucune règle de transfert pour SQL et abandonne le trafic</span><span class="sxs-lookup"><span data-stu-id="4fdea-275">Firewall has no forwarding rules for SQL and drops the traffic</span></span>

## <a name="conclusion"></a><span data-ttu-id="4fdea-276">Conclusion</span><span class="sxs-lookup"><span data-stu-id="4fdea-276">Conclusion</span></span>
<span data-ttu-id="4fdea-277">Il s’agit d’un moyen relativement simple de protéger votre application avec un pare-feu et d’isoler le sous-réseau principal du trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="4fdea-277">This is a relatively straight forward way of protecting your application with a firewall and isolating the back end subnet from inbound traffic.</span></span>

<span data-ttu-id="4fdea-278">Vous trouverez d’autres exemples et une vue d’ensemble des frontières de sécurité réseau [ici][HOME].</span><span class="sxs-lookup"><span data-stu-id="4fdea-278">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="4fdea-279">Références</span><span class="sxs-lookup"><span data-stu-id="4fdea-279">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="4fdea-280">Script principal et configuration réseau</span><span class="sxs-lookup"><span data-stu-id="4fdea-280">Main Script and Network Config</span></span>
<span data-ttu-id="4fdea-281">Enregistrez le script complet dans un fichier de script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4fdea-281">Save the Full Script in a PowerShell script file.</span></span> <span data-ttu-id="4fdea-282">Enregistrez la configuration réseau dans un fichier nommé « NetworkConf2.xml ».</span><span class="sxs-lookup"><span data-stu-id="4fdea-282">Save the Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="4fdea-283">Modifiez les variables définies par l’utilisateur selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="4fdea-283">Modify the user defined variables as needed.</span></span> <span data-ttu-id="4fdea-284">Exécutez le script, puis suivez les instructions d’installation de règle de pare-feu ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="4fdea-284">Run the script, then follow the Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="4fdea-285">Script complet</span><span class="sxs-lookup"><span data-stu-id="4fdea-285">Full Script</span></span>
<span data-ttu-id="4fdea-286">Ce script exécutera les actions suivantes en fonction des variables définies par l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="4fdea-286">This script will, based on the user defined variables:</span></span>

1. <span data-ttu-id="4fdea-287">Connexion à un abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="4fdea-287">Connect to an Azure subscription</span></span>
2. <span data-ttu-id="4fdea-288">Création d’un nouveau compte de stockage</span><span class="sxs-lookup"><span data-stu-id="4fdea-288">Create a new storage account</span></span>
3. <span data-ttu-id="4fdea-289">Création d’un nouveau réseau virtuel et de deux sous-réseaux, comme indiqué dans le fichier de configuration du réseau</span><span class="sxs-lookup"><span data-stu-id="4fdea-289">Create a new VNet and two subnets as defined in the Network Config file</span></span>
4. <span data-ttu-id="4fdea-290">Génération de 4 machines virtuelles Windows Server</span><span class="sxs-lookup"><span data-stu-id="4fdea-290">Build 4 windows server VMs</span></span>
5. <span data-ttu-id="4fdea-291">Configurez un groupe de sécurité réseau, notamment :</span><span class="sxs-lookup"><span data-stu-id="4fdea-291">Configure NSG including:</span></span>
   * <span data-ttu-id="4fdea-292">Création d’un groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="4fdea-292">Creating a NSG</span></span>
   * <span data-ttu-id="4fdea-293">Ajout de règles à ce dernier</span><span class="sxs-lookup"><span data-stu-id="4fdea-293">Populating it with rules</span></span>
   * <span data-ttu-id="4fdea-294">La liaison du groupe de sécurité réseaux au sous-réseaux appropriés</span><span class="sxs-lookup"><span data-stu-id="4fdea-294">Binding the NSG to the appropriate subnets</span></span>

<span data-ttu-id="4fdea-295">Ce script PowerShell doit être exécuté localement sur un PC ou un serveur connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="4fdea-295">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4fdea-296">Lorsque ce script est exécuté, des avertissements ou autres messages d’information peuvent s’afficher dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4fdea-296">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="4fdea-297">Seuls les messages d’erreur affichés en rouge sont source de préoccupation.</span><span class="sxs-lookup"><span data-stu-id="4fdea-297">Only error messages in red are cause for concern.</span></span>
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and Network Security Groups in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Two new cloud services
       - Two Subnets (FrontEnd and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on the FrontEnd Subnet (plus the NVA on the FrontEnd subnet)
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
       myFirewall - 10.0.1.4
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
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf2.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: To ensure proper NSG Rule creation later in this script:
        #       - The Web Server must be VM 1
        #       - The AppVM1 Server must be VM 2
        #       - The DNS server must be VM 4
        #
        #       Otherwise the NSG rules in the last section of this
        #       script will need to be changed to match the modified
        #       VM array numbers ($i) so the NSG Rule IP addresses
        #       are aligned to the associated VM IP addresses.

        # VM 0 - The Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $FrontEndService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 1 - The Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.5"

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
                # Note: Web traffic goes through the firewall, so we'll need to set up a HTTP endpoint.
                #       Also, the firewall will be redirecting web traffic to a new IP and Port in a
                #       forwarding rule, so the HTTP endpoint here will have the same public and local
                #       port and the firewall will do the NATing and redirection as declared in the
                #       firewall rule.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when the appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                    # Note: A Remote Desktop endpoint is automatically created when each VM is created.
                }
            $i++
        }

    # Configure NSG
        Write-Host "Configuring the Network Security Group (NSG)" -ForegroundColor Cyan

      # Build the NSG
        Write-Host "Building the NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rules
        Write-Host "Writing rules into the NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
            -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[4] -DestinationPortRange '53' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP to $VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet to $($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
            -SourceAddressPrefix Internet -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[1]) to $($VMName[2])" -Type Inbound -Priority 130 -Action Allow `
            -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[2] -DestinationPortRange '*' `
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


#### <a name="network-config-file"></a><span data-ttu-id="4fdea-298">Fichier de configuration réseau</span><span class="sxs-lookup"><span data-stu-id="4fdea-298">Network Config File</span></span>
<span data-ttu-id="4fdea-299">Enregistrer ce fichier XML avec l’emplacement mis à jour et ajouter le lien vers ce fichier à la variable $NetworkConfigFile dans le script ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="4fdea-299">Save this xml file with updated location and add the link to this file to the $NetworkConfigFile variable in the script above.</span></span>

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

#### <a name="sample-application-scripts"></a><span data-ttu-id="4fdea-300">Exemples de scripts d’application</span><span class="sxs-lookup"><span data-stu-id="4fdea-300">Sample Application Scripts</span></span>
<span data-ttu-id="4fdea-301">Si vous souhaitez installer un exemple d’application et d’autres exemples de zone DMZ, vous en trouverez à l’adresse suivante : [Exemple de script d’application][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="4fdea-301">If you wish to install a sample application for this, and other DMZ Examples, one has been provided at the following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
<span data-ttu-id="4fdea-302">[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "Zone DMZ avec groupe de sécurité réseau (NSG)"</span><span class="sxs-lookup"><span data-stu-id="4fdea-302">[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "Inbound DMZ with NSG"</span></span>
<span data-ttu-id="4fdea-303">[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "Icône NAT de destination"</span><span class="sxs-lookup"><span data-stu-id="4fdea-303">[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "Destination NAT Icon"</span></span>
<span data-ttu-id="4fdea-304">[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "Règle de pare-feu"</span><span class="sxs-lookup"><span data-stu-id="4fdea-304">[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "Firewall Rule"</span></span>
<span data-ttu-id="4fdea-305">[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "Activation de règle de pare-feu"</span><span class="sxs-lookup"><span data-stu-id="4fdea-305">[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "Firewall Rule Activation"</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
[Example1]: ./virtual-networks-dmz-nsg-asm.md
