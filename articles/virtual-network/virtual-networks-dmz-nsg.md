---
title: "aaaAzure DMZ, exemple : créer un réseau de périmètre Simple avec des groupes de sécurité réseau | Documents Microsoft"
description: "Générer une zone DMZ avec des groupes de sécurité réseau (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 11c5c6026da30fbc9c5e585f5c16e2d411d6fd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a><span data-ttu-id="c6618-103">Exemple 1 – Créer une zone DMZ simple à l’aide de groupes de sécurité réseau avec un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c6618-103">Example 1 – Build a simple DMZ using NSGs with an Azure Resource Manager template</span></span>
<span data-ttu-id="c6618-104">[Retour toohello Page meilleures pratiques de sécurité limite][HOME]</span><span class="sxs-lookup"><span data-stu-id="c6618-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c6618-105">Modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c6618-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="c6618-106">Classic - PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6618-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="c6618-107">Cet exemple crée une zone DMZ primitive avec quatre serveurs Windows et des groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="c6618-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="c6618-108">Cet exemple décrit chacune des sections tooprovide une meilleure compréhension de chaque étape de hello modèle approprié.</span><span class="sxs-lookup"><span data-stu-id="c6618-108">This example describes each of hello relevant template sections tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="c6618-109">Il existe également un tooprovide de section de scénario de trafic détaillée approfondi comment le trafic passe par le biais des couches de défense dans hello réseau de périmètre hello.</span><span class="sxs-lookup"><span data-stu-id="c6618-109">There is also a Traffic Scenario section tooprovide an in-depth step-by-step look at how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="c6618-110">Enfin, dans la section des références hello est toobuild de code et les instructions de modèle complète hello cette tootest d’environnement et de faire des essais avec différents scénarios.</span><span class="sxs-lookup"><span data-stu-id="c6618-110">Finally, in hello references section is hello complete template code and instructions toobuild this environment tootest and experiment with various scenarios.</span></span> 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

<span data-ttu-id="c6618-111">![Réseau de périmètre entrant avec groupe de sécurité réseau][1]</span><span class="sxs-lookup"><span data-stu-id="c6618-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="c6618-112">Description de l’environnement</span><span class="sxs-lookup"><span data-stu-id="c6618-112">Environment description</span></span>
<span data-ttu-id="c6618-113">Dans cet exemple, un abonnement contient hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="c6618-113">In this example a subscription contains hello following resources:</span></span>

* <span data-ttu-id="c6618-114">un seul groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="c6618-114">A single resource group</span></span>
* <span data-ttu-id="c6618-115">un réseau virtuel avec deux sous-réseaux « FrontEnd » et « BackEnd »,</span><span class="sxs-lookup"><span data-stu-id="c6618-115">A Virtual Network with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="c6618-116">Un groupe de sécurité réseau qui est appliquée tooboth sous-réseaux</span><span class="sxs-lookup"><span data-stu-id="c6618-116">A Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="c6618-117">un serveur Windows Server représentant un serveur web d’application (« IIS01 »),</span><span class="sxs-lookup"><span data-stu-id="c6618-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="c6618-118">Deux serveurs Windows Server qui représentent les serveurs principaux d’applications (« AppVM01 », « AppVM02 »)</span><span class="sxs-lookup"><span data-stu-id="c6618-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="c6618-119">Un serveur Windows Server qui représente un serveur DNS (« DNS01 »),</span><span class="sxs-lookup"><span data-stu-id="c6618-119">A Windows server that represents a DNS server (“DNS01”)</span></span>
* <span data-ttu-id="c6618-120">Une adresse IP publique associée au serveur web d’application hello</span><span class="sxs-lookup"><span data-stu-id="c6618-120">A public IP address associated with hello application web server</span></span>

<span data-ttu-id="c6618-121">Dans la section des références de hello, il est un modèle de gestionnaire de ressources Azure de tooan de lien qui génère l’environnement hello décrite dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="c6618-121">In hello references section, there is a link tooan Azure Resource Manager template that builds hello environment described in this example.</span></span> <span data-ttu-id="c6618-122">Machines virtuelles de génération hello et réseaux virtuels, bien que le fait par le modèle d’exemple hello, ne sont pas décrits en détail dans ce document.</span><span class="sxs-lookup"><span data-stu-id="c6618-122">Building hello VMs and Virtual Networks, although done by hello example template, are not described in detail in this document.</span></span> 

<span data-ttu-id="c6618-123">**toobuild cet environnement** (obtenir des instructions détaillées sont dans la section des références hello de ce document) ;</span><span class="sxs-lookup"><span data-stu-id="c6618-123">**toobuild this environment** (detailed instructions are in hello references section of this document);</span></span>

1. <span data-ttu-id="c6618-124">Déployer hello modèle du Gestionnaire de ressources Azure à : [modèles de démarrage rapide Azure][Template]</span><span class="sxs-lookup"><span data-stu-id="c6618-124">Deploy hello Azure Resource Manager Template at: [Azure Quickstart Templates][Template]</span></span>
2. <span data-ttu-id="c6618-125">Installer l’application d’exemple hello sur : [Application exemple de Script][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="c6618-125">Install hello sample application at: [Sample Application Script][SampleApp]</span></span>

>[!NOTE]
><span data-ttu-id="c6618-126">tooRDP tooany sur les serveurs principaux dans ce cas, le serveur IIS hello est utilisé comme une zone « saut ».</span><span class="sxs-lookup"><span data-stu-id="c6618-126">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="c6618-127">Serveur IIS de première RDP toohello puis à partir de serveur de hello IIS Server RDP toohello principal.</span><span class="sxs-lookup"><span data-stu-id="c6618-127">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span> <span data-ttu-id="c6618-128">Une adresse IP publique peut être associée à chaque carte réseau du serveur pour faciliter la connexion RDP.</span><span class="sxs-lookup"><span data-stu-id="c6618-128">Alternately a Public IP can be associated with each server NIC for easier RDP.</span></span>
> 
>

<span data-ttu-id="c6618-129">Hello sections suivantes fournissent une description détaillée de hello groupe de sécurité réseau et son mode de fonctionnement pour cet exemple en parcourant les lignes de clé de hello modèle du Gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="c6618-129">hello following sections provide a detailed description of hello Network Security Group and how it functions for this example by walking through key lines of hello Azure Resource Manager Template.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="c6618-130">Groupes de sécurité réseau (NSG)</span><span class="sxs-lookup"><span data-stu-id="c6618-130">Network Security Groups (NSG)</span></span>
<span data-ttu-id="c6618-131">Pour cet exemple, un groupe NSG est créé, puis chargé avec six règles.</span><span class="sxs-lookup"><span data-stu-id="c6618-131">For this example, an NSG group is built and then loaded with six rules.</span></span> 

>[!TIP]
><span data-ttu-id="c6618-132">En règle générale, vous devez créer vos règles « Autoriser » spécifiques tout d’abord et puis hello dernière plus générique « Refuser » règles.</span><span class="sxs-lookup"><span data-stu-id="c6618-132">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="c6618-133">Hello priorité détermine les règles sont évaluées en premier.</span><span class="sxs-lookup"><span data-stu-id="c6618-133">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="c6618-134">Une fois que le trafic est trouvé règle spécifique de tooapply tooa, aucune autre règle n’est évaluées.</span><span class="sxs-lookup"><span data-stu-id="c6618-134">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="c6618-135">Les règles de groupe de sécurité réseau peuvent être appliquées, que ce soit dans hello direction entrante ou sortante (du point de vue hello du sous-réseau de hello).</span><span class="sxs-lookup"><span data-stu-id="c6618-135">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
>
>

<span data-ttu-id="c6618-136">De façon déclarative, hello suivant les règles est généré pour le trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="c6618-136">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="c6618-137">Le trafic DNS interne (port 53) est autorisé</span><span class="sxs-lookup"><span data-stu-id="c6618-137">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="c6618-138">Le trafic RDP (port 3389) à partir d’Internet de hello tooany machine virtuelle est autorisé.</span><span class="sxs-lookup"><span data-stu-id="c6618-138">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="c6618-139">Le trafic HTTP (port 80) à partir du serveur de tooweb hello Internet (IIS01) est autorisé.</span><span class="sxs-lookup"><span data-stu-id="c6618-139">HTTP traffic (port 80) from hello Internet tooweb server (IIS01) is allowed</span></span>
4. <span data-ttu-id="c6618-140">Tout trafic (tous les ports) à partir de IIS01 tooAppVM1 est autorisée.</span><span class="sxs-lookup"><span data-stu-id="c6618-140">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="c6618-141">Tout trafic (tous les ports) à partir de hello Internet toohello réseau virtuel entier (les deux sous-réseaux) est refusé.</span><span class="sxs-lookup"><span data-stu-id="c6618-141">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="c6618-142">Tout trafic (tous les ports) à partir du sous-réseau principal toohello hello frontal sous-réseau est refusé.</span><span class="sxs-lookup"><span data-stu-id="c6618-142">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="c6618-143">Avec ces sous-réseau tooeach dépendant de règles, si une requête HTTP a été entrante à partir de hello toohello le serveur web Internet, les deux règles 3 (autoriser) et 5 (refuser) s’appliquent, mais étant donné que la règle 3 a une priorité plus élevée s’appliquerait et règle 5 ne serait pas entrent en jeu.</span><span class="sxs-lookup"><span data-stu-id="c6618-143">With these rules bound tooeach subnet, if an HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="c6618-144">Par conséquent, demande HTTP de hello serait autorisée serveur web de toohello.</span><span class="sxs-lookup"><span data-stu-id="c6618-144">Thus hello HTTP request would be allowed toohello web server.</span></span> <span data-ttu-id="c6618-145">Si ce trafic même a essayé de serveur de DNS01 tooreach hello, règle 5 (Deny) serait hello premier tooapply hello le trafic et ne serait pas autorisé toopass toohello serveur.</span><span class="sxs-lookup"><span data-stu-id="c6618-145">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="c6618-146">Règle 6 (Deny) bloque le sous-réseau frontal hello communique avec le sous-réseau du serveur principal toohello (à l’exception du trafic autorisé dans les règles 1 et 4), cet ensemble de règles protège le réseau principal de hello au cas où une personne malveillante compromet hello application web sur hello serveur frontal, serait de personne malveillante de hello limitée toohello d’accès réseau (uniquement tooresources exposée sur le serveur de AppVM01 hello) principal « protégé ».</span><span class="sxs-lookup"><span data-stu-id="c6618-146">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="c6618-147">Il existe une règle sortante par défaut qui autorise le trafic sortant toohello internet.</span><span class="sxs-lookup"><span data-stu-id="c6618-147">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="c6618-148">Pour cet exemple, nous allons autoriser le trafic sortant sans modifier les règles de trafic sortant.</span><span class="sxs-lookup"><span data-stu-id="c6618-148">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="c6618-149">tooapply sécurité stratégie tootraffic dans les deux sens, utilisateur défini par routage est obligatoire et est exploré dans « Exemple 3 » sur hello [Page meilleures pratiques de sécurité limite][HOME].</span><span class="sxs-lookup"><span data-stu-id="c6618-149">tooapply security policy tootraffic in both directions, User Defined Routing is required and is explored in “Example 3” on hello [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="c6618-150">Chaque règle est décrite plus en détail comme suit :</span><span class="sxs-lookup"><span data-stu-id="c6618-150">Each rule is discussed in more detail as follows:</span></span>

1. <span data-ttu-id="c6618-151">Une ressource de groupe de sécurité réseau doit être instancié toohold hello règles :</span><span class="sxs-lookup"><span data-stu-id="c6618-151">A Network Security Group resource must be instantiated toohold hello rules:</span></span>

    ```JSON
    "resources": [
      {
        "apiVersion": "2015-05-01-preview",
        "type": "Microsoft.Network/networkSecurityGroups",
        "name": "[variables('NSGName')]",
        "location": "[resourceGroup().location]",
        "properties": { }
      }
    ]
    ``` 

2. <span data-ttu-id="c6618-152">Hello première règle de cet exemple autorise le trafic DNS entre tous les réseaux internes toohello serveur DNS hello principal sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="c6618-152">hello first rule in this example allows DNS traffic between all internal networks toohello DNS server on hello backend subnet.</span></span> <span data-ttu-id="c6618-153">règle de Hello a certains paramètres importants :</span><span class="sxs-lookup"><span data-stu-id="c6618-153">hello rule has some important parameters:</span></span>
  * <span data-ttu-id="c6618-154">« destinationAddressPrefix » - les règles peuvent utiliser un type spécial de préfixe d’adresse appelée une « balise par défaut », ces balises sont des identificateurs fournis par le système qui permettent une tooaddress facilement une catégorie supérieure de préfixes d’adresses.</span><span class="sxs-lookup"><span data-stu-id="c6618-154">"destinationAddressPrefix" - Rules can use a special type of address prefix called a "Default Tag", these tags are system-provided identifiers that allow an easy way tooaddress a larger category of address prefixes.</span></span> <span data-ttu-id="c6618-155">Cette règle utilise hello balise par défaut « Internet » toosignify d’adresses en dehors de hello réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="c6618-155">This rule uses hello Default Tag “Internet” toosignify any address outside of hello VNet.</span></span> <span data-ttu-id="c6618-156">Les autres étiquettes de préfixe sont VirtualNetwork et AzureLoadBalancer.</span><span class="sxs-lookup"><span data-stu-id="c6618-156">Other prefix labels are VirtualNetwork and AzureLoadBalancer.</span></span>
  * <span data-ttu-id="c6618-157">« Direction » indique le sens du trafic qui sera appliqué à cette règle.</span><span class="sxs-lookup"><span data-stu-id="c6618-157">“Direction” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="c6618-158">direction de Hello est hello du point de vue de l’ordinateur virtuel ou le sous-réseau de hello (selon où ce groupe de sécurité réseau est lié).</span><span class="sxs-lookup"><span data-stu-id="c6618-158">hello direction is from hello perspective of hello subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="c6618-159">Par conséquent, si Direction est « Entrant » et le trafic est entrant sous-réseau de hello, hello règle s’applique et le trafic en laissant le sous-réseau de hello ne serait pas affecté par cette règle.</span><span class="sxs-lookup"><span data-stu-id="c6618-159">Thus if Direction is “Inbound” and traffic is entering hello subnet, hello rule would apply and traffic leaving hello subnet would not be affected by this rule.</span></span>
  * <span data-ttu-id="c6618-160">« Priority » définit la commande hello dans lequel un flux de trafic est évalué.</span><span class="sxs-lookup"><span data-stu-id="c6618-160">“Priority” sets hello order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="c6618-161">Hello inférieur hello numéro hello hello prioritaires.</span><span class="sxs-lookup"><span data-stu-id="c6618-161">hello lower hello number hello higher hello priority.</span></span> <span data-ttu-id="c6618-162">Lorsqu’une règle s’applique le flux de trafic spécifique tooa, aucune autre règle n’est traitées.</span><span class="sxs-lookup"><span data-stu-id="c6618-162">When a rule applies tooa specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="c6618-163">Par conséquent, si une règle avec la priorité 1 autorise le trafic et une règle de priorité 2 refuse le trafic et les deux règles s’appliquent tootraffic alors le trafic de hello serait autorisé tooflow (étant donné que la règle 1 a une priorité plus élevée qu’il a pris effet et aucune autre règle n’ont été appliquées).</span><span class="sxs-lookup"><span data-stu-id="c6618-163">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply tootraffic then hello traffic would be allowed tooflow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
  * <span data-ttu-id="c6618-164">« Accès » indique si le trafic concerné par cette règle est bloqué (« Deny ») ou autorisé (« Allow »).</span><span class="sxs-lookup"><span data-stu-id="c6618-164">“Access” signifies if traffic affected by this rule is blocked ("Deny") or allowed ("Allow").</span></span>

    ```JSON
    "properties": {
    "securityRules": [
      {
        "name": "enable_dns_rule",
        "properties": {
          "description": "Enable Internal DNS",
          "protocol": "*",
          "sourcePortRange": "*",
          "destinationPortRange": "53",
          "sourceAddressPrefix": "VirtualNetwork",
          "destinationAddressPrefix": "10.0.2.4",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
    ```

3. <span data-ttu-id="c6618-165">Cette règle permet de tooflow de trafic RDP à partir de port RDP hello internet toohello sur n’importe quel serveur hello lié sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="c6618-165">This rule allows RDP traffic tooflow from hello internet toohello RDP port on any server on hello bound subnet.</span></span> 

    ```JSON
    {
      "name": "enable_rdp_rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "*",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 110,
        "direction": "Inbound"
      }
    },
    ```

4. <span data-ttu-id="c6618-166">Cette règle permet de trafic entrant du trafic toohit hello le serveur web internet.</span><span class="sxs-lookup"><span data-stu-id="c6618-166">This rule allows inbound internet traffic toohit hello web server.</span></span> <span data-ttu-id="c6618-167">Cette règle ne modifie pas le comportement de routage hello.</span><span class="sxs-lookup"><span data-stu-id="c6618-167">This rule does not change hello routing behavior.</span></span> <span data-ttu-id="c6618-168">règle de Hello autorise uniquement le trafic destiné à IIS01 toopass.</span><span class="sxs-lookup"><span data-stu-id="c6618-168">hello rule only allows traffic destined for IIS01 toopass.</span></span> <span data-ttu-id="c6618-169">Par conséquent, si le trafic à partir de hello Internet avait le serveur web de hello comme destination cette règle est autoriser et arrêter le traitement des règles.</span><span class="sxs-lookup"><span data-stu-id="c6618-169">Thus if traffic from hello Internet had hello web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="c6618-170">(Dans la règle hello avec une priorité de 140 tous les autres trafic internet entrant est bloqué).</span><span class="sxs-lookup"><span data-stu-id="c6618-170">(In hello rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="c6618-171">Si vous traitez uniquement le trafic HTTP, cette règle pourrait être plue restreint tooonly autoriser Destination Port 80.</span><span class="sxs-lookup"><span data-stu-id="c6618-171">If you're only processing HTTP traffic, this rule could be further restricted tooonly allow Destination Port 80.</span></span>

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet too[variables('VM01Name')]",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "10.0.1.5",
        "access": "Allow",
        "priority": 120,
        "direction": "Inbound"
        }
      },
    ```

5. <span data-ttu-id="c6618-172">Cette règle permet toopass le trafic à partir du serveur de IIS01 hello toohello AppVM01 serveur, une règle ultérieure bloque tout autre trafic tooBackend de serveur frontal.</span><span class="sxs-lookup"><span data-stu-id="c6618-172">This rule allows traffic toopass from hello IIS01 server toohello AppVM01 server, a later rule blocks all other Frontend tooBackend traffic.</span></span> <span data-ttu-id="c6618-173">tooimprove cette règle, si le port de hello est connu, qui doit être ajoutée.</span><span class="sxs-lookup"><span data-stu-id="c6618-173">tooimprove this rule, if hello port is known that should be added.</span></span> <span data-ttu-id="c6618-174">Par exemple, si le serveur IIS hello accède uniquement à SQL Server sur AppVM01, plage de ports de Destination hello doit être changé de « * » (tout) too1433 (hello port SQL), permettant ainsi une surface d’attaque entrante réduite sur AppVM01 doit hello web application jamais être compromise.</span><span class="sxs-lookup"><span data-stu-id="c6618-174">For example, if hello IIS server is hitting only SQL Server on AppVM01, hello Destination Port Range should be changed from “*” (Any) too1433 (hello SQL port) thus allowing a smaller inbound attack surface on AppVM01 should hello web application ever be compromised.</span></span>

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] too[variables('VM02Name')]",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "10.0.1.5",
        "destinationAddressPrefix": "10.0.2.5",
        "access": "Allow",
        "priority": 130,
        "direction": "Inbound"
      }
    },
     ```

6. <span data-ttu-id="c6618-175">Cette règle refuse le trafic à partir des serveurs de tooany hello internet sur le réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="c6618-175">This rule denies traffic from hello internet tooany servers on hello network.</span></span> <span data-ttu-id="c6618-176">Les règles hello avec une priorité de 110 et 120, effet de hello est tooallow uniquement internet trafic toohello pare-feu entrantes et ports RDP sur les serveurs et bloque tout le reste.</span><span class="sxs-lookup"><span data-stu-id="c6618-176">With hello rules at priority 110 and 120, hello effect is tooallow only inbound internet traffic toohello firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="c6618-177">Cette règle est une « sécurité intégrée » règle tooblock tous les flux inattendues.</span><span class="sxs-lookup"><span data-stu-id="c6618-177">This rule is a "fail-safe" rule tooblock all unexpected flows.</span></span>

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate hello [variables('VNetName')] VNet from hello Internet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "VirtualNetwork",
        "access": "Deny",
        "priority": 140,
        "direction": "Inbound"
      }
    },
     ```

7. <span data-ttu-id="c6618-178">règle finale de Hello refuse le trafic du sous-réseau de hello frontal sous-réseau toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="c6618-178">hello final rule denies traffic from hello Frontend subnet toohello Backend subnet.</span></span> <span data-ttu-id="c6618-179">Étant donné que cette règle est la seule règle de trafic entrant, le trafic inverse est autorisé (à partir de toohello de back-end hello frontal).</span><span class="sxs-lookup"><span data-stu-id="c6618-179">Since this rule is an Inbound only rule, reverse traffic is allowed (from hello Backend toohello Frontend).</span></span>

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate hello [variables('Subnet1Name')] subnet from hello [variables('Subnet2Name')] subnet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "[variables('Subnet1Prefix')]",
        "destinationAddressPrefix": "[variables('Subnet2Prefix')]",
        "access": "Deny",
        "priority": 150,
        "direction": "Inbound"
      }
    }
    ```

## <a name="traffic-scenarios"></a><span data-ttu-id="c6618-180">Scénarios de trafic</span><span class="sxs-lookup"><span data-stu-id="c6618-180">Traffic scenarios</span></span>
#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="c6618-181">(*Autorisées*) Internet tooweb server</span><span class="sxs-lookup"><span data-stu-id="c6618-181">(*Allowed*) Internet tooweb server</span></span>
1. <span data-ttu-id="c6618-182">Un utilisateur internet demande une page HTTP à partir de l’adresse IP publique de hello Hello que NIC associée hello IIS01 NIC</span><span class="sxs-lookup"><span data-stu-id="c6618-182">An internet user requests an HTTP page from hello public IP address of hello NIC associated with hello IIS01 NIC</span></span>
2. <span data-ttu-id="c6618-183">adresse IP publique de Hello passe toohello de trafic réseau virtuel vers IIS01 (serveur web de hello)</span><span class="sxs-lookup"><span data-stu-id="c6618-183">hello Public IP address passes traffic toohello VNet towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="c6618-184">Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="c6618-184">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="c6618-185">Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="c6618-185">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="c6618-186">Règle de groupe de sécurité réseau 2 (RDP) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="c6618-186">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="c6618-187">Règle de groupe de sécurité réseau 3 (tooIIS01 Internet) s’applique, le trafic est le traitement des règles autorisées, arrêter</span><span class="sxs-lookup"><span data-stu-id="c6618-187">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="c6618-188">Le trafic atteint l’adresse IP interne du serveur web de hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="c6618-188">Traffic hits internal IP address of hello web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="c6618-189">IIS01 écoute pour le trafic web, reçoit la requête et démarre le traitement de demande de hello</span><span class="sxs-lookup"><span data-stu-id="c6618-189">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
6. <span data-ttu-id="c6618-190">IIS01 demande hello SQL Server sur AppVM01 pour plus d’informations</span><span class="sxs-lookup"><span data-stu-id="c6618-190">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="c6618-191">Aucune règle sur le trafic sortant sur le sous-réseau du serveur frontal. Le trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="c6618-191">No outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="c6618-192">sous-réseau du serveur principal Hello commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="c6618-192">hello Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="c6618-193">Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="c6618-193">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="c6618-194">Règle de groupe de sécurité réseau 2 (RDP) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="c6618-194">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="c6618-195">Règle de groupe de sécurité réseau 3 (tooFirewall Internet) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="c6618-195">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
  4. <span data-ttu-id="c6618-196">Règle de groupe de sécurité réseau 4 (IIS01 tooAppVM01) s’applique, le trafic est le traitement des règles autorisées, arrêter</span><span class="sxs-lookup"><span data-stu-id="c6618-196">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="c6618-197">AppVM01 reçoit hello requête SQL et répond</span><span class="sxs-lookup"><span data-stu-id="c6618-197">AppVM01 receives hello SQL Query and responds</span></span>
10. <span data-ttu-id="c6618-198">Dans la mesure où il n’y a aucune règles de trafic sortant sur le sous-réseau du serveur principal hello, réponse de hello est autorisée.</span><span class="sxs-lookup"><span data-stu-id="c6618-198">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
11. <span data-ttu-id="c6618-199">Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="c6618-199">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="c6618-200">Il n’existe aucune règle de groupe de sécurité réseau qui applique des tooInbound trafic de sous-réseau du serveur frontal de toohello de sous-réseau hello back-end, donc aucune des règles du groupe de sécurité réseau hello s’appliquent</span><span class="sxs-lookup"><span data-stu-id="c6618-200">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="c6618-201">règle du système par défaut Hello autorisant le trafic entre sous-réseaux permettrait ce trafic donc hello le trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="c6618-201">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
12. <span data-ttu-id="c6618-202">le serveur IIS Hello reçoit la réponse SQL hello et termine la réponse HTTP de hello et envoie toohello demandeur</span><span class="sxs-lookup"><span data-stu-id="c6618-202">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requester</span></span>
13. <span data-ttu-id="c6618-203">Dans la mesure où il n’y a aucune règles de trafic sortant sur le sous-réseau du serveur frontal hello, hello réponse soit autorisée et hello utilisateur Internet reçoit hello web page est demandée.</span><span class="sxs-lookup"><span data-stu-id="c6618-203">Since there are no outbound rules on hello Frontend subnet, hello response is allowed and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-tooiis-server"></a><span data-ttu-id="c6618-204">(*Autorisées*) serveur de tooIIS RDP</span><span class="sxs-lookup"><span data-stu-id="c6618-204">(*Allowed*) RDP tooIIS server</span></span>
1. <span data-ttu-id="c6618-205">Un administrateur de serveur sur internet demande un tooIIS01 de session RDP sur hello adresse IP publique de hello que NIC associée hello NIC IIS01 (cette adresse IP publique accessible via hello portail ou PowerShell)</span><span class="sxs-lookup"><span data-stu-id="c6618-205">A Server Admin on internet requests an RDP session tooIIS01 on hello public IP address of hello NIC associated with hello IIS01 NIC (this public IP address can be found via hello Portal or PowerShell)</span></span>
2. <span data-ttu-id="c6618-206">adresse IP publique de Hello passe toohello de trafic réseau virtuel vers IIS01 (serveur web de hello)</span><span class="sxs-lookup"><span data-stu-id="c6618-206">hello Public IP address passes traffic toohello VNet towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="c6618-207">Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="c6618-207">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="c6618-208">Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="c6618-208">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="c6618-209">La règle NSG 2 (RDP) s’applique, le trafic est autorisé, arrêter le traitement des règles</span><span class="sxs-lookup"><span data-stu-id="c6618-209">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="c6618-210">En l’absence de réseau sortant, les règles par défaut s’appliquent et le retour de trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="c6618-210">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="c6618-211">La Session RDP est activée.</span><span class="sxs-lookup"><span data-stu-id="c6618-211">RDP session is enabled</span></span>
6. <span data-ttu-id="c6618-212">Invites IIS01 hello nom d’utilisateur et mot de passe</span><span class="sxs-lookup"><span data-stu-id="c6618-212">IIS01 prompts for hello user name and password</span></span>

>[!NOTE]
><span data-ttu-id="c6618-213">tooRDP tooany sur les serveurs principaux dans ce cas, le serveur IIS hello est utilisé comme une zone « saut ».</span><span class="sxs-lookup"><span data-stu-id="c6618-213">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="c6618-214">Serveur IIS de première RDP toohello puis à partir de serveur de hello IIS Server RDP toohello principal.</span><span class="sxs-lookup"><span data-stu-id="c6618-214">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="c6618-215">(*Autorisé*) recherche DNS du serveur web sur le serveur DNS</span><span class="sxs-lookup"><span data-stu-id="c6618-215">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="c6618-216">Web des besoins du serveur, IIS01, de flux de données à www.data.gov, mais doit tooresolve hello adresse.</span><span class="sxs-lookup"><span data-stu-id="c6618-216">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="c6618-217">Hello configuration réseau pour les listes de réseau virtuel hello DNS01 (10.0.2.4 sur le sous-réseau du serveur principal hello) en tant que serveur DNS principal de hello, IIS01 envoie hello DNS demande tooDNS01</span><span class="sxs-lookup"><span data-stu-id="c6618-217">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="c6618-218">Aucune règle sur le trafic sortant sur le sous-réseau du serveur frontal. Le trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="c6618-218">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="c6618-219">Le sous-réseau du serveur principal entame le traitement du réseau entrant :</span><span class="sxs-lookup"><span data-stu-id="c6618-219">Backend subnet begins inbound rule processing:</span></span>
  * <span data-ttu-id="c6618-220">La règle NSG 1 (DNS) s’applique, le trafic est autorisé, arrêter le traitement des règles</span><span class="sxs-lookup"><span data-stu-id="c6618-220">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="c6618-221">Serveur DNS reçoit la demande de hello</span><span class="sxs-lookup"><span data-stu-id="c6618-221">DNS server receives hello request</span></span>
6. <span data-ttu-id="c6618-222">Serveur DNS n’a pas adresse hello mis en cache et demande à un serveur DNS racine sur hello internet</span><span class="sxs-lookup"><span data-stu-id="c6618-222">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="c6618-223">Aucune règle sortante sur le sous-réseau du serveur principal, le trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="c6618-223">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="c6618-224">Serveur DNS Internet répond, étant donné que cette session a été lancée en interne, réponse de hello est autorisée.</span><span class="sxs-lookup"><span data-stu-id="c6618-224">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="c6618-225">Le serveur DNS met en cache la réponse de hello et répond tooIIS01 arrière de demande initiale toohello</span><span class="sxs-lookup"><span data-stu-id="c6618-225">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="c6618-226">Aucune règle sortante sur le sous-réseau du serveur principal, le trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="c6618-226">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="c6618-227">Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="c6618-227">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="c6618-228">Il n’existe aucune règle de groupe de sécurité réseau qui applique des tooInbound trafic de sous-réseau du serveur frontal de toohello de sous-réseau hello back-end, donc aucune des règles du groupe de sécurité réseau hello s’appliquent</span><span class="sxs-lookup"><span data-stu-id="c6618-228">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="c6618-229">règle du système par défaut Hello autorisant le trafic entre sous-réseaux permet ce trafic donc hello le trafic est autorisé</span><span class="sxs-lookup"><span data-stu-id="c6618-229">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="c6618-230">IIS01 reçoit hello réponse DNS01</span><span class="sxs-lookup"><span data-stu-id="c6618-230">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="c6618-231">(*Autorisé*) fichier d’accès de serveur Web sur AppVM01</span><span class="sxs-lookup"><span data-stu-id="c6618-231">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="c6618-232">IIS01 demande un fichier sur AppVM01</span><span class="sxs-lookup"><span data-stu-id="c6618-232">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="c6618-233">Aucune règle sur le trafic sortant sur le sous-réseau du serveur frontal. Le trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="c6618-233">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="c6618-234">sous-réseau du serveur principal Hello commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="c6618-234">hello Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="c6618-235">Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="c6618-235">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="c6618-236">Règle de groupe de sécurité réseau 2 (RDP) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="c6618-236">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="c6618-237">Règle de groupe de sécurité réseau 3 (tooIIS01 Internet) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="c6618-237">NSG Rule 3 (Internet tooIIS01) doesn’t apply, move toonext rule</span></span>
  4. <span data-ttu-id="c6618-238">Règle de groupe de sécurité réseau 4 (IIS01 tooAppVM01) s’applique, le trafic est le traitement des règles autorisées, arrêter</span><span class="sxs-lookup"><span data-stu-id="c6618-238">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="c6618-239">AppVM01 reçoit la demande de hello et répond avec le fichier (en supposant que l’accès est autorisé)</span><span class="sxs-lookup"><span data-stu-id="c6618-239">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="c6618-240">Dans la mesure où il n’y a aucune règles de trafic sortant sur le sous-réseau du serveur principal hello, réponse de hello est autorisée.</span><span class="sxs-lookup"><span data-stu-id="c6618-240">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
6. <span data-ttu-id="c6618-241">Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="c6618-241">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="c6618-242">Il n’existe aucune règle de groupe de sécurité réseau qui applique des tooInbound trafic de sous-réseau du serveur frontal de toohello de sous-réseau hello back-end, donc aucune des règles du groupe de sécurité réseau hello s’appliquent</span><span class="sxs-lookup"><span data-stu-id="c6618-242">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="c6618-243">règle du système par défaut Hello autorisant le trafic entre sous-réseaux permettrait ce trafic donc hello le trafic est autorisé.</span><span class="sxs-lookup"><span data-stu-id="c6618-243">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="c6618-244">le serveur IIS Hello reçoit le fichier de hello</span><span class="sxs-lookup"><span data-stu-id="c6618-244">hello IIS server receives hello file</span></span>

#### <a name="denied-rdp-toobackend"></a><span data-ttu-id="c6618-245">(*Refusé*) RDP toobackend</span><span class="sxs-lookup"><span data-stu-id="c6618-245">(*Denied*) RDP toobackend</span></span>
1. <span data-ttu-id="c6618-246">Un utilisateur internet tente de tooRDP tooserver AppVM01</span><span class="sxs-lookup"><span data-stu-id="c6618-246">An internet user tries tooRDP tooserver AppVM01</span></span>
2. <span data-ttu-id="c6618-247">Étant donné qu’aucune adresse IP publique associée à cette carte réseau de serveurs, ce trafic ne doivent jamais entrer hello réseau virtuel et ne fait de joindre le serveur de hello</span><span class="sxs-lookup"><span data-stu-id="c6618-247">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="c6618-248">Toutefois, si une adresse IP publique a été activée pour une raison quelconque, la règle du groupe de sécurité réseau 2 (RDP) autorise ce trafic</span><span class="sxs-lookup"><span data-stu-id="c6618-248">However if a Public IP address was enabled for some reason, NSG rule 2 (RDP) would allow this traffic</span></span>

>[!NOTE]
><span data-ttu-id="c6618-249">tooRDP tooany sur les serveurs principaux dans ce cas, le serveur IIS hello est utilisé comme une zone « saut ».</span><span class="sxs-lookup"><span data-stu-id="c6618-249">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="c6618-250">Serveur IIS de première RDP toohello puis à partir de serveur de hello IIS Server RDP toohello principal.</span><span class="sxs-lookup"><span data-stu-id="c6618-250">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="c6618-251">(*Refusé*) serveur de toobackend Web</span><span class="sxs-lookup"><span data-stu-id="c6618-251">(*Denied*) Web toobackend server</span></span>
1. <span data-ttu-id="c6618-252">Un utilisateur internet tente de tooaccess un fichier sur AppVM01</span><span class="sxs-lookup"><span data-stu-id="c6618-252">An internet user tries tooaccess a file on AppVM01</span></span>
2. <span data-ttu-id="c6618-253">Étant donné qu’aucune adresse IP publique associée à cette carte réseau de serveurs, ce trafic ne doivent jamais entrer hello réseau virtuel et ne fait de joindre le serveur de hello</span><span class="sxs-lookup"><span data-stu-id="c6618-253">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="c6618-254">Si une adresse IP publique a été activée pour une raison quelconque, la règle de groupe de sécurité réseau 5 (tooVNet Internet) susceptibles de bloquer ce trafic</span><span class="sxs-lookup"><span data-stu-id="c6618-254">If a Public IP address was enabled for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="c6618-255">(*Refusé*) recherche DNS web sur le serveur DNS</span><span class="sxs-lookup"><span data-stu-id="c6618-255">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="c6618-256">Un utilisateur internet tente de toolook d’un enregistrement DNS interne sur DNS01</span><span class="sxs-lookup"><span data-stu-id="c6618-256">An internet user tries toolook up an internal DNS record on DNS01</span></span>
2. <span data-ttu-id="c6618-257">Étant donné qu’aucune adresse IP publique associée à cette carte réseau de serveurs, ce trafic ne doivent jamais entrer hello réseau virtuel et ne fait de joindre le serveur de hello</span><span class="sxs-lookup"><span data-stu-id="c6618-257">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="c6618-258">Si une adresse IP publique a été activée pour une raison quelconque, la règle de groupe de sécurité réseau 5 (tooVNet Internet) susceptibles de bloquer ce trafic (Remarque : que règle 1 (DNS) s’appliquera pas car hello demande adresse source est hello internet et 1 de la règle s’applique uniquement toohello réseau local en tant que source de hello)</span><span class="sxs-lookup"><span data-stu-id="c6618-258">If a Public IP address was enabled for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply because hello requests source address is hello internet and Rule 1 only applies toohello local VNet as hello source)</span></span>

#### <a name="denied-sql-access-on-hello-web-server"></a><span data-ttu-id="c6618-259">(*Refusé*) sur le serveur web de hello l’accès à SQL</span><span class="sxs-lookup"><span data-stu-id="c6618-259">(*Denied*) SQL access on hello web server</span></span>
1. <span data-ttu-id="c6618-260">Un utilisateur Internet demande des données SQL à partir de IIS01</span><span class="sxs-lookup"><span data-stu-id="c6618-260">An internet user requests SQL data from IIS01</span></span>
2. <span data-ttu-id="c6618-261">Étant donné qu’aucune adresse IP publique associée à cette carte réseau de serveurs, ce trafic ne doivent jamais entrer hello réseau virtuel et ne fait de joindre le serveur de hello</span><span class="sxs-lookup"><span data-stu-id="c6618-261">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="c6618-262">Si une adresse IP publique a été activée pour une raison quelconque, sous-réseau du serveur frontal hello commence le traitement de la règle de trafic entrant :</span><span class="sxs-lookup"><span data-stu-id="c6618-262">If a Public IP address was enabled for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="c6618-263">Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="c6618-263">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="c6618-264">Règle de groupe de sécurité réseau 2 (RDP) ne s’applique pas, déplacer toonext règle</span><span class="sxs-lookup"><span data-stu-id="c6618-264">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="c6618-265">Règle de groupe de sécurité réseau 3 (tooIIS01 Internet) s’applique, le trafic est le traitement des règles autorisées, arrêter</span><span class="sxs-lookup"><span data-stu-id="c6618-265">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="c6618-266">Le trafic atteint l’adresse IP interne de hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="c6618-266">Traffic hits internal IP address of hello IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="c6618-267">IIS01 n’est pas à l’écoute sur le port 1433, par conséquent, aucune demande toohello de réponse</span><span class="sxs-lookup"><span data-stu-id="c6618-267">IIS01 isn't listening on port 1433, so no response toohello request</span></span>

## <a name="conclusion"></a><span data-ttu-id="c6618-268">Conclusion</span><span class="sxs-lookup"><span data-stu-id="c6618-268">Conclusion</span></span>
<span data-ttu-id="c6618-269">Cet exemple est un moyen relativement simple et direct d’isoler le sous-réseau principal hello le trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="c6618-269">This example is a relatively simple and straight forward way of isolating hello back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="c6618-270">Vous trouverez d’autres exemples et une vue d’ensemble des frontières de sécurité réseau [ici][HOME].</span><span class="sxs-lookup"><span data-stu-id="c6618-270">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="c6618-271">Références</span><span class="sxs-lookup"><span data-stu-id="c6618-271">References</span></span>
### <a name="azure-resource-manager-template"></a><span data-ttu-id="c6618-272">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c6618-272">Azure Resource Manager template</span></span>
<span data-ttu-id="c6618-273">Cet exemple utilise un modèle Azure Resource Manager prédéfini dans un référentiel GitHub maintenu par Microsoft et ouvrez toohello Communauté.</span><span class="sxs-lookup"><span data-stu-id="c6618-273">This example uses a predefined Azure Resource Manager template in a GitHub repository maintained by Microsoft and open toohello community.</span></span> <span data-ttu-id="c6618-274">Ce modèle peut être déployé directement GitHub, ou téléchargé et modifié toofit à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="c6618-274">This template can be deployed straight out of GitHub, or downloaded and modified toofit your needs.</span></span> 

<span data-ttu-id="c6618-275">les modèles principal Hello sont dans le fichier hello nommé « azuredeploy.json ».</span><span class="sxs-lookup"><span data-stu-id="c6618-275">hello main template is in hello file named "azuredeploy.json."</span></span> <span data-ttu-id="c6618-276">Ce modèle peut être envoyé via PowerShell ou CLI (avec le fichier de « azuredeploy.parameters.json » associé de hello) toodeploy ce modèle.</span><span class="sxs-lookup"><span data-stu-id="c6618-276">This template can be submitted via PowerShell or CLI (with hello associated "azuredeploy.parameters.json" file) toodeploy this template.</span></span> <span data-ttu-id="c6618-277">Je pense que hello plus simple est de façon toouse hello « Déployer tooAzure » sur bouton hello README.md page à GitHub.</span><span class="sxs-lookup"><span data-stu-id="c6618-277">I find hello easiest way is toouse hello "Deploy tooAzure" button on hello README.md page at GitHub.</span></span>

<span data-ttu-id="c6618-278">modèle hello toodeploy qui génère cet exemple à partir de GitHub et hello portail Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c6618-278">toodeploy hello template that builds this example from GitHub and hello Azure portal, follow these steps:</span></span>

1. <span data-ttu-id="c6618-279">À partir d’un navigateur, accédez à toohello [modèle][Template]</span><span class="sxs-lookup"><span data-stu-id="c6618-279">From a browser, navigate toohello [Template][Template]</span></span>
2. <span data-ttu-id="c6618-280">Cliquez sur le bouton de « Déployer tooAzure » hello (ou bouton toosee une représentation graphique de ce modèle de hello « Visualiser »)</span><span class="sxs-lookup"><span data-stu-id="c6618-280">Click hello "Deploy tooAzure" button (or hello "Visualize" button toosee a graphical representation of this template)</span></span>
3. <span data-ttu-id="c6618-281">Puis entrez hello compte de stockage, le nom d’utilisateur et mot de passe dans le panneau de paramètres hello **OK**</span><span class="sxs-lookup"><span data-stu-id="c6618-281">Enter hello Storage Account, User Name, and Password in hello Parameters blade, then click **OK**</span></span>
5. <span data-ttu-id="c6618-282">Créez un groupe de ressources pour ce déploiement (vous pouvez utiliser un groupe existant, mais il est recommandé d'en créer un nouveau pour obtenir de meilleurs résultats)</span><span class="sxs-lookup"><span data-stu-id="c6618-282">Create a Resource Group for this deployment (You can use an existing one, but I recommend a new one for best results)</span></span>
6. <span data-ttu-id="c6618-283">Si nécessaire, modifiez les paramètres d’abonnement et l’emplacement hello pour votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="c6618-283">If necessary, change hello Subscription and Location settings for your VNet.</span></span>
7. <span data-ttu-id="c6618-284">Cliquez sur **passez en revue les conditions juridiques**, lisez les termes du contrat de hello, puis cliquez sur **achat** tooagree.</span><span class="sxs-lookup"><span data-stu-id="c6618-284">Click **Review legal terms**, read hello terms, and click **Purchase** tooagree.</span></span>
8. <span data-ttu-id="c6618-285">Cliquez sur **créer** déploiement de hello toobegin de ce modèle.</span><span class="sxs-lookup"><span data-stu-id="c6618-285">Click **Create** toobegin hello deployment of this template.</span></span>
9. <span data-ttu-id="c6618-286">Une fois le déploiement de hello se termine correctement, accédez à toohello que groupe de ressources créé pour ce déploiement toosee hello les ressources configurées à l’intérieur.</span><span class="sxs-lookup"><span data-stu-id="c6618-286">Once hello deployment finishes successfully, navigate toohello Resource Group created for this deployment toosee hello resources configured inside.</span></span>

>[!NOTE]
><span data-ttu-id="c6618-287">Ce modèle permet de RDP toohello IIS01 serveur uniquement (hello Rechercher adresse IP publique pour IIS01 sur hello portail).</span><span class="sxs-lookup"><span data-stu-id="c6618-287">This template enables RDP toohello IIS01 server only (find hello Public IP for IIS01 on hello Portal).</span></span> <span data-ttu-id="c6618-288">tooRDP tooany sur les serveurs principaux dans ce cas, le serveur IIS hello est utilisé comme une zone « saut ».</span><span class="sxs-lookup"><span data-stu-id="c6618-288">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="c6618-289">Serveur IIS de première RDP toohello puis à partir de serveur de hello IIS Server RDP toohello principal.</span><span class="sxs-lookup"><span data-stu-id="c6618-289">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

<span data-ttu-id="c6618-290">tooremove cette suppression hello du déploiement, groupe de ressources et toutes les ressources enfants seront également supprimés.</span><span class="sxs-lookup"><span data-stu-id="c6618-290">tooremove this deployment, delete hello Resource Group and all child resources will also be deleted.</span></span>

#### <a name="sample-application-scripts"></a><span data-ttu-id="c6618-291">Exemples de scripts d’application</span><span class="sxs-lookup"><span data-stu-id="c6618-291">Sample application scripts</span></span>
<span data-ttu-id="c6618-292">Une fois le modèle de hello s’exécute correctement, vous pouvez définir les serveur web de hello et le serveur d’applications avec un tooallow d’application web simple test avec cette configuration de réseau de périmètre.</span><span class="sxs-lookup"><span data-stu-id="c6618-292">Once hello template runs successfully, you can set up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span> <span data-ttu-id="c6618-293">tooinstall un exemple d’application pour ce, ainsi que d’autres exemples de réseau de périmètre, un a été fourni au lien de hello : [Application exemple de Script][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="c6618-293">tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6618-294">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c6618-294">Next steps</span></span>

* <span data-ttu-id="c6618-295">Déployer cet exemple</span><span class="sxs-lookup"><span data-stu-id="c6618-295">Deploy this example</span></span>
* <span data-ttu-id="c6618-296">Générer l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="c6618-296">Build hello sample application</span></span>
* <span data-ttu-id="c6618-297">Tester différents flux de trafic via cette zone DMZ</span><span class="sxs-lookup"><span data-stu-id="c6618-297">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "Zone DMZ avec groupe de sécurité réseau (NSG)"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md