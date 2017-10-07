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
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a>Exemple 1 : Générer une zone DMZ simple en utilisant des groupes de sécurité réseau (NSG) avec Classic PowerShell
[Retour toohello Page meilleures pratiques de sécurité limite][HOME]

> [!div class="op_single_selector"]
> * [Modèle Resource Manager](virtual-networks-dmz-nsg.md)
> * [Classic - PowerShell](virtual-networks-dmz-nsg-asm.md)
> 
>

Cet exemple crée une zone DMZ primitive avec quatre serveurs Windows et des groupes de sécurité réseau. Cet exemple décrit chacun des hello pertinentes PowerShell commandes tooprovide une meilleure compréhension de chaque étape. Il existe également un scénario de trafic section tooprovide un détaillées étape par étape comment le trafic passe par le biais des couches de défense dans hello hello réseau de périmètre. Enfin, dans la section des références hello est code complet de hello et instruction toobuild cette tootest d’environnement et de faire des essais avec différents scénarios. 

![Réseau de périmètre entrant avec groupe de sécurité réseau][1]

## <a name="environment-description"></a>Description de l’environnement
Dans cet exemple, un abonnement contient hello suivant des ressources :

* deux services cloud : « FrontEnd001 », « BackEnd001 »,
* Un réseau virtuel « CorpNetwork » avec deux sous-réseaux « FrontEnd » et « BackEnd »
* Un groupe de sécurité réseau qui est appliquée tooboth sous-réseaux
* un serveur Windows Server représentant un serveur web d’application (« IIS01 »),
* Deux serveurs Windows Server qui représentent les serveurs principaux d’applications (« AppVM01 », « AppVM02 »)
* Un serveur Windows Server qui représente un serveur DNS (« DNS01 »),

Dans la section des références de hello, il existe un script PowerShell qui génère la plupart des environnement hello décrite dans cet exemple. Machines virtuelles de génération hello et réseaux virtuels, bien que s’effectuent par le script d’exemple hello, ne sont pas décrits en détail dans ce document. 

environnement de hello toobuild ;

1. Fichier hello réseau config xml figurant dans la section de références hello (mis à jour avec les noms, l’emplacement et scénario de hello donné toomatch IP adresses)
2. Variables utilisateur hello script toomatch hello environnement hello de script de mise à jour hello est toobe exécutée (abonnements, les noms de service, etc.).
3. Exécutez le script de hello dans PowerShell

>[!Note]
>région Hello signifiée Bonjour script PowerShell doit correspondre à la région hello signifiée dans le fichier xml de configuration de réseau hello.
>
>

Une fois que hello script s’exécute correctement supplémentaire étapes facultatives peuvent être prises, dans la section des références de hello sont deux tooset de scripts de serveur web de hello et le serveur d’applications à un tooallow d’application web simple test avec cette configuration de réseau de périmètre.

Hello sections suivantes fournissent une description détaillée des groupes de sécurité réseau et leur fonctionnement pour cet exemple en parcourant des lignes de clés de script PowerShell de hello.

## <a name="network-security-groups-nsg"></a>Groupes de sécurité réseau (NSG)
Pour cet exemple, un groupe NSG est créé, puis chargé avec six règles. 

> [!TIP]
> En règle générale, vous devez créer vos règles « Autoriser » spécifiques tout d’abord et puis hello dernière plus générique « Refuser » règles. Hello priorité détermine les règles sont évaluées en premier. Une fois que le trafic est trouvé règle spécifique de tooapply tooa, aucune autre règle n’est évaluées. Les règles de groupe de sécurité réseau peuvent être appliquées, que ce soit dans hello direction entrante ou sortante (du point de vue hello du sous-réseau de hello).
> 
> 

De façon déclarative, hello suivant les règles est généré pour le trafic entrant :

1. Le trafic DNS interne (port 53) est autorisé
2. Le trafic RDP (port 3389) à partir d’Internet de hello tooany machine virtuelle est autorisé.
3. Le trafic HTTP (port 80) à partir du serveur de tooweb hello Internet (IIS01) est autorisé.
4. Tout trafic (tous les ports) à partir de IIS01 tooAppVM1 est autorisée.
5. Tout trafic (tous les ports) à partir de hello Internet toohello réseau virtuel entier (les deux sous-réseaux) est refusé.
6. Tout trafic (tous les ports) à partir du sous-réseau principal toohello hello frontal sous-réseau est refusé.

Avec ces sous-réseau tooeach dépendant de règles, si une requête HTTP a été entrante à partir de hello toohello le serveur web Internet, les deux règles 3 (autoriser) et 5 (refuser) s’appliquent, mais étant donné que la règle 3 a une priorité plus élevée s’appliquerait et règle 5 ne serait pas entrent en jeu. Par conséquent, demande HTTP de hello serait autorisée serveur web de toohello. Si ce trafic même a essayé de serveur de DNS01 tooreach hello, règle 5 (Deny) serait hello premier tooapply hello le trafic et ne serait pas autorisé toopass toohello serveur. Règle 6 (Deny) bloque le sous-réseau frontal hello communique avec le sous-réseau du serveur principal toohello (à l’exception du trafic autorisé dans les règles 1 et 4), cet ensemble de règles protège le réseau principal de hello au cas où une personne malveillante compromet hello application web sur hello serveur frontal, serait de personne malveillante de hello limitée toohello d’accès réseau (uniquement tooresources exposée sur le serveur de AppVM01 hello) principal « protégé ».

Il existe une règle sortante par défaut qui autorise le trafic sortant toohello internet. Pour cet exemple, nous allons autoriser le trafic sortant sans modifier les règles de trafic sortant. toolock vers le bas le trafic dans les deux directions, utilisateur défini par routage est obligatoire et est exploré dans « Exemple 3 » sur hello [Page meilleures pratiques de sécurité limite][HOME].

Chaque règle est décrite plus en détail comme suit (**Remarque**: n’importe quel élément Bonjour suivant le début de liste avec un signe dollar (par exemple : $NSGName) est une variable définie par l’utilisateur à partir du script hello dans la section de référence hello de ce document) :

1. Tout d’abord un groupe de sécurité réseau doivent être généré des règles toohold hello :

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. Hello première règle de cet exemple autorise le trafic DNS entre tous les réseaux internes toohello serveur DNS hello principal sous-réseau. règle de Hello a certains paramètres importants :
   
   * « Type » indique le sens du trafic qui sera appliqué à cette règle. direction de Hello est hello du point de vue de l’ordinateur virtuel ou le sous-réseau de hello (selon où ce groupe de sécurité réseau est lié). Par conséquent, si le Type est « Entrant » et le trafic est entrant sous-réseau de hello, hello règle s’applique et le trafic en laissant le sous-réseau de hello ne serait pas affecté par cette règle.
   * « Priority » définit la commande hello dans lequel un flux de trafic est évalué. Hello inférieur hello numéro hello hello prioritaires. Lorsqu’une règle s’applique le flux de trafic spécifique tooa, aucune autre règle n’est traitées. Par conséquent, si une règle avec la priorité 1 autorise le trafic et une règle de priorité 2 refuse le trafic et les deux règles s’appliquent tootraffic alors le trafic de hello serait autorisé tooflow (étant donné que la règle 1 a une priorité plus élevée qu’il a pris effet et aucune autre règle n’ont été appliquées).
   * « Action » indique si le trafic concerné par cette règle est bloqué ou autorisé.

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. Cette règle permet de tooflow de trafic RDP à partir de port RDP hello internet toohello sur n’importe quel serveur hello lié sous-réseau. Cette règle utilise deux types spéciaux de préfixes d’adresses ; « VIRTUAL_NETWORK » et « INTERNET ». Ces balises sont un tooaddress facilement une catégorie supérieure de préfixes d’adresses.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. Cette règle permet de trafic entrant du trafic toohit hello le serveur web internet. Cette règle ne modifie pas le comportement de routage hello. règle de Hello autorise uniquement le trafic destiné à IIS01 toopass. Par conséquent, si le trafic à partir de hello Internet avait le serveur web de hello comme destination cette règle est autoriser et arrêter le traitement des règles. (Dans la règle hello avec une priorité de 140 tous les autres trafic internet entrant est bloqué). Si vous traitez uniquement le trafic HTTP, cette règle pourrait être plue restreint tooonly autoriser Destination Port 80.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet too$VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. Cette règle permet toopass le trafic à partir du serveur de IIS01 hello toohello AppVM01 serveur, une règle ultérieure bloque tout autre trafic tooBackend de serveur frontal. tooimprove cette règle, si le port de hello est connu, qui doit être ajoutée. Par exemple, si le serveur IIS hello accède uniquement à SQL Server sur AppVM01, plage de ports de Destination hello doit être changé de « * » (tout) too1433 (hello port SQL), permettant ainsi une surface d’attaque entrante réduite sur AppVM01 doit hello web application jamais être compromise.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] too$VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. Cette règle refuse le trafic à partir des serveurs de tooany hello internet sur le réseau de hello. Les règles hello avec une priorité de 110 et 120, effet de hello est tooallow uniquement internet trafic toohello pare-feu entrantes et ports RDP sur les serveurs et bloque tout le reste. Cette règle est une « sécurité intégrée » règle tooblock tous les flux inattendues.
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
7. règle finale de Hello refuse le trafic du sous-réseau de hello frontal sous-réseau toohello back-end. Étant donné que cette règle est la seule règle de trafic entrant, le trafic inverse est autorisé (à partir de toohello de back-end hello frontal).

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

## <a name="traffic-scenarios"></a>Scénarios de trafic
#### <a name="allowed-internet-tooweb-server"></a>(*Autorisées*) Internet tooweb server
1. Un utilisateur Internet demande une page HTTP en provenance de FrontEnd001.CloudApp.Net (service cloud face à Internet)
2. Le trafic via le point de terminaison ouvert sur le port 80 vers IIS01 passe du service de cloud computing (serveur web de hello)
3. Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :
   1. Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle
   2. Règle de groupe de sécurité réseau 2 (RDP) ne s’applique pas, déplacer toonext règle
   3. Règle de groupe de sécurité réseau 3 (tooIIS01 Internet) s’applique, le trafic est le traitement des règles autorisées, arrêter
4. Le trafic atteint l’adresse IP interne du serveur web de hello IIS01 (10.0.1.5)
5. IIS01 écoute pour le trafic web, reçoit la requête et démarre le traitement de demande de hello
6. IIS01 demande hello SQL Server sur AppVM01 pour plus d’informations
7. Comme il n'existe aucune règle sortante sur le sous-réseau du serveur frontal, le trafic est autorisé
8. sous-réseau du serveur principal Hello commence le traitement de la règle de trafic entrant :
   1. Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle
   2. Règle de groupe de sécurité réseau 2 (RDP) ne s’applique pas, déplacer toonext règle
   3. Règle de groupe de sécurité réseau 3 (tooFirewall Internet) ne s’applique pas, déplacer toonext règle
   4. Règle de groupe de sécurité réseau 4 (IIS01 tooAppVM01) s’applique, le trafic est le traitement des règles autorisées, arrêter
9. AppVM01 reçoit hello requête SQL et répond
10. Dans la mesure où il n’y a aucune règles de trafic sortant sur le sous-réseau du serveur principal hello, réponse de hello est autorisée.
11. Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :
    1. Il n’existe aucune règle de groupe de sécurité réseau qui applique des tooInbound trafic de sous-réseau du serveur frontal de toohello de sous-réseau hello back-end, donc aucune des règles du groupe de sécurité réseau hello s’appliquent
    2. règle du système par défaut Hello autorisant le trafic entre sous-réseaux permettrait ce trafic donc hello le trafic est autorisé.
12. le serveur IIS Hello reçoit la réponse SQL hello et termine la réponse HTTP de hello et envoie toohello demandeur
13. Étant donné qu’aucune règle sortante sur le sous-réseau du serveur frontal hello hello réponse soit autorisée, et hello internet utilisateur reçoit hello web page est demandée.

#### <a name="allowed-rdp-toobackend"></a>(*Autorisées*) RDP toobackend
1. Administrateur du serveur sur internet demande tooAppVM01 de session RDP sur BackEnd001.CloudApp.Net:xxxxx où xxxxx représente le numéro de port hello affecté de façon aléatoire pour RDP tooAppVM01 (port de hello affecté sont accessibles sur hello portail Azure ou via PowerShell)
2. Le sous-réseau du serveur principal entame le traitement du réseau entrant :
   1. Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle
   2. La règle NSG 2 (RDP) s’applique, le trafic est autorisé, arrêter le traitement des règles
3. En l’absence de réseau sortant, les règles par défaut s’appliquent et le retour de trafic est autorisé
4. La Session RDP est activée.
5. Invites AppVM01 hello nom d’utilisateur et mot de passe

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a>(*Autorisé*) recherche DNS du serveur web sur le serveur DNS
1. Web des besoins du serveur, IIS01, de flux de données à www.data.gov, mais doit tooresolve hello adresse.
2. Hello configuration réseau pour les listes de réseau virtuel hello DNS01 (10.0.2.4 sur le sous-réseau du serveur principal hello) en tant que serveur DNS principal de hello, IIS01 envoie hello DNS demande tooDNS01
3. Aucune règle sur le trafic sortant sur le sous-réseau du serveur frontal. Le trafic est autorisé.
4. Le sous-réseau du serveur principal entame le traitement du réseau entrant :
   * La règle NSG 1 (DNS) s’applique, le trafic est autorisé, arrêter le traitement des règles
5. Serveur DNS reçoit la demande de hello
6. Serveur DNS n’a pas adresse hello mis en cache et demande à un serveur DNS racine sur hello internet
7. Aucune règle sortante sur le sous-réseau du serveur principal, le trafic est autorisé
8. Serveur DNS Internet répond, étant donné que cette session a été lancée en interne, réponse de hello est autorisée.
9. Le serveur DNS met en cache la réponse de hello et répond tooIIS01 arrière de demande initiale toohello
10. Aucune règle sortante sur le sous-réseau du serveur principal, le trafic est autorisé
11. Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :
    1. Il n’existe aucune règle de groupe de sécurité réseau qui applique des tooInbound trafic de sous-réseau du serveur frontal de toohello de sous-réseau hello back-end, donc aucune des règles du groupe de sécurité réseau hello s’appliquent
    2. règle du système par défaut Hello autorisant le trafic entre sous-réseaux permet ce trafic donc hello le trafic est autorisé
12. IIS01 reçoit hello réponse DNS01

#### <a name="allowed-web-server-access-file-on-appvm01"></a>(*Autorisé*) fichier d’accès de serveur Web sur AppVM01
1. IIS01 demande un fichier sur AppVM01
2. Aucune règle sur le trafic sortant sur le sous-réseau du serveur frontal. Le trafic est autorisé.
3. sous-réseau du serveur principal Hello commence le traitement de la règle de trafic entrant :
   1. Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle
   2. Règle de groupe de sécurité réseau 2 (RDP) ne s’applique pas, déplacer toonext règle
   3. Règle de groupe de sécurité réseau 3 (tooIIS01 Internet) ne s’applique pas, déplacer toonext règle
   4. Règle de groupe de sécurité réseau 4 (IIS01 tooAppVM01) s’applique, le trafic est le traitement des règles autorisées, arrêter
4. AppVM01 reçoit la demande de hello et répond avec le fichier (en supposant que l’accès est autorisé)
5. Dans la mesure où il n’y a aucune règles de trafic sortant sur le sous-réseau du serveur principal hello, réponse de hello est autorisée.
6. Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :
   1. Il n’existe aucune règle de groupe de sécurité réseau qui applique des tooInbound trafic de sous-réseau du serveur frontal de toohello de sous-réseau hello back-end, donc aucune des règles du groupe de sécurité réseau hello s’appliquent
   2. règle du système par défaut Hello autorisant le trafic entre sous-réseaux permettrait ce trafic donc hello le trafic est autorisé.
7. le serveur IIS Hello reçoit le fichier de hello

#### <a name="denied-web-toobackend-server"></a>(*Refusé*) serveur de toobackend Web
1. Un utilisateur internet tente de tooaccess un fichier sur AppVM01 via hello BackEnd001.CloudApp.Net service
2. Étant donné qu’aucun point de terminaison ouvert pour le partage de fichiers, ce trafic ne peut pas passer hello Service Cloud et ne pas de joindre le serveur de hello
3. Si les points de terminaison hello étaient ouverts pour une raison quelconque, la règle de groupe de sécurité réseau 5 (tooVNet Internet) susceptibles de bloquer ce trafic

#### <a name="denied-web-dns-look-up-on-dns-server"></a>(*Refusé*) recherche DNS web sur le serveur DNS
1. Un utilisateur internet tente de toolook d’un enregistrement DNS interne sur DNS01 via hello BackEnd001.CloudApp.Net service
2. Étant donné qu’aucun point de terminaison ouvert pour un serveur DNS, ce trafic ne peut pas passer hello Service Cloud et ne pas de joindre le serveur de hello
3. Si les points de terminaison hello étaient ouverts pour une raison quelconque, la règle de groupe de sécurité réseau 5 (tooVNet Internet) susceptibles de bloquer ce trafic (Remarque : cette règle 1 (DNS) ne peuvent pas s’appliquer pour deux raisons, première adresse de la source hello est hello internet, cette règle s’applique uniquement toohello réseau local en tant que hello source, Cette règle est une règle d’autorisation, donc il n’est jamais refuser le trafic)

#### <a name="denied-web-toosql-access-through-firewall"></a>(*Refusé*) Web tooSQL l’accès via le pare-feu
1. Un utilisateur Internet demande des données SQL de FrontEnd001.CloudApp.Net (Service cloud face à Internet)
2. Étant donné qu’aucun point de terminaison ouvert pour SQL, ce trafic ne peut pas passer hello Service Cloud et ne pas atteindre le pare-feu hello
3. Si les points de terminaison ont été ouverts pour une raison quelconque, sous-réseau du serveur frontal hello commence le traitement de la règle de trafic entrant :
   1. Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle
   2. Règle de groupe de sécurité réseau 2 (RDP) ne s’applique pas, déplacer toonext règle
   3. Règle de groupe de sécurité réseau 3 (tooIIS01 Internet) s’applique, le trafic est le traitement des règles autorisées, arrêter
4. Le trafic atteint l’adresse IP interne de hello IIS01 (10.0.1.5)
5. IIS01 n’est pas à l’écoute sur le port 1433, par conséquent, aucune demande toohello de réponse

## <a name="conclusion"></a>Conclusion
Cet exemple est un moyen relativement simple et direct d’isoler le sous-réseau principal hello le trafic entrant.

Vous trouverez d’autres exemples et une vue d’ensemble des frontières de sécurité réseau [ici][HOME].

## <a name="references"></a>Références
### <a name="main-script-and-network-config"></a>Script principal et configuration réseau
Enregistrez hello Script complet dans un fichier de script PowerShell. Enregistrer hello configuration réseau dans un fichier nommé « NetworkConf1.xml ».
Modifier les variables de défini par l’utilisateur de hello en tant que script de hello nécessaires et les exécuter.

#### <a name="full-script"></a>Script complet
Ce script sera, en fonction des variables définies par l’utilisateur de hello ;

1. Se connecter tooan abonnement Azure
2. Créez un compte de stockage.
3. Créer un réseau virtuel et deux sous-réseaux, tel que défini dans le fichier de configuration de réseau de hello
4. Génération de quatre machines virtuelles Windows Server
5. Configurez un groupe de sécurité réseau, notamment :
   * Création d’un groupe de sécurité réseau
   * Ajout de règles à ce dernier
   * Sous-réseaux appropriés de liaison hello NSG toohello

Ce script PowerShell doit être exécuté localement sur un PC ou un serveur connecté à Internet.

> [!IMPORTANT]
> Lorsque ce script est exécuté, des avertissements ou autres messages d’information peuvent s’afficher dans PowerShell. Seuls les messages d’erreur affichés en rouge sont source de préoccupation.
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

#### <a name="network-config-file"></a>Fichier de configuration réseau
Enregistrez ce fichier xml avec l’emplacement mis à jour et du fichier toohello $NetworkConfigFile variable hello lien toothis dans hello précédant le script.

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

#### <a name="sample-application-scripts"></a>Exemples de scripts d’application
Si vous le souhaitez tooinstall un exemple d’application pour ce, ainsi que d’autres exemples de réseau de périmètre, un a été fourni au lien de hello : [Application exemple de Script][SampleApp]

## <a name="next-steps"></a>Étapes suivantes
* Mise à jour et enregistrement du fichier XML
* Exécuter hello PowerShell script toobuild hello environnement
* Installer l’application d’exemple hello
* Tester différents flux de trafic via cette zone DMZ

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "Zone DMZ avec groupe de sécurité réseau (NSG)"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

