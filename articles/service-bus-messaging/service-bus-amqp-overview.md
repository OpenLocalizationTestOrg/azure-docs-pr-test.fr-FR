---
title: "aaaOverview d’AMQP 1.0 dans Azure Service Bus | Documents Microsoft"
description: "En savoir plus sur l’utilisation de hello Advanced Message Queuing Protocol (AMQP) 1.0 dans Azure."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0e8d19cc-de36-478e-84ae-e089bbc2d515
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/27/2017
ms.author: sethm
ms.openlocfilehash: c35a20c50dd24845d9a4c7a0251e8240848a6f4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="amqp-10-support-in-service-bus"></a>Prise en charge d’AMQP 1.0 dans Service Bus
Les deux hello Service service Bus Azure cloud et locales [Service Bus pour Windows Server (Service Bus 1.1)](https://msdn.microsoft.com/library/dn282144.aspx) prise en charge hello Message Queueing protocole AMQP (Advanced) 1.0. AMQP permet de vous toobuild inter-plateformes d’applications hybrides à l’aide d’un protocole standard ouvert. Vous pouvez générer des applications à l’aide de composants créés avec plusieurs langages et infrastructures, exécutées sur différents systèmes d’exploitation. Tous ces composants peuvent se connecter tooService Bus et échanger des messages professionnels structurés en toute transparence avec une fidélité optimale et efficacement.

## <a name="introduction-what-is-amqp-10-and-why-is-it-important"></a>Introduction : qu’est-ce qu’AMQP 1.0 ? En quoi ce protocole est-il important ?
Traditionnellement, les produits intergiciels (middleware) utilisent des protocoles propriétaires pour la communication entre les applications clientes et les services Broker. Cela signifie qu’une fois que vous avez sélectionné le broker de messagerie d’un fournisseur particulier, vous devez utiliser tooconnect de bibliothèques de ce fournisseur votre courtier de toothat d’applications client. Cela entraîne un degré de dépendance sur ce fournisseur, étant donné que le portage d’un produit de différentes applications tooa nécessite des modifications de code dans toutes les applications hello connecté. 

De plus, il est compliqué de connecter les services Broker de messagerie de différents fournisseurs. Ceci nécessite généralement les messages toomove pontage de niveau application à partir d’un système tooanother et tootranslate entre leurs formats de message propriétaire. Il s’agit d’une exigence courante ; par exemple, lorsque vous devez fournir un tooolder interface unifiée de nouveaux systèmes disparates, ou intégrer des systèmes informatiques suite de la fusion.

logiciels Hello est une entreprise rapide ; nouveaux langages de programmation et les infrastructures d’application sont introduits à un rythme parfois déconcertante. De même, les besoins de hello des systèmes informatiques évoluent au fil du temps et développeurs souhaitent parti tootake dernières fonctionnalités de plateforme hello. Cependant, parfois hello fournisseur de messagerie sélectionné ne prend pas en charge ces plateformes. Étant donné que les protocoles de messagerie sont propriétaires, il n’est pas possible pour d’autres bibliothèques tooprovide de ces nouvelles plateformes. Par conséquent, vous devez utiliser les approches tels que la création des passerelles ou ponts qui permettent de produit de messagerie toocontinue toouse hello.

développement Hello Hello Advanced Message Queuing Protocol (AMQP) 1.0 a été motivé par ces problèmes. Il a vu le jour chez JP Morgan Chase, qui, comme la plupart des entreprises proposant des services financiers, est un grand consommateur d’intergiciels orientés messagerie. objectif de Hello était simple : toocreate un protocole de messagerie sur une norme ouverte qui rend possible toobuild basée sur message des applications à l’aide des composants créés à l’aide de différents langages, structures et systèmes d’exploitation, tous à l’aide des composants à partir de pointe un plage de fournisseurs.

## <a name="amqp-10-technical-features"></a>Fonctionnalités techniques d’AMQP 1.0
AMQP 1.0 est un protocole de messagerie efficace et fiable, au niveau du réseau que vous pouvez utiliser toobuild robuste, inter-plateformes, applications de messagerie. protocole de Hello a un objectif simple : toodefine les mécanismes de hello hello sécurisée, fiable et efficace de transfert de messages entre deux parties. messages Hello eux-mêmes sont encodés à l’aide d’une représentation de données portable permettant hétérogènes messages à caractère commercial tooexchange structuré expéditeurs et destinataires avec une fidélité optimale. Hello Voici un résumé des fonctionnalités les plus importantes hello :

* **Efficace**: AMQP 1.0 est un protocole orienté connexion qu’utilise un codage de hello binaire des instructions de protocole et hello messages professionnels transférés par son biais. Il intègre le contrôle de flux sophistiqués schémas toomaximize hello l’utilisation de hello composants réseau et hello connecté. Ceci dit, le protocole de hello a été conçue toostrike un équilibre entre efficacité, flexibilité et interopérabilité.
* **Fiable**: hello protocole AMQP 1.0 permet de toobe de messages échangé avec une plage de garanties de fiabilité, d’incendie et oubliez tooreliable, exactement-remise EOD.
* **Flexible**: AMQP 1.0 est un protocole souple qui peut être utilisé toosupport différentes topologies. Hello même protocole peut être utilisé pour les communications client à client-à-un courtier et broker à l’autre.
* **Modèle de service Broker indépendant**: hello spécification AMQP 1.0 ne rend pas toutes les conditions requises sur le modèle de messagerie hello utilisé par un service broker. Cela signifie qu’il est possible tooeasily ajouter tooexisting de prise en charge d’AMQP 1.0 courtiers de messagerie.

## <a name="amqp-10-is-a-standard-with-a-capital-s"></a>AMQP 1.0 est une Norme (avec une majuscule N)
AMQP 1.0 est une norme internationale approuvée par les organismes ISO et IEC sous la dénomination ISO/IEC 19464:2014.

AMQP 1.0 est développé depuis 2008 par un groupe de plus de 20 entreprises, aussi bien fournisseurs de technologie que sociétés utilisatrices. Pendant ce temps, utilisatrices ont contribué à leurs besoins réels et hello ont fait évoluer hello protocole toomeet ces exigences. Tout au long du processus de hello, les fournisseurs ont participé ateliers dans lequel ils ont collaboré interopérabilité de hello toovalidate entre leurs implémentations.

En octobre 2011, le travail de développement hello transition tooa le comité technique au sein de l’organisation de hello pour hello OASIS Advancement of Structured Information Standards () et hello norme OASIS AMQP 1.0 a été publiée en octobre 2012. Hello entreprises suivantes ont participé au comité technique de hello pendant le développement hello Hello standard :

* **Fournisseurs de technologie** : Axway Software, Huawei Technologies, IIT Software, INETCO Systems, Kaazing, Microsoft, Mitre Corporation, Primeton Technologies, Progress Software, Red Hat, SITA, Software AG, Solace Systems, VMware, WSO2, Zenika.
* **Sociétés utilisatrices** : Bank of America, Crédit Suisse, Deutsche Boerse, Goldman Sachs, JPMorgan Chase.

Certaines des hello citée couramment des normes ouvertes avantages :

* Moins de risque de dépendance vis-à-vis d’un fournisseur
* Interopérabilité
* Large disponibilité des bibliothèques et outils
* Protection contre l’obsolescence
* Disponibilité du personnel qualifié
* Risque inférieur et gérable

## <a name="amqp-10-and-service-bus"></a>AMQP 1.0 et Service Bus
Prise en charge d’AMQP 1.0 dans Azure Service Bus signifie que vous pouvez maintenant tirer parti de hello queuing de Service Bus et de publication/abonnement des fonctionnalités de messagerie réparties dans une plage de plateformes à l’aide d’un protocole binaire efficace. De plus, vous pouvez générer des applications constituées de composants créés à l'aide de divers langages, structures et systèmes d'exploitation.

Hello figure suivante illustre un exemple de déploiement dans lequel les clients Java en cours d’exécution sur Linux, écrit à l’aide des API de Service JMS (Java Message) hello standard et les clients .NET s’exécutant sous Windows, échangent des messages via le Bus de Service à l’aide d’AMQP 1.0.

![][0]

**Figure 1 : exemple de scénario de déploiement illustrant la messagerie interplateforme avec Service Bus et AMQP 1.0**

À ce hello temps bibliothèques clientes suivantes sont connus toowork avec Service Bus :

| language | Bibliothèque |
| --- | --- |
| Java |Client Apache Qpid Java Message Service (JMS)<br/>Client IIT Software SwiftMQ Java |
| C |Apache Qpid Proton-C |
| PHP |Apache Qpid Proton-PHP |
| Python |Apache Qpid Proton-Python |
| C# |AMQP .Net Lite |

**Figure 2 : table des bibliothèques clientes d’AMQP 1.0**

## <a name="summary"></a>Résumé
* AMQP 1.0 est un protocole de messagerie ouvert et fiable, que vous pouvez utiliser les applications hybrides toobuild inter-plateformes. AMQP 1.0 est une norme OASIS.
* La prise en charge d’AMQP 1.0 est désormais disponible dans Azure Service Bus et Service Bus pour Windows Server (Service Bus 1.1). Le prix est hello que même que pour hello existant de protocoles.

## <a name="next-steps"></a>Étapes suivantes
Prêt toolearn plus ? Visitez hello suivant liens :

* [Utilisation de Service Bus à partir de .NET avec AMQP]
* [Utilisation de Service Bus à partir de Java avec AMQP]
* [Installation d’Apache Qpid Proton-C sur une machine virtuelle Linux Azure]
* [AMQP dans Service Bus pour Windows Server]

[0]: ./media/service-bus-amqp-overview/service-bus-amqp-1.png
[Utilisation de Service Bus à partir de .NET avec AMQP]: service-bus-amqp-dotnet.md
[Utilisation de Service Bus à partir de Java avec AMQP]: service-bus-amqp-java.md
[Installation d’Apache Qpid Proton-C sur une machine virtuelle Linux Azure]: service-bus-amqp-apache.md
[AMQP dans Service Bus pour Windows Server]: https://msdn.microsoft.com/library/dn574799.aspx
