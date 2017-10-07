---
title: aaaOverview des notions de base Azure Service Bus | Documents Microsoft
description: "Une présentation toousing Service Bus tooconnect logiciel de tooother applications Azure."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 12654cdd-82ab-4b95-b56f-08a5a8bbc6f9
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/15/2017
ms.author: sethm
ms.openlocfilehash: 1abd5cf310ef06ba35e1e2489a7c0a07e1797736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-bus"></a>Azure Service Bus

Si une application ou un service s’exécute dans le cloud de hello ou local, il doit souvent toointeract avec d’autres applications ou services. tooprovide un toodo largement utile, offres Microsoft Azure Service Bus. Cet article examine cette technologie, qui décrit ce qu’il est et vous pouvez souhaiter toouse il.

## <a name="service-bus-fundamentals"></a>Concepts de base de Service Bus

À chaque situation correspond un style de communication. Parfois, laissant les applications envoyer et recevoir des messages via une file d’attente simple est mieux hello. Dans d’autres situations, une file d’attente ordinaire n’est pas suffisante et une file avec mécanisme de publication et d’abonnement est une meilleure solution. Dans certains cas, vous avez simplement besoin d’une connexion entre les applications, sans file d’attente. Service Bus fournit les trois options, l’activation de votre toointeract d’applications de plusieurs façons différentes.

Service Bus est un service cloud mutualisée, ce qui signifie que le service de hello est partagé par plusieurs utilisateurs. Chaque utilisateur, telles que développeur d’applications, crée un *espace de noms*, puis définit les mécanismes de communication hello nécessaires au sein de cet espace de noms. La figure 1 montre à quoi ressemble cette architecture.

![][1]

**Figure 1 : Service Bus fournit un service de plusieurs locataire pour connecter des applications via le cloud de hello.**

Dans un espace de noms, vous pouvez utiliser une ou plusieurs instances de trois mécanismes de communication distincts, chacun se connectant de manière différente à l’application. choix de Hello sont :

* Les *files d’attente* permettent la communication unidirectionnelle. Chacune agit comme un intermédiaire (ou *broker*) qui stocke les messages envoyés jusqu’à leur réception. Chaque message est reçu par un destinataire unique.
* Les *rubriques* fournissent une communication unidirectionnelle à l’aide *d’abonnements* : une seule rubrique peut avoir plusieurs abonnements. Comme une file d’attente, une rubrique agit comme un service broker, mais chaque abonnement peut éventuellement utiliser un filtre tooreceive uniquement les messages qui correspondent aux critères spécifiques.
* Les *relais* permettent la communication bidirectionnelle. À l’inverse des files d’attente et des rubriques, le relais ne stocke pas les messages en transit ; il ne s’agit pas d’un intermédiaire. Au lieu de cela, il les transmet simplement sur l’application de destination toohello.

Lorsque vous créez une file d'attente, une rubrique ou un relais, vous lui donnez un nom. Associé à votre votre espace de noms, ce nom crée un identificateur unique pour l’objet de hello. Applications, vous peuvent fournir cette tooService nom Bus, puis utiliser cette file d’attente, rubrique ou relais toocommunicate avec l’autre. 

toouse un de ces objets dans le scénario de relais hello, Windows permet aux applications Windows Communication Foundation (WCF). Ce service est appelé [Relais WCF](../service-bus-relay/relay-what-is-it.md). Pour les files d’attente et les rubriques, les applications Windows peuvent utiliser des API de messagerie définie par Service Bus. toomake ces objets toouse plus facile à partir d’applications autres que Windows, Microsoft fournit des kits de développement logiciel pour Java, Node.js et d’autres langages. Vous pouvez également accéder aux files d’attente et aux rubriques à l’aide des [API REST](/rest/api/servicebus/) sur HTTP(s). 

Il est important de toounderstand que même si Service Bus lui-même s’exécute dans le cloud de hello (autrement dit, dans les centres de données de Microsoft Azure), les applications qui l’utilisent peuvent exécuter n’importe quel endroit. Vous pouvez utiliser des applications de tooconnect de Bus des services s’exécutant sur Azure, par exemple, ou les applications qui s’exécutent à l’intérieur de votre centre de données. Vous pouvez également l’utiliser tooconnect une application exécutée sur Azure ou une autre plateforme de cloud avec une application sur site ou avec des tablettes et téléphones. Il est même possible tooconnect appareils ménagers, capteurs et autres application centrale tooa de périphériques ou les tooone autres. Service Bus est un mécanisme de communication dans le cloud hello qui est accessible à partir de presque n’importe quel endroit. Comment vous utilisez cela dépend de quelles vos applications ont besoin toodo.

## <a name="queues"></a>Files d’attente

Supposons que vous décidez de tooconnect deux applications à l’aide d’une file d’attente Service Bus. La figure 2 illustre cette situation.

![][2]

**Figure 2 : les files d’attente Service Bus offrent un système de files d’attente unidirectionnelles asynchrones.**

processus de Hello est simple : un expéditeur envoie une file d’attente Service Bus de messages tooa et un récepteur récupère ce message à un moment ultérieur. Une file d’attente peut avoir un seul destinataire, comme l’indique la Figure 2, Ou, plusieurs applications peuvent lire à partir de hello même file d’attente. Dans ce dernier cas de hello, chaque message est lu par un seul récepteur. Dans le cas d’un service de multidiffusion, utilisez plutôt une rubrique.

Chaque message se compose de deux parties : un jeu de propriétés (chacun de type paire clé/valeur) et une charge utile de message. charge utile de Hello peut être binaire, texte ou même du XML. Leur utilisation dépend une application tente de toodo. Par exemple, une application qui envoie un message concernant une vente récente peut inclure des propriétés de hello **vendeur = « Ava »** et **quantité = 10000**. corps du message de salutation contient une image numérisée hello contrat de vente signé ou, s’il n’existe pas, reste vide.

Le destinataire peut lire le message de file d’attente Service Bus de deux façons. Hello première option, appelée  *[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode)*, supprime un message de la file d’attente hello et le supprime immédiatement. Cette option est simple, mais si le récepteur de hello se bloque avant la fin du traitement du message de type hello, le message de type hello est perdu. Car il est supprimé de la file d’attente hello, aucune autre récepteur ne peut y accéder. 

Hello deuxième option  *[PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode)*, est destiné à toohelp avec ce problème. Comme **ReceiveAndDelete**, un **PeekLock** lecture supprime un message de file d’attente hello. Elle ne supprime pas le message de salutation, toutefois. Au lieu de cela, il verrouille le message de type hello, rendant les récepteurs tooother invisible, puis attend qu’un des trois événements :

* Si le processus de récepteur hello hello message avec succès, elle appelle [Complete()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete), et de la file d’attente hello supprime le message de type hello. 
* Si le récepteur de hello décide qu’il ne peut pas traiter un message de type hello avec succès, elle appelle [Abandon()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon). file d’attente Hello supprime les verrous hello de message de type hello et rend disponible tooother récepteurs.
* Si le récepteur de hello appelle aucune de ces méthodes dans un délai configurable (par défaut, 60 secondes), file d’attente hello suppose de récepteur de hello a échoué. Dans ce cas, il se comporte comme si le récepteur de hello avait appelé **abandonner**, rendre hello tooother disponibles les récepteurs de messages.

Notez ce qui peut se produire : hello même message peut être remis à deux reprises, peut-être tootwo différents destinataires. Les applications qui utilisent des files d’attente Service Bus doivent pouvoir faire face à cet événement. toomake détection des doublons plus facile, chaque message possède un [MessageID](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) propriété par défaut reste hello identiques, quel que soit le nombre de fois message de type hello sont lu à partir d’une file d’attente. 

Les files d’attente sont utiles dans de nombreuses situations. Ils permettent des applications toocommunicate même lorsque les deux ne sont pas en cours d’exécution à hello même moment, ce qui s’avère particulièrement utile avec des applications mobiles et de lot. Une file d'attente avec plusieurs destinataires assure aussi un équilibrage automatique de la charge, car les messages sont répartis vers ces différents destinataires.

## <a name="topics"></a>Rubriques

Utile lorsqu’ils sont, les files d’attente ne sont pas toujours une solution adaptée hello. Parfois, les rubriques Service Bus sont plus utiles. La figure 3 illustre cette idée.

![][3]

**Figure 3 : En fonction de filtre hello spécifie d’une application abonnée, il peut recevoir certains ou tous les messages hello envoyé tooa la rubrique Service Bus.**

A *rubrique* est similaire dans la file d’attente de nombreuses façons tooa. Envoyer des expéditeurs rubrique tooa de messages Bonjour même manière qu’ils envoient la file d’attente de messages tooa et détaillée de ces messages hello même chose avec les files d’attente. Bonjour différence est que les rubriques activent chaque toocreate application réceptrice son propre *abonnement* en définissant un *filtre*. Un abonné puis voit uniquement les messages hello qui correspondent au filtre. Par exemple, la figure 3 présente un expéditeur et une rubrique avec trois abonnés, chacun disposant de son propre filtre :

* Abonné 1 reçoit uniquement les messages qui contiennent la propriété de hello *vendeur = « Ava »*.
* Abonné 2 reçoit les messages qui contiennent la propriété de hello *vendeur = « Ruby »* et/ou contiennent une *quantité* propriété dont la valeur est supérieure à 100 000. Peut-être Ruby est responsable des ventes hello, afin qu’elle veut toosee propres sales et toutes les ventes de grande taille, quelle que soit la qui les rend.
* Abonné 3 a défini son filtre trop*True*, ce qui signifie qu’il reçoit tous les messages. Par exemple, cette application peut être chargée pour la gestion d’une piste d’audit et il doit donc toosee tous les messages de type hello.

Comme avec les files d’attente, rubrique tooa d’abonnés peut lire les messages à l’aide [ReceiveAndDelete ou PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode). Contrairement aux files d’attente, toutefois, un seul message envoyé à tooa rubrique peut être reçu par plusieurs abonnements. Cette approche, souvent appelée *publier et s’abonner* (ou *pub/sub*), est utile lorsque plusieurs applications intéressent hello messages mêmes. En définissant un filtre de droite hello, chaque abonné peut exploiter simplement les partie hello du flux de messages hello qu’il doit toosee.

## <a name="relays"></a>relais

Les files d’attente et les rubriques permettent la communication asynchrone unidirectionnelle via un intermédiaire. Le trafic circule dans une seule direction, et il n’y a pas de connexion directe entre expéditeur et destinataire. Mais que faire si vous ne voulez pas de cette connexion ? Supposons que vos applications doivent tooboth envoyer et recevoir des messages peut-être vous souhaitez un lien direct entre eux et vous n’avez pas besoin d’un toostore de messages service broker. l’offre de Service Bus tooaddress des scénarios comme celui-ci, *relaie*, comme le montre la Figure 4.

![][4]

**Figure 4 : le relais Service Bus permet la communication bidirectionnelle synchrone entre applications.**

Hello tooask question évidente à propos des relais s’agit-il : Pourquoi dois-je l’utiliser ? Même si vous ne devez pas les files d’attente, pourquoi créer des applications communiquent via un service cloud au lieu de simplement interagir directement ? les réponses Hello sont qu’ils s’adressent directement peut être difficile que vous ne le pensez.

Supposons que vous souhaitez tooconnect deux applications locales, les deux en cours d’exécution à l’intérieur des centres de données d’entreprise. Chaque application se trouve derrière un pare-feu et chaque centre de données utilise probablement la traduction d’adresses réseau. Hello pare-feu bloque les données entrantes sur tous les ports quelques et NAT implique que chaque application s’exécute sur l’ordinateur hello ne dispose d’une adresse IP fixe, vous pouvez également accéder directement à partir de centre de données externe hello. Sans une aide supplémentaire, la connexion de ces applications sur hello internet public peut être problématique.

Un Service Bus Relay peut être utile. toocommunicate bidirectionnelle via un relais, chaque application établit une connexion TCP sortante avec Service Bus, puis conserve ouverte. Toutes les communications entre deux applications de hello transitent par ces connexions. Étant donné que chaque connexion a été établie à partir d’à l’intérieur du centre de données hello, hello pare-feu autorise application tooeach au trafic entrant sans ouvrir de nouveaux ports. Cette approche obtient également contourner problème NAT hello, étant donné que chaque application possède un point de terminaison cohérent dans le cloud hello tout au long de communication de hello. En échangeant des données via le relais de hello, les applications hello peuvent éviter les problèmes de hello qui seraient autrement difficile communication. 

toouse des relais Service Bus, les applications reposent sur hello Windows Communication Foundation (WCF). Service Bus fournit des liaisons WCF qui la rendent simple pour toointeract des applications Windows via le relais. Applications qui utilisent déjà WCF peuvent généralement spécifier l’une de ces liaisons, puis contactez tooeach autres via un relais. En effet, aucune bibliothèque standard n’est fournie.

Contrairement aux files d’attente et aux rubriques, les applications ne créent pas de relais de façon explicite. En revanche, lorsqu’une application qui souhaite tooreceive messages établit une connexion TCP avec Service Bus, un relais est créé automatiquement. Lors de la connexion de hello est supprimée, les relais hello sont supprimé. tooenable un relais de hello toofind application créé par un récepteur spécifique, Service Bus fournit un Registre permettant aux applications toolocate un relais spécifique par nom.

Les relais sont une solution adaptée hello lorsque vous avez besoin d’une communication directe entre les applications. Prenons par exemple le système de réservation d’une compagnie aérienne qui s’exécute sur un centre de données local qui peut être accessible à partir de bornes d’enregistrement, d’appareils mobiles et d’ordinateurs. Applications en cours d’exécution sur tous ces systèmes pourraient reposent sur les relais Service Bus dans hello cloud toocommunicate, partout où elles peuvent être en cours d’exécution.

## <a name="summary"></a>Résumé

Connexion d’applications a été toujours partie de la création de solutions complètes et plage hello de scénarios qui requièrent des applications et toocommunicate services avec l’autre a la valeur tooincrease étant plus d’applications et les périphériques connecté toohello internet. Grâce aux technologies informatiques pour atteindre une communication via les files d’attente, rubriques et relais, Service Bus vise toomake cette tooimplement plus facilement des fonctions essentielles et plus largement disponibles.

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez appris les notions de base de hello du Bus des services Azure, suivez ces liens de toolearn plus.

* Comment toouse [files d’attente Service Bus](service-bus-dotnet-get-started-with-queues.md)
* Comment toouse [rubriques Service Bus](service-bus-dotnet-how-to-use-topics-subscriptions.md)
* Comment toouse [relais Service Bus](../service-bus-relay/service-bus-dotnet-how-to-use-relay.md)
* [Exemples Service Bus](service-bus-samples.md)

[1]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_01_architecture.png
[2]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_02_queues.png
[3]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_03_topicsandsubscriptions.png
[4]: ./media/service-bus-fundamentals-hybrid-solutions/SvcBus_04_relay.png
