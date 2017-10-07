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
# <a name="example-2--build-a-dmz-tooprotect-applications-with-a-firewall-and-nsgs"></a>Exemple 2 : créer un réseau de périmètre tooprotect des applications avec un pare-feu et des groupes de sécurité réseau
[Retour toohello Page meilleures pratiques de sécurité limite][HOME]

Cet exemple crée une zone DMZ avec un pare-feu, quatre serveurs Windows et des groupes de sécurité réseau. Il vous guide également dans chacun des hello des commandes tooprovide une meilleure compréhension de chaque étape. Il existe également un scénario de trafic section tooprovide un détaillées étape par étape comment le trafic passe par le biais des couches de défense dans hello hello réseau de périmètre. Enfin, dans la section des références hello est code complet de hello et instruction toobuild cette tootest d’environnement et de faire des essais avec différents scénarios. 

![Zone DMZ entrante avec NVA et NSG][1]

## <a name="environment-description"></a>Description de l’environnement
Dans cet exemple, il existe un abonnement qui contient les éléments suivants de hello :

* deux services cloud : « FrontEnd001 », « BackEnd001 »,
* Un réseau virtuel « CorpNetwork » avec deux sous-réseaux : « FrontEnd » et « BackEnd »
* Un groupe de sécurité réseau unique qui est appliqué tooboth sous-réseaux
* Une appliance virtuelle de réseau, dans cet exemple, un pare-feu Barracuda NextGen connecté toohello frontal sous-réseau
* un serveur Windows Server représentant un serveur web d’application (« IIS01 »),
* Deux serveurs Windows Server qui représentent les serveurs principaux d’applications (« AppVM01 », « AppVM02 »)
* Un serveur Windows Server qui représente un serveur DNS (« DNS01 »),

> [!NOTE]
> Bien que cet exemple utilise un pare-feu Barracuda NextGen, nombreux hello que différentes solutions de réseau virtuel peut être utilisées pour cet exemple.
> 
> 

Dans la section des références hello ci-dessous, il existe un script PowerShell qui générera la plupart des environnement hello décrite ci-dessus. Machines virtuelles de génération hello et réseaux virtuels, bien que s’effectuent par le script d’exemple hello, ne sont pas décrits en détail dans ce document.

environnement de hello toobuild :

1. Fichier hello réseau config xml figurant dans la section de références hello (mis à jour avec les noms, l’emplacement et scénario de hello donné toomatch IP adresses)
2. Variables utilisateur hello script toomatch hello environnement hello de script de mise à jour hello est toobe exécutée (abonnements, les noms de service, etc.)
3. Exécutez le script de hello dans PowerShell

**Remarque**: région hello signifiée Bonjour script PowerShell doit correspondre à la région hello signifiée dans le fichier xml de configuration de réseau hello.

Une fois hello script s’exécute correctement fallu hello postérieur au script comme suit :

1. Configurez des règles de pare-feu hello, celle-ci est décrite dans la section hello ci-dessous intitulée : règles de pare-feu.
2. Si vous le souhaitez dans la section des références de hello sont deux tooset de scripts de serveur web de hello et le serveur d’applications à un tooallow d’application web simple test avec cette configuration de réseau de périmètre.

section suivante de Hello explique la plupart des hello scripts instructions relatif tooNetwork groupes de sécurité.

## <a name="network-security-groups-nsg"></a>Groupes de sécurité réseau (NSG)
Dans cet exemple, un groupe NSG est créé, puis chargé avec six règles. 

> [!TIP]
> En règle générale, vous devez créer vos règles « Autoriser » spécifiques tout d’abord et puis hello dernière plus générique « Refuser » règles. Hello priorité détermine les règles sont évaluées en premier. Une fois que le trafic est trouvé règle spécifique de tooapply tooa, aucune autre règle n’est évaluées. Les règles de groupe de sécurité réseau peuvent être appliquées, que ce soit dans hello direction entrante ou sortante (du point de vue hello du sous-réseau de hello).
> 
> 

De façon déclarative, hello suivant les règles est généré pour le trafic entrant :

1. Le trafic DNS interne (port 53) est autorisé
2. Le trafic RDP (port 3389) à partir d’Internet de hello tooany machine virtuelle est autorisé.
3. Le trafic HTTP (port 80) à partir de hello Internet toohello NVA (pare-feu) est autorisé.
4. Tout trafic (tous les ports) à partir de IIS01 tooAppVM1 est autorisée.
5. Tout trafic (tous les ports) à partir de hello Internet toohello réseau virtuel entier (les deux sous-réseaux) est refusé.
6. Tout trafic (tous les ports) à partir du sous-réseau principal toohello hello frontal sous-réseau est refusé.

Avec ces sous-réseau tooeach dépendant de règles, si une requête HTTP a été entrante à partir de hello toohello le serveur web Internet, les deux règles 3 (autoriser) et 5 (refuser) s’appliquent, mais étant donné que la règle 3 a une priorité plus élevée s’appliquerait et règle 5 ne serait pas entrent en jeu. Par conséquent, la demande de hello HTTP serait autorisée toohello pare-feu. Si ce trafic même a essayé de serveur de DNS01 tooreach hello, règle 5 (Deny) serait hello premier tooapply hello le trafic et ne serait pas autorisé toopass toohello serveur. Règle 6 (Deny) blocs hello frontal sous-réseau communique avec le sous-réseau du serveur principal toohello (à l’exception du trafic autorisé dans les règles 1 et 4), cela protège le réseau principal de hello au cas où une personne malveillante compromet hello application web sur hello serveur frontal, hello attaquant accès limité toohello principal « protégé » (uniquement tooresources exposée sur le serveur de AppVM01 hello) de réseau.

Il existe une règle sortante par défaut qui autorise le trafic sortant toohello internet. Pour cet exemple, nous allons autoriser le trafic sortant sans modifier les règles de trafic sortant. toolock vers le bas le trafic dans les deux directions, utilisateur défini par routage est requise, cela est examiné dans un autre exemple peut-il hello [document de limite de sécurité principal][HOME].

règles de groupe de sécurité réseau Hello ci-dessus présenté sont des règles de groupe de sécurité réseau toohello très similaires dans [exemple 1 : créer un réseau de périmètre Simple avec des groupes de sécurité réseau][Example1]. Passez en revue hello Description du groupe de sécurité réseau dans ce document pour une présentation détaillée de chaque règle de groupe de sécurité réseau et de ses attributs.

## <a name="firewall-rules"></a>Règles de pare-feu
Un client de gestion sera peut-être toobe installé sur un pare-feu de hello toomanage PC et créer des configurations hello nécessaires. Consultez le fournisseur de documentation de votre pare-feu (ou autres NVA) hello sur comment toomanage hello appareil. reste Hello de cette section décrivent la configuration hello du pare-feu de hello lui-même, via le client de gestion des fournisseurs hello (c'est-à-dire, non hello portail Azure ou PowerShell).

Instructions de téléchargement du client et de connexion toohello Barracuda utilisé dans cet exemple se trouve ici : [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)

Sur le pare-feu hello, règles de transfert devez toobe créé. Cet exemple achemine uniquement les pare-feu entrantes toohello internet, puis le serveur web de toohello, transfert qu’une seule règle NAT est nécessaire. Sur hello Barracuda NextGen Firewall utilisé dans cette hello exemple règle serait un NAT de Destination de règle (heure d’été « NAT ») toopass ce trafic.

suivant de hello toocreate règle (ou vérifiez les règles par défaut existant), à partir du tableau de bord hello Barracuda NG administrateur client, accédez d’onglet de configuration toohello, Bonjour Configuration opérationnelle de section, cliquez sur règles. Une grille est appelée, « Règles de Main » affiche hello désactivés et actives des règles sur les pare-feu hello existantes. Hello coin supérieur droit de cette grille est une petite, verte « + », sur cette toocreate une nouvelle règle (Remarque : votre pare-feu peut être « verrouillé » pour les modifications, si vous voyez un bouton marqué « Verrouiller » et vous toocreate impossible ou modifiez les règles, cliquez sur ce bouton trop « déverrouiller » hello groupe de règles et d’autoriser la modification). Si vous le souhaitez tooedit une règle existante, sélectionnez cette règle, avec le bouton droit et sélectionnez Modifier la règle.

Créez une nouvelle règle et indiquez un nom, par exemple « WebTraffic ». 

icône de la règle NAT de Destination Hello ressemble à ceci : ![icône NAT de Destination][2]

règle Hello elle-même ressemblerait à ceci :

![Règle de pare-feu][3]

Ici n’importe quelle adresse entrant qu’accès hello pare-feu lors de la tentative tooreach HTTP (port 80 ou 443 pour HTTPS) est envoyé hello du pare-feu interface « DHCP1 Local IP » et toohello redirigé serveur Web avec hello adresse IP de 10.0.1.5. Étant donné que le trafic de hello arrive sur le port 80 et le serveur de web toohello continu sur le port 80, aucune modification du port a été nécessaire. Toutefois, hello liste cible auraient pu être 10.0.1.5:8080 si notre serveur Web était à l’écoute sur le port 8080 ainsi traduction hello entrant port 80 sur hello pare-feu tooinbound port 8080 hello serveur web.

Une méthode de connexion doit également être signifiée, pourquoi la règle de Destination à partir d’Internet, de hello « SNAT dynamique » est la plus appropriée. 

Bien qu'une seule règle soit créée, il est important de définir correctement sa priorité. Si dans la grille hello de toutes les règles de pare-feu de hello cette nouvelle règle est bas hello (sous la règle « BLOCKALL » de hello) il ne sera jamais entrent en jeu. Vérifiez la règle hello qui vient d’être créé pour le trafic web se situe au-dessus de la règle BLOCKALL hello.

Une fois que la règle de hello est créée, elle doit être transmise toohello pare-feu et puis activé, si cela n’est pas fait règle hello modification ne prendra effet. processus de push et l’activation de Hello est décrit dans la section suivante de hello.

## <a name="rule-activation"></a>Activation d’une règle
Avec hello ruleset modifiées tooadd cette règle, hello ruleset doit être téléchargé toohello pare-feu et activé.

![Activation de règle de pare-feu][4]

Dans l’angle supérieur droit de hello du client de gestion hello sont un cluster de boutons. Cliquez sur hello « envoyer des modifications » bouton toosend hello modifié règles toohello pare-feu, puis cliquez sur le bouton « Activer » de hello.

L’activation de l’ensemble de règles de pare-feu hello hello cette build d’environnement exemple est terminée. Si vous le souhaitez, scripts de compilation hello post Bonjour section peut être des références exécutent tooadd une application toothis environnement tootest hello ci-dessous des scénarios de trafic.

> [!IMPORTANT]
> Il est critique toorealize que vous ne serez pas d’accès au serveur web de hello directement. Lorsqu’un navigateur demande une page HTTP à partir de FrontEnd001.CloudApp.Net, serveur web transmet de point de terminaison (port 80) HTTP hello ce pare-feu toohello ne Hello pas. Hello pare-feu puis, selon la règle de toohello créé ci-dessus, NAT qui demandent toohello serveur Web.
> 
> 

## <a name="traffic-scenarios"></a>Scénarios de trafic
#### <a name="allowed-web-tooweb-server-through-firewall"></a>(Autorisé) Web tooWeb serveur via le pare-feu
1. Un utilisateur Internet demande une page HTTP en provenance de FrontEnd001.CloudApp.Net (service cloud face à Internet)
2. Cloud service transmet le trafic via le point de terminaison ouvert sur l’interface locale de toofirewall le port 80 sur 10.0.1.4:80
3. Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :
   1. Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle
   2. Règle de groupe de sécurité réseau 2 (RDP) ne s’applique pas, déplacer toonext règle
   3. Règle de groupe de sécurité réseau 3 (tooFirewall Internet) s’applique, le trafic est le traitement des règles autorisées, arrêter
4. Le trafic atteint l’adresse IP interne du pare-feu de hello (10.0.1.4)
5. Règle de pare-feu transfert voir ceci est le trafic du port 80, il redirige le serveur web de toohello IIS01
6. IIS01 écoute pour le trafic web, reçoit la requête et démarre le traitement de demande de hello
7. IIS01 demande hello SQL Server sur AppVM01 pour plus d’informations
8. Aucune règle sur le trafic sortant sur le sous-réseau du serveur frontal. Le trafic est autorisé.
9. sous-réseau du serveur principal Hello commence le traitement de la règle de trafic entrant :
   1. Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle
   2. Règle de groupe de sécurité réseau 2 (RDP) ne s’applique pas, déplacer toonext règle
   3. Règle de groupe de sécurité réseau 3 (tooFirewall Internet) ne s’applique pas, déplacer toonext règle
   4. Règle de groupe de sécurité réseau 4 (IIS01 tooAppVM01) s’applique, le trafic est le traitement des règles autorisées, arrêter
10. AppVM01 reçoit hello requête SQL et répond
11. Dans la mesure où il n’y a aucune règles de trafic sortant sur hello réponse de hello sous-réseau principal n’est autorisé
12. Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :
    1. Il n’existe aucune règle de groupe de sécurité réseau qui applique des tooInbound trafic de sous-réseau du serveur frontal de toohello de sous-réseau hello back-end, donc aucune des règles du groupe de sécurité réseau hello s’appliquent
    2. règle du système par défaut Hello autorisant le trafic entre sous-réseaux permettrait ce trafic donc hello le trafic est autorisé.
13. le serveur IIS Hello reçoit la réponse SQL hello et termine la réponse HTTP de hello et envoie toohello demandeur
14. Dans la mesure où il s’agit d’une session NAT à partir de pare-feu de hello, destination de réponse hello est (initialement) pour hello pare-feu
15. les pare-feu Hello reçoit hello réponse hello serveur Web et transfère toohello précédent utilisateur Internet
16. Dans la mesure où il n’y a aucune règles de trafic sortant sur hello réponse de hello sous-réseau frontal n’est autorisé et hello utilisateur Internet reçoit hello web page est demandée.

#### <a name="allowed-rdp-toobackend"></a>(Autorisé) RDP tooBackend
1. Administrateur du serveur sur internet demande tooAppVM01 de session RDP sur BackEnd001.CloudApp.Net:xxxxx où xxxxx représente le numéro de port hello affecté de façon aléatoire pour RDP tooAppVM01 (port de hello affecté sont accessibles sur hello portail Azure ou via PowerShell)
2. Depuis hello que pare-feu n’écoute que sur hello FrontEnd001.CloudApp.Net adresse, il n’est pas impliquée dans ce flux de trafic
3. Le sous-réseau du serveur principal entame le traitement du réseau entrant :
   1. Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle
   2. La règle NSG 2 (RDP) s’applique, le trafic est autorisé, arrêter le traitement des règles
4. En l’absence de réseau sortant, les règles par défaut s’appliquent et le retour de trafic est autorisé
5. La session RDP est activée
6. AppVM01 demande le mot de passe utilisateur

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a>(Autorisé) recherche DNS du serveur web sur le serveur DNS
1. Web des besoins du serveur, IIS01, de flux de données à www.data.gov, mais doit tooresolve hello adresse.
2. Hello configuration réseau pour les listes de réseau virtuel hello DNS01 (10.0.2.4 sur le sous-réseau du serveur principal hello) en tant que serveur DNS principal de hello, IIS01 envoie hello DNS demande tooDNS01
3. Aucune règle sur le trafic sortant sur le sous-réseau du serveur frontal. Le trafic est autorisé.
4. Le sous-réseau du serveur principal entame le traitement du réseau entrant :
   1. La règle NSG 1 (DNS) s’applique, le trafic est autorisé, arrêter le traitement des règles
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

#### <a name="allowed-web-server-access-file-on-appvm01"></a>(Autorisé) fichier d’accès de serveur Web sur AppVM01
1. IIS01 demande un fichier sur AppVM01
2. Aucune règle sur le trafic sortant sur le sous-réseau du serveur frontal. Le trafic est autorisé.
3. sous-réseau du serveur principal Hello commence le traitement de la règle de trafic entrant :
   1. Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle
   2. Règle de groupe de sécurité réseau 2 (RDP) ne s’applique pas, déplacer toonext règle
   3. Règle de groupe de sécurité réseau 3 (tooFirewall Internet) ne s’applique pas, déplacer toonext règle
   4. Règle de groupe de sécurité réseau 4 (IIS01 tooAppVM01) s’applique, le trafic est le traitement des règles autorisées, arrêter
4. AppVM01 reçoit la demande de hello et répond avec le fichier (en supposant que l’accès est autorisé)
5. Dans la mesure où il n’y a aucune règles de trafic sortant sur hello réponse de hello sous-réseau principal n’est autorisé
6. Le sous-réseau du serveur frontal commence le traitement des règles de trafic entrant :
   1. Il n’existe aucune règle de groupe de sécurité réseau qui applique des tooInbound trafic de sous-réseau du serveur frontal de toohello de sous-réseau hello back-end, donc aucune des règles du groupe de sécurité réseau hello s’appliquent
   2. règle du système par défaut Hello autorisant le trafic entre sous-réseaux permettrait ce trafic donc hello le trafic est autorisé.
7. le serveur IIS Hello reçoit le fichier de hello

#### <a name="denied-web-direct-tooweb-server"></a>(Refusé) TooWeb directe de Web Server
Puisque hello serveur Web, IIS01 et hello pare-feu sont Bonjour même Service Cloud qui ils partagent hello même adresse IP publique. Par conséquent, tout le trafic HTTP est dirigé toohello pare-feu. Lors de la demande de hello serait servi avec succès, il ne peut pas accéder directement toohello serveur Web, il est passé, comme prévu, hello par le biais du pare-feu tout d’abord. Consultez hello premier scénario de cette section pour le flux de trafic hello.

#### <a name="denied-web-toobackend-server"></a>(Refusé) Web tooBackend Server
1. Utilisateur Internet tente tooaccess un fichier sur AppVM01 via hello BackEnd001.CloudApp.Net service
2. Étant donné qu’aucun point de terminaison ouvert pour le partage de fichiers, cela ne peut pas passer hello Service Cloud et ne pas de joindre le serveur de hello
3. Si les points de terminaison hello étaient ouverts pour une raison quelconque, la règle de groupe de sécurité réseau 5 (tooVNet Internet) susceptibles de bloquer ce trafic

#### <a name="denied-web-dns-lookup-on-dns-server"></a>(Refusé) recherche DNS web sur le serveur DNS
1. Utilisateur Internet tente toolookup un enregistrement DNS interne sur DNS01 via hello BackEnd001.CloudApp.Net service
2. Étant donné qu’aucun point de terminaison ouvert pour un serveur DNS, cela ne peut pas passer hello Service Cloud et ne pas de joindre le serveur de hello
3. Si les points de terminaison hello étaient ouverts pour une raison quelconque, la règle de groupe de sécurité réseau 5 (tooVNet Internet) susceptibles de bloquer ce trafic (Remarque : cette règle 1 (DNS) ne peuvent pas s’appliquer pour deux raisons, première adresse de la source hello est hello internet, cette règle s’applique uniquement toohello réseau local en tant que hello source, Il s’agit d’une règle d’autorisation, donc il n’est jamais refuser le trafic)

#### <a name="denied-web-toosql-access-through-firewall"></a>(Refusé) Accès Web tooSQL via le pare-feu
1. Un utilisateur Internet demande des données SQL de FrontEnd001.CloudApp.Net (Service cloud face à Internet)
2. Étant donné qu’aucun point de terminaison ouvert pour SQL, cela ne peut pas passer hello Service Cloud et ne pas atteindre le pare-feu hello
3. Si les points de terminaison ont été ouverts pour une raison quelconque, sous-réseau du serveur frontal hello commence le traitement de la règle de trafic entrant :
   1. Groupe de sécurité réseau règle 1 (DNS) ne s’applique pas, déplacer toonext règle
   2. Règle de groupe de sécurité réseau 2 (RDP) ne s’applique pas, déplacer toonext règle
   3. Règle de groupe de sécurité réseau 2 (tooFirewall Internet) s’applique, le trafic est le traitement des règles autorisées, arrêter
4. Le trafic atteint l’adresse IP interne du pare-feu de hello (10.0.1.4)
5. Le pare-feu n’a aucune règle de transfert pour SQL et supprime hello du trafic

## <a name="conclusion"></a>Conclusion
Il s’agit d’un moyen relativement simple de protection de votre application avec un pare-feu et l’isolement de sous-réseau de back-end hello du trafic entrant.

Vous trouverez d’autres exemples et une vue d’ensemble des frontières de sécurité réseau [ici][HOME].

## <a name="references"></a>Références
### <a name="main-script-and-network-config"></a>Script principal et configuration réseau
Enregistrez hello Script complet dans un fichier de script PowerShell. Enregistrez hello configuration réseau dans un fichier nommé « NetworkConf2.xml ».
Modifier les variables de défini par l’utilisateur de hello en fonction des besoins. Exécuter le script de hello, puis suivez le programme d’installation hello pare-feu règle instructions ci-dessus.

#### <a name="full-script"></a>Script complet
Ce script sera, en fonction des variables définies par l’utilisateur de hello :

1. Se connecter tooan abonnement Azure
2. Création d’un nouveau compte de stockage
3. Créer un nouveau réseau virtuel et deux sous-réseaux, tel que défini dans le fichier de configuration de réseau de hello
4. Génération de 4 machines virtuelles Windows Server
5. Configurez un groupe de sécurité réseau, notamment :
   * Création d’un groupe de sécurité réseau
   * Ajout de règles à ce dernier
   * Sous-réseaux appropriés de liaison hello NSG toohello

Ce script PowerShell doit être exécuté localement sur un PC ou un serveur connecté à Internet.

> [!IMPORTANT]
> Lorsque ce script est exécuté, des avertissements ou autres messages d’information peuvent s’afficher dans PowerShell. Seuls les messages d’erreur affichés en rouge sont source de préoccupation.
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
[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "Zone DMZ avec groupe de sécurité réseau (NSG)"
[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "Icône NAT de destination"
[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "Règle de pare-feu"
[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "Activation de règle de pare-feu"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
[Example1]: ./virtual-networks-dmz-nsg-asm.md
