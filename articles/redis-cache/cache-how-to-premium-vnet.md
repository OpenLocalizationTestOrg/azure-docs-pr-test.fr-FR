---
title: "aaaConfigure un réseau virtuel pour un Premium le Cache Redis Azure | Documents Microsoft"
description: "Découvrez comment toocreate et gérer la prise en charge de réseau virtuel pour vos instances de Cache Redis Azure de niveau Premium"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 8b1e43a0-a70e-41e6-8994-0ac246d8bf7f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: sdanie
ms.openlocfilehash: fab715f4d9365ee4c2f8b89d2e2e58768c25b671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-virtual-network-support-for-a-premium-azure-redis-cache"></a>Comment tooconfigure réseau virtuel prend en charge un Premium Azure Redis cache
Cache Redis Azure a différentes offres de cache, qui fournissent une certaine flexibilité hello les choix de la taille du cache et de fonctionnalités, y compris les fonctionnalités de niveau Premium telles que le clustering, la persistance et la prise en charge du réseau virtuel. Un réseau virtuel est un réseau privé dans le cloud de hello. Lorsqu’une instance de Cache Redis Azure est configurée avec un réseau virtuel, il n’est pas publiquement adressable et sont accessibles à partir d’ordinateurs virtuels et les applications de hello réseau virtuel. Cet article décrit comment les réseaux virtuels tooconfigure prennent en charge pour une instance de Cache Redis Azure premium.

> [!NOTE]
> Le Cache Redis Azure prend en charge les réseaux virtuels classiques et de Gestionnaire de ressources.
> 
> 

Pour plus d’informations sur d’autres fonctionnalités de cache premium, consultez [couche de présentation toohello Azure Redis Cache Premium](cache-premium-tier-intro.md).

## <a name="why-vnet"></a>Pourquoi un réseau virtuel ?
[Réseau virtuel Azure (VNet)](https://azure.microsoft.com/services/virtual-network/) déploiement offre une sécurité accrue et isolation pour votre Cache Redis Azure, ainsi que des sous-réseaux, les stratégies de contrôle d’accès, et d’autres fonctionnalités toofurther restreindre l’accès.

## <a name="virtual-network-support"></a>Prise en charge des réseaux virtuels
Prise en charge du réseau virtuel virtuel est configuré sur hello **nouveau Cache Redis** panneau lors de la création du cache. 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-premium-create.md)]

Une fois que vous avez sélectionné un niveau tarifaire premium, vous pouvez configurer l’intégration de réseau virtuel de Redis en sélectionnant un réseau virtuel qui se trouve dans hello même abonnement et l’emplacement que votre cache. toouse un nouveau réseau virtuel, créez-le tout d’abord en suivant les étapes de hello dans [créer un réseau virtuel à l’aide de hello portail Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) ou [créer un réseau virtuel (classiques) à l’aide de hello portail Azure](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) , puis revenez toohello **Nouveau Cache Redis** panneau toocreate et configurer votre cache premium.

tooconfigure hello réseau virtuel pour votre nouveau cache, cliquez sur **réseau virtuel** sur hello **nouveau Cache Redis** panneau et sélectionnez hello souhaitée réseau virtuel à partir de la liste déroulante de hello.

![Réseau virtuel][redis-cache-vnet]

Sélectionnez hello sous-réseau souhaité à partir de hello **sous-réseau** déroulante répertorier et spécifiez hello souhaité **adresse IP statique**. Si vous utilisez un Bonjour de réseau virtuel classique **adresse IP statique** champ est facultatif, et si aucun n’est spécifié, un est choisi de sous-réseau de hello sélectionné.

> [!IMPORTANT]
> Lorsque vous déployez un tooa de Cache Redis Azure Resource Manager VNet, le cache de hello doit être dans un sous-réseau dédié qui ne contient aucuns autres ressources à l’exception des instances de Cache Redis Azure. Si une tentative est faite toodeploy un tooa de Cache Redis Azure Resource Manager VNet tooa sous-réseau qui contient d’autres ressources, le déploiement de hello échoue.
> 
> 

![Réseau virtuel][redis-cache-vnet-ip]

> [!IMPORTANT]
> Azure réserve dans chaque sous-réseau des adresses IP qui ne peuvent pas être utilisées. Hello prénom et adresses IP des sous-réseaux de hello sont réservés pour la conformité de protocole, ainsi que les trois adresses plus utilisé pour les services Azure. Pour plus d’informations, consultez [Existe-t-il des restrictions sur l’utilisation des adresses IP au sein de ces sous-réseaux ?](../virtual-network/virtual-networks-faq.md#are-there-any-restrictions-on-using-ip-addresses-within-these-subnets)
> 
> Ajout des adresses IP toohello utilisé par l’infrastructure de réseau virtuel Azure hello, chaque Redis instance hello sous-réseau utilise deux adresses IP par partition et une adresse IP supplémentaire pour l’équilibrage de charge hello. Un cache non cluster est considéré comme toohave une seule partition.
> 
> 

Une fois le cache de hello est créé, vous pouvez afficher la configuration hello pour hello réseau virtuel en cliquant sur **réseau virtuel** de hello **menu ressource**.

![Réseau virtuel][redis-cache-vnet-info]

tooconnect tooyour Azure Redis cache instance lors de l’utilisation d’un réseau virtuel, spécifiez le nom d’hôte hello de votre cache dans la chaîne de connexion hello comme indiqué dans hello l’exemple suivant :

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5premium.redis.cache.windows.net,abortConnect=false,ssl=true,password=password");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

## <a name="azure-redis-cache-vnet-faq"></a>Forum aux questions sur le réseau virtuel de Cache Redis Azure
Hello suivant liste contient toocommonly des réponses aux questions sur la mise à l’échelle du Cache Redis Azure hello.

* [Quels sont les problèmes de configuration les plus courants au niveau du Cache Redis Azure et des réseaux virtuels ?](#what-are-some-common-misconfiguration-issues-with-azure-redis-cache-and-vnets)
* [Comment puis-je vérifier que mon cache fonctionne dans un réseau virtuel ?](#how-can-i-verify-that-my-cache-is-working-in-a-vnet)
* [Puis-je utiliser des réseaux virtuels avec un cache De base ou Standard ?](#can-i-use-vnets-with-a-standard-or-basic-cache)
* [Pourquoi la création d’un cache Redis échoue-t-elle dans certains sous-réseaux mais pas d’autres ?](#why-does-creating-a-redis-cache-fail-in-some-subnets-but-not-others)
* [Quelles sont les conditions d’espace d’adressage hello sous-réseau ?](#what-are-the-subnet-address-space-requirements)
* [Toutes les fonctionnalités fonctionnent-elles lorsque vous hébergez un cache dans un réseau virtuel ?](#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)

## <a name="what-are-some-common-misconfiguration-issues-with-azure-redis-cache-and-vnets"></a>Quels sont les problèmes de configuration les plus courants au niveau du Cache Redis Azure et des réseaux virtuels ?
Lorsque le Cache Redis Azure est hébergé dans un réseau virtuel, les ports hello Bonjour les tableaux suivants sont utilisés. 

>[!IMPORTANT]
>Si les ports hello Bonjour les tableaux suivants sont bloqués, le cache de hello peut ne pas fonctionne correctement. Un ou plusieurs de ces ports bloqués est problème de configuration incorrecte hello plus courant lors de l’utilisation du Cache Redis Azure dans un réseau virtuel.
> 
> 

- [Configuration requise de port sortant](#outbound-port-requirements)
- [Configuration requise de port entrant](#inbound-port-requirements)

### <a name="outbound-port-requirements"></a>Configuration requise de port sortant

Il existe sept configurations requises de port sortant.

- Si vous le souhaitez, toutes les connexions sortantes toohello internet peut être effectuées par le biais d’un client audit appareil local.
- Trois des ports de hello acheminer les points de terminaison du trafic tooAzure maintenance Azure Storage et Azure DNS.
- Hello restant des plages de ports et les communications de sous-réseau internes Redis. Aucune règle de groupe de sécurité réseau de sous-réseau n’est requise pour les communications sur sous-réseau Redis interne.

| Port(s) | Direction | Protocole de transfert | Objectif | Adresse IP locale | Adresse IP distante |
| --- | --- | --- | --- | --- | --- |
| 80, 443 |Règle de trafic sortant |TCP |Dépendances Redis sur Azure Storage/l’infrastructure à clé publique (Internet) | (sous-réseau Redis) |* |
| 53 |Règle de trafic sortant |TCP/UDP |Dépendances Redis sur le DNS (Internet/réseau virtuel) | (sous-réseau Redis) |* |
| 8443 |Règle de trafic sortant |TCP |Communications internes pour Redis | (sous-réseau Redis) | (sous-réseau Redis) |
| 10221-10231 |Règle de trafic sortant |TCP |Communications internes pour Redis | (sous-réseau Redis) | (sous-réseau Redis) |
| 20226 |Règle de trafic sortant |TCP |Communications internes pour Redis | (sous-réseau Redis) |(sous-réseau Redis) |
| 13000-13999 |Règle de trafic sortant |TCP |Communications internes pour Redis | (sous-réseau Redis) |(sous-réseau Redis) |
| 15000-15999 |Règle de trafic sortant |TCP |Communications internes pour Redis | (sous-réseau Redis) |(sous-réseau Redis) |


### <a name="inbound-port-requirements"></a>Configuration requise des ports entrants

Il existe huit configurations requises de port entrant. Les demandes entrantes de ces plages sont entrantes à partir d’autres services hébergés dans hello même réseau virtuel ou interne toohello communications de sous-réseau Redis.

| Port(s) | Direction | Protocole de transfert | Objectif | Adresse IP locale | Adresse IP distante |
| --- | --- | --- | --- | --- | --- |
| 6379, 6380 |Trafic entrant |TCP |L’équilibrage de charge de Azure tooRedis de communication client, | (sous-réseau Redis) |Réseau virtuel, Azure Load Balancer |
| 8443 |Trafic entrant |TCP |Communications internes pour Redis | (sous-réseau Redis) |(sous-réseau Redis) |
| 8500 |Trafic entrant |TCP/UDP |Équilibrage de charge Azure | (sous-réseau Redis) |Azure Load Balancer |
| 10221-10231 |Trafic entrant |TCP |Communications internes pour Redis | (sous-réseau Redis) |(Sous-réseau Redis) Azure Load Balancer |
| 13000-13999 |Trafic entrant |TCP |L’équilibrage de charge de Clusters, Azure tooRedis de communication client | (sous-réseau Redis) |Réseau virtuel, Azure Load Balancer |
| 15000-15999 |Trafic entrant |TCP |L’équilibrage de charge de Clusters, Azure tooRedis de communication client | (sous-réseau Redis) |Réseau virtuel, Azure Load Balancer |
| 16001 |Trafic entrant |TCP/UDP |Équilibrage de charge Azure | (sous-réseau Redis) |Azure Load Balancer |
| 20226 |Trafic entrant |TCP |Communications internes pour Redis | (sous-réseau Redis) |(sous-réseau Redis) |

### <a name="additional-vnet-network-connectivity-requirements"></a>Conditions supplémentaires pour la connectivité réseau VNET

Il existe des exigences de connectivité réseau pour le Cache Redis Azure qui peuvent ne pas être initialement satisfaites dans un réseau virtuel. Cache Redis Azure nécessite que tous les hello suivant toofunction éléments correctement lorsqu’il est utilisé dans un réseau virtuel.

* Réseau sortant connectivité tooAzure stockage points de terminaison dans le monde entier. Cela inclut les points de terminaison situés dans hello même région que l’instance de Cache Redis Azure hello, ainsi que les points de terminaison de stockage situés dans **autres** régions Azure. Résoudre les points de terminaison de stockage Azure sous hello suivant domaines DNS : *table.core.windows.net*, *blob.core.windows.net*, *queue.core.windows.net*et *file.core.windows.net*. 
* Sortant trop de connectivité réseau*ocsp.msocsp.com*, *mscrl.microsoft.com*, et *crl.microsoft.com*. Cette connectivité est une fonctionnalité SSL toosupport nécessaires.
* configuration du DNS pour le réseau virtuel de hello Hello doit être capable de résoudre tous les points de terminaison hello et domaines mentionné dans hello points précédents. Ces exigences DNS peuvent être remplies en garantissant une infrastructure DNS valide est configurée et gérée pour le réseau virtuel de hello.
* Toohello de connectivité réseau sortant suivant de surveillance Azure points de terminaison résoudre sous hello suivant domaines DNS : shoebox2-black.shoebox2.metrics.nsatc.net, Nord-prod2.prod2.metrics.nsatc.net, azglobal black.azglobal.metrics.nsatc.net, shoebox2-red.shoebox2.metrics.nsatc.net, est-prod2.prod2.metrics.nsatc.net, azglobal-red.azglobal.metrics.nsatc.net.

### <a name="how-can-i-verify-that-my-cache-is-working-in-a-vnet"></a>Comment puis-je vérifier que mon cache fonctionne dans un réseau virtuel ?

>[!IMPORTANT]
>Lors de la connexion d’instance de Cache Redis Azure tooan qui est hébergé dans un réseau virtuel, les clients doivent être dans le cache de votre hello même réseau virtuel, y compris les applications de test ou les outils de diagnostic de test ping.
>
>

Une fois les exigences du port hello sont configurés comme décrit dans la section précédente de hello, vous pouvez vérifier que votre cache fonctionne en effectuant hello comme suit.

- [Redémarrez](cache-administration.md#reboot) hello tous les nœuds de cache. Si toutes les Hello requises de dépendances de cache n’est pas accessible (comme décrit dans [entrant des exigences de ports](cache-how-to-premium-vnet.md#inbound-port-requirements) et [les exigences de port de sortie](cache-how-to-premium-vnet.md#outbound-port-requirements)), cache de hello ne pourra plus être en mesure de toorestart avec succès.
- Une fois les nœuds de cache hello ont redémarré (comme indiqué par état du cache hello Bonjour portail Azure), vous pouvez effectuer hello suite de tests :
  - ping hello cache du point de terminaison (à l’aide du port 6380) à partir d’un ordinateur qui se trouve dans hello même réseau virtuel en tant que hello mise en cache, à l’aide de [tcping](https://www.elifulkerson.com/projects/tcping.php). Par exemple :
    
    `tcping.exe contosocache.redis.cache.windows.net 6380`
    
    Si hello `tcping` outil signale que hello port est ouvert, le cache de hello est disponible pour la connexion à partir de clients Bonjour réseau virtuel.

  - Une autre façon tootest est toocreate un client de cache de test (qui peut être une simple application console à l’aide de StackExchange.Redis) qui se connecte toohello cache et ajoute et récupère des éléments du cache de hello. Installer hello exemple d’application cliente sur un ordinateur virtuel qui se trouve dans hello même réseau virtuel en tant que cache de hello et exécutez-le toohello cache de la connectivité tooverify.


### <a name="can-i-use-vnets-with-a-standard-or-basic-cache"></a>Puis-je utiliser des réseaux virtuels avec un cache De base ou Standard ?
Vous ne pouvez utiliser des réseaux virtuels qu’avec les caches de niveau Premium.

### <a name="why-does-creating-a-redis-cache-fail-in-some-subnets-but-not-others"></a>Pourquoi la création d’un cache Redis échoue-t-elle dans certains sous-réseaux mais pas d’autres ?
Si vous déployez un tooa de Cache Redis Azure Resource Manager VNet, le cache de hello doit être dans un sous-réseau dédié qui ne contient aucun autre type de ressource. Si une tentative est faite toodeploy un tooa de Cache Redis Azure Resource Manager VNet sous-réseau qui contient d’autres ressources, le déploiement de hello échoue. Vous devez supprimer les ressources existantes de hello hello sous-réseau avant de pouvoir créer un nouveau cache Redis.

Vous pouvez déployer plusieurs types de ressources tooa réseau virtuel classique tant que vous disposez d’assez IP adresses disponibles.

### <a name="what-are-hello-subnet-address-space-requirements"></a>Quelles sont les conditions d’espace d’adressage hello sous-réseau ?
Azure réserve dans chaque sous-réseau des adresses IP qui ne peuvent pas être utilisées. Hello prénom et adresses IP des sous-réseaux de hello sont réservés pour la conformité de protocole, ainsi que les trois adresses plus utilisé pour les services Azure. Pour plus d’informations, consultez [Existe-t-il des restrictions sur l’utilisation des adresses IP au sein de ces sous-réseaux ?](../virtual-network/virtual-networks-faq.md#are-there-any-restrictions-on-using-ip-addresses-within-these-subnets)

Ajout des adresses IP toohello utilisé par l’infrastructure de réseau virtuel Azure hello, chaque Redis instance hello sous-réseau utilise deux adresses IP par partition et une adresse IP supplémentaire pour l’équilibrage de charge hello. Un cache non cluster est considéré comme toohave une seule partition.

### <a name="do-all-cache-features-work-when-hosting-a-cache-in-a-vnet"></a>Toutes les fonctionnalités fonctionnent-elles lorsque vous hébergez un cache dans un réseau virtuel ?
Lorsque votre cache fait partie d’un réseau virtuel, uniquement les clients Bonjour réseau virtuel peuvent accéder les cache hello. Par conséquent, hello des fonctionnalités de gestion de cache suivantes ne fonctionnent pas pour l’instant.

* Redis Console - Redis la Console s’exécutant dans votre navigateur, qui est en dehors de hello réseau virtuel, il ne peut pas se connecter à tooyour cache.

## <a name="use-expressroute-with-azure-redis-cache"></a>Utiliser ExpressRoute avec le Cache Redis Azure
Les clients peuvent se connecter une [Azure ExpressRoute](https://azure.microsoft.com/services/expressroute/) infrastructure de réseau virtuel tootheir du circuit, en étendant leur tooAzure de réseau local. 

Par défaut, un circuit ExpressRoute nouvellement créé n’effectue pas de tunneling forcé (publication d’un routage par défaut, 0.0.0.0/0) sur un réseau virtuel. Par conséquent, connectivité Internet sortante est autorisée directement à partir de hello réseau virtuel et les applications clientes sont en mesure de tooconnect tooother Azure points de terminaison, y compris le Cache Redis Azure.

Cependant une configuration de client courants est toouse le tunneling forcé (publier un itinéraire par défaut) qui oblige sortant Internet trafic tooinstead flux localement. Ce flux de trafic sauts de connectivité avec le Cache Redis Azure si le trafic sortant de hello est ensuite bloqué locaux tels que hello instance de Cache Redis Azure n’est pas en mesure de toocommunicate avec ses dépendances.

solution de Hello est toodefine un (ou plusieurs) défini par l’utilisateur itinéraires (UDRs) sur le sous-réseau hello contenant hello du Cache Redis Azure. Un UDR définit les itinéraires de sous-réseau spécifique qui seront respectées au lieu de l’itinéraire par défaut hello.

Si possible, il est recommandé de hello toouse configuration suivante :

* configuration de ExpressRoute Hello annonce 0.0.0.0/0 et par défaut force tunnels tout le trafic sortant sur site.
* sous-réseau de toohello UDR appliqué contenant hello du Cache Redis Azure Hello définit 0.0.0.0/0 avec un itinéraire de travail pour toohello de trafic TCP/IP internet public ; par exemple en définissant un hello de tronçon suivant too'Internet de type'.

Bonjour effets combinés de ces étapes est qu’au niveau du sous-réseau UDR hello est prioritaire sur hello ExpressRoute forcé tunneling, garantissant ainsi un accès Internet sortant à partir de hello du Cache Redis Azure.

Instance de Cache Redis Azure tooan se connectant à partir d’une application locale à l’aide d’ExpressRoute n’est pas un scénario classique d’utilisation en raison des raisons de tooperformance (pour optimiser les performances du Cache Redis Azure, les clients doivent être Bonjour même région que hello du Cache Redis Azure).

>[!IMPORTANT] 
>Hello itinéraires définis dans un UDR **doit** être suffisamment spécifique tootake priorité sur les itinéraires annoncés par la configuration de ExpressRoute hello. Hello exemple suivant utilise la plage d’adresses 0.0.0.0/0 large hello et par conséquent peut potentiellement être accidentellement remplacée par les annonces d’itinéraires à l’aide de plages d’adresses plus spécifiques.

>[!WARNING]  
>Cache Redis Azure n’est pas pris en charge avec des configurations de ExpressRoute qui **incorrectement cross-publier d’itinéraires de hello publics d’homologation toohello privés d’homologation chemin**. Les configurations ExpressRoute ayant une homologation publique configurée reçoivent des annonces de routage en provenance de Microsoft pour un grand ensemble de plages d’adresses IP Microsoft Azure. Si ces plages d’adresses sont incorrectement entre publiés sur le chemin d’accès d’homologation privée hello, hello résulte que tous les paquets réseau sortant à partir du sous-réseau de l’instance de Cache Redis Azure hello sont incorrectement en tunnel force le tooa local réseau client infrastructure. Ce flux réseau interrompt le Cache Redis Azure. problème de toothis solution Hello est itinéraires de publication entre toostop de hello publics d’homologation toohello privés d’homologation chemin d’accès.


Vous trouverez des informations générales sur les itinéraires définis par l'utilisateur dans cette [présentation](../virtual-network/virtual-networks-udr-overview.md).

Pour plus d’informations sur ExpressRoute, voir [Aperçu technique d’ExpressRoute](../expressroute/expressroute-introduction.md).

## <a name="next-steps"></a>Étapes suivantes
Découvrez comment mettre en cache des fonctionnalités par toouse plus premium.

* [Couche de présentation toohello Azure Redis Cache Premium](cache-premium-tier-intro.md)

<!-- IMAGES -->

[redis-cache-vnet]: ./media/cache-how-to-premium-vnet/redis-cache-vnet.png

[redis-cache-vnet-ip]: ./media/cache-how-to-premium-vnet/redis-cache-vnet-ip.png

[redis-cache-vnet-info]: ./media/cache-how-to-premium-vnet/redis-cache-vnet-info.png

