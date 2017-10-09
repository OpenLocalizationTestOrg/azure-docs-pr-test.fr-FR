---
title: "aaaWhat est Azure relais et pourquoi utiliser vue d’ensemble | Documents Microsoft"
description: "Présentation d’Azure Relay"
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1e3e971d-2a24-4f96-a88a-ce3ea2b1a1cd
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: 4cfd77048210a435c446b908b7896737cad0edbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-relay"></a>Qu’est-ce qu’Azure Relay ?

Hello relais Azure service facilite hybride applications en activant toosecurely vous exposent des services qui résident dans un cloud entreprise réseau toohello public, sans avoir tooopen connexion via un pare-feu, ou nécessitent contraignant change tooa infrastructure de réseau d’entreprise. Azure Relay prend en charge une grande variété de protocoles de transport et normes de services web.

service de relais Hello prend en charge traditionnelle à sens unique, de demande/réponse et le trafic de pair à pair. Il prend également en charge la distribution des événements sur les scénarios de publication/abonnement tooenable étendue d’internet et de communication de socket bidirectionnelle pour une efficacité accrue de point à point. 

Dans le modèle de transfert de données hello relayée, un service local connecte de service de relais toohello via un port sortant et crée un socket bidirectionnel pour l’adresse de communication liée tooa rendezvous particulier. Hello client peut ensuite communiquer avec service local de hello en envoyant le service de relais du trafic toohello ciblant hello rendezvous adresse. service de relais Hello « relaie ensuite « service local toohello des données via un client dédié tooeach de socket bidirectionnel. Hello client ne requiert un connexion directe toohello local service, il n’est pas requis tooknow hello service réside, alors que service local de hello n’a pas besoin de ports entrants ouverts sur les pare-feu hello.

les éléments de fonctionnalité clé Hello fournies par relais sont une communication bidirectionnelle, tamponnée au-delà des limites du réseau avec TCP semblable à la limitation, découverte de point de terminaison, le statut de connectivité et à superposer de sécurité du point de terminaison. capacités de relais Hello diffèrent des technologies d’intégration au niveau du réseau telles que VPN, dans ce relais peut être étendue tooa application unique point de terminaison sur un seul ordinateur, alors que la technologie VPN est beaucoup plus contraignant comme il s’appuie sur la modification d’environnement de réseau hello .

Azure Relay comprend deux fonctionnalités :

1. [Connexions hybrides](#hybrid-connections) - sockets d’ouvrir un site web standard hello utilise des scénarios de multi-plateforme.
2. [WCF relais](#wcf-relays) -appels de procédure distante tooenable utilise Windows Communication Foundation (WCF). Relais de WCF est relais hérité de hello offre que de nombreux clients utilisent déjà avec leur modèles de programmation de WCF.

Connexions hybrides et les relais WCF activer tooassets de connexion sécurisée qui existent au sein d’un réseau d’entreprise. Utilisation d’une par rapport à hello autres est dépend de vos besoins, comme décrit dans hello tableau suivant :

|  | Relais WCF | les connexions hybrides |
| --- |:---:|:---:|
| **WCF** |x | |
| **.NET Core** | |x |
| **.NET Framework** |x |x |
| **JavaScript/NodeJS** | |x |
| **Protocole Open basé sur des normes** | |x |
| **Plusieurs modèles de programmation RPC** | |x |

## <a name="hybrid-connections"></a>les connexions hybrides

Hello [connexions hybrides de relais Azure](relay-hybrid-connections-protocol.md) fonctionnalité est une évolution sécurisée, protocole ouvert de hello existants des fonctionnalités de relais qui peuvent être implémentées sur n’importe quelle plateforme et dans n’importe quel langage qui dispose d’une fonctionnalité WebSocket de base, qui n’inclut pas explicitement hello API WebSocket dans les navigateurs web. Les connexions hybrides sont basées sur HTTP et WebSockets.

### <a name="service-history"></a>Historique des services

Connexions HYBRIDES remplace l’ancienne hello, nommées fonctionnalité « Services BizTalk » qui a été générée hello Azure Service Bus Relay WCF de façon similaire. nouvelle fonctionnalité de connexions hybrides Hello complète la fonctionnalité de relais de WCF existante hello et ces deux fonctionnalités existent côte à côte dans le service de relais d’Azure hello. Elles partagent une passerelle commune, mais ont des implémentations différentes.

## <a name="wcf-relays"></a>Relais WCF

fonctionnement de relais de WCF Hello pour hello complet .NET Framework (NETFX) et pour WCF. Vous lancez la connexion hello entre votre service local et le service de relais hello à l’aide d’une suite de « relais » des liaisons WCF. Coulisses de hello, les liaisons de relais hello mappent toonew transport liaison éléments conçus toocreate canal composants WCF qui s’intègrent à Service Bus dans le cloud de hello.

## <a name="architecture-processing-of-incoming-relay-requests"></a>Architecture : Traitement des requêtes de relais entrantes
Lorsqu’un client envoie une demande toohello [Azure relais](/azure/service-bus-relay/) tooany de nœuds de passerelle hello achemine service, équilibrage de charge Azure hello. Si la demande de hello est une demande à l’écoute, nœud de passerelle hello crée un relais. Si la demande de hello est un relais spécifique de tooa de demande de connexion, nœud de passerelle hello transfère hello demande toohello passerelle nœud de connexion qui possède les relais hello. nœud de passerelle Hello qui possède les relais hello envoie un rendezvous demande toohello écoute client, demandant hello écouteur toocreate un nœud de passerelle toohello canal temporaire qui a reçu la demande de connexion hello.

Lors de la connexion de relais hello est établie, les clients de hello peuvent échanger des messages via le nœud de passerelle hello qui est utilisé pour les rendezvous hello.

![Traitement des requêtes WCF Relay entrantes](./media/relay-what-is-it/ic690645.png)

## <a name="next-steps"></a>Étapes suivantes

* [FAQ sur Azure Relay](relay-faq.md)
* [Créer un espace de noms](relay-create-namespace-portal.md)
* [Prise en main de .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Prise en main de Node](relay-hybrid-connections-node-get-started.md)

