---
title: "aaaHow toouse gestion des API Azure avec des réseaux virtuels"
description: "Découvrez comment toosetup un réseau virtuel tooa de connexion dans Gestion des API Azure et l’accès web des services par son biais."
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 64b58f7b-ca22-47dc-89c0-f6bb0af27a48
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 426b3974e4fed7daffdb0c3f02381edbc326dc28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-api-management-with-virtual-networks"></a>Comment toouse gestion des API Azure avec des réseaux virtuels
Réseaux virtuels Azure (réseaux virtuels) permettent de tooplace une de vos ressources Azure dans un réseau routables non internet que vous contrôlez l’accès à. Ces réseaux peut ensuite être tooyour connectés sur des réseaux locaux à l’aide de différentes technologies VPN. toolearn plus d’informations sur les réseaux virtuels Azure démarrer avec les informations de hello ici : [vue d’ensemble du réseau virtuel Azure](../virtual-network/virtual-networks-overview.md).

Gestion des API Azure peuvent être déployée à l’intérieur de hello de réseau virtuel (VNET), pour qu’il puisse accéder aux services principaux dans le réseau de hello. Hello portail des développeurs et la passerelle API, peut être accessible à partir de hello Internet ou uniquement dans le réseau virtuel de hello toobe configuré.

> [!NOTE]
> La gestion des API Azure prend en charge les réseaux virtuels classiques et Azure Resource Manager.
>
>

## <a name="enable-vpn"></a>Activer la connexion au réseau virtuel
> [!NOTE]
> Connectivité de réseau virtuel n’est disponible dans hello **Premium** et **développeur** niveaux. tooswitch entre les couches de hello, ouvrez votre service de gestion des API Bonjour portail Azure, puis hello **mise à l’échelle et la tarification** onglet. Sous hello **niveau tarifaire** , sélectionnez le niveau Premium ou le développeur de hello et cliquez sur Enregistrer.
>

connectivité de réseau virtuel tooenable, ouvrez votre service de gestion des API Bonjour portail Azure, hello **réseau virtuel** page.

![Menu Réseau virtuel du service Gestion des API][api-management-using-vnet-menu]

Sélectionnez le type d’accès hello souhaité :

* **Externe**: portail de passerelle et le développeur de la gestion des API hello sont accessibles à partir de hello internet public via un équilibreur de charge externe. passerelle de Hello peut accéder aux ressources au sein du réseau virtuel de hello.

![Homologation publique][api-management-vnet-public]

* **Interne**: portail de passerelle et le développeur de la gestion des API hello sont accessibles uniquement à partir de réseau virtuel de hello via un équilibreur de charge interne. passerelle de Hello peut accéder aux ressources au sein du réseau virtuel de hello.

![Homologation privée][api-management-vnet-private]

Vous voyez maintenant une liste de toutes les régions où votre service Gestion des API est créé. Sélectionnez un réseau VNET et un sous-réseau pour chaque région. liste de Hello est remplie avec classique et réseaux virtuels de gestionnaire de ressources disponibles dans vos abonnements Azure qui sont configurés dans la région de hello que vous configurez.

> [!NOTE]
> **Point de terminaison de service** dans hello diagramme ci-dessus inclut passerelle/Proxy, portail de publication, portail des développeurs, GIT et hello point de terminaison de gestion directe.
> **Point de terminaison de gestion** Bonjour diagramme ci-dessus est le point de terminaison hello hébergé sur la configuration du service de hello toomanage via le portail Azure et Powershell.
> Notez également, que, bien que le diagramme de hello affiche les adresses IP de ses points de terminaison différents, le service de gestion des API **uniquement** répond à ses noms d’hôtes configurés.

> [!IMPORTANT]
> Lorsque vous déployez un tooa d’instance gestion des API Azure Resource Manager VNET, hello service doit être un sous-réseau dédié qui ne contient aucuns autres ressources à l’exception des instances de la gestion des API Azure. Si une tentative est faite toodeploy un tooa d’instance gestion des API Azure sous-réseau de gestionnaire de ressources du VNET qui contient d’autres ressources, le déploiement de hello échoue.
>
>

![Sélectionner le VPN][api-management-setup-vpn-select]

Cliquez sur **enregistrer** haut hello écran hello.

> [!NOTE]
> Hello adresse VIP de l’instance de gestion des API hello change chaque fois réseau virtuel est activé ou désactivé.  
> Hello adresse VIP modifiera également lors de la gestion des API est déplacée de **externe** trop**interne** ou vice versa
>


> [!IMPORTANT]
> Si vous supprimez la gestion des API à partir d’un réseau virtuel ou que vous modifiez hello une qu’il est déployé dans, hello réseau virtuel précédemment utilisé peut rester verrouillé pour les heures de too4. Pendant cette période il ne sera pas possible de toodelete hello réseau virtuel ou déployer une nouvelle tooit de ressources.

## <a name="enable-vnet-powershell"></a>Activation de la connexion au réseau virtuel à l’aide d’applets de commande PowerShell
Vous pouvez également activer la connectivité de réseau virtuel à l’aide des applets de commande PowerShell hello

* **Créer un service de gestion des API à l’intérieur d’un réseau virtuel**: utiliser l’applet de commande hello [New-AzureRmApiManagement](/powershell/module/azurerm.apimanagement/new-azurermapimanagement) toocreate un service de gestion des API Azure à l’intérieur d’un réseau virtuel.

* **Déployer un service de gestion des API existant à l’intérieur d’un réseau virtuel**: utiliser l’applet de commande hello [AzureRmApiManagementDeployment de mise à jour](/powershell/module/azurerm.apimanagement/update-azurermapimanagementdeployment) toomove un service de gestion des API Azure existant à l’intérieur d’un réseau virtuel.

## <a name="connect-vnet"></a>Connecter tooa web service est hébergé dans un réseau virtuel
Une fois votre service de gestion des API toohello connecté réseau virtuel, l’accès à des services principaux qu’il contient n’est pas différente de l’accès aux services publics. Tapez simplement dans hello nom d’hôte (si un serveur DNS est configuré pour le réseau virtuel de hello) de votre service web ou une adresse IP locale de hello en hello **URL du service Web** champ lors de la création d’une nouvelle API ou modifier un existant.

![Ajouter des API à partir du VPN][api-management-setup-vpn-add-api]

## <a name="network-configuration-issues"></a>Problèmes courants liés à la configuration du réseau
Voici une liste des problèmes courants de configuration incorrecte qui peuvent se produire lors du déploiement du service de gestion des API dans un réseau virtuel.

* **Installation du serveur DNS personnalisée**: hello service de gestion des API dépend de plusieurs services Azure. Lors de la gestion des API est hébergée dans un réseau virtuel avec un serveur DNS personnalisé, il doit les noms d’hôte tooresolve hello de ces services Azure. Veuillez suivre [ce](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) guide sur la configuration de serveurs DNS personnalisée. Consultez le tableau de ports hello ci-dessous et autres exigences réseau pour référence.

> [!IMPORTANT]
> Il est recommandé que, si vous utilisez un ou les serveurs DNS personnalisé pour hello réseau virtuel, vous définir qui **avant** déploiement d’un service de gestion des API dans celui-ci. Sinon vous devez trop mettre à jour service de gestion des API hello chaque fois que vous modifiez les serveurs DNS hello (s) en exécutant hello [appliquer une opération de Configuration réseau](https://docs.microsoft.com/en-us/rest/api/apimanagement/apimanagementservice#ApiManagementService_ApplyNetworkConfigurationUpdates)

* **Ports requis pour la gestion des API**: trafic entrant et sortant dans le sous-réseau hello dans lequel est déployée gestion des API peut être contrôlé à l’aide de [groupe de sécurité réseau][Network Security Group]. Si ces ports ne sont pas disponibles, la gestion des API risque de ne pas fonctionner correctement et d’être inaccessible. Le blocage d’un ou plusieurs de ces ports constitue un autre problème de configuration courant lorsque vous utilisez la gestion des API dans un réseau virtuel.

Lorsqu’une instance de service de gestion des API est hébergée dans un réseau virtuel, les ports hello Bonjour tableau suivant sont utilisées.

| Port(s) source / de destination | Direction | Protocole de transfert | Objectif | Source / Destination | Type d’accès |
| --- | --- | --- | --- | --- | --- |
| * / 80, 443 |Trafic entrant |TCP |TooAPI de communication client Management |INTERNET / VIRTUAL_NETWORK |Externe |
| * / 3443 |Trafic entrant |TCP |Point de terminaison de gestion pour le portail Azure et Powershell |INTERNET / VIRTUAL_NETWORK |Externe et interne |
| * / 80, 443 |Règle de trafic sortant |TCP |Dépendance sur Stockage Azure et Azure Service Bus |VIRTUAL_NETWORK / INTERNET |Externe et interne |
| * / 1433 |Règle de trafic sortant |TCP |Dépendance sur SQL Azure |VIRTUAL_NETWORK / INTERNET |Externe et interne |
| * / 11000 - 11999 |Règle de trafic sortant |TCP |Dépendance Azure SQL V12 |VIRTUAL_NETWORK / INTERNET |Externe et interne |
| * / 14000 - 14999 |Règle de trafic sortant |TCP |Dépendance Azure SQL V12 |VIRTUAL_NETWORK / INTERNET |Externe et interne |
| * / 5671 |Règle de trafic sortant |AMQP |Dépendance de stratégie du Hub tooEvent journal et l’agent d’analyse |VIRTUAL_NETWORK / INTERNET |Externe et interne |
| 6381 - 6383 / 6381 - 6383 |Trafic entrant et sortant |UDP |Dépendance sur Cache Redis |VIRTUAL_NETWORK / VIRTUAL_NETWORK |Externe et interne |-
| * / 445 |Règle de trafic sortant |TCP |Dépendance sur le partage de fichiers Azure pour GIT |VIRTUAL_NETWORK / INTERNET |Externe et interne |
| * / * | Trafic entrant |TCP |Équilibrage de charge de l’infrastructure Azure | AZURE_LOAD_BALANCER / VIRTUAL_NETWORK |Externe et interne |

* **Fonctionnalité SSL**: certificat SSL de tooenable a besoin d’un service de gestion des API hello création et la validation des chaîne tooocsp.msocsp.com de connectivité réseau sortant, mscrl.microsoft.com et crl.microsoft.com. Cette dépendance n’est pas obligatoire, si n’importe quel certificat que vous téléchargez tooAPI gestion contiennent la racine d’autorité de certification de toohello hello chaîne complète.

* **Accès DNS** : l’accès sortant sur le port 53 est nécessaire pour la communication avec des serveurs DNS. Si un serveur DNS personnalisé existe sur hello l’autre extrémité d’une passerelle VPN, le serveur DNS de hello doit être accessible à partir du sous-réseau hello gestion des API d’hébergement.

* **Contrôle d’intégrité et métriques**: réseau sortant connectivité tooAzure analyse points de terminaison résoudre sous hello suivant domaines : global.metrics.nsatc.net, shoebox2.metrics.nsatc.net, prod3.metrics.nsatc.net.

* **Itinéraire installation rapide**: une configuration de client commune est toodefine leur propres itinéraire par défaut (0.0.0.0/0), ce qui force sortant Internet trafic tooinstead flux localement. Ce flux de trafic sauts invariablement de connectivité avec la gestion des API Azure, car le trafic sortant de hello est bloqué localement ou NAT qui a recours à ensemble non reconnaissable de tooan d’adresses qui ne fonctionnent plus avec différents points de terminaison Azure. solution Hello est toodefine un (ou plusieurs) des itinéraires définis par l’utilisateur ([UDRs][UDRs]) sur le sous-réseau hello contenant hello gestion des API Azure. Un UDR définit les itinéraires de sous-réseau spécifique qui seront respectées au lieu de l’itinéraire par défaut hello.
  Si possible, il est recommandé de hello toouse configuration suivante :
 * configuration de ExpressRoute Hello annonce 0.0.0.0/0 et par défaut force tunnels tout le trafic sortant sur site.
 * Hello UDR appliqué toohello sous-réseau contenant hello gestion des API Azure définit 0.0.0.0/0 avec un type de tronçon suivant d’Internet.
 Bonjour effets combinés de ces étapes est qu’au niveau du sous-réseau UDR hello est prioritaire sur hello ExpressRoute forcé tunneling, garantissant ainsi un accès Internet sortant à partir de hello gestion des API Azure.

>[!WARNING]  
>Gestion des API Azure n’est pas pris en charge avec des configurations de ExpressRoute qui **incorrectement cross-publier d’itinéraires de hello publics d’homologation toohello privés d’homologation chemin**. Les configurations ExpressRoute ayant une homologation publique configurée reçoivent les annonces de routage depuis Microsoft pour un grand ensemble de plages d'adresses IP Microsoft Azure. Si ces plages d’adresses sont incorrectement entre publiés sur le chemin d’accès d’homologation privée hello, le résultat final de hello est que tous les paquets réseau sortant à partir du sous-réseau de l’instance de gestion des API Azure hello sont incorrectement en tunnel force le tooa local réseau client infrastructure. Ce flux réseau interrompt la gestion des API Azure. problème de toothis solution Hello est itinéraires de publication entre toostop de hello publics d’homologation toohello privés d’homologation chemin d’accès.


## <a name="troubleshooting"></a>Résolution des problèmes
Lorsque vous élaborez réseau tooyour de modifications, consultez trop[NetworkStatus API](https://docs.microsoft.com/en-us/rest/api/apimanagement/networkstatus), toovalidate si hello service de gestion des API n’a pas perdu tooany accès Hello ressources critiques qui il dépend. état de connectivité Hello doit être mis à jour toutes les 15 minutes.

## <a name="limitations"></a>Limitations
* Un sous-réseau contenant des instances du service Gestion des API ne peut pas contenir d’autres types de ressource Azure.
* sous-réseau de Hello et hello gestion des API service doit être hello même abonnement.
* Un sous-réseau contenant des instances du service Gestion des API ne peut pas être déplacé entre des abonnements.
* Lors de l’utilisation d’un réseau virtuel interne, seule une adresse IP interne sera disponible à partir de la plage de hello indiqué dans [RFC 1918](https://tools.ietf.org/html/rfc1918), une adresse IP publique ne peut pas être fournie.
* Pour les déploiements de gestion des API de plusieurs régions, avec des réseaux virtuels internes configurées, les utilisateurs sont chargés de gérer leur propres comme ils possèdent hello DNS d’équilibrage de charge.


## <a name="related-content"></a>Contenu connexe
* [Connexion d’un toobackend de réseau virtuel à l’aide de la passerelle Vpn](../vpn-gateway/vpn-gateway-about-vpngateways.md#s2smulti)
* [Connexion d’un réseau virtuel utilisant des modèles de déploiement différents](../vpn-gateway/vpn-gateway-connect-different-deployment-models-powershell.md)
* [Méthode d’appel de toouse hello tootrace d’inspecteur de l’API de gestion des API Azure](api-management-howto-api-inspector.md)

[api-management-using-vnet-menu]: ./media/api-management-using-with-vnet/api-management-menu-vnet.png
[api-management-setup-vpn-select]: ./media/api-management-using-with-vnet/api-management-using-vnet-type.png
[api-management-setup-vpn-select]: ./media/api-management-using-with-vnet/api-management-using-vnet-select.png
[api-management-setup-vpn-add-api]: ./media/api-management-using-with-vnet/api-management-using-vnet-add-api.png
[api-management-vnet-private]: ./media/api-management-using-with-vnet/api-management-vnet-private.png
[api-management-vnet-public]: ./media/api-management-using-with-vnet/api-management-vnet-public.png

[Enable VPN connections]: #enable-vpn
[Connect tooa web service behind VPN]: #connect-vpn
[Related content]: #related-content

[UDRs]: ../virtual-network/virtual-networks-udr-overview.md
[Network Security Group]: ../virtual-network/virtual-networks-nsg.md
