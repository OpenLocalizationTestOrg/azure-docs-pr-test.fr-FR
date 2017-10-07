---
title: "aaaDMZ exemple : créer un réseau de périmètre tooprotect des applications avec un pare-feu et des groupes de sécurité réseau | Documents Microsoft"
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
ms.openlocfilehash: 18f116dc3897567bff14a509ae8c13f449182bfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="example-2--build-a-dmz-tooprotect-applications-with-a-firewall-and-nsgs"></a><span data-ttu-id="12fa3-103">Exemple 2 : créer un réseau de périmètre tooprotect des applications avec un pare-feu et des groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="12fa3-103">Example 2 – Build a DMZ tooprotect applications with a Firewall and NSGs</span></span>
<span data-ttu-id="12fa3-104">[Retour toohello Page meilleures pratiques de sécurité limite][HOME]</span><span class="sxs-lookup"><span data-stu-id="12fa3-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="12fa3-105">Cet exemple crée une zone DMZ avec un pare-feu, quatre serveurs Windows et des groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="12fa3-105">This example will create a DMZ with a firewall, four windows servers, and Network Security Groups.</span></span> <span data-ttu-id="12fa3-106">Il vous guide également dans chacun des hello des commandes tooprovide une meilleure compréhension de chaque étape.</span><span class="sxs-lookup"><span data-stu-id="12fa3-106">It will also walk through each of hello relevant commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="12fa3-107">Il existe également un scénario de trafic section tooprovide un détaillées étape par étape comment le trafic passe par le biais des couches de défense dans hello hello réseau de périmètre.</span><span class="sxs-lookup"><span data-stu-id="12fa3-107">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="12fa3-108">Enfin, dans la section des références hello est code complet de hello et instruction toobuild cette tootest d’environnement et de faire des essais avec différents scénarios.</span><span class="sxs-lookup"><span data-stu-id="12fa3-108">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="12fa3-109">![Zone DMZ entrante avec NVA et NSG][1]</span><span class="sxs-lookup"><span data-stu-id="12fa3-109">![Inbound DMZ with NVA and NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="12fa3-110">Description de l’environnement</span><span class="sxs-lookup"><span data-stu-id="12fa3-110">Environment Description</span></span>
<span data-ttu-id="12fa3-111">Dans cet exemple, il existe un abonnement qui contient les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="12fa3-111">In this example there is a subscription that contains hello following:</span></span>

* <span data-ttu-id="12fa3-112">deux services cloud : « FrontEnd001 », « BackEnd001 »,</span><span class="sxs-lookup"><span data-stu-id="12fa3-112">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="12fa3-113">Un réseau virtuel « CorpNetwork » avec deux sous-réseaux : « FrontEnd » et « BackEnd »</span><span class="sxs-lookup"><span data-stu-id="12fa3-113">A Virtual Network “CorpNetwork”, with two subnets: “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="12fa3-114">Un groupe de sécurité réseau unique qui est appliqué tooboth sous-réseaux</span><span class="sxs-lookup"><span data-stu-id="12fa3-114">A single Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="12fa3-115">Une appliance virtuelle de réseau, dans cet exemple, un pare-feu Barracuda NextGen connecté toohello frontal sous-réseau</span><span class="sxs-lookup"><span data-stu-id="12fa3-115">A network virtual appliance, in this example a Barracuda NextGen Firewall, connected toohello Frontend subnet</span></span>
* <span data-ttu-id="12fa3-116">un serveur Windows Server représentant un serveur web d’application (« IIS01 »),</span><span class="sxs-lookup"><span data-stu-id="12fa3-116">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="12fa3-117">Deux serveurs Windows Server qui représentent les serveurs principaux d’applications (« AppVM01 », « AppVM02 »)</span><span class="sxs-lookup"><span data-stu-id="12fa3-117">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="12fa3-118">Un serveur Windows Server qui représente un serveur DNS (« DNS01 »),</span><span class="sxs-lookup"><span data-stu-id="12fa3-118">A Windows server that represents a DNS server (“DNS01”)</span></span>

> [!NOTE]
> <span data-ttu-id="12fa3-119">Bien que cet exemple utilise un pare-feu Barracuda NextGen, nombreux hello que différentes solutions de réseau virtuel peut être utilisées pour cet exemple.</span><span class="sxs-lookup"><span data-stu-id="12fa3-119">Although this example uses a Barracuda NextGen Firewall, many of hello different Network Virtual Appliances could be used for this example.</span></span>
> 
> 

<span data-ttu-id="12fa3-120">Dans la section des références hello ci-dessous, il existe un script PowerShell qui générera la plupart des environnement hello décrite ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="12fa3-120">In hello references section below there is a PowerShell script that will build most of hello environment described above.</span></span> <span data-ttu-id="12fa3-121">Machines virtuelles de génération hello et réseaux virtuels, bien que s’effectuent par le script d’exemple hello, ne sont pas décrits en détail dans ce document.</span><span class="sxs-lookup"><span data-stu-id="12fa3-121">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span>

<span data-ttu-id="12fa3-122">environnement de hello toobuild :</span><span class="sxs-lookup"><span data-stu-id="12fa3-122">toobuild hello environment:</span></span>

1. <span data-ttu-id="12fa3-123">Fichier hello réseau config xml figurant dans la section de références hello (mis à jour avec les noms, l’emplacement et scénario de hello donné toomatch IP adresses)</span><span class="sxs-lookup"><span data-stu-id="12fa3-123">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="12fa3-124">Variables utilisateur hello script toomatch hello environnement hello de script de mise à jour hello est toobe exécutée (abonnements, les noms de service, etc.)</span><span class="sxs-lookup"><span data-stu-id="12fa3-124">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="12fa3-125">Exécutez le script de hello dans PowerShell</span><span class="sxs-lookup"><span data-stu-id="12fa3-125">Execute hello script in PowerShell</span></span>

<span data-ttu-id="12fa3-126">**Remarque**: région hello signifiée Bonjour script PowerShell doit correspondre à la région hello signifiée dans le fichier xml de configuration de réseau hello.</span><span class="sxs-lookup"><span data-stu-id="12fa3-126">**Note**: hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>

<span data-ttu-id="12fa3-127">Une fois hello script s’exécute correctement fallu hello postérieur au script comme suit :</span><span class="sxs-lookup"><span data-stu-id="12fa3-127">Once hello script runs successfully hello following post-script steps may be taken:</span></span>

1. <span data-ttu-id="12fa3-128">Configurez des règles de pare-feu hello, celle-ci est décrite dans la section hello ci-dessous intitulée : règles de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="12fa3-128">Set up hello firewall rules, this is covered in hello section below titled: Firewall Rules.</span></span>
2. <span data-ttu-id="12fa3-129">Si vous le souhaitez dans la section des références de hello sont deux tooset de scripts de serveur web de hello et le serveur d’applications à un tooallow d’application web simple test avec cette configuration de réseau de périmètre.</span><span class="sxs-lookup"><span data-stu-id="12fa3-129">Optionally in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="12fa3-130">section suivante de Hello explique la plupart des hello scripts instructions relatif tooNetwork groupes de sécurité.</span><span class="sxs-lookup"><span data-stu-id="12fa3-130">hello next section explains most of hello scripts statements relative tooNetwork Security Groups.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="12fa3-131">Groupes de sécurité réseau (NSG)</span><span class="sxs-lookup"><span data-stu-id="12fa3-131">Network Security Groups (NSG)</span></span>
<span data-ttu-id="12fa3-132">Dans cet exemple, un groupe NSG est créé, puis chargé avec six règles.</span><span class="sxs-lookup"><span data-stu-id="12fa3-132">For this example, a NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="12fa3-133">En règle générale, vous devez créer vos règles « Autoriser » spécifiques tout d’abord et puis hello dernière plus générique « Refuser » règles.</span><span class="sxs-lookup"><span data-stu-id="12fa3-133">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="12fa3-134">Hello priorité détermine les règles sont évaluées en premier.</span><span class="sxs-lookup"><span data-stu-id="12fa3-134">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="12fa3-135">Une fois que le trafic est trouvé règle spécifique de tooapply tooa, aucune autre règle n’est évaluées.</span><span class="sxs-lookup"><span data-stu-id="12fa3-135">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="12fa3-136">Les règles de groupe de sécurité réseau peuvent être appliquées, que ce soit dans hello direction entrante ou sortante (du point de vue hello du sous-réseau de hello).</span><span class="sxs-lookup"><span data-stu-id="12fa3-136">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
> 
> 

<span data-ttu-id="12fa3-137">De façon déclarative, hello suivant les règles est généré pour le trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="12fa3-137">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="12fa3-138">Le trafic DNS interne (port 53) est autorisé</span><span class="sxs-lookup"><span data-stu-id="12fa3-138">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="12fa3-139">Le trafic RDP (port 3389) à partir d’Internet de hello tooany machine virtuelle est autorisé.</span><span class="sxs-lookup"><span data-stu-id="12fa3-139">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="12fa3-140">Le trafic HTTP (port 80) à partir de hello Internet toohello NVA (pare-feu) est autorisé.</span><span class="sxs-lookup"><span data-stu-id="12fa3-140">HTTP traffic (port 80) from hello Internet toohello NVA (firewall) is allowed</span></span>
4. <span data-ttu-id="12fa3-141">Tout trafic (tous les ports) à partir de IIS01 tooAppVM1 est autorisée.</span><span class="sxs-lookup"><span data-stu-id="12fa3-141">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="12fa3-142">Tout trafic (tous les ports) à partir de hello Internet toohello réseau virtuel entier (les deux sous-réseaux) est refusé.</span><span class="sxs-lookup"><span data-stu-id="12fa3-142">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="12fa3-143">Tout trafic (tous les ports) à partir du sous-réseau principal toohello hello frontal sous-réseau est refusé.</span><span class="sxs-lookup"><span data-stu-id="12fa3-143">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="12fa3-144">Avec ces sous-réseau tooeach dépendant de règles, si une requête HTTP a été entrante à partir de hello toohello le serveur web Internet, les deux règles 3 (autoriser) et 5 (refuser) s’appliquent, mais étant donné que la règle 3 a une priorité plus élevée s’appliquerait et règle 5 ne serait pas entrent en jeu.</span><span class="sxs-lookup"><span data-stu-id="12fa3-144">With these rules bound tooeach subnet, if a HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="12fa3-145">Par conséquent, la demande de hello HTTP serait autorisée toohello pare-feu.</span><span class="sxs-lookup"><span data-stu-id="12fa3-145">Thus hello HTTP request would be allowed toohello firewall.</span></span> <span data-ttu-id="12fa3-146">Si ce trafic même a essayé de serveur de DNS01 tooreach hello, règle 5 (Deny) serait hello premier tooapply hello le trafic et ne serait pas autorisé toopass toohello serveur.</span><span class="sxs-lookup"><span data-stu-id="12fa3-146">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="12fa3-147">Règle 6 (Deny) blocs hello frontal sous-réseau communique avec le sous-réseau du serveur principal toohello (à l’exception du trafic autorisé dans les règles 1 et 4), cela protège le réseau principal de hello au cas où une personne malveillante compromet hello application web sur hello serveur frontal, hello attaquant accès limité toohello principal « protégé » (uniquement tooresources exposée sur le serveur de AppVM01 hello) de réseau.</span><span class="sxs-lookup"><span data-stu-id="12fa3-147">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="12fa3-148">Il existe une règle sortante par défaut qui autorise le trafic sortant toohello internet.</span><span class="sxs-lookup"><span data-stu-id="12fa3-148">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="12fa3-149">Pour cet exemple, nous allons autoriser le trafic sortant sans modifier les règles de trafic sortant.</span><span class="sxs-lookup"><span data-stu-id="12fa3-149">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="12fa3-150">toolock vers le bas le trafic dans les deux directions, utilisateur défini par routage est requise, cela est examiné dans un autre exemple peut-il hello [document de limite de sécurité principal][HOME].</span><span class="sxs-lookup"><span data-stu-id="12fa3-150">toolock down traffic in both directions, User Defined Routing is required, this is explored in a different example that can found in hello [main security boundary document][HOME].</span></span>

<span data-ttu-id="12fa3-151">règles de groupe de sécurité réseau Hello ci-dessus présenté sont des règles de groupe de sécurité réseau toohello très similaires dans [exemple 1 : créer un réseau de périmètre Simple avec des groupes de sécurité réseau][Example1].</span><span class="sxs-lookup"><span data-stu-id="12fa3-151">hello above discussed NSG rules are very similar toohello NSG rules in [Example 1 - Build a Simple DMZ with NSGs][Example1].</span></span> <span data-ttu-id="12fa3-152">Passez en revue hello Description du groupe de sécurité réseau dans ce document pour une présentation détaillée de chaque règle de groupe de sécurité réseau et de ses attributs.</span><span class="sxs-lookup"><span data-stu-id="12fa3-152">Please review hello NSG Description in that document for a detailed look at each NSG rule and it's attributes.</span></span>

## <a name="firewall-rules"></a><span data-ttu-id="12fa3-153">Règles de pare-feu</span><span class="sxs-lookup"><span data-stu-id="12fa3-153">Firewall Rules</span></span>
<span data-ttu-id="12fa3-154">Un client de gestion sera peut-être toobe installé sur un pare-feu de hello toomanage PC et créer des configurations hello nécessaires.</span><span class="sxs-lookup"><span data-stu-id="12fa3-154">A management client will need toobe installed on a PC toomanage hello firewall and create hello configurations needed.</span></span> <span data-ttu-id="12fa3-155">Consultez le fournisseur de documentation de votre pare-feu (ou autres NVA) hello sur comment toomanage hello appareil.</span><span class="sxs-lookup"><span data-stu-id="12fa3-155">See hello documentation from your firewall (or other NVA) vendor on how toomanage hello device.</span></span> <span data-ttu-id="12fa3-156">reste Hello de cette section décrivent la configuration hello du pare-feu de hello lui-même, via le client de gestion des fournisseurs hello (c'est-à-dire, non hello portail Azure ou PowerShell).</span><span class="sxs-lookup"><span data-stu-id="12fa3-156">hello remainder of this section will describe hello configuration of hello firewall itself, through hello vendors management client (i.e. not hello Azure portal or PowerShell).</span></span>

<span data-ttu-id="12fa3-157">Instructions de téléchargement du client et de connexion toohello Barracuda utilisé dans cet exemple se trouve ici : [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="12fa3-157">Instructions for client download and connecting toohello Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="12fa3-158">Sur le pare-feu hello, règles de transfert devez toobe créé.</span><span class="sxs-lookup"><span data-stu-id="12fa3-158">On hello firewall, forwarding rules will need toobe created.</span></span> <span data-ttu-id="12fa3-159">Cet exemple achemine uniquement les pare-feu entrantes toohello internet, puis le serveur web de toohello, transfert qu’une seule règle NAT est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="12fa3-159">Since this example only routes internet traffic in-bound toohello firewall and then toohello web server, only one forwarding NAT rule is needed.</span></span> <span data-ttu-id="12fa3-160">Sur hello Barracuda NextGen Firewall utilisé dans cette hello exemple règle serait un NAT de Destination de règle (heure d’été « NAT ») toopass ce trafic.</span><span class="sxs-lookup"><span data-stu-id="12fa3-160">On hello Barracuda NextGen Firewall used in this example hello rule would be a Destination NAT rule (“Dst NAT”) toopass this traffic.</span></span>

<span data-ttu-id="12fa3-161">suivant de hello toocreate règle (ou vérifiez les règles par défaut existant), à partir du tableau de bord hello Barracuda NG administrateur client, accédez d’onglet de configuration toohello, Bonjour Configuration opérationnelle de section, cliquez sur règles.</span><span class="sxs-lookup"><span data-stu-id="12fa3-161">toocreate hello following rule (or verify existing default rules), starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="12fa3-162">Une grille est appelée, « Règles de Main » affiche hello désactivés et actives des règles sur les pare-feu hello existantes.</span><span class="sxs-lookup"><span data-stu-id="12fa3-162">A grid called, “Main Rules” will show hello existing active and deactivated rules on hello firewall.</span></span> <span data-ttu-id="12fa3-163">Hello coin supérieur droit de cette grille est une petite, verte « + », sur cette toocreate une nouvelle règle (Remarque : votre pare-feu peut être « verrouillé » pour les modifications, si vous voyez un bouton marqué « Verrouiller » et vous toocreate impossible ou modifiez les règles, cliquez sur ce bouton trop « déverrouiller » hello groupe de règles et d’autoriser la modification).</span><span class="sxs-lookup"><span data-stu-id="12fa3-163">In hello upper right corner of this grid is a small, green “+” button, click this toocreate a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable toocreate or edit rules, click this button too“unlock” hello ruleset and allow editing).</span></span> <span data-ttu-id="12fa3-164">Si vous le souhaitez tooedit une règle existante, sélectionnez cette règle, avec le bouton droit et sélectionnez Modifier la règle.</span><span class="sxs-lookup"><span data-stu-id="12fa3-164">If you wish tooedit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="12fa3-165">Créez une nouvelle règle et indiquez un nom, par exemple « WebTraffic ».</span><span class="sxs-lookup"><span data-stu-id="12fa3-165">Create a new rule and provide a name, such as "WebTraffic".</span></span> 

<span data-ttu-id="12fa3-166">icône de la règle NAT de Destination Hello ressemble à ceci : ![icône NAT de Destination][2]</span><span class="sxs-lookup"><span data-stu-id="12fa3-166">hello Destination NAT rule icon looks like this: ![Destination NAT Icon][2]</span></span>

<span data-ttu-id="12fa3-167">règle Hello elle-même ressemblerait à ceci :</span><span class="sxs-lookup"><span data-stu-id="12fa3-167">hello rule itself would look something like this:</span></span>

<span data-ttu-id="12fa3-168">![Règle de pare-feu][3]</span><span class="sxs-lookup"><span data-stu-id="12fa3-168">![Firewall Rule][3]</span></span>

<span data-ttu-id="12fa3-169">Ici n’importe quelle adresse entrant qu’accès hello pare-feu lors de la tentative tooreach HTTP (port 80 ou 443 pour HTTPS) est envoyé hello du pare-feu interface « DHCP1 Local IP » et toohello redirigé serveur Web avec hello adresse IP de 10.0.1.5.</span><span class="sxs-lookup"><span data-stu-id="12fa3-169">Here any inbound address that hits hello Firewall trying tooreach HTTP (port 80 or 443 for HTTPS) will be sent out hello Firewall’s “DHCP1 Local IP” interface and redirected toohello Web Server with hello IP Address of 10.0.1.5.</span></span> <span data-ttu-id="12fa3-170">Étant donné que le trafic de hello arrive sur le port 80 et le serveur de web toohello continu sur le port 80, aucune modification du port a été nécessaire.</span><span class="sxs-lookup"><span data-stu-id="12fa3-170">Since hello traffic is coming in on port 80 and going toohello web server on port 80 no port change was needed.</span></span> <span data-ttu-id="12fa3-171">Toutefois, hello liste cible auraient pu être 10.0.1.5:8080 si notre serveur Web était à l’écoute sur le port 8080 ainsi traduction hello entrant port 80 sur hello pare-feu tooinbound port 8080 hello serveur web.</span><span class="sxs-lookup"><span data-stu-id="12fa3-171">However, hello Target List could have been 10.0.1.5:8080 if our Web Server listened on port 8080 thus translating hello inbound port 80 on hello firewall tooinbound port 8080 on hello web server.</span></span>

<span data-ttu-id="12fa3-172">Une méthode de connexion doit également être signifiée, pourquoi la règle de Destination à partir d’Internet, de hello « SNAT dynamique » est la plus appropriée.</span><span class="sxs-lookup"><span data-stu-id="12fa3-172">A Connection Method should also be signified, for hello Destination Rule from hello Internet, "Dynamic SNAT" is most appropriate.</span></span> 

<span data-ttu-id="12fa3-173">Bien qu'une seule règle soit créée, il est important de définir correctement sa priorité.</span><span class="sxs-lookup"><span data-stu-id="12fa3-173">Although only one rule has been created it's important that its priority is set correctly.</span></span> <span data-ttu-id="12fa3-174">Si dans la grille hello de toutes les règles de pare-feu de hello cette nouvelle règle est bas hello (sous la règle « BLOCKALL » de hello) il ne sera jamais entrent en jeu.</span><span class="sxs-lookup"><span data-stu-id="12fa3-174">If in hello grid of all rules on hello firewall this new rule is on hello bottom (below hello "BLOCKALL" rule) it will never come into play.</span></span> <span data-ttu-id="12fa3-175">Vérifiez la règle hello qui vient d’être créé pour le trafic web se situe au-dessus de la règle BLOCKALL hello.</span><span class="sxs-lookup"><span data-stu-id="12fa3-175">Ensure hello newly created rule for web traffic is above hello BLOCKALL rule.</span></span>

<span data-ttu-id="12fa3-176">Une fois que la règle de hello est créée, elle doit être transmise toohello pare-feu et puis activé, si cela n’est pas fait règle hello modification ne prendra effet.</span><span class="sxs-lookup"><span data-stu-id="12fa3-176">Once hello rule is created, it must be pushed toohello firewall and then activated, if this is not done hello rule change will not take effect.</span></span> <span data-ttu-id="12fa3-177">processus de push et l’activation de Hello est décrit dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="12fa3-177">hello push and activation process is described in hello next section.</span></span>

## <a name="rule-activation"></a><span data-ttu-id="12fa3-178">Activation d’une règle</span><span class="sxs-lookup"><span data-stu-id="12fa3-178">Rule Activation</span></span>
<span data-ttu-id="12fa3-179">Avec hello ruleset modifiées tooadd cette règle, hello ruleset doit être téléchargé toohello pare-feu et activé.</span><span class="sxs-lookup"><span data-stu-id="12fa3-179">With hello ruleset modified tooadd this rule, hello ruleset must be uploaded toohello firewall and activated.</span></span>

<span data-ttu-id="12fa3-180">![Activation de règle de pare-feu][4]</span><span class="sxs-lookup"><span data-stu-id="12fa3-180">![Firewall Rule Activation][4]</span></span>

<span data-ttu-id="12fa3-181">Dans l’angle supérieur droit de hello du client de gestion hello sont un cluster de boutons.</span><span class="sxs-lookup"><span data-stu-id="12fa3-181">In hello upper right hand corner of hello management client are a cluster of buttons.</span></span> <span data-ttu-id="12fa3-182">Cliquez sur hello « envoyer des modifications » bouton toosend hello modifié règles toohello pare-feu, puis cliquez sur le bouton « Activer » de hello.</span><span class="sxs-lookup"><span data-stu-id="12fa3-182">Click hello “Send Changes” button toosend hello modified rules toohello firewall, then click hello “Activate” button.</span></span>

<span data-ttu-id="12fa3-183">L’activation de l’ensemble de règles de pare-feu hello hello cette build d’environnement exemple est terminée.</span><span class="sxs-lookup"><span data-stu-id="12fa3-183">With hello activation of hello firewall ruleset this example environment build is complete.</span></span> <span data-ttu-id="12fa3-184">Si vous le souhaitez, scripts de compilation hello post Bonjour section peut être des références exécutent tooadd une application toothis environnement tootest hello ci-dessous des scénarios de trafic.</span><span class="sxs-lookup"><span data-stu-id="12fa3-184">Optionally, hello post build scripts in hello References section can be run tooadd an application toothis environment tootest hello below traffic scenarios.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12fa3-185">Il est critique toorealize que vous ne serez pas d’accès au serveur web de hello directement.</span><span class="sxs-lookup"><span data-stu-id="12fa3-185">It is critical toorealize that you will not hit hello web server directly.</span></span> <span data-ttu-id="12fa3-186">Lorsqu’un navigateur demande une page HTTP à partir de FrontEnd001.CloudApp.Net, serveur web transmet de point de terminaison (port 80) HTTP hello ce pare-feu toohello ne Hello pas.</span><span class="sxs-lookup"><span data-stu-id="12fa3-186">When a browser requests an HTTP page from FrontEnd001.CloudApp.Net, hello HTTP endpoint (port 80) passes this traffic toohello firewall not hello web server.</span></span> <span data-ttu-id="12fa3-187">Hello pare-feu puis, selon la règle de toohello créé ci-dessus, NAT qui demandent toohello serveur Web.</span><span class="sxs-lookup"><span data-stu-id="12fa3-187">hello firewall then, according toohello rule created above, NATs that request toohello Web Server.</span></span>
> 
> 

## <a name="traffic-scenarios"></a><span data-ttu-id="12fa3-188">Scénarios de trafic</span><span class="sxs-lookup"><span data-stu-id="12fa3-188">Traffic Scenarios</span></span>
#### <a name="allowed-web-tooweb-server-through-firewall"></a><span data-ttu-id="12fa3-189">(Autorisé) Web tooWeb serveur via le pare-feu</span><span class="sxs-lookup"><span data-stu-id="12fa3-189">(Allowed) Web tooWeb Server through Firewall</span></span>
1. <span data-ttu-id="12fa3-190">Un utilisateur Internet demande une page HTTP en provenance de FrontEnd001.CloudApp.Net (service cloud face à Internet)</span><span class="sxs-lookup"><span data-stu-id="12fa3-190">Internet user requests HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="12fa3-191">Cloud service transmet le trafic via le point de terminaison ouvert sur l’interface locale de toofirewall le port 80 sur 10.0.1.4:80</span><span class="sxs-lookup"><span data-stu-id="12fa3-191">Cloud service passes traffic through open endpoint on port 80 toofirewall local interface on 10.0.1.4:80</span></span>
3. <span data-ttu-id="12fa3-192">Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="12fa3-192">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="12fa3-193">Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="12fa3-193">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="12fa3-194">Règle de groupe de sécurité réseau 2 (RDP) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="12fa3-194">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="12fa3-195">Règle de groupe de sécurité réseau 3 (tooFirewall Internet) s’applique, le trafic est le traitement des règles autorisées, arrêter</span><span class="sxs-lookup"><span data-stu-id="12fa3-195">NSG Rule 3 (Internet tooFirewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="12fa3-196">Le trafic atteint l’adresse IP interne du pare-feu de hello (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="12fa3-196">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="12fa3-197">Règle de pare-feu transfert voir ceci est le trafic du port 80, il redirige le serveur web de toohello IIS01</span><span class="sxs-lookup"><span data-stu-id="12fa3-197">Firewall forwarding rule see this is port 80 traffic, redirects it toohello web server IIS01</span></span>
6. <span data-ttu-id="12fa3-198">IIS01 écoute pour le trafic web, reçoit la requête et démarre le traitement de demande de hello</span><span class="sxs-lookup"><span data-stu-id="12fa3-198">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
7. <span data-ttu-id="12fa3-199">IIS01 demande hello SQL Server sur AppVM01 pour plus d’informations</span><span class="sxs-lookup"><span data-stu-id="12fa3-199">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
8. <span data-ttu-id="12fa3-200">Aucune règle sur le trafic sortant sur le sous-réseau du serveur frontal. Le trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="12fa3-200">No outbound rules on Frontend subnet, traffic is allowed</span></span>
9. <span data-ttu-id="12fa3-201">sous-réseau du serveur principal Hello commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="12fa3-201">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="12fa3-202">Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="12fa3-202">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="12fa3-203">Règle de groupe de sécurité réseau 2 (RDP) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="12fa3-203">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="12fa3-204">Règle de groupe de sécurité réseau 3 (tooFirewall Internet) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="12fa3-204">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="12fa3-205">Règle de groupe de sécurité réseau 4 (IIS01 tooAppVM01) s’applique, le trafic est le traitement des règles autorisées, arrêter</span><span class="sxs-lookup"><span data-stu-id="12fa3-205">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
10. <span data-ttu-id="12fa3-206">AppVM01 reçoit hello requête SQL et répond</span><span class="sxs-lookup"><span data-stu-id="12fa3-206">AppVM01 receives hello SQL Query and responds</span></span>
11. <span data-ttu-id="12fa3-207">Dans la mesure où il n’y a aucune règles de trafic sortant sur hello réponse de hello sous-réseau principal n’est autorisé</span><span class="sxs-lookup"><span data-stu-id="12fa3-207">Since there are no outbound rules on hello Backend subnet hello response is allowed</span></span>
12. <span data-ttu-id="12fa3-208">Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="12fa3-208">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="12fa3-209">Il n’existe aucune règle de groupe de sécurité réseau qui applique des tooInbound trafic de sous-réseau du serveur frontal de toohello de sous-réseau hello back-end, donc aucune des règles du groupe de sécurité réseau hello s’appliquent</span><span class="sxs-lookup"><span data-stu-id="12fa3-209">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="12fa3-210">règle du système par défaut Hello autorisant le trafic entre sous-réseaux permettrait ce trafic donc hello le trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="12fa3-210">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
13. <span data-ttu-id="12fa3-211">le serveur IIS Hello reçoit la réponse SQL hello et termine la réponse HTTP de hello et envoie toohello demandeur</span><span class="sxs-lookup"><span data-stu-id="12fa3-211">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requestor</span></span>
14. <span data-ttu-id="12fa3-212">Dans la mesure où il s’agit d’une session NAT à partir de pare-feu de hello, destination de réponse hello est (initialement) pour hello pare-feu</span><span class="sxs-lookup"><span data-stu-id="12fa3-212">Since this is a NAT session from hello firewall, hello response destination (initially) is for hello Firewall</span></span>
15. <span data-ttu-id="12fa3-213">les pare-feu Hello reçoit hello réponse hello serveur Web et transfère toohello précédent utilisateur Internet</span><span class="sxs-lookup"><span data-stu-id="12fa3-213">hello firewall receives hello response from hello Web Server and forwards back toohello Internet User</span></span>
16. <span data-ttu-id="12fa3-214">Dans la mesure où il n’y a aucune règles de trafic sortant sur hello réponse de hello sous-réseau frontal n’est autorisé et hello utilisateur Internet reçoit hello web page est demandée.</span><span class="sxs-lookup"><span data-stu-id="12fa3-214">Since there are no outbound rules on hello Frontend subnet hello response is allowed, and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-toobackend"></a><span data-ttu-id="12fa3-215">(Autorisé) RDP tooBackend</span><span class="sxs-lookup"><span data-stu-id="12fa3-215">(Allowed) RDP tooBackend</span></span>
1. <span data-ttu-id="12fa3-216">Administrateur du serveur sur internet demande tooAppVM01 de session RDP sur BackEnd001.CloudApp.Net:xxxxx où xxxxx représente le numéro de port hello affecté de façon aléatoire pour RDP tooAppVM01 (port de hello affecté sont accessibles sur hello portail Azure ou via PowerShell)</span><span class="sxs-lookup"><span data-stu-id="12fa3-216">Server Admin on internet requests RDP session tooAppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is hello randomly assigned port number for RDP tooAppVM01 (hello assigned port can be found on hello Azure Portal or via PowerShell)</span></span>
2. <span data-ttu-id="12fa3-217">Depuis hello que pare-feu n’écoute que sur hello FrontEnd001.CloudApp.Net adresse, il n’est pas impliquée dans ce flux de trafic</span><span class="sxs-lookup"><span data-stu-id="12fa3-217">Since hello Firewall is only listening on hello FrontEnd001.CloudApp.Net address, it is not involved with this traffic flow</span></span>
3. <span data-ttu-id="12fa3-218">Le sous-réseau du serveur principal entame le traitement du réseau entrant :</span><span class="sxs-lookup"><span data-stu-id="12fa3-218">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="12fa3-219">Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="12fa3-219">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="12fa3-220">La règle NSG 2 (RDP) s’applique, le trafic est autorisé, arrêter le traitement des règles</span><span class="sxs-lookup"><span data-stu-id="12fa3-220">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="12fa3-221">En l’absence de réseau sortant, les règles par défaut s’appliquent et le retour de trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="12fa3-221">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="12fa3-222">La session RDP est activée</span><span class="sxs-lookup"><span data-stu-id="12fa3-222">RDP session is enabled</span></span>
6. <span data-ttu-id="12fa3-223">AppVM01 demande le mot de passe utilisateur</span><span class="sxs-lookup"><span data-stu-id="12fa3-223">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="12fa3-224">(Autorisé) recherche DNS du serveur web sur le serveur DNS</span><span class="sxs-lookup"><span data-stu-id="12fa3-224">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="12fa3-225">Web des besoins du serveur, IIS01, de flux de données à www.data.gov, mais doit tooresolve hello adresse.</span><span class="sxs-lookup"><span data-stu-id="12fa3-225">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="12fa3-226">Hello configuration réseau pour les listes de réseau virtuel hello DNS01 (10.0.2.4 sur le sous-réseau du serveur principal hello) en tant que serveur DNS principal de hello, IIS01 envoie hello DNS demande tooDNS01</span><span class="sxs-lookup"><span data-stu-id="12fa3-226">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="12fa3-227">Aucune règle sur le trafic sortant sur le sous-réseau du serveur frontal. Le trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="12fa3-227">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="12fa3-228">Le sous-réseau du serveur principal entame le traitement du réseau entrant :</span><span class="sxs-lookup"><span data-stu-id="12fa3-228">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="12fa3-229">La règle NSG 1 (DNS) s’applique, le trafic est autorisé, arrêter le traitement des règles</span><span class="sxs-lookup"><span data-stu-id="12fa3-229">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="12fa3-230">Serveur DNS reçoit la demande de hello</span><span class="sxs-lookup"><span data-stu-id="12fa3-230">DNS server receives hello request</span></span>
6. <span data-ttu-id="12fa3-231">Serveur DNS n’a pas adresse hello mis en cache et demande à un serveur DNS racine sur hello internet</span><span class="sxs-lookup"><span data-stu-id="12fa3-231">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="12fa3-232">Aucune règle sortante sur le sous-réseau du serveur principal, le trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="12fa3-232">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="12fa3-233">Serveur DNS Internet répond, étant donné que cette session a été lancée en interne, réponse de hello est autorisée.</span><span class="sxs-lookup"><span data-stu-id="12fa3-233">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="12fa3-234">Le serveur DNS met en cache la réponse de hello et répond tooIIS01 arrière de demande initiale toohello</span><span class="sxs-lookup"><span data-stu-id="12fa3-234">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="12fa3-235">Aucune règle sortante sur le sous-réseau du serveur principal, le trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="12fa3-235">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="12fa3-236">Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="12fa3-236">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="12fa3-237">Il n’existe aucune règle de groupe de sécurité réseau qui applique des tooInbound trafic de sous-réseau du serveur frontal de toohello de sous-réseau hello back-end, donc aucune des règles du groupe de sécurité réseau hello s’appliquent</span><span class="sxs-lookup"><span data-stu-id="12fa3-237">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="12fa3-238">règle du système par défaut Hello autorisant le trafic entre sous-réseaux permet ce trafic donc hello le trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="12fa3-238">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="12fa3-239">IIS01 reçoit hello réponse DNS01</span><span class="sxs-lookup"><span data-stu-id="12fa3-239">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="12fa3-240">(Autorisé) fichier d’accès de serveur Web sur AppVM01</span><span class="sxs-lookup"><span data-stu-id="12fa3-240">(Allowed) Web Server access file on AppVM01</span></span>
1. <span data-ttu-id="12fa3-241">IIS01 demande un fichier sur AppVM01</span><span class="sxs-lookup"><span data-stu-id="12fa3-241">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="12fa3-242">Aucune règle sur le trafic sortant sur le sous-réseau du serveur frontal. Le trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="12fa3-242">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="12fa3-243">sous-réseau du serveur principal Hello commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="12fa3-243">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="12fa3-244">Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="12fa3-244">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="12fa3-245">Règle de groupe de sécurité réseau 2 (RDP) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="12fa3-245">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="12fa3-246">Règle de groupe de sécurité réseau 3 (tooFirewall Internet) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="12fa3-246">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="12fa3-247">Règle de groupe de sécurité réseau 4 (IIS01 tooAppVM01) s’applique, le trafic est le traitement des règles autorisées, arrêter</span><span class="sxs-lookup"><span data-stu-id="12fa3-247">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="12fa3-248">AppVM01 reçoit la demande de hello et répond avec le fichier (en supposant que l’accès est autorisé)</span><span class="sxs-lookup"><span data-stu-id="12fa3-248">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="12fa3-249">Dans la mesure où il n’y a aucune règles de trafic sortant sur hello réponse de hello sous-réseau principal n’est autorisé</span><span class="sxs-lookup"><span data-stu-id="12fa3-249">Since there are no outbound rules on hello Backend subnet hello response is allowed</span></span>
6. <span data-ttu-id="12fa3-250">Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="12fa3-250">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="12fa3-251">Il n’existe aucune règle de groupe de sécurité réseau qui applique des tooInbound trafic de sous-réseau du serveur frontal de toohello de sous-réseau hello back-end, donc aucune des règles du groupe de sécurité réseau hello s’appliquent</span><span class="sxs-lookup"><span data-stu-id="12fa3-251">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
   2. <span data-ttu-id="12fa3-252">règle du système par défaut Hello autorisant le trafic entre sous-réseaux permettrait ce trafic donc hello le trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="12fa3-252">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="12fa3-253">le serveur IIS Hello reçoit le fichier de hello</span><span class="sxs-lookup"><span data-stu-id="12fa3-253">hello IIS server receives hello file</span></span>

#### <a name="denied-web-direct-tooweb-server"></a><span data-ttu-id="12fa3-254">(Refusé) TooWeb directe de Web Server</span><span class="sxs-lookup"><span data-stu-id="12fa3-254">(Denied) Web direct tooWeb Server</span></span>
<span data-ttu-id="12fa3-255">Puisque hello serveur Web, IIS01 et hello pare-feu sont Bonjour même Service Cloud qui ils partagent hello même adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="12fa3-255">Since hello Web Server, IIS01, and hello Firewall are in hello same Cloud Service they share hello same public facing IP address.</span></span> <span data-ttu-id="12fa3-256">Par conséquent, tout le trafic HTTP est dirigé toohello pare-feu.</span><span class="sxs-lookup"><span data-stu-id="12fa3-256">Thus any HTTP traffic would be directed toohello firewall.</span></span> <span data-ttu-id="12fa3-257">Lors de la demande de hello serait servi avec succès, il ne peut pas accéder directement toohello serveur Web, il est passé, comme prévu, hello par le biais du pare-feu tout d’abord.</span><span class="sxs-lookup"><span data-stu-id="12fa3-257">While hello request would be successfully served, it cannot go directly toohello Web Server, it passed, as designed, through hello Firewall first.</span></span> <span data-ttu-id="12fa3-258">Consultez hello premier scénario de cette section pour le flux de trafic hello.</span><span class="sxs-lookup"><span data-stu-id="12fa3-258">See hello first Scenario in this section for hello traffic flow.</span></span>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="12fa3-259">(Refusé) Web tooBackend Server</span><span class="sxs-lookup"><span data-stu-id="12fa3-259">(Denied) Web tooBackend Server</span></span>
1. <span data-ttu-id="12fa3-260">Utilisateur Internet tente tooaccess un fichier sur AppVM01 via hello BackEnd001.CloudApp.Net service</span><span class="sxs-lookup"><span data-stu-id="12fa3-260">Internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="12fa3-261">Étant donné qu’aucun point de terminaison ouvert pour le partage de fichiers, cela ne peut pas passer hello Service Cloud et ne pas de joindre le serveur de hello</span><span class="sxs-lookup"><span data-stu-id="12fa3-261">Since there are no endpoints open for file share, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="12fa3-262">Si les points de terminaison hello étaient ouverts pour une raison quelconque, la règle de groupe de sécurité réseau 5 (tooVNet Internet) susceptibles de bloquer ce trafic</span><span class="sxs-lookup"><span data-stu-id="12fa3-262">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-lookup-on-dns-server"></a><span data-ttu-id="12fa3-263">(Refusé) recherche DNS web sur le serveur DNS</span><span class="sxs-lookup"><span data-stu-id="12fa3-263">(Denied) Web DNS lookup on DNS server</span></span>
1. <span data-ttu-id="12fa3-264">Utilisateur Internet tente toolookup un enregistrement DNS interne sur DNS01 via hello BackEnd001.CloudApp.Net service</span><span class="sxs-lookup"><span data-stu-id="12fa3-264">Internet user tries toolookup an internal DNS record on DNS01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="12fa3-265">Étant donné qu’aucun point de terminaison ouvert pour un serveur DNS, cela ne peut pas passer hello Service Cloud et ne pas de joindre le serveur de hello</span><span class="sxs-lookup"><span data-stu-id="12fa3-265">Since there are no endpoints open for DNS, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="12fa3-266">Si les points de terminaison hello étaient ouverts pour une raison quelconque, la règle de groupe de sécurité réseau 5 (tooVNet Internet) susceptibles de bloquer ce trafic (Remarque : cette règle 1 (DNS) ne peuvent pas s’appliquer pour deux raisons, première adresse de la source hello est hello internet, cette règle s’applique uniquement toohello réseau local en tant que hello source, Il s’agit d’une règle d’autorisation, donc il n’est jamais refuser le trafic)</span><span class="sxs-lookup"><span data-stu-id="12fa3-266">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first hello source address is hello internet, this rule only applies toohello local VNet as hello source, also this is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-toosql-access-through-firewall"></a><span data-ttu-id="12fa3-267">(Refusé) Accès Web tooSQL via le pare-feu</span><span class="sxs-lookup"><span data-stu-id="12fa3-267">(Denied) Web tooSQL access through Firewall</span></span>
1. <span data-ttu-id="12fa3-268">Un utilisateur Internet demande des données SQL de FrontEnd001.CloudApp.Net (Service cloud face à Internet)</span><span class="sxs-lookup"><span data-stu-id="12fa3-268">Internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="12fa3-269">Étant donné qu’aucun point de terminaison ouvert pour SQL, cela ne peut pas passer hello Service Cloud et ne pas atteindre le pare-feu hello</span><span class="sxs-lookup"><span data-stu-id="12fa3-269">Since there are no endpoints open for SQL, this would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="12fa3-270">Si les points de terminaison ont été ouverts pour une raison quelconque, sous-réseau du serveur frontal hello commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="12fa3-270">If endpoints were open for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="12fa3-271">Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="12fa3-271">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="12fa3-272">Règle de groupe de sécurité réseau 2 (RDP) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="12fa3-272">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="12fa3-273">Règle de groupe de sécurité réseau 2 (tooFirewall Internet) s’applique, le trafic est le traitement des règles autorisées, arrêter</span><span class="sxs-lookup"><span data-stu-id="12fa3-273">NSG Rule 2 (Internet tooFirewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="12fa3-274">Le trafic atteint l’adresse IP interne du pare-feu de hello (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="12fa3-274">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="12fa3-275">Le pare-feu n’a aucune règle de transfert pour SQL et supprime hello du trafic</span><span class="sxs-lookup"><span data-stu-id="12fa3-275">Firewall has no forwarding rules for SQL and drops hello traffic</span></span>

## <a name="conclusion"></a><span data-ttu-id="12fa3-276">Conclusion</span><span class="sxs-lookup"><span data-stu-id="12fa3-276">Conclusion</span></span>
<span data-ttu-id="12fa3-277">Il s’agit d’un moyen relativement simple de protection de votre application avec un pare-feu et l’isolement de sous-réseau de back-end hello du trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="12fa3-277">This is a relatively straight forward way of protecting your application with a firewall and isolating hello back end subnet from inbound traffic.</span></span>

<span data-ttu-id="12fa3-278">Vous trouverez d’autres exemples et une vue d’ensemble des frontières de sécurité réseau [ici][HOME].</span><span class="sxs-lookup"><span data-stu-id="12fa3-278">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="12fa3-279">Références</span><span class="sxs-lookup"><span data-stu-id="12fa3-279">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="12fa3-280">Script principal et configuration réseau</span><span class="sxs-lookup"><span data-stu-id="12fa3-280">Main Script and Network Config</span></span>
<span data-ttu-id="12fa3-281">Enregistrez hello Script complet dans un fichier de script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="12fa3-281">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="12fa3-282">Enregistrez hello configuration réseau dans un fichier nommé « NetworkConf2.xml ».</span><span class="sxs-lookup"><span data-stu-id="12fa3-282">Save hello Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="12fa3-283">Modifier les variables de défini par l’utilisateur de hello en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="12fa3-283">Modify hello user defined variables as needed.</span></span> <span data-ttu-id="12fa3-284">Exécuter le script de hello, puis suivez le programme d’installation hello pare-feu règle instructions ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="12fa3-284">Run hello script, then follow hello Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="12fa3-285">Script complet</span><span class="sxs-lookup"><span data-stu-id="12fa3-285">Full Script</span></span>
<span data-ttu-id="12fa3-286">Ce script sera, en fonction des variables définies par l’utilisateur de hello :</span><span class="sxs-lookup"><span data-stu-id="12fa3-286">This script will, based on hello user defined variables:</span></span>

1. <span data-ttu-id="12fa3-287">Se connecter tooan abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="12fa3-287">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="12fa3-288">Création d’un nouveau compte de stockage</span><span class="sxs-lookup"><span data-stu-id="12fa3-288">Create a new storage account</span></span>
3. <span data-ttu-id="12fa3-289">Créer un nouveau réseau virtuel et deux sous-réseaux, tel que défini dans le fichier de configuration de réseau de hello</span><span class="sxs-lookup"><span data-stu-id="12fa3-289">Create a new VNet and two subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="12fa3-290">Génération de 4 machines virtuelles Windows Server</span><span class="sxs-lookup"><span data-stu-id="12fa3-290">Build 4 windows server VMs</span></span>
5. <span data-ttu-id="12fa3-291">Configurez un groupe de sécurité réseau, notamment :</span><span class="sxs-lookup"><span data-stu-id="12fa3-291">Configure NSG including:</span></span>
   * <span data-ttu-id="12fa3-292">Création d’un groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="12fa3-292">Creating a NSG</span></span>
   * <span data-ttu-id="12fa3-293">Ajout de règles à ce dernier</span><span class="sxs-lookup"><span data-stu-id="12fa3-293">Populating it with rules</span></span>
   * <span data-ttu-id="12fa3-294">Sous-réseaux appropriés de liaison hello NSG toohello</span><span class="sxs-lookup"><span data-stu-id="12fa3-294">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="12fa3-295">Ce script PowerShell doit être exécuté localement sur un PC ou un serveur connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="12fa3-295">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12fa3-296">Lorsque ce script est exécuté, des avertissements ou autres messages d’information peuvent s’afficher dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="12fa3-296">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="12fa3-297">Seuls les messages d’erreur affichés en rouge sont source de préoccupation.</span><span class="sxs-lookup"><span data-stu-id="12fa3-297">Only error messages in red are cause for concern.</span></span>
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
       - One server on hello FrontEnd Subnet (plus hello NVA on hello FrontEnd subnet)
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
       myFirewall - 10.0.1.4
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
        # Note: tooensure proper NSG Rule creation later in this script:
        #       - hello Web Server must be VM 1
        #       - hello AppVM1 Server must be VM 2
        #       - hello DNS server must be VM 4
        #
        #       Otherwise hello NSG rules in hello last section of this
        #       script will need toobe changed toomatch hello modified
        #       VM array numbers ($i) so hello NSG Rule IP addresses
        #       are aligned toohello associated VM IP addresses.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $FrontEndService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.5"

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
                # Note: Web traffic goes through hello firewall, so we'll need tooset up a HTTP endpoint.
                #       Also, hello firewall will be redirecting web traffic tooa new IP and Port in a
                #       forwarding rule, so hello HTTP endpoint here will have hello same public and local
                #       port and hello firewall will do hello NATing and redirection as declared in the
                #       firewall rule.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
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
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rules
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
            -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[4] -DestinationPortRange '53' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
            -SourceAddressPrefix Internet -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[1]) too$($VMName[2])" -Type Inbound -Priority 130 -Action Allow `
            -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[2] -DestinationPortRange '*' `
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


#### <a name="network-config-file"></a><span data-ttu-id="12fa3-298">Fichier de configuration réseau</span><span class="sxs-lookup"><span data-stu-id="12fa3-298">Network Config File</span></span>
<span data-ttu-id="12fa3-299">Enregistrez ce fichier xml avec l’emplacement mis à jour et ajouter hello lien toothis fichier toohello $NetworkConfigFile variable dans le script hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="12fa3-299">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello script above.</span></span>

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

#### <a name="sample-application-scripts"></a><span data-ttu-id="12fa3-300">Exemples de scripts d’application</span><span class="sxs-lookup"><span data-stu-id="12fa3-300">Sample Application Scripts</span></span>
<span data-ttu-id="12fa3-301">Si vous le souhaitez tooinstall un exemple d’application pour ce, ainsi que d’autres exemples de réseau de périmètre, un a été fourni au lien de hello : [Application exemple de Script][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="12fa3-301">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "Zone DMZ avec groupe de sécurité réseau (NSG)"
[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "Icône NAT de destination"
[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "Règle de pare-feu"
[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "Activation de règle de pare-feu"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
[Example1]: ./virtual-networks-dmz-nsg-asm.md
