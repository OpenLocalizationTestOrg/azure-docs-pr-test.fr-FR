---
title: aaaHow tooControl trafic entrant tooan environnement App Service
description: "Découvrez comment toocontrol de règles de sécurité de réseau tooconfigure entrants trafic tooan environnement App Service."
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: 
ms.assetid: 4cc82439-8791-48a4-9485-de6d8e1d1a08
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: stefsch
ms.openlocfilehash: e7c6e6201db6a1ea77f7a2eee29a3b5445175495
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocontrol-inbound-traffic-tooan-app-service-environment"></a>Comment tooan de trafic entrant tooControl environnement App Service
## <a name="overview"></a>Vue d'ensemble
Un environnement App Service peut être créé **soit** dans un réseau virtuel Azure Resource Manager, **soit** dans un [réseau virtuel][virtualnetwork] de modèle de déploiement classique.  Un nouveau réseau virtuel et un nouveau sous-réseau peuvent être définies au moment de hello qu'un environnement App Service est créé.  Vous pouvez également créer un environnement App Service dans un réseau virtuel préexistant et un sous-réseau préexistant.  Suite à une modification effectuée en juin 2016, les environnements ASE peuvent également être déployés dans les réseaux virtuels qui utilisent soit des plages d’adresses publiques soit des espaces d’adressage RFC1918 (par exemple, des adresses privées).  Pour plus d’informations sur la création d’un environnement App Service, consultez [comment tooCreate un environnement App Service][HowToCreateAnAppServiceEnvironment].

Un environnement App Service doit toujours être créé dans un sous-réseau, car un sous-réseau fournit une limite réseau qui peut être utilisé toolock vers le bas le trafic entrant derrière les périphériques en amont et de services tels que le trafic HTTP et HTTPS n’est accepté de spécifique en amont Adresses IP.

Le trafic réseau entrant et sortant sur un sous-réseau est contrôlé à l'aide d’un [groupe de sécurité réseau][NetworkSecurityGroups]. Contrôler le trafic entrant nécessite la création de règles de sécurité réseau dans un groupe de sécurité réseau et en assignant hello réseau sécurité groupe hello sous-réseau contenant hello environnement App Service.

Une fois un groupe de sécurité réseau affecté tooa sous-réseau, tooapps le trafic entrant Bonjour Qu'environnement App Service est autorisés/bloqués en fonction de hello autoriser et refuser des règles définies dans le groupe de sécurité réseau hello.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="inbound-network-ports-used-in-an-app-service-environment"></a>Ports réseau entrants dans un environnement App Service
Avant de verrouiller le trafic réseau entrant avec un groupe de sécurité réseau, il est ensemble de hello tooknow important de ports réseau requis et facultatifs utilisés par un environnement App Service.  Fermer accidentellement désactiver trafic toosome ports peut entraîner une perte de fonctionnalité dans un environnement App Service.

Hello Voici une liste des ports utilisés par un environnement App Service. Tous les ports sont **TCP**, sauf indication contraire clairement spécifiée :

* 454 : **Port obligatoire** utilisé par l'infrastructure Azure pour la gestion et la maintenance des environnements App Service par le biais de SSL.  Ne bloquent pas le port toothis de trafic.  Ce port est toujours lié toohello une adresse IP virtuelle publique d’un environnement app service.
* 455 : **Port obligatoire** utilisé par l'infrastructure Azure pour la gestion et la maintenance des environnements App Service par le biais de SSL.  Ne bloquent pas le port toothis de trafic.  Ce port est toujours lié toohello une adresse IP virtuelle publique d’un environnement app service.
* 80 : port pour tooapps de trafic HTTP entrant en cours d’exécution dans l’application des Plans de Service dans un environnement App Service par défaut.  Sur un environnement app service activé d’équilibrage de charge interne, ce port est adresse d’équilibrage de charge interne toohello dépendant de hello ASE.
* 443 : port pour tooapps de trafic entrant SSL en cours d’exécution dans l’application des Plans de Service dans un environnement App Service par défaut.  Sur un environnement app service activé d’équilibrage de charge interne, ce port est adresse d’équilibrage de charge interne toohello dépendant de hello ASE.
* 21 : Canal de contrôle pour FTP.  Ce port peut être bloqué en toute sécurité si FTP n'est pas utilisé.  Un environnement app service activé d’équilibrage de charge interne, ce port peut être adresse d’équilibrage de charge interne toohello lié pour un environnement app service.
* 990 : Canal de contrôle pour FTPS.  Ce port peut être bloqué en toute sécurité si FTPS n’est pas utilisé.  Un environnement app service activé d’équilibrage de charge interne, ce port peut être adresse d’équilibrage de charge interne toohello lié pour un environnement app service.
* 10001-10020 : Canaux de données pour FTP.  Comme avec le canal de contrôle hello, ces ports peuvent être bloquées en toute sécurité si FTP n’est pas utilisé.  Sur un environnement app service activé d’équilibrage de charge interne, ce port peut être adresse d’équilibrage de charge interne toohello dépendant du ASE.
* 4016 : Utilisé pour le débogage à distance avec Visual Studio 2012.  Ce port peut être bloqué en toute sécurité si la fonctionnalité de hello n’est pas utilisée.  Sur un environnement app service activé d’équilibrage de charge interne, ce port est adresse d’équilibrage de charge interne toohello dépendant de hello ASE.
* 4018 : Utilisé pour le débogage à distance avec Visual Studio 2013.  Ce port peut être bloqué en toute sécurité si la fonctionnalité de hello n’est pas utilisée.  Sur un environnement app service activé d’équilibrage de charge interne, ce port est adresse d’équilibrage de charge interne toohello dépendant de hello ASE.
* 4020 : Utilisé pour le débogage à distance avec Visual Studio 2015.  Ce port peut être bloqué en toute sécurité si la fonctionnalité de hello n’est pas utilisée.  Sur un environnement app service activé d’équilibrage de charge interne, ce port est adresse d’équilibrage de charge interne toohello dépendant de hello ASE.

## <a name="outbound-connectivity-and-dns-requirements"></a>Connectivité sortante et configuration DNS requise
Pour une environnement App Service de toofunction correctement, il requiert également points de terminaison toovarious un accès sortant. Une liste complète des points de terminaison externes hello utilisé par un environnement app service est Bonjour section « Connectivité de réseau requis » Hello [Configuration du réseau pour ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) l’article.

Les environnements App Service nécessitent une infrastructure DNS valide configurée pour le réseau virtuel de hello.  Si pour n’importe quel hello raison configuration DNS est modifiée après la création d’un environnement App Service, les développeurs peuvent forcer un toopick environnement App Service de configuration DNS de la nouvelle hello.  Déclenchement d’un redémarrage environnement propagée à l’aide de hello « Redémarrer » située en haut de hello du Panneau de gestion d’environnement App Service hello Bonjour [portail Azure] [ NewPortal] entraîne hello environnement toopick la nouvelle configuration du DNS hello.

Il est également recommandé que tous les serveurs DNS personnalisés sur le réseau virtuel de hello être configuré à l’avance toocreating de temps préalable un environnement App Service.  Si la configuration de DNS d’un réseau virtuel est modifiée pendant la création d’un environnement App Service, qui entraîne au basculement de processus de création d’environnement App Service hello.  De la même manière, si un serveur DNS personnalisé existe sur hello autre extrémité d’une passerelle VPN et le serveur DNS de hello est inaccessible ou indisponible, hello environnement App Service processus de création échoue également.

## <a name="creating-a-network-security-group"></a>Création d'un groupe de sécurité réseau
Pour plus d’informations sur la manière dont des groupes de sécurité réseau Voir hello [informations][NetworkSecurityGroups].  exemple de gestion des services Azure Hello ci-dessous sur des touches finales met en surbrillance des groupes de sécurité réseau, en mettant l’accent sur la configuration et l’application d’un sous-réseau tooa groupe sécurité réseau qui contient un environnement App Service.

**Remarque :** groupes de sécurité réseau peuvent être configurés sous forme graphique à l’aide de hello [portail Azure](https://portal.azure.com) ou Azure PowerShell.

Les groupes de sécurité réseau sont tout d’abord créés en tant qu’entités autonomes associées à un abonnement. Étant donné que les groupes de sécurité réseau sont créées dans une région Azure, assurez-vous que ce groupe de sécurité réseau hello est créé dans hello, même région de hello environnement App Service.

suivant de Hello illustre la création d’un groupe de sécurité réseau :

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

Une fois un groupe de sécurité réseau est créé, une ou plusieurs règles de sécurité réseau sont ajoutées tooit.  Étant donné que l’ensemble de hello de règles peut-être changer au fil du temps, il est recommandé de toospace out hello numérotation utilisé pour toomake des priorités de règle tooinsert simple des règles supplémentaires au fil du temps.

exemple Hello ci-dessous montre une règle qui accorde l’accès toohello gestion des ports par toomanage d’infrastructure Azure hello explicitement et de maintenance un environnement App Service.  Notez que tout le trafic de gestion transmet via le protocole SSL et est sécurisé par des certificats de client, même si hello ports sont ouverts afin de les rendre inaccessibles à n’importe quel autre entité que l’infrastructure de gestion Azure.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP


Lors du verrouillage tooport accès 80 et 443 trop « masquez » un environnement App Service derrière les périphériques situés en amont ou services, vous devez adresse tooknow hello en amont.  Par exemple, si vous utilisez un pare-feu d’applications web (WAF), hello WAF aura sa propre adresse IP (ou les adresses) qu’il utilise quand tooa le trafic de proxy en aval environnement App Service.  Vous devez toouse cette adresse IP Bonjour *SourceAddressPrefix* paramètre d’une règle de sécurité réseau.

Dans l’exemple hello ci-dessous, le trafic entrant à partir d’une adresse IP en amont spécifique est explicitement autorisé.  Hello adresse *1.2.3.4* est utilisé comme espace réservé pour l’adresse IP hello un WAF en amont.  Modifier hello valeur toomatch hello adresse utilisée par votre appareil en amont ou d’un service.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT HTTP" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT HTTPS" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

Si vous le souhaitez est prise en charge FTP, hello suivant les règles utilisable comme une voie de contrôle de modèle toogrant accès toohello FTP et les ports de canal de données.  Étant donné que FTP est un protocole avec état, vous ne soyez pas trafic tooroute en mesure de FTP via un périphérique de pare-feu ou un proxy HTTP/HTTPS traditionnel.  Dans ce cas, vous devez tooset hello *SourceAddressPrefix* tooa autre valeur - par exemple hello IP adresse gamme d’ordinateurs de développement ou de déploiement sur FTP les clients sont en cours d’exécution. 

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT FTPCtrl" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '21' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT FTPDataRange" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '10001-10020' -Protocol TCP

(**Remarque :** plage de ports de canal de données hello peut-être changer au cours de la période d’évaluation hello.)

Si le débogage distant avec Visual Studio est utilisé, suivant les règles de hello montrent comment accéder à toogrant.  Il existe une règle distincte pour chaque version prise en charge de Visual Studio, car chaque version utilise un port différent pour le débogage à distance.  Comme avec l'accès FTP, il est possible que le trafic du débogage à distance ne transite pas correctement via un pare-feu d'applications web (WAF) ou un appareil proxy traditionnel.  Hello *SourceAddressPrefix* toohello plage d’adresses IP des ordinateurs de développement Visual Studio en cours d’exécution à la place peut être définie.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2012" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4016' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2013" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4018' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2015" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4020' -Protocol TCP

## <a name="assigning-a-network-security-group-tooa-subnet"></a>Affectation d’un sous-réseau de tooa groupe de sécurité réseau
Un groupe de sécurité réseau a une règle de sécurité par défaut qui refuse le trafic d’accès tooall externe.  Hello résultat à partir de la combinaison de règles de sécurité réseau hello décrites ci-dessus et hello de règle de sécurité par défaut bloque le trafic entrant, que seul le trafic à partir de plages d’adresses source associé à une *autoriser* action pourra toosend trafic tooapps est en cours d’exécution dans un environnement App Service.

Une fois un groupe de sécurité réseau est rempli avec les règles de sécurité, il doit sous-réseau de toohello toobe attribué contenant hello environnement App Service.  commande d’attribution de Hello fait référence à deux nom hello du réseau virtuel de hello où hello environnement App Service se trouve, ainsi que les nom hello du sous-réseau hello où hello environnement App Service a été créé.  

exemple Hello ci-dessous montre un groupe de sécurité réseau assigné tooa sous-réseau et le réseau virtuel :

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-test'

Une fois que l’affectation du groupe de sécurité réseau hello réussit (attribution de hello est une opération longue et peut prendre quelques minutes toocomplete), uniquement entrants le trafic correspondant *autoriser* règles atteindra correctement des applications Bonjour application Environnement de service.

Pourquoi d’exhaustivité exemple suivant montre comment tooremove et, par conséquent, la sécurité du réseau hello associer au groupe à partir du sous-réseau de hello :

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Remove-AzureNetworkSecurityGroupFromSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-test'

## <a name="special-considerations-for-explicit-ip-ssl"></a>Considérations spécifiques concernant les adresses IP SSL explicites
Si une application est configurée avec une adresse IP SSL explicite (applicable *uniquement* tooASEs qui ont une adresse VIP publique), au lieu d’utiliser l’adresse IP hello environnement App Service hello par défaut, HTTP et HTTPS flux dans le sous-réseau de hello du trafic sur un ensemble différent de ports autres que les ports 80 et 443.

Vous trouverez la paire individuelle de Hello des ports utilisés par chaque adresse IP SSL dans l’interface utilisateur du portail à partir du panneau UX de détails de l’environnement Service hello application hello.  Sélectionnez « Tous les paramètres » --> « Adresses IP ».  Panneau de Hello « IP adresses » affiche un tableau de toutes les adresses IP SSL configurées de manière explicite pour hello environnement App Service, ainsi que de la paire de port spécial hello tooroute utilisé le trafic HTTP et HTTPS associé à chaque adresse IP SSL.  Il s’agit de cette paire de port doit toobe utilisé pour les paramètres de DestinationPortRange hello lors de la configuration des règles dans un groupe de sécurité réseau.

Lorsqu’une application sur un environnement app service est configuré toouse IP-SSL, les clients externes n’apparaît pas et n’avez pas besoin de tooworry sur le mappage de paire port spécial hello.  Les applications toohello le trafic circule normalement toohello configuré SSL IP adresse.  paire de port spécial Hello traduction toohello automatiquement s’effectue en interne pendant hello dernière section de routage du trafic dans hello contenant du sous-réseau hello ASE. 

## <a name="getting-started"></a>Prise en main
tooget démarré avec les environnements de Service d’application, consultez [Introduction tooApp environnement de Service][IntroToAppServiceEnvironment]

Tous les articles et comment-de pour les environnements App Service sont disponibles dans hello [fichier Lisezmoi pour les environnements de Service d’Application](../app-service/app-service-app-service-environments-readme.md).

Pour plus d’informations sur les applications en toute sécurité se connectant toobackend ressource à partir d’un environnement App Service, consultez [en toute sécurité de connexion tooBackend ressources à partir d’un environnement App Service][SecurelyConnecttoBackend]

Pour plus d’informations sur la plateforme Azure App Service de hello, consultez [Azure App Service][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[SecurelyConnecttoBackend]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-securely-connecting-to-backend-resources/
[NewPortal]:  https://portal.azure.com  

<!-- IMAGES -->

