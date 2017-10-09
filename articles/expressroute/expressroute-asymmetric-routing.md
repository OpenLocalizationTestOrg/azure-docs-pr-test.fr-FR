---
title: le routage aaaAsymmetric | Documents Microsoft
description: "Cet article vous guide tout au long des problèmes hello que peut sont confrontés à un client de routage asymétrique dans un réseau qui possède plusieurs destination tooa de liens."
documentationcenter: na
services: expressroute
author: osamazia
manager: carmonm
editor: 
ms.assetid: a754bff9-95c9-44b5-9796-377fc21e8322
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: osamam
ms.openlocfilehash: 01a16242437a3674dcfe27b074911a829a6c1abd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="asymmetric-routing-with-multiple-network-paths"></a>Routage asymétrique avec chemins d’accès réseau multiples
Cet article explique comment le trafic réseau entrant et sortant peut emprunter différentes voies lorsque plusieurs chemins d’accès sont disponibles entre la source et la destination réseau.

Son important toounderstand deux concepts toounderstand asymétrique de routage. Un est effet hello de plusieurs chemins d’accès réseau. Hello autres est la façon dont les appareils, comme un pare-feu, conserver l’état de. Ces types d’appareils sont appelés appareils avec état. Une combinaison de ces deux facteurs crée des scénarios dans le réseau auquel le trafic est supprimé par un périphérique avec état, car les périphériques avec état hello n’a pas détecté que le trafic émane de périphérique hello lui-même.

## <a name="multiple-network-paths"></a>Chemins d’accès réseau multiples
Lorsqu’un réseau d’entreprise possède uniquement un lien toohello Internet via leur fournisseur de services Internet, tous les tooand le trafic à partir de hello Internet transite hello même chemin d’accès. Souvent, les entreprises achètent plusieurs circuits, en tant que chemins d’accès redondants, temps d’activité réseau tooimprove. Dans ce cas, il est possible que le trafic qui passe en dehors du réseau de hello, toohello Internet, passe par une liaison et hello retournent le trafic passe par un autre lien. Cela est communément appelé routage asymétrique. Dans le routage asymétrique, un trafic réseau inverse prend un autre chemin d’accès à partir de flux d’origine de hello.

![Réseau avec plusieurs chemins d’accès](./media/expressroute-asymmetric-routing/AsymmetricRouting3.png)

Bien qu’il se produit principalement sur hello Internet, également le routage asymétrique s’applique les combinaisons de tooother de plusieurs chemins d’accès. Il s’applique, par exemple, le chemin d’accès de tooan Internet et un chemin d’accès privé qui vont toohello même destination et toomultiple privé chemins toohello même destination.

Chaque routeur sur la façon de hello, à partir de la source toodestination, calcule hello meilleures chemin d’accès tooreach une destination. Hello détermination du routeur de la meilleure solution possible est basée sur deux facteurs principaux :

* Le routage entre des réseaux externes repose sur le protocole de routage BGP (protocole de passerelle frontière). BGP prend des publications de voisins et les exécute une série d’étapes toodetermine hello meilleures chemin toohello prévu de destination. Il stocke le chemin d’accès de la meilleure hello dans sa table de routage.
* la longueur d’un masque de sous-réseau associé à un itinéraire Hello influence des chemins de routage. Si un routeur reçoit plusieurs publications pour hello la même adresse IP mais avec les masques de sous-réseau différents, le routeur de hello préfère la publication hello avec un masque de sous-réseau plus long, car elle est considérée comme un routage plus spécifique.

## <a name="stateful-devices"></a>Appareils avec état
Routeurs rechercher l’en-tête IP d’un paquet hello à des fins de routage. Certains appareils Rechercher encore plus grande dans les paquets hello. En règle générale, ces appareils examinent les en-têtes Layer4 (Transmission Control Protocol ou TCP ; ou User Datagram Protocol ou UDP), ou même Layer7 (couche application). Ces types d’appareils sont soit des appareils de sécurité, soit des appareils d’optimisation de la bande passante. 

Un pare-feu est un exemple courant d’appareil avec état. Un pare-feu autorise ou refuse l’un toopass paquet via ses interfaces en fonction des différents champs comme protocole, port TCP/UDP et les en-têtes d’URL. Ce niveau de l’inspection des paquets place une charge importante sur les appareils hello. tooimprove des performances, les pare-feu hello inspecte hello du premier paquet un flux. Si elle autorise tooproceed de paquets hello, elle conserve les informations de flux de hello dans sa table d’état. Tous les flux de toothis connexes de paquets suivants sont autorisés en fonction de la détermination d’initiale hello. Sur le pare-feu hello peut-être arriver dans un paquet qui fait partie d’un flux existant. Si le pare-feu hello n’a aucune information de l’état antérieur à son sujet, le pare-feu hello supprime les paquets hello.

## <a name="asymmetric-routing-with-expressroute"></a>Routage asymétrique avec ExpressRoute
Lorsque vous vous connectez tooMicrosoft via Azure ExpressRoute, votre réseau est modifié comme suit :

* Vous avez plusieurs liens tooMicrosoft. Un lien est votre connexion Internet existante et hello autres est via ExpressRoute. Certains tooMicrosoft le trafic peut passer par hello Internet mais revenez via ExpressRoute, ou vice versa.
* ExpressRoute retourne des adresses IP plus spécifiques. Par conséquent, pour le trafic à partir de votre tooMicrosoft réseau pour les services offerts via ExpressRoute, les routeurs préfèrent toujours ExpressRoute.

toounderstand hello impact ces deux modifications sur un réseau, nous allons prendre en compte certains scénarios. Par exemple, vous avez uniquement un circuit toohello Internet et consommer de tous les services de Microsoft via Internet de hello. trafic Hello à partir de votre qui traverse le tooMicrosoft et inversement réseau hello même lien Internet et passe à travers le pare-feu hello. enregistrements de pare-feu Hello hello flux lorsqu’il voit le premier paquet de hello et renvoyer les paquets sont autorisés, car les flux hello existe dans la table d’état hello.

![Routage asymétrique avec ExpressRoute](./media/expressroute-asymmetric-routing/AsymmetricRouting1.png)

Ensuite, vous activez ExpressRoute et utilisez des services proposés par Microsoft via ExpressRoute. Tous les autres services de Microsoft sont consommées sur hello Internet. Vous déployez un pare-feu distinct à votre session est tooExpressRoute connecté. Microsoft publie plus préfixes tooyour réseau via ExpressRoute pour des services spécifiques. Votre infrastructure de routage choisit ExpressRoute comme chemin d’accès préféré de hello pour ces préfixes. Si vous publiez pas votre tooMicrosoft d’adresses IP publique via ExpressRoute, Microsoft communique avec vos adresses IP publiques via hello Internet. Transférer le trafic à partir de votre réseau de tooMicrosoft utilise ExpressRoute, et inverse le trafic à partir de Microsoft hello Internet. Lorsque le pare-feu sur le périmètre de hello hello voit un paquet de réponse pour un flux qu’il ne trouve pas dans la table d’état hello, il supprime le trafic de retour hello.

Si vous choisissez hello toouse pour ExpressRoute et hello Internet du pool même traduction d’adresses réseau (NAT), vous verrez des problèmes similaires avec des clients hello dans votre réseau sur des adresses IP privées. Demandes de services, telles que Windows Update accéder via hello Internet, car les adresses IP pour ces services ne sont pas publiés via ExpressRoute. Toutefois, le trafic de retour hello est restauré via ExpressRoute. Si Microsoft reçoit une adresse IP avec hello même masque de sous-réseau de hello Internet et ExpressRoute, il préfère ExpressRoute hello Internet. Si un pare-feu ou un autre périphérique avec état qui se trouve sur la périphérie du réseau et faisant face à ExpressRoute ne comporte aucune information préalable sur le flux de hello, il dépose les paquets hello appartenant toothat flux.

## <a name="asymmetric-routing-solutions"></a>Solutions de routage asymétrique
Vous avez deux problème de hello toosolve principales options de routage asymétrique. Une est par routage et hello autres est à l’aide de NAT basée sur la source (SNAT).

### <a name="routing"></a>Routage
Assurez-vous que vos adresses IP publiques sont des liaisons réseau (étendu WAN) tooappropriate publié. Par exemple, si vous souhaitez toouse hello Internet pour le trafic d’authentification et ExpressRoute pour le trafic de votre messagerie, vous ne devez pas publier vos adresses IP publiques de Services de fédération Active Directory (AD FS) via ExpressRoute. De même, veillez pas tooexpose un local reçoit des adresses tooIP du serveur AD FS qui hello routeur via ExpressRoute. Itinéraires reçus via ExpressRoute sont plus spécifiques afin qu’ils prendre le chemin d’accès préféré ExpressRoute hello pour l’authentification du trafic tooMicrosoft. Cela engendre un routage asymétrique.

Si vous souhaitez toouse ExpressRoute pour l’authentification, assurez-vous que vous publiez des adresses IP publiques AD FS via ExpressRoute sans NAT. De cette manière, le trafic provenant de Microsoft et passe tooan local passe de serveur AD FS via ExpressRoute. Trafic de retour provenant de clients tooMicrosoft utilise ExpressRoute, car il est privilégie hello sur hello Internet.

### <a name="source-based-nat"></a>NAT basé sur la source
Les problèmes de routage asymétrique peuvent également être résolus à l’aide d’une NAT basée sur la source (SNAT). Par exemple, vous n’avez pas publié les adresse IP publique hello d’un serveur de transfert de protocole SMTP (Simple Mail) sur site via ExpressRoute, car vous avez l’intention toouse hello Internet pour ce type de communication. Une demande qui est associée à Microsoft, puis se tooyour local serveur SMTP traverse hello Internet. Vous SNAT hello adresse IP entrante demande tooan interne. Inverse le trafic de hello SMTP serveur va toohello pare-feu de périmètre (que vous utilisez pour NAT) au lieu de via ExpressRoute. trafic de retour Hello repasse via hello Internet.

![Configuration réseau avec NAT basée sur la source](./media/expressroute-asymmetric-routing/AsymmetricRouting2.png)

## <a name="asymmetric-routing-detection"></a>Détection du routage asymétrique
Traceroute est toomake moyen hello meilleures sûr que votre trafic réseau transite par chemin d’accès hello attendu. Si vous pensez que le trafic à partir de votre local SMTP server tooMicrosoft tootake hello Internet chemin d’accès, hello attendu traceroute provient hello SMTP server tooOffice 365. résultat de Hello valide que le trafic sortant en effet de votre réseau vers hello Internet et non vers ExpressRoute.

