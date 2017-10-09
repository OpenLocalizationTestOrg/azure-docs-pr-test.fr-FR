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
# <a name="example-3--build-a-dmz-tooprotect-networks-with-a-firewall-udr-and-nsg"></a>Exemple 3 : créer un réseau de périmètre tooProtect réseaux avec un pare-feu, UDR et groupe de sécurité réseau
[Retour toohello Page meilleures pratiques de sécurité limite][HOME]

Cet exemple va créer un réseau de périmètre avec un pare-feu, quatre serveurs Windows, Routage défini par l’utilisateur (UDR), Transfert IP et groupes de sécurité réseau. Il vous guide également dans chacun des hello des commandes tooprovide une meilleure compréhension de chaque étape. Il existe également un scénario de trafic section tooprovide un détaillées étape par étape comment le trafic passe par le biais des couches de défense dans hello hello réseau de périmètre. Enfin, dans la section des références hello est code complet de hello et instruction toobuild cette tootest d’environnement et de faire des essais avec différents scénarios. 

![Zone DMZ bidirectionnelle avec NVA, NSG et UDR][1]

## <a name="environment-setup"></a>Configuration de l’environnement
Dans cet exemple, il existe un abonnement qui contient les éléments suivants de hello :

* Trois services cloud : « SecSvc001 », « FrontEnd001 » et « BackEnd001 »
* Un réseau virtuel « CorpNetwork », avec trois sous-réseaux : « SecNet », « FrontEnd » et « BackEnd »
* Un réseau virtuel, dans cet exemple, un pare-feu, connecté toohello SecNet sous-réseau
* un serveur Windows Server représentant un serveur web d’application (« IIS01 »),
* Deux serveurs Windows Server qui représentent les serveurs principaux d’applications (« AppVM01 », « AppVM02 »)
* Un serveur Windows Server qui représente un serveur DNS (« DNS01 »),

Dans la section des références hello ci-dessous, il existe un script PowerShell qui générera la plupart des environnement hello décrite ci-dessus. Machines virtuelles de génération hello et réseaux virtuels, bien que s’effectuent par le script d’exemple hello, ne sont pas décrits en détail dans ce document.

environnement de hello toobuild :

1. Fichier hello réseau config xml figurant dans la section de références hello (mis à jour avec les noms, l’emplacement et scénario de hello donné toomatch IP adresses)
2. Variables utilisateur hello script toomatch hello environnement hello de script de mise à jour hello est toobe exécutée (abonnements, les noms de service, etc.)
3. Exécutez le script de hello dans PowerShell

**Remarque**: région hello signifiée Bonjour script PowerShell doit correspondre à la région hello signifiée dans le fichier xml de configuration de réseau hello.

Une fois hello script s’exécute correctement fallu hello postérieur au script comme suit :

1. Configurez des règles de pare-feu hello, celle-ci est décrite dans la section hello ci-dessous intitulée : Description de règle de pare-feu.
2. Si vous le souhaitez dans la section des références de hello sont deux tooset de scripts de serveur web de hello et le serveur d’applications à un tooallow d’application web simple test avec cette configuration de réseau de périmètre.

Une fois hello script s’exécute correctement les règles de pare-feu hello devez toobe terminée, celle-ci est décrite dans la section hello intitulée : règles de pare-feu.

## <a name="user-defined-routing-udr"></a>Itinéraire défini par l’utilisateur (UDR)
Par défaut, hello suivant les itinéraires du système est définie en tant que :

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

Hello VNETLocal est toujours des préfixes d’adresse hello défini de hello réseau virtuel pour ce réseau spécifique (c.-à-d. qu’il ne pourra tooVNet de réseau virtuel en fonction de la façon dont chaque réseau virtuel spécifique est définie). les itinéraires système restantes Hello sont statiques et par défaut comme indiqué ci-dessus.

Comme pour la priorité, les itinéraires sont traités via la méthode de correspondance de préfixe plus longue (locales) hello, ainsi hello itinéraire plus spécifique dans la table de hello appliquerait tooa adresse de destination donnée.

Par conséquent, le trafic du (par exemple serveur toohello DNS01, 10.0.2.4) pour le réseau local de hello (10.0.0.0/16) serait routé sur la destination de tooits hello réseau virtuel en raison de l’itinéraire de 10.0.0.0/16 toohello. En d’autres termes, pour 10.0.2.4, hello 10.0.0.0/16 itinéraire est hello plus spécifique, bien que 0.0.0.0/0 et hello 10.0.0.0/8 pourraient s’appliquent également, mais dans la mesure où elles sont moins spécifiques qu’ils n’affectent pas ce trafic. Par conséquent, hello trafic too10.0.2.4 aurait un saut suivant de hello réseau virtuel local et transmettre simplement toohello destination.

Si le trafic a été conçu pour 10.1.1.1, par exemple, itinéraire de 10.0.0.0/16 hello semblent ne s’appliquent pas, mais hello 10.0.0.0/8 serait hello plus spécifique, et ce trafic hello serait supprimé (« dipositif noir »), car le saut suivant de hello est Null. 

Si destination de hello n’avez pas appliqué tooany de préfixes d’espaces Null hello ou les préfixes VNETLocal hello, puis suivez les hello moins spécifique Router, 0.0.0.0/0 et être acheminée toohello Internet en tant que tronçon suivant de hello et donc à bord d’internet d’Azure.

S’il existe deux préfixes identiques dans la table d’itinéraires hello, hello Voici hello ordre de préférence basé sur l’attribut de « source » itinéraires hello :

1. « VirtualAppliance » = une toohello ajoutés manuellement la table défini par l’utilisateur un itinéraire
2. « VPNGateway » = un itinéraire dynamique BGP (Border lorsqu’il est utilisé avec les réseaux hybrides), ajouté par un protocole réseau dynamique, ces itinéraires peuvent changer au fil du temps comme protocole dynamique de hello reflète automatiquement les modifications dans les ressources réseau
3. « Default » = hello système itinéraires, hello entrées statiques hello et de réseau virtuel locales, comme indiqué dans la table d’itinéraires hello ci-dessus.

> [!NOTE]
> Vous pouvez maintenant utiliser le routage défini par utilisateur (UDR) avec tooforce ExpressRoute et les passerelles VPN sortante et entrantes entre différents locaux trafic appliance virtuelle toobe tooa routé réseau (NVA).
> 
> 

#### <a name="creating-hello-local-routes"></a>Création d’itinéraires locaux hello
Dans cet exemple, deux tables de routage sont nécessaires, un pour chacun des sous-réseaux de frontales et principales hello. Chaque table est chargée avec des itinéraires statiques appropriés pour hello donné de sous-réseau. Pour les besoins de hello de cet exemple, chaque table possède trois itinéraires :

1. Trafic de sous-réseau local sans tronçon suivant défini tooallow sous-réseau local du trafic toobypass hello pare-feu
2. Le trafic réseau virtuel avec un tronçon suivant défini en tant que pare-feu, cette règle par défaut hello permettant directement tooroute de trafic de réseau virtuel local est ignoré
3. Trafic de tous les autres (0/0) avec un tronçon suivant défini comme hello pare-feu

Après avoir créé les tables de routage hello, elles sont liées tootheir sous-réseaux. Pour la table routage hello frontal sous-réseau, une fois créé et lié toohello sous-réseau doit ressembler à ceci :

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active 
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active


Pour cet exemple, commandes sont utilisés toobuild la table d’itinéraires hello hello suivantes, ajoutez un itinéraire défini par l’utilisateur et lier sous-réseau de tooa hello itinéraire table (Remarque ; tous les éléments ci-dessous commençant par un signe dollar (par exemple : $BESubnet) sont des variables définies par l’utilisateur à partir de script hello Hello section de référence de ce document) :

1. Première table de routage base hello doit être créé. Cet extrait de code illustre la création de table hello pour le sous-réseau du serveur principal hello hello. Dans le script de hello, une table correspondante est également créée pour le sous-réseau du serveur frontal hello.
   
     New-AzureRouteTable -Name $BERouteTableName `
   
         -Location $DeploymentLocation `
         -Label "Route table for $BESubnet subnet"
2. Une fois la table d’itinéraires hello est créée, les itinéraires définis par l’utilisateur spécifiques peuvent être ajoutés. Dans cet extrait, tout le trafic (0.0.0.0/0) sera routé par le biais d’appareil virtuel hello (une variable, $VMIP [0], est toopass utilisé dans l’adresse IP de hello affecté lors de l’appliance virtuelle hello créé précédemment dans le script de hello). Dans le script de hello, une règle correspondante est également créée dans la table du serveur frontal hello.
   
     Get-AzureRouteTable $BERouteTableName | `
   
         Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
         -NextHopType VirtualAppliance `
         -NextHopIpAddress $VMIP[0]
3. Hello ci-dessus entrée d’itinéraire remplace l’itinéraire par défaut « 0.0.0.0/0 » hello, mais règle de 10.0.0.0/16 par défaut hello toujours existante qui permettrait et du trafic au sein de tooroute de réseau virtuel hello directement toohello destination pas toohello Appliance virtuelle de réseau. toocorrect que cette règle de suivi hello comportement doit être ajoutée.
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
4. À ce stade est un toobe choix effectué. Tout le trafic achemine avec hello ci-dessus deux itinéraires pare-feu toohello pour l’évaluation, même le trafic au sein d’un sous-réseau unique. Cela peut s’avérer utile, mais tooallow le trafic au sein d’un tooroute sous-réseau localement sans l’intervention de pare-feu hello une troisième règle très spécifique peut être ajoutée. Cet itinéraire États destine de n’importe quelle adresse de sous-réseau local de hello peut être simplement il acheminer directement (type de tronçon suivant = VNETLocal).
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
5. Enfin, avec hello table de routage créés et remplis avec une itinéraires définis par l’utilisateur, table de hello doit maintenant être lié tooa sous-réseau. Dans le script de hello, table d’itinéraires hello frontal est également lié toohello sous-réseau frontal. Voici le script de liaison hello pour le sous-réseau de back-end hello.
   
     Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
   
        -SubnetName $BESubnet `
        -RouteTableName $BERouteTableName

## <a name="ip-forwarding"></a>transfert IP
Un tooUDR de fonctionnalité d’accompagnement, est le transfert IP. Il s’agit d’un paramètre sur une Appliance virtuelle qui autorise le trafic de tooreceive ne sont pas spécifiquement traités toohello appliance et puis transférer cette destination finale tooits de trafic.

Par exemple, si le trafic à partir de AppVM01 rend un serveur demande toohello DNS01 UDR acheminent ce pare-feu toohello. Avec le transfert IP activé, le trafic de hello pour la destination de DNS01 hello (10.0.2.4) sera accepté par l’application hello (10.0.0.4) et ensuite transmis tooits sa destination finale (10.0.2.4). Sans le transfert IP activé sur hello pare-feu, le trafic ne serait pas accepté par appliance de hello même si la table d’itinéraires hello a pare-feu hello en tant que tronçon suivant de hello. 

> [!IMPORTANT]
> Il est critique tooremember tooenable le transfert IP conjointement avec l’utilisateur définie par le routage.
> 
> 

La configuration du transfert IP est une commande unique et peut être exécutée au moment de la création d’une machine virtuelle. Pourquoi flux de cet extrait de code exemple hello est vers fin hello du script de hello et regroupé avec les commandes UDR hello :

1. Appeler l’instance de machine virtuelle hello qui est votre appliance virtuelle, hello pare-feu dans ce cas et activer le transfert IP (Remarque ; un élément de début rouge avec un signe dollar (par exemple : $VMName[0]) est une variable définie par l’utilisateur à partir du script hello dans la section de référence hello de ce document. Hello zéro entre crochets, [0] représente hello première machine virtuelle dans le tableau hello toowork de script d’exemple hello sans modification de machines virtuelles, hello premier ordinateur virtuel (VM 0) doit être hello pare-feu) :
   
     Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | `
   
        Set-AzureIPForwarding -Enable

## <a name="network-security-groups-nsg"></a>Groupes de sécurité réseau (NSG)
Dans cet exemple, un groupe NSG est créé, puis chargé avec une seule règle. Ce groupe est ensuite lié uniquement toohello frontales et principales sous-réseaux (pas hello SecNet). Déclarative hello règle est en cours de génération :

1. Tout trafic (tous les ports) à partir de hello Internet toohello réseau virtuel entier (tous les sous-réseaux) est refusé.

Bien que dans cet exemple, on utilise des NSG, son principal objectif est celui d’une couche secondaire de défense contre les erreurs de configuration manuelle. Nous souhaitons tooblock tooeither hello serveur frontal de hello internet le trafic entrant de tous les ou principal des sous-réseaux, le trafic doivent uniquement transitent par hello pare-feu de toohello SecNet sous-réseau (et ensuite, si nécessaire sur toohello frontal ou principal sous-réseaux). De plus, avec des règles UDR hello en place, tout le trafic qui faites-en hello sous-réseaux frontal ou serveur principal serait dirigé out toohello pare-feu (Merci tooUDR). pare-feu de Hello verriez cela comme un flux asymétrique et tomberaient le trafic sortant de hello. Par conséquent, il existe trois couches de hello de protection de sécurité serveur frontal et principal sous-réseaux ; aucun des points de terminaison ouverts sur hello FrontEnd001 et des services de cloud BackEnd001, 2) groupes de sécurité réseau refuser le trafic à partir de 1) hello Internet, pare-feu hello (3) la suppression du trafic asymétrique.

Un point intéressant concernant hello groupe de sécurité réseau dans cet exemple est qu’il contient une seule règle, illustrée ci-dessous, qui est toodeny internet trafic toohello réseau virtuel entier qui comprend le sous-réseau de sécurité hello. 

    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet `
        from hello Internet" `
        -Type Inbound -Priority 100 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *

Toutefois, étant donné que hello NSG n’est lié toohello serveur frontal et principal sous-réseaux, règle de hello n’est pas traitée sur le trafic entrant de sous-réseau de sécurité toohello. Par conséquent, même si la règle de groupe de sécurité réseau hello n’indique aucune adresse tooany du trafic Internet sur le réseau virtuel, de hello car hello que NSG n’a jamais été lié sous-réseau de sécurité toohello, le trafic circule de sous-réseau de sécurité toohello.

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $FESubnet -VirtualNetworkName $VNetName

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $BESubnet -VirtualNetworkName $VNetName

## <a name="firewall-rules"></a>Règles de pare-feu
Sur le pare-feu hello, règles de transfert devez toobe créé. Étant donné que les pare-feu hello est le trafic de blocage ou transfert tout entrant, sortant et intra-réseau virtuel de règles de pare-feu sont nécessaires. En outre, tout le trafic entrant sera atteint adresse IP publique de hello Service de sécurité (sur des ports différents), toobe traitée par le pare-feu hello. Un flux logique de hello toodiagram avant de configurer ultérieurement des sous-réseaux hello et reprise de tooavoid de règles de pare-feu, il est préférable. Bonjour figure suivante est une vue logique de règles de pare-feu hello pour cet exemple :

![Affichage logique de règles de pare-feu de hello][2]

> [!NOTE]
> En fonction de hello Qu'appliance virtuelle de réseau utilisé, les ports de gestion hello peuvent varier. Dans cet exemple, il est fait référence à un pare-feu Barracuda NextGen Firewall utilisant les ports 22, 801 et 807. Veuillez consulter hello appliance fournisseur documentation toofind hello exacte ports utilisés pour la gestion de périphérique hello utilisé.
> 
> 

### <a name="logical-rule-description"></a>Description de la logique de règle
Dans le diagramme de la logique de hello ci-dessus, sous-réseau de sécurité hello n’est pas affiché dans la mesure où le pare-feu de hello est la seule ressource de hello sur ce sous-réseau ce diagramme affiche les règles de pare-feu hello et comment ils logiquement autoriser ou refuser des flux de trafic et pas hello routé chemin d’accès réel. En outre, des ports externes hello sélectionnés pour hello le trafic RDP sont des ports sont plus élevées (8014 – 8026) et ont été toosomewhat sélectionné s’alignent hello a deux octets de l’adresse IP locale de hello pour faciliter la lisibilité (par exemple, l’adresse du serveur local 10.0.1.4 est associé port externe 8014), cependant les ports non conflictuel plus élevées peut être utilisées.

Dans cet exemple, nous avons besoin de 7 types de règles, qui se présentent comme suit :

* Règles externes (pour le trafic entrant) :
  1. Règle de pare-feu de gestion : Cette règle de redirection de l’application autorise les ports de gestion du trafic toopass toohello de l’appliance virtuelle de réseau hello.
  2. Règles de RDP (pour chaque serveur windows) : ces quatre règles (une pour chaque serveur) autorise la gestion de hello des serveurs individuels via RDP. Cela pourrait également regroupé dans une règle en fonction des capacités hello Hello Appliance virtuelle de réseau utilisée.
  3. Règles de trafic d’application : Il existe deux règles de trafic d’Application, hello tout d’abord pour le trafic de hello frontal web et hello seconde pour le trafic de back-end de hello (par exemple, niveau de toodata serveur web). configuration de Hello de ces règles dépendra de l’architecture de réseau hello (où sont placés vos serveurs) et flux de trafic (le trafic hello direction du flux, et quels ports sont utilisés).
     * règle de première Hello permettra de serveur d’applications hello application réelle du trafic tooreach hello. Alors que hello autres règles permettent de sécurité, de gestion, etc., règles d’Application sont ce qu’Autoriser tooaccess d’utilisateurs ou des services externes ou les applications hello. Pour cet exemple, il existe un serveur web sur le port 80, par conséquent, une seule application règle de pare-feu redirige le trafic entrant toohello adresse IP externe, interne adresse IP des serveurs toohello web. Hello redirigé session du trafic serait NAT avait toohello interne au serveur.
     * Hello deuxième règle de trafic d’Application hello règle tooallow hello Web Server tootalk toohello AppVM01 le serveur principal (mais pas AppVM02) via n’importe quel port.
* Règles internes (pour le trafic réseau virtuel interne)
  1. Sortant tooInternet règle : cette règle autorise le trafic à partir de n’importe quel réseau toopass toohello sélectionné réseaux. Cette règle est généralement une règle par défaut déjà présent sur le pare-feu hello, mais dans un état désactivé. Pour cet exemple, cette règle doit être activée.
  2. Règle DNS : Cette règle permet uniquement DNS (port 53) le trafic toopass toohello serveurDNS. Pour cet environnement, la plupart du trafic à partir de hello frontal toohello back-end est bloqué, cette règle permet en particulier DNS à partir de n’importe quel sous-réseau local.
  3. Sous-réseau tooSubnet règle : cette règle est tooallow n’importe quel serveur DOS de hello sous-réseau tooconnect tooany serveur sur le sous-réseau frontal de hello principal (mais pas hello inverse).
* Règle de prévention de défaillance (pour le trafic qui ne correspond pas hello ci-dessus) :
  1. Refuser toutes les règles de trafic : Cela doit toujours être règle finale de hello (en termes de priorité) et par conséquent si un trafic acheminé échoue toomatch des hello précédant les règles, qu'elles seront supprimées par cette règle. Il s’agit d’une règle par défaut qui est en général activée, et en général, aucune modification n’est nécessaire.

> [!TIP]
> Sur la deuxième règle de trafic d’application hello, n’importe quel port n’est autorisée pour cet exemple simple, un Bonjour scénario réel, des plages de port et l’adresse la plus spécifiques doivent être surface d’attaque hello tooreduce utilisés de cette règle.
> 
> 

<br />

> [!IMPORTANT]
> Une fois que tous les hello au-dessus de règles sont créées, il est important priorité hello tooreview chacun le trafic tooensure de règle sera autorisée ou refusée comme vous le souhaitez. Pour cet exemple, les règles de hello sont dans l’ordre de priorité. Il est facile toobe verrouillé hors de pare-feu hello échéance toomis ordonné de règles. Au minimum, assurez-vous de gestion hello pour le pare-feu hello elle-même est toujours de règle de priorité la plus élevée absolu hello.
> 
> 

### <a name="rule-prerequisites"></a>Préalable en matière de règles
Une configuration requise pour le pare-feu de hello hello Machine virtuelle en cours d’exécution sont des points de terminaison publics. Pour le trafic de hello pare-feu tooprocess les points de terminaison publics hello approprié doivent être ouverts. Il existe trois types de trafic dans cet exemple ; (1) gestion du trafic toocontrol hello pare-feu et les règles de pare-feu, les serveurs windows hello RDP (2) le trafic toocontrol et le trafic d’Application (3). Il s’agit hello trois colonnes de types de trafic hello supérieure la moitié de la vue logique de règles de pare-feu hello ci-dessus.

> [!IMPORTANT]
> Un takeway clé ici est tooremember qui **tous les** trafic proviendront via le pare-feu hello. C’est le cas toohello de bureau tooremote IIS01 server, même s’il est Bonjour Service de Cloud Front End et de sous-réseau frontal hello tooaccess ce serveur, nous devons tooRDP toohello pare-feu sur port 8014 et laissez demande RDP hello pare-feu tooroute hello en interne toohello IIS01 le Port RDP. Hello « Se connecter » du portail Azure bouton ne fonctionne pas, car il n’existe aucun tooIIS01 de chemin d’accès RDP direct (pour autant que le portail de hello peut voir). Cela signifie que toutes les connexions à partir de hello internet seront toohello Service de sécurité et un Port, par exemple, secscv001.cloudapp.net:xxxx (hello référence diagramme pour le mappage de Port externe et adresse IP interne et le Port de hello ci-dessus).
> 
> 

Un point de terminaison peuvent être ouverts lors de la création d’ordinateurs virtuels hello ou valider la génération est effectuée dans le script d’exemple hello et indiqué ci-dessous dans cet extrait de code (Remarque ; tout début de l’élément avec un signe dollar (par exemple : $VMName[$i]) est une variable définie par l’utilisateur à partir de script hello hello referen section de ce de ce document. Hello « $i » entre crochets, [$i], représente hello tableau quantité, pour un ordinateur virtuel spécifique dans un tableau d’ordinateurs virtuels) :

    Add-AzureEndpoint -Name "HTTP" -Protocol tcp -PublicPort 80 -LocalPort 80 `
        -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | `
        Update-AzureVM

Bien que pas clairement indiqué ici en raison d’utilisation de toohello de variables, mais les points de terminaison sont **uniquement** ouvert sur hello Service de Cloud de sécurité. Il s’agit de tooensure que tout le trafic entrant est géré (acheminés, NAT avait, supprimée) par le pare-feu hello.

Un client de gestion sera peut-être toobe installé sur un pare-feu de hello toomanage PC et créer des configurations hello nécessaires. Consultez le fournisseur de documentation de votre pare-feu (ou autres NVA) hello sur comment toomanage hello appareil. suite de Hello de cette section et de la section suivante hello, la création de règles de pare-feu, décrit la configuration hello du pare-feu de hello lui-même, via le client de gestion des fournisseurs hello (c'est-à-dire, non hello portail Azure ou PowerShell).

Instructions de téléchargement du client et de connexion toohello Barracuda utilisé dans cet exemple se trouve ici : [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)

Une fois connecté sur le pare-feu hello mais avant de créer des règles de pare-feu, il existe deux classes d’objet requis qui peuvent faciliter la création de règles hello ; Objets de Service et de réseau.

Pour cet exemple, trois objets réseau nommé doivent être défini (un pour le sous-réseau du serveur frontal hello et sous-réseau du serveur principal hello, également un objet réseau pour l’adresse IP de hello du serveur DNS de hello). toocreate un réseau nommé ; à partir du tableau de bord hello Barracuda NG administrateur client, accédez d’onglet de configuration toohello, dans la section de Configuration opérationnelle de hello cliquez sur le groupe de règles, puis cliquez sur « Réseaux » sous le menu des objets de pare-feu hello, puis cliquez sur Nouveau dans le menu de modifier des réseaux hello. objet de réseau Hello peut maintenant être créé, en ajoutant le nom de la hello et un préfixe de hello :

![Créer un objet réseau de serveur frontal][3]

Cette opération crée un réseau nommé pour le sous-réseau du serveur frontal hello, un objet similaire doit être créé pour hello principal sous-réseau. Maintenant les sous-réseaux hello peuvent être plus facilement référencées par son nom dans les règles de pare-feu hello.

Pourquoi objet serveur DNS :

![Créer un objet de serveur DNS][4]

Cette référence d’adresse IP unique sera utilisée dans une règle DNS plus loin dans le document de hello.

les objets requis deuxième Hello sont des objets de Services. Ces représentent des ports de connexion RDP hello pour chaque serveur. Étant donné que l’objet de service RDP hello existant est le port RDP toohello liée par défaut, 3389, nouveaux Services peuvent être créés tooallow trafic à partir des ports externes hello (8014-8026). Hello nouveaux ports peuvent également être ajoutées à service RDP toohello existant, mais pour faciliter la démonstration, vous pouvez créer une règle individuelle pour chaque serveur. toocreate une nouvelle règle RDP pour un serveur ; démarrage à partir du tableau de bord hello Barracuda NG administrateur client, accédez à onglet de configuration toohello, hello Configuration opérationnelle de section cliquez sur le groupe de règles, puis cliquez sur « Services » sous hello menu des objets de pare-feu, défiler la liste hello des services et sélectionnez hello Service « RDP ». Effectuez un clic droit et sélectionnez Copier, puis avec le bouton droit, cliquez et sélectionnez Coller. Il existe désormais un objet de Service RDP-Copie1 qui peut être modifié. RDP-Copie1 d’avec le bouton droit et sélectionnez Modifier, hello modifier l’objet Service fenêtre s’affiche comme illustré ici :

![Copie de la règle RDP par défaut][5]

les valeurs Hello peuvent ensuite être modifié toorepresent hello service RDP pour un serveur spécifique. Pour hello AppVM01 ci-dessus par défaut règle RDP doit tooreflect modifié un nouveau nom de Service, Description, et le Port RDP externe utilisé dans hello diagramme de la Figure 8 (Remarque : les ports hello sont modifiés à partir de hello RDP comme valeur par défaut le port 3389 toohello externe qui est utilisé pour ce un serveur spécifique, dans les cas de hello du Port externe de AppVM01 hello est 8025) service modifié hello est indiqué ci-dessous :

![Règle AppVM01][6]

Ce processus doit être répété toocreate Services RDP pour hello restant serveurs ; AppVM02, DNS01 et IIS01. Création de Hello de ces Services permettront à la création de règle hello plus simple et plus évidente dans la section suivante de hello.

> [!NOTE]
> Un service de protocole RDP pour hello pare-feu n’est pas nécessaire pour deux raisons. (1) le premier pare-feu hello VM est une image de Linux en fonction SSH étaient utilisée sur le port 22 pour la gestion des ordinateurs virtuels au lieu de RDP et (2) le port 22 et deux autres ports de gestion sont autorisées dans la première règle de gestion hello décrite ci-dessous tooallow pour la connectivité de gestion.
> 
> 

### <a name="firewall-rules-creation"></a>Création de règles de pare-feu
Il existe trois types de règles de pare-feu utilisées dans cet exemple, et elles sont toutes représentées par des icônes distinctes :

règle de redirection de l’Application Hello : ![l’icône de redirection de l’Application][7]

une règle NAT de Destination Hello : ![icône NAT de Destination][8]

règle de Pass Hello : ![passer une icône][9]

Vous trouverez plus d’informations sur ces règles sur le site web de Barracuda hello.

toocreate hello suivant les règles (ou vérifiez les règles par défaut existant), à partir du tableau de bord hello Barracuda NG administrateur client, accédez d’onglet de configuration toohello, Bonjour Configuration opérationnelle de section, cliquez sur règles. Une grille est appelée, « Règles de Main » affiche hello règles actifs et désactivés sur ce pare-feu existantes. Hello coin supérieur droit de cette grille est une petite, verte « + », sur cette toocreate une nouvelle règle (Remarque : votre pare-feu peut être « verrouillé » pour les modifications, si vous voyez un bouton marqué « Verrouillage » et vous toocreate impossible ou modifiez les règles, cliquez sur ce bouton trop « déverrouiller » hello se de règle t et autoriser la modification). Si vous le souhaitez tooedit une règle existante, sélectionnez cette règle, avec le bouton droit et sélectionnez Modifier la règle.

Une fois vos règles sont créés ou modifiés, ils doivent être envoyées toohello pare-feu et puis activé, si cela n’est pas fait règle hello modifications ne prendront pas effet. processus par émission de données et l’activation de Hello est décrite ci-dessous descriptions de règles de détails hello.

caractéristiques de Hello de chaque règle requis toocomplete cet exemple sont décrits comme suit :

* **Gestion des règles de pare-feu**: redirection de cette application de règle autorise le trafic toopass toohello les ports de gestion de hello network appliance virtuelle, dans cet exemple, un pare-feu de NextGen Barracuda. les ports de gestion Hello sont 801, 807 et éventuellement 22. les ports internes et externes Hello sont hello même (autrement dit, aucune traduction de port). Cette règle, SETUP-MGMT-ACCESS, est une règle par défaut et elle est activée par défaut (dans la version 6.1 du pare-feu Barracuda NextGen Firewall).
  
    ![Règle de gestion de pare-feu][10]

> [!TIP]
> Hello source espace d’adressage dans cette règle est un, si hello connus des plages d’adresses IP gestion, réduire cette étendue permettrait également de limiter les ports de gestion hello attaque toohello aire de conception.
> 
> 

* **Règles de RDP**: les règles NAT de Destination ces permettra gestion Hello des serveurs individuels via RDP.
  Il existe quatre champs critiques nécessaires toocreate cette règle :
  
  1. Source : tooallow RDP à partir de n’importe où, référence hello « Tout » est utilisé dans le champ de Source de hello.
  2. Service – utiliser hello objet approprié de Service créé précédemment, dans ce cas « RDP AppVM01 », des ports externes hello rediriger l’adresse IP locale toohello serveurs et tooport 3386 (hello par défaut le port RDP). Cette règle spécifique est pour RDP accès tooAppVM01.
  3. Destination – doit être hello *port local sur les pare-feu hello*, « IP locale DCHP 1 » ou eth0 si vous utilisez des adresses IP statiques. un nombre ordinal Hello (eth0, eth1, etc.) peut être différent si votre matériel de réseau possède plusieurs interfaces de locales. Hello port envoie le pare-feu hello à partir de (peut-être même hello comme hello port de réception), destination de routage réelle hello est dans le champ de liste cible hello.
  4. La redirection – cette section explique l’appliance virtuelle hello où tooultimately rediriger ce trafic. redirection de la plus simple de Hello est tooplace hello IP et Port (facultatif) dans le champ de liste cible hello. Si aucun port n’est le port de destination hello utilisé sur la demande entrante de hello sera utilisé (c.-à-d. aucune traduction), si un port est désigné port de hello sera également NAT, ainsi que les IP hello réponde.
     
     ![Règle RDP de pare-feu][11]
     
     Un total de quatre règles RDP devez toobe créé : 
     
     | Nom de la règle | Serveur | de diffusion en continu | Liste des cibles |
     | --- | --- | --- | --- |
     | RDP-vers-IIS01 |IIS01 |IIS01 RDP |10.0.1.4:3389 |
     | RDP-vers-DNS01 |DNS01 |DNS01 RDP |10.0.2.4:3389 |
     | RDP 0 AppVM01 |AppVM01 |RDP AppVM01 |10.0.2.5:3389 |
     | RDP-vers-AppVM02 |AppVM02 |AppVm02 RDP |10.0.2.6:3389 |

> [!TIP]
> Restreindre les résultats de portée hello Hello Source et les champs Service réduira la surface d’attaque hello. étendue de Hello plus limitée qui permettra de fonctionnalité doit être utilisée.
> 
> 

* **Règles de trafic d’application**: il existe deux règles de trafic d’Application, hello tout d’abord pour le trafic web de serveur frontal hello et hello seconde pour le trafic de back-end hello (par exemple, niveau serveur web toodata). Ces règles dépendent de l’architecture en réseau hello (où sont placés vos serveurs) et flux de trafic (le trafic hello direction du flux, et quels ports sont utilisés).
  
    Tout d’abord indiqué est règle de serveur frontal hello pour le trafic web :
  
    ![Règle web de pare-feu][12]
  
    Cette règle NAT de Destination permet de serveur d’applications hello application réelle du trafic tooreach hello. Alors que hello autres règles permettent de sécurité, de gestion, etc., règles d’Application sont ce qu’Autoriser tooaccess d’utilisateurs ou des services externes ou les applications hello. Pour cet exemple, il existe un serveur web sur le port 80, par conséquent hello seule application règle de pare-feu redirige le trafic entrant toohello adresse IP externe, interne adresse IP des serveurs toohello web.
  
    **Remarque**: qu’il n’existe aucun port assigné dans le champ de liste cible hello, donc hello entrants port 80 (ou 443 pour hello Service sélectionné) sera utilisé dans la redirection de hello du serveur web de hello. Si le serveur web de hello est à l’écoute sur un port différent, par exemple le port 8080, champ de liste cible hello peut-être tooallow too10.0.1.4:8080 mis à jour pour la redirection de Port hello également.
  
    Hello règle de trafic d’Application suivant hello règle tooallow hello Web Server tootalk toohello AppVM01 le serveur principal (mais pas AppVM02) via un service :
  
    ![Règle AppVM01 de pare-feu][13]
  
    Cette règle passe permet de n’importe quel serveur IIS sur Bonjour frontal sous-réseau tooreach Bonjour AppVM01 (adresse IP 10.0.2.5) sur n’importe quel port, à l’aide de toutes les données de tooaccess de protocole requises par l’application web de hello.
  
    Dans cette capture d’écran une «\<explicite-dest\>» est utilisé comme destination de hello dans hello Destination champ toosignify 10.0.2.5. Il peut s’agir soit nommé explicite du comme illustré, ou un objet de réseau (tel qu’il a été effectuée dans les conditions préalables de hello pour le serveur DNS de hello). Il est administrateur toohello du pare-feu de hello comme la méthode toowhich sera utilisée. tooadd 10.0.2.5 comme un Explict Desitnation, double-cliquez sur la première ligne vide hello sous \<explicite-dest\> et entrez l’adresse de hello dans la fenêtre hello qui s’affiche.
  
    Cette règle passer aucun NAT n’est nécessaire car il s’agit le trafic interne, donc hello méthode de connexion peut être défini trop « No SNAT ».
  
    **Remarque**: réseau Source de hello dans cette règle est n’importe quelle ressource de sous-réseau frontal hello si il sera uniquement un, ou un nombre connu spécifique de serveurs web, un objet réseau de ressource peut être créé toobe plus toothose exacte des adresses IP spécifiques à la place de tout sous-réseau du serveur frontal Hello.

> [!TIP]
> Cette règle utilise le service hello « Any » toomake hello toosetup plus facile d’application exemple et utiliser, cela vous permet également de ICMPv4 (ping) dans une seule règle. Toutefois, cela n’est pas recommandé. ports de Hello et protocoles (« Services ») doivent être filtrés toohello possible minimale qui permet la surface d’attaque application opération tooreduce hello sur cette limite.
> 
> 

<br />

> [!TIP]
> Bien que cette règle indique une référence explicite-dest utilisée, une approche cohérente doit être utilisée dans la configuration du pare-feu hello. Il est recommandé d’utiliser tout au long de ce hello nommé d’objet réseau pour faciliter la lisibilité et la prise en charge. Hello explicite-dest est utilisé ici tooshow d’uniquement une méthode autre référence et n’est généralement pas recommandé (en particulier pour des configurations complexes).
> 
> 

* **Sortant tooInternet règle**: passer ce règle autorise le trafic à partir de n’importe quel réseau toopass toohello sélectionné Destination réseaux Source. Cette règle est une règle par défaut généralement déjà sur le pare-feu Barracuda NextGen hello, mais il est dans un état désactivé. Vous pouvez accéder à hello activer la règle commande en cliquant sur cette règle. règle Hello ci-après a été modifiée tooadd hello deux sous-réseaux locaux qui ont été créés en tant que références dans la section Configuration requise de hello de cet attribut de Source de document toohello de cette règle.
  
    ![Règle de trafic sortant de pare-feu][14]
* **Règle de DNS**: règle de passer ce permet uniquement serveur DNS de toohello de toopass DNS (port 53) le trafic. Pour cet environnement, la plupart du trafic à partir de hello frontal toohello back-end est bloqué, cette règle permet en particulier DNS.
  
    ![Règle DNS de pare-feu][15]
  
    **Remarque**: dans cet écran hello shot méthode de connexion est inclus. Étant donné que cette règle est interne toointernal IP adresse du trafic IP, aucune utilisation n’est requise, cette hello méthode de connexion est trop « No SNAT » pour cette règle de test.
* **Sous-réseau tooSubnet règle**: passer cette règle est une règle par défaut qui a été activée et tooallow modifiée n’importe quel serveur sur hello précédent se terminent par serveur de sous-réseau tooconnect tooany hello sous-réseau du serveur frontal. Cette règle étant le trafic interne tout hello méthode de connexion peut être définie tooNo SNAT.
  
    ![Règle Intra-réseau virtuel de pare-feu][16]
  
    **Remarque**: case à cocher hello bidirectionnelle n’est pas vérifiée (et n’est pas activée dans la plupart des règles), c’est important pour cette règle, elle rend cette règle « une seule direction », une connexion peut être lancée à partir de réseau de serveur frontal hello back-end sous-réseau toohello, mais pas hello inverse. Si cette case à cocher est activée, cette règle permet le trafic bidirectionnel, ce qui n’est pas souhaitable pour notre diagramme logique.
* **Refuser toutes les règles de trafic**: cela doit toujours être règle finale de hello (en termes de priorité), et par conséquent si un trafic acheminé échoue toomatch des hello précédant les règles qu’il ne sera supprimé par cette règle. Il s’agit d’une règle par défaut qui est en général activée, et en général, aucune modification n’est nécessaire. 
  
    ![Règle de refus de pare-feu][17]

> [!IMPORTANT]
> Une fois que tous les hello au-dessus de règles sont créées, il est important priorité hello tooreview chacun le trafic tooensure de règle sera autorisée ou refusée comme vous le souhaitez. Pour cet exemple, les règles de hello sont dans l’ordre de hello qu'ils doivent apparaître dans la grille principale règles Bonjour Client de gestion Barracuda de transfert de hello.
> 
> 

## <a name="rule-activation"></a>Activation d’une règle
Hello ruleset modifiée toohello spécification de diagramme logique de hello, hello ruleset doit être téléchargé toohello pare-feu et puis activé.

![Activation de règle de pare-feu][18]

Dans l’angle supérieur droit de hello du client de gestion hello sont un cluster de boutons. Cliquez sur hello « envoyer des modifications » bouton toosend hello modifié règles toohello pare-feu, puis cliquez sur le bouton « Activer » de hello.

L’activation de l’ensemble de règles de pare-feu hello hello cette build d’environnement exemple est terminée.

## <a name="traffic-scenarios"></a>Scénarios de trafic
> [!IMPORTANT]
> Une clé takeway est tooremember qui **tous les** trafic proviendront via le pare-feu hello. C’est le cas toohello de bureau tooremote IIS01 server, même s’il est Bonjour Service de Cloud Front End et de sous-réseau frontal hello tooaccess ce serveur, nous devons tooRDP toohello pare-feu sur port 8014 et laissez demande RDP hello pare-feu tooroute hello en interne toohello IIS01 le Port RDP. Hello « Se connecter » du portail Azure bouton ne fonctionne pas, car il n’existe aucun tooIIS01 de chemin d’accès RDP direct (pour autant que le portail de hello peut voir). Cela signifie que toutes les connexions à partir de hello internet seront toohello Service de sécurité et un Port, par exemple, secscv001.cloudapp.net:xxxx.
> 
> 

Pour ces scénarios, hello suivant les règles de pare-feu doit être en place :

1. Gestion de pare-feu
2. RDP tooIIS01
3. RDP tooDNS01
4. RDP tooAppVM01
5. RDP tooAppVM02
6. Toohello du trafic de l’application Web
7. Le trafic d’application tooAppVM01
8. Sortant toohello Internet
9. Serveur frontal tooDNS01
10. Trafic intra-sous-réseau (fin de toofront back-end uniquement)
11. Refuser tout

groupe de règles de pare-feu Hello aura probablement bien d’autres règles dans toothese d’addition, règles hello sur n’importe quel pare-feu donné aura également les numéros de priorité différents que ceux répertoriés ici hello. Cette liste et les numéros associés sont pertinence tooprovide entre simplement ces onze règles et la priorité relative de hello entre elles. En d’autres termes ; sur le pare-feu hello, hello « RDP tooIIS01 » peut être le numéro de la règle 5, mais à condition qu’il soit sous la règle de « Gestion de pare-feu » hello et versions ultérieures de la règle de « RDP tooDNS01 » hello qu'elle est alignée avec intention de hello de cette liste. liste de Hello vous aide également Bonjour ci-dessous scénarios permettant le souci de concision ; par exemple « Règle de pare-feu 9 (DNS) ». Également par souci de concision, hello quatre règles RDP sera collectivement appelés, « hello règles RDP » lorsque le scénario de trafic hello est tooRDP non liée.

Rappelez-vous également que les groupes de sécurité réseau sont sur place pour le trafic internet entrant sur hello frontal et principal des sous-réseaux.

#### <a name="allowed-internet-tooweb-server"></a>(Autorisé) Internet tooWeb Server
1. Un utilisateur Internet demande une page HTTP en provenance de SecSvc001.CloudApp.Net (Service cloud Internet)
2. Cloud service transmet le trafic via le point de terminaison ouvert sur l’interface toofirewall le port 80 sur 10.0.0.4:80
3. Aucun groupe de sécurité réseau n’assigné tooSecurity sous-réseau, afin d’autorisent les règles du groupe de sécurité réseau système toofirewall de trafic
4. Le trafic atteint l’adresse IP interne du pare-feu de hello (10.0.1.4)
5. Le pare-feu commence le traitement de la règle :
   1. FW règle 1 (FW Mgmt) ne s’applique pas, déplacer toonext règle
   2. Règles 2 à 5 (règles RDP) ne s’appliquent, déplacer toonext règle
   3. FW règle 6 (application : Web) s’applique, le trafic est autorisé, un pare-feu NAT il too10.0.1.4 (IIS01)
6. sous-réseau du serveur frontal Hello commence le traitement de la règle de trafic entrant :
   1. NSG règle 1 (bloc Internet) ne s’applique pas (ce trafic a été NAT serait par le pare-feu hello, donc hello adresse source est maintenant pare-feu hello qui se trouve sur le sous-réseau de sécurité hello et visibles par le sous-réseau du serveur frontal hello trafic de groupe de sécurité réseau toobe « local » et est donc autorisé), déplacer toonext règle
   2. Règles du groupe de sécurité réseau par défaut autoriser le trafic de toosubnet de sous-réseau, le trafic est autorisé, d’arrêter le traitement des règles de groupe de sécurité réseau
7. IIS01 écoute pour le trafic web, reçoit la requête et démarre le traitement de demande de hello
8. IIS01 tente tooinitiates un tooAppVM01 de session FTP sur le sous-réseau du serveur principal
9. itinéraire UDR Hello sur le sous-réseau frontal rend le saut suivant de hello pare-feu hello
10. Aucune règle sur le trafic sortant sur le sous-réseau du serveur frontal. Le trafic est autorisé.
11. Le pare-feu commence le traitement de la règle :
    1. FW règle 1 (FW Mgmt) ne s’applique pas, déplacer toonext règle
    2. FW règle 2-5 (règles RDP) ne s’appliquent pas, déplacer toonext règle
    3. FW règle 6 (application : Web) ne s’appliquent, déplacez la règle de toonext
    4. La règle 7 FW (application : back-end) s’applique, le trafic est autorisé, le pare-feu transmet le trafic too10.0.2.5 (AppVM01)
12. sous-réseau du serveur principal Hello commence le traitement de la règle de trafic entrant :
    1. Groupe de sécurité réseau règle 1 (bloc Internet) ne s’applique pas, déplacer toonext règle
    2. Règles du groupe de sécurité réseau par défaut autoriser le trafic de toosubnet de sous-réseau, le trafic est autorisé, d’arrêter le traitement des règles de groupe de sécurité réseau
13. AppVM01 reçoit la demande de hello et lance la session de hello et répond
14. itinéraire UDR Hello sur le sous-réseau du serveur principal effectue le saut suivant de hello pare-feu hello
15. Dans la mesure où il n’y a aucune règle de groupe de sécurité réseau sortant sur hello réponse de hello sous-réseau principal n’est autorisé.
16. Car cela retourne le trafic sur un pare-feu de hello session établie passe serveur web (IIS01) de hello réponse toohello précédent
17. Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :
    1. Groupe de sécurité réseau règle 1 (bloc Internet) ne s’applique pas, déplacer toonext règle
    2. Règles du groupe de sécurité réseau par défaut autoriser le trafic de toosubnet de sous-réseau, le trafic est autorisé, d’arrêter le traitement des règles de groupe de sécurité réseau
18. Hello IIS reçoit la réponse de hello, termine la transaction hello avec AppVM01 et puis termine la construction hello réponse HTTP, cette réponse HTTP est envoyée toohello demandeur
19. Dans la mesure où il n’y a aucune règle de groupe de sécurité réseau sortant sur hello réponse de hello sous-réseau frontal n’est autorisée.
20. Hello HTTP réponse accès hello pare-feu et car il s’agit de hello tooan de réponse établie session NAT est acceptée par le pare-feu hello
21. les pare-feu Hello redirige ensuite hello réponse toohello précédent utilisateur Internet
22. Dans la mesure où aucune des règles de groupe de sécurité réseau sortantes ou les sauts UDR sur le sous-réseau du serveur frontal hello réponse de hello est autorisé et hello utilisateur Internet reçoit hello web page est demandée.

#### <a name="allowed-internet-rdp-toobackend"></a>(Autorisé) Internet RDP tooBackend
1. Administrateur du serveur sur internet demande tooAppVM01 de session RDP via SecSvc001.CloudApp.Net:8025, où 8025 est numéro de port hello utilisateur affecté pour la règle de pare-feu « RDP tooAppVM01 » hello
2. service de cloud computing Hello transmet le trafic via le point de terminaison ouvert hello sur interface toofirewall port 8025 10.0.0.4:8025
3. Aucun groupe de sécurité réseau n’assigné tooSecurity sous-réseau, afin d’autorisent les règles du groupe de sécurité réseau système toofirewall de trafic
4. Le pare-feu commence le traitement de la règle :
   1. FW règle 1 (FW Mgmt) ne s’applique pas, déplacer toonext règle
   2. FW règle 2 (RDP IIS) ne s’applique pas, déplacer toonext règle
   3. FW règle 3 (DNS01 RDP) ne s’applique pas, déplacer toonext règle
   4. FW règle 4 (AppVM01 RDP) s’applique, le trafic est autorisé, un pare-feu NAT il too10.0.2.5:3386 (port RDP sur AppVM01)
5. sous-réseau du serveur principal Hello commence le traitement de la règle de trafic entrant :
   1. NSG règle 1 (bloc Internet) ne s’applique pas (ce trafic a été NAT serait par le pare-feu hello, donc hello adresse source est maintenant pare-feu hello qui se trouve sur le sous-réseau de sécurité hello et visibles par le sous-réseau principal de hello trafic de groupe de sécurité réseau toobe « local » et est donc autorisé), déplacer toonext règle
   2. Règles du groupe de sécurité réseau par défaut autoriser le trafic de toosubnet de sous-réseau, le trafic est autorisé, d’arrêter le traitement des règles de groupe de sécurité réseau
6. AppVM01 est à l’écoute du trafic RDP et répond
7. En l’absence de règle NSG sur le trafic sortant, les règles par défaut s’appliquent et le retour de trafic est autorisé.
8. Pare-feu de toohello UDR itinéraires du trafic sortant en tant que tronçon suivant de hello
9. Car cela retourne le trafic sur un pare-feu de hello session établie passe utilisateur internet de hello réponse toohello précédent
10. La Session RDP est activée.
11. AppVM01 demande le mot de passe utilisateur

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a>(Autorisé) recherche DNS du serveur web sur le serveur DNS
1. Web des besoins du serveur, IIS01, de flux de données à www.data.gov, mais doit tooresolve hello adresse.
2. Hello configuration réseau pour les listes de réseau virtuel hello DNS01 (10.0.2.4 sur le sous-réseau du serveur principal hello) en tant que serveur DNS principal de hello, IIS01 envoie hello DNS demande tooDNS01
3. Pare-feu de toohello UDR itinéraires du trafic sortant en tant que tronçon suivant de hello
4. Aucune règle de groupe de sécurité réseau sortantes n’est liées toohello frontal sous-réseau, le trafic est autorisé.
5. Le pare-feu commence le traitement de la règle :
   1. FW règle 1 (FW Mgmt) ne s’applique pas, déplacer toonext règle
   2. FW règle 2-5 (règles RDP) ne s’appliquent pas, déplacer toonext règle
   3. FW règles 6 et 7 (règles d’application) ne s’appliquent pas, déplacer toonext règle
   4. FW règle 8 (tooInternet) ne s’applique pas, déplacer toonext règle
   5. FW règle 9 (DNS) s’applique, le trafic est autorisé, le pare-feu transfère le trafic too10.0.2.4 (DNS01)
6. sous-réseau du serveur principal Hello commence le traitement de la règle de trafic entrant :
   1. Groupe de sécurité réseau règle 1 (bloc Internet) ne s’applique pas, déplacer toonext règle
   2. Règles du groupe de sécurité réseau par défaut autoriser le trafic de toosubnet de sous-réseau, le trafic est autorisé, d’arrêter le traitement des règles de groupe de sécurité réseau
7. Serveur DNS reçoit la demande de hello
8. Serveur DNS n’a pas adresse hello mis en cache et demande à un serveur DNS racine sur hello internet
9. Pare-feu de toohello UDR itinéraires du trafic sortant en tant que tronçon suivant de hello
10. Aucune règle NSG sur le trafic sortant sur le sous-réseau du serveur principal. Le trafic est autorisé.
11. Le pare-feu commence le traitement de la règle :
    1. FW règle 1 (FW Mgmt) ne s’applique pas, déplacer toonext règle
    2. FW règle 2-5 (règles RDP) ne s’appliquent pas, déplacer toonext règle
    3. FW règles 6 et 7 (règles d’application) ne s’appliquent pas, déplacer toonext règle
    4. FW règle 8 (tooInternet) s’applique, le trafic est autorisé, la session est SNAT des serveurs DNS tooroot hello Internet
12. Serveur DNS Internet répond, étant donné que cette session a été lancée à partir de pare-feu de hello, réponse de hello est accepté par le pare-feu hello
13. Comme il s’agit d’une session établie, les pare-feu hello transfère toohello de réponse hello lancer le serveur, DNS01
14. sous-réseau du serveur principal Hello commence le traitement de la règle de trafic entrant :
    1. Groupe de sécurité réseau règle 1 (bloc Internet) ne s’applique pas, déplacer toonext règle
    2. Règles du groupe de sécurité réseau par défaut autoriser le trafic de toosubnet de sous-réseau, le trafic est autorisé, d’arrêter le traitement des règles de groupe de sécurité réseau
15. serveur DNS de Hello reçoit et met en cache la réponse de hello et répond ensuite tooIIS01 arrière de demande initiale toohello
16. itinéraire UDR Hello sur le sous-réseau du serveur principal effectue le saut suivant de hello pare-feu hello
17. Il n’existe aucune règle de groupe de sécurité réseau sortant sur le sous-réseau du serveur principal hello, le trafic est autorisé.
18. Il s’agit d’une session établie sur les pare-feu hello, réponse de hello est transmis par le serveur IIS de hello pare-feu toohello précédent
19. Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :
    1. Il n’existe aucune règle de groupe de sécurité réseau qui applique des tooInbound trafic de sous-réseau du serveur frontal de toohello de sous-réseau hello back-end, donc aucune des règles du groupe de sécurité réseau hello s’appliquent
    2. règle du système par défaut Hello autorisant le trafic entre sous-réseaux permet ce trafic donc hello le trafic est autorisé
20. IIS01 reçoit hello réponse DNS01

#### <a name="allowed-backend-server-toofrontend-server"></a>(Autorisé) Serveur tooFrontend de serveur principal
1. Un administrateur connecté tooAppVM02 via RDP demande un fichier directement hello IIS01 serveur via l’Explorateur de fichiers windows
2. itinéraire UDR Hello sur le sous-réseau du serveur principal effectue le saut suivant de hello pare-feu hello
3. Dans la mesure où il n’y a aucune règle de groupe de sécurité réseau sortant sur hello réponse de hello sous-réseau principal n’est autorisé.
4. Le pare-feu commence le traitement de la règle :
   1. FW règle 1 (FW Mgmt) ne s’applique pas, déplacer toonext règle
   2. FW règle 2-5 (règles RDP) ne s’appliquent pas, déplacer toonext règle
   3. FW règles 6 et 7 (règles d’application) ne s’appliquent pas, déplacer toonext règle
   4. FW règle 8 (tooInternet) ne s’applique pas, déplacer toonext règle
   5. Règle de pare-feu 9 (DNS) ne s’applique pas, déplacer toonext règle
   6. 10 de règle FW (Intra-sous-réseau) s’applique, le trafic est autorisé, le pare-feu transmet le trafic too10.0.1.4 (IIS01)
5. Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :
   1. Groupe de sécurité réseau règle 1 (bloc Internet) ne s’applique pas, déplacer toonext règle
   2. Règles du groupe de sécurité réseau par défaut autoriser le trafic de toosubnet de sous-réseau, le trafic est autorisé, d’arrêter le traitement des règles de groupe de sécurité réseau
6. En supposant que d’autorisation et authentification appropriée, IIS01 hello accepte et répond
7. itinéraire UDR Hello sur le sous-réseau frontal rend le saut suivant de hello pare-feu hello
8. Dans la mesure où il n’y a aucune règle de groupe de sécurité réseau sortant sur hello réponse de hello sous-réseau frontal n’est autorisée.
9. Comme il s’agit d’une session existante sur le pare-feu hello cette réponse est autorisée et les pare-feu hello retourne hello réponse tooAppVM02
10. Le sous-réseau du serveur principal entame le traitement du réseau entrant :
    1. Groupe de sécurité réseau règle 1 (bloc Internet) ne s’applique pas, déplacer toonext règle
    2. Règles du groupe de sécurité réseau par défaut autoriser le trafic de toosubnet de sous-réseau, le trafic est autorisé, d’arrêter le traitement des règles de groupe de sécurité réseau
11. AppVM02 reçoit la réponse de hello

#### <a name="denied-internet-direct-tooweb-server"></a>(Refusé) Internet, tooWeb directe serveur
1. Utilisateur Internet tente tooaccess hello serveur web, IIS01, via hello FrontEnd001.CloudApp.Net service
2. Étant donné qu’aucun point de terminaison ouvert pour le trafic HTTP, cela ne peut pas passer via hello Service Cloud et ne pas de joindre le serveur de hello
3. Si les points de terminaison hello étaient ouverts pour une raison quelconque, hello NSG (bloc Internet) sur le sous-réseau du serveur frontal hello susceptibles de bloquer ce trafic
4. Enfin, itinéraire UDR sous-réseau hello frontal envoie tout le trafic sortant à partir de pare-feu de toohello IIS01 en tant que tronçon suivant de hello, les pare-feu hello seraient et consultez ce trafic asymétrique déposez hello de réponse sortants ainsi il y a au moins trois couches indépendantes de défense entre hello internet et IIS01 via son service de cloud empêche l’accès non autorisé/inappropriés.

#### <a name="denied-internet-toobackend-server"></a>(Refusé) Internet tooBackend Server
1. Utilisateur Internet tente tooaccess un fichier sur AppVM01 via hello BackEnd001.CloudApp.Net service
2. Étant donné qu’aucun point de terminaison ouvert pour le partage de fichiers, cela ne peut pas passer hello Service Cloud et ne pas de joindre le serveur de hello
3. Si les points de terminaison hello étaient ouverts pour une raison quelconque, hello NSG (bloc Internet) susceptibles de bloquer ce trafic
4. Enfin, itinéraire UDR hello envoie tout le trafic sortant à partir de pare-feu de toohello AppVM01 en tant que tronçon suivant de hello, les pare-feu hello seraient et consultez ce trafic asymétrique déposez hello de réponse sortants ainsi il y a au moins trois couches indépendantes de défense entre Bonjour internet et AppVM01 via son service de cloud empêche l’accès non autorisé/inappropriés.

#### <a name="denied-frontend-server-toobackend-server"></a>(Refusé) Serveur frontal serveur tooBackend serveur
1. Supposez IIS01 a été compromis et que la tentative de serveurs de sous-réseau tooscan hello principaux programmes malveillants est en cours d’exécution.
2. itinéraire UDR sous-réseau Hello frontal envoie tout le trafic sortant IIS01 toohello pare-feu en tant que tronçon suivant de hello. Ce n’est pas un élément qui peut être modifiée par hello compromis de machine virtuelle.
3. les pare-feu Hello seraient traiter le trafic hello, si la demande de hello a été tooAppVM01 ou serveur DNS de toohello pour les recherches DNS, que le trafic peut potentiellement par pare-feu hello (échéance tooFW règles 7 et 9). Tout autre trafic est bloqué par la règle de pare-feu 11 (Refuser tout).
4. Si la détection des menaces a été activée sur le pare-feu hello (qui n’est pas abordé dans ce document, consultez la documentation du fournisseur hello pour votre solution de réseau spécifique des fonctionnalités de menaces avancées), même le trafic qui serait autorisé par hello base de règles de transfert abordés dans ce document ne soient pas si le trafic de hello contenait des signatures connus ou des modèles que l’indicateur d’une règle avancée.

#### <a name="denied-internet-dns-lookup-on-dns-server"></a>(Refusé) Recherche Internet DNS sur le serveur DNS.
1. Utilisateur Internet tente toolookup un enregistrement DNS interne sur DNS01 via BackEnd001.CloudApp.Net service 
2. Étant donné qu’aucun point de terminaison ouvert pour le trafic DNS, cela ne peut pas passer via hello Service Cloud et ne pas de joindre le serveur de hello
3. Si les points de terminaison hello étaient ouverts pour une raison quelconque, règle de groupe de sécurité réseau hello (bloc Internet) sur le sous-réseau du serveur frontal hello susceptibles de bloquer ce trafic
4. Enfin, itinéraire UDR sous-réseau hello principal envoie tout le trafic sortant à partir de pare-feu de toohello DNS01 en tant que tronçon suivant de hello, les pare-feu hello seraient et consultez ce trafic asymétrique déposez hello de réponse sortants ainsi il y a au moins trois couches indépendantes de défense entre hello internet et DNS01 via son service de cloud empêche l’accès non autorisé/inappropriés.

#### <a name="denied-internet-toosql-access-through-firewall"></a>(Refusé) Accès à Internet tooSQL via le pare-feu
1. Un utilisateur Internet demande des données SQL de SecSvc001.CloudApp.Net (Service cloud Internet)
2. Étant donné qu’aucun point de terminaison ouvert pour SQL, cela ne peut pas passer hello Service Cloud et ne pas atteindre le pare-feu hello
3. Si les points de terminaison SQL a été ouvertes pour une raison quelconque, les pare-feu hello seraient commencer le traitement de la règle :
   1. FW règle 1 (FW Mgmt) ne s’applique pas, déplacer toonext règle
   2. Règles 2 à 5 (règles RDP) ne s’appliquent, déplacer toonext règle
   3. FW règle 6 et 7 (règles d’Application) ne s’appliquent pas, déplacer toonext règle
   4. FW règle 8 (tooInternet) ne s’applique pas, déplacer toonext règle
   5. Règle de pare-feu 9 (DNS) ne s’applique pas, déplacer toonext règle
   6. Règle de pare-feu 10 (Intra-sous-réseau) ne s’applique pas, déplacer toonext règle
   7. La règle de pare-feu 11 (Refuser tout) s’applique, le trafic est autorisé, arrêter le traitement des règles.

## <a name="references"></a>Références
### <a name="main-script-and-network-config"></a>Script principal et configuration réseau
Enregistrez hello Script complet dans un fichier de script PowerShell. Enregistrez hello configuration réseau dans un fichier nommé « NetworkConf2.xml ».
Modifier les variables de défini par l’utilisateur de hello en fonction des besoins. Exécuter le script de hello, puis suivez le programme d’installation hello pare-feu règle instructions ci-dessus.

#### <a name="full-script"></a>Script complet
Ce script sera, en fonction des variables définies par l’utilisateur de hello :

1. Se connecter tooan abonnement Azure
2. Création d’un nouveau compte de stockage
3. Créer un nouveau réseau virtuel et trois sous-réseaux tel que défini dans le fichier de configuration de réseau de hello
4. Créer cinq machines virtuelles, 1 pare-feu et 4 machines virtuelles Windows Server 
5. Configurer UDR, notamment :
   1. Création de deux nouvelles tables d’itinéraire
   2. Ajouter des itinéraires toohello tables
   3. Lier les sous-réseaux tooappropriate de tables
6. Activer le transfert IP hello NVA
7. Configurez un groupe de sécurité réseau, notamment :
   1. Création d’un groupe de protection réseau
   2. Ajout d’une règle
   3. Sous-réseaux appropriés de liaison hello NSG toohello

Ce script PowerShell doit être exécuté localement sur un PC ou un serveur connecté à Internet.

> [!IMPORTANT]
> Lorsque ce script est exécuté, des avertissements ou autres messages d’information peuvent s’afficher dans PowerShell. Seuls les messages d’erreur affichés en rouge sont source de préoccupation.
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


#### <a name="network-config-file"></a>Fichier de configuration réseau
Enregistrez ce fichier xml avec l’emplacement mis à jour et ajouter hello lien toothis fichier toohello $NetworkConfigFile variable dans le script hello ci-dessus.

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

#### <a name="sample-application-scripts"></a>Exemples de scripts d’application
Si vous le souhaitez tooinstall un exemple d’application pour ce, ainsi que d’autres exemples de réseau de périmètre, un a été fourni au lien de hello : [Application exemple de Script][SampleApp]

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
