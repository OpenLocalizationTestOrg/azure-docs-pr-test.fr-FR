---
title: "Considérations sur la topologie aaaNetwork lors de l’utilisation du Proxy d’Application Azure Active Directory | Documents Microsoft"
description: "Couvre les considérations sur la topologie du réseau lors de l’utilisation du proxy d’application Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 9b8cdd2196efeb92a74e44dde6511f7d3091a968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="network-topology-considerations-when-using-azure-active-directory-application-proxy"></a>Considérations sur la topologie du réseau lors de l’utilisation du proxy d’application Azure Active Directory

Cet article explique les considérations de topologie réseau lors de l’utilisation de l’application de proxy d’application Azure Active Directory (Azure AD) pour la publication et l’accès à distance de vos applications.

## <a name="traffic-flow"></a>Flux de trafic

Lorsqu’une application est publiée via le Proxy d’Application Azure AD, le trafic à partir d’applications de toohello utilisateurs hello passe par trois connexions :

1. Hello se connecte toohello Proxy d’Application Azure AD service point de terminaison public sur Azure
2. Hello service Proxy d’Application connecte le connecteur de Proxy d’Application toohello
3. connecteur de Proxy d’Application Hello connecte l’application cible de toohello

![Diagramme montrant le flux de trafic à partir de l’application utilisateur tootarget](./media/application-proxy-network-topologies/application-proxy-three-hops.png)

## <a name="tenant-location-and-application-proxy-service"></a>Emplacement du locataire et service de proxy d’application

Lorsque vous vous inscrivez pour un locataire Azure AD, région de hello de votre client est déterminée par pays hello que vous spécifiez. Lorsque vous activez le Proxy d’Application, les instances de service de Proxy d’Application hello pour votre client sont choisis ou créées Bonjour même région que votre client Azure AD ou tooit de région hello le plus proche.

Par exemple, si la région de votre locataire Azure AD est hello Union européenne (UE), tous les connecteurs de Proxy d’Application utilisent des instances de service dans des centres de données Azure Bonjour Europe. Lorsque vos utilisateurs un accès des applications publiées, leur trafic passe par les instances de service de Proxy d’Application hello dans cet emplacement.

## <a name="considerations-for-reducing-latency"></a>Considérations relatives à la réduction de la latence

Toutes les solutions de proxy ajoutent de la latence à votre connexion réseau. Quel que soit le proxy ou une solution VPN que vous choisissez en tant que votre solution d’accès à distance, il inclut toujours un ensemble de serveurs, l’activation de hello connexion tooinside votre réseau d’entreprise.

Les organisations comptent généralement des points de terminaison de serveur dans leur réseau de périmètre. Proxy d’Application Azure AD, toutefois, le trafic acheminé via le service de proxy hello dans le cloud de hello tandis que les connecteurs hello résident sur votre réseau d’entreprise. Aucun réseau de périmètre n’est requis.

les sections suivantes Hello contient toohelp d’autres suggestions vous réduisez encore davantage la latence. 

### <a name="connector-placement"></a>Placement d’un connecteur

Le Proxy d’application choisit emplacement hello d’instances pour vous, en fonction de votre emplacement du client. Toutefois, vous obtenez toodecide où le connecteur de hello tooinstall, ce qui vous donne hello caractéristiques de latence d’alimentation toodefine hello de votre trafic réseau.

Lorsque vous configurez hello service Proxy d’Application, demander hello suivant questions :

* Application hello emplacement ?
* Où se trouvent la plupart des utilisateurs qui ont accès à application hello située ?
* Instance de Proxy d’Application hello emplacement ?
* Vous disposez déjà d’un réseau dédié connexion tooAzure des centres de données configuré, comme Azure ExpressRoute ou d’un réseau privé virtuel similaire ?

connecteur de Hello a toocommunicate avec Azure et vos applications (étapes 2 et 3 dans le diagramme de flux de trafic hello), donc hello la sélection élective de la latence de hello hello connecteur affecte ces deux connexions. Lorsque vous évaluez la sélection élective hello du connecteur de hello, gardez Bonjour l’esprit les points suivants :

* Si vous souhaitez toouse la délégation Kerberos contrainte (KCD) pour l’authentification unique, puis connecteur de hello a besoin d’un centre de données de tooa de ligne de vue. En outre, le serveur de connecteur hello doit toobe joint au domaine.  
* En cas de doute, installez application toohello proche de hello connecteur.

### <a name="general-approach-toominimize-latency"></a>Latence de toominimize approche générale

Vous pouvez réduire la latence de hello du trafic de bout en bout hello en optimisant chaque connexion réseau. Chaque connexion peut être optimisée en :

* Réduire la distance entre deux extrémités de hello du saut de hello hello.
* En choisissant l’option tootraverse de réseau adéquat hello. Par exemple, parcourir un réseau privé et non hello Internet public peut être plus rapide, en raison des liens de toodedicated.

Si vous disposez d’une liaison VPN ou ExpressRoute dédiée entre Azure et votre réseau d’entreprise, vous souhaiterez peut-être toouse qui.

## <a name="focus-your-optimization-strategy"></a>Concentrer votre stratégie d’optimisation

Il est peu que vous pouvez effectuer la connexion de hello toocontrol entre vos utilisateurs et le service Proxy d’Application de hello. Les utilisateurs peuvent accéder à vos applications à partir d’un réseau domestique, d’un café ou d’un autre pays. Au lieu de cela, vous pouvez optimiser les connexions à partir des connecteurs toohello applications du Proxy d’Application toohello hello Proxy d’Application service hello. Incorporez hello suivant des modèles dans votre environnement.

### <a name="pattern-1-put-hello-connector-close-toohello-application"></a>Modèle 1 : Put hello connecteur toohello fermer application

Application cible place hello connecteur toohello Fermer dans le réseau de client hello. Cette configuration réduit l’étape 3 dans le diagramme de topographie hello, étant donné que l’application et le connecteur de hello sont proches. 

Si votre connecteur a besoin d’un contrôleur de domaine de ligne de vue toohello, ce modèle est avantageux. La plupart de nos clients utilisent ce modèle, car il fonctionne bien pour la majorité des scénarios. Ce modèle peut aussi être combiné avec le trafic de 2 toooptimize modèle entre le service de hello et de connecteur de hello.

### <a name="pattern-2-take-advantage-of-expressroute-with-public-peering"></a>Modèle 2 : Tirer parti d’ExpressRoute avec l’homologation publique

Si vous avez configuré avec l’homologation publique de ExpressRoute, vous pouvez utiliser la connexion ExpressRoute plus rapide de hello pour le trafic entre le Proxy d’Application et le connecteur de hello. connecteur de Hello est toujours sur votre réseau, fermer toohello application.

### <a name="pattern-3-take-advantage-of-expressroute-with-private-peering"></a>Modèle 3 : Tirer parti d’ExpressRoute avec l’homologation privée

Si vous avez une installation VPN ou ExpressRoute dédiée avec l’homologation privée entre Azure et votre réseau d’entreprise, vous avez une autre option. Dans cette configuration, réseau virtuel de hello dans Azure est généralement considéré comme une extension du réseau d’entreprise de hello. Par conséquent, vous pouvez installer le connecteur de hello Bonjour centre de données Azure et toujours satisfaire aux exigences de faible latence de hello de connexion du connecteur pour application hello.

La latence n’est pas compromise, car le trafic circule sur une connexion dédiée. Vous obtenez également améliorer la latence de connecteur de service Proxy d’Application, car le connecteur de hello est installé dans un emplacement du client Azure AD du centre de données Azure fermer tooyour.

![Diagramme illustrant un connecteur installé dans un centre de données Azure](./media/application-proxy-network-topologies/application-proxy-expressroute-private.png)

### <a name="other-approaches"></a>Autres approches

Bien que le focus hello de cet article est l’emplacement d’un connecteur, vous pouvez également modifier la sélection élective hello de hello application tooget meilleure latence.

De plus en plus d’organisations déplacent leurs réseaux dans des environnements hébergés. Cela leur permet de tooplace leurs applications dans un environnement hébergé qui fait également partie de leur réseau d’entreprise et être toujours dans le domaine de hello. Dans ce cas, les modèles de hello décrits dans les sections précédentes de hello peuvent être appliqué toohello nouvel emplacement d’application. Si vous envisagez cette option, consultez la page [Services de domaine Azure AD](../active-directory-domain-services/active-directory-ds-overview.md).

En outre, envisagez d’organiser vos connecteurs à l’aide de [groupes de connecteurs](active-directory-application-proxy-connectors.md) tootarget les applications qui se trouvent dans différents emplacements et des réseaux. 

## <a name="common-use-cases"></a>Cas d’utilisation courants

Dans cette section, nous allons étudier quelques scénarios courants. Supposons que hello locataire Azure AD (et par conséquent un point de terminaison de service proxy) se trouve dans hello États-Unis (US). Hello les observations présentées dans ces cas d’utilisation s’appliquent également des régions tooother monde hello.

Dans ces scénarios, nous appelons chaque connexion un « tronçon » et nous les numérotons dans un souci de simplification :

- **Sauts 1**: utilisateur toohello service Proxy d’Application
- **Sauts 2**: connecteur de Proxy d’Application de Proxy d’Application service toohello
- **Sauts 3**: application de Proxy d’Application connecteur toohello cible 

### <a name="use-case-1"></a>Cas d’utilisation 1

**Scénario :** application hello est dans un réseau d’entreprise Bonjour US, avec des utilisateurs dans hello même région. Aucun ExpressRoute ou un VPN n’existe entre hello centre de données Azure et de réseau d’entreprise de hello.

**Recommandation :** modèle de suivi 1, expliqué dans la section précédente de hello. Pour une latence améliorée, envisagez l’utilisation d’ExpressRoute, si nécessaire.

Il s’agit d’un modèle simple. Pour optimiser les sauts 3 en plaçant le connecteur hello côté application hello. C’est également un choix naturel, car le connecteur de hello est généralement installé avec ligne de vue toohello application et toohello centre de données tooperform KCD operations.

![Diagramme montrant que les utilisateurs, proxy, connecteur et application figurent tous dans hello nous](./media/application-proxy-network-topologies/application-proxy-pattern1.png)

### <a name="use-case-2"></a>Cas d’utilisation 2

**Scénario :** application hello est dans un réseau d’entreprise Bonjour US, avec des utilisateurs répartis de manière globale. Aucun ExpressRoute ou un VPN n’existe entre hello centre de données Azure et de réseau d’entreprise de hello.

**Recommandation :** modèle de suivi 1, expliqué dans la section précédente de hello. 

Là encore, hello est courant toooptimize saut 3, où vous placez le connecteur hello côté application hello. Saut 3 n’est pas généralement coûteuse, s’il s’agit dans hello même région. Toutefois, tronçon 1 peut être plus coûteux selon l’emplacement utilisateur de hello, étant donné que les utilisateurs au sein de Bonjour doivent accéder à l’instance de Proxy d’Application hello Bonjour des États-Unis. Il est important de noter que toutes les solutions de proxy ont des caractéristiques similaires en ce qui concerne les utilisateurs répartis globalement.

![Diagramme montrant que les utilisateurs sont réparties globalement, mais application connecteur et proxy de hello dans hello des États-Unis](./media/application-proxy-network-topologies/application-proxy-pattern2.png)

### <a name="use-case-3"></a>Cas d’utilisation 3

**Scénario :** application hello est dans un réseau d’entreprise Bonjour US. ExpressRoute avec l’homologation publique existe entre Azure et hello réseau d’entreprise.

**Recommandation :** suivent des modèles 1 et 2, expliqué dans la section précédente de hello.

Placez d’abord, connecteur hello aussi proche que possible toohello application. Ensuite, système de hello utilise automatiquement ExpressRoute tronçon 2. 

Si le lien de connexion ExpressRoute hello est à l’aide de l’homologation publique, hello passe le trafic entre le proxy de hello et le connecteur de hello sur ce lien. Le tronçon 2 a une latence optimisée.

![Diagramme montrant ExpressRoute entre le connecteur et le proxy de hello](./media/application-proxy-network-topologies/application-proxy-pattern3.png)

### <a name="use-case-4"></a>Cas d’utilisation 4

**Scénario :** application hello est dans un réseau d’entreprise Bonjour US. ExpressRoute avec l’homologation privée existe entre Azure et hello réseau d’entreprise.

**Recommandation :** modèle de suivi 3, expliqué dans la section précédente de hello.

Placez le connecteur de hello Bonjour centre de données Azure qui est connecté toohello le réseau d’entreprise via l’homologation privée ExpressRoute. 

connecteur de Hello peut être placée dans hello centre de données Azure. Étant donné que le connecteur de hello a toujours une ligne de vue toohello application et le centre de données de hello via le réseau privé de hello, saut 3 reste optimisé. En outre, le tronçon 2 est davantage optimisé.

![Diagramme montrant le connecteur de hello dans un centre de données Azure et ExpressRoute entre l’application et le connecteur de hello](./media/application-proxy-network-topologies/application-proxy-pattern4.png)

### <a name="use-case-5"></a>Cas d’utilisation 5

**Scénario :** application hello est dans un réseau d’entreprise Bonjour Europe, avec une instance de Proxy d’Application de hello et la plupart des utilisateurs Bonjour US.

**Recommandation :** connecteur de hello sur Place vers une application hello. Étant donné que les États-Unis utilisateurs accèdent à une instance de Proxy d’Application qui se produit toobe Bonjour même région, tronçon 1 n’est pas trop onéreuse. Le tronçon 3 est optimisé. Envisagez d’utiliser ExpressRoute toooptimize tronçon 2. 

![Diagramme indiquant les utilisateurs et proxy hello US, avec le connecteur de hello et l’application en hello Europe](./media/application-proxy-network-topologies/application-proxy-pattern5b.png)

Vous pouvez également envisager d’utiliser une autre variante dans cette situation. Si la plupart des utilisateurs dans l’organisation de hello sont Bonjour nous, puis sans doute que votre réseau s’étend toohello nous ainsi. Placer le connecteur de hello Bonjour des États-Unis et utiliser application toohello en ligne de réseau d’entreprise interne hello dédié Bonjour Europe. Les tronçons 2 et 3 sont ainsi optimisés.

![Diagramme montrant les utilisateurs, de proxy et de connecteur Bonjour US, application Bonjour Europe](./media/application-proxy-network-topologies/application-proxy-pattern5c.png)

## <a name="next-steps"></a>Étapes suivantes

- [Activer le proxy d’application](active-directory-application-proxy-enable.md)
- [Activer l’authentification unique](active-directory-application-proxy-sso-using-kcd.md)
- [Activer l’accès conditionnel](active-directory-application-proxy-conditional-access.md)
- [Résoudre les problèmes rencontrés avec le proxy d’application](active-directory-application-proxy-troubleshoot.md)
