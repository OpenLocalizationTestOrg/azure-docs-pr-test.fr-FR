---
title: messagerie asynchrone du Bus aaaService | Documents Microsoft
description: Description de la messagerie asynchrone Azure Service Bus.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f1435549-e1f2-40cb-a280-64ea07b39fc7
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: sethm
ms.openlocfilehash: 5ab6ddf052155a9dd975b413cfaf393119c1999d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="asynchronous-messaging-patterns-and-high-availability"></a>Modèles de messagerie asynchrone et haute disponibilité

Une messagerie asynchrone peut être mise en œuvre de différentes façons. Avec les files d’attente, rubriques et abonnements, Azure Service Bus prend en charge des opérations asynchrones en utilisant un mécanisme de stockage et de transfert. Dans un fonctionnement normal (synchrone), vous envoyez des rubriques et des messages tooqueues et recevez des messages à partir de files d’attente et les abonnements. Les applications que vous rédigez dépendent de la disponibilité permanente de ces entités. Lors de l’intégrité de l’entité hello change, en raison de tooa d’autres circonstances, vous devez un tooprovide de façon une entité de fonctionnalité réduite qui peut satisfaire la plupart des besoins.

Les applications utilisent les échanges asynchrones modèles tooenable un nombre de scénarios de communication. Vous pouvez générer des applications dans lequel les clients peuvent envoyer des messages tooservices, même lorsque le service de hello n’est pas en cours d’exécution. Pour les applications qui rencontrent des pics de communications, une file d’attente peut aider à niveau hello charger en fournissant une communication de toobuffer sur place. Enfin, vous pouvez obtenir une charge simple mais efficace les messages toodistribute équilibrage sur plusieurs ordinateurs.

Commande toomaintain groupe à haute disponibilité d’un de ces entités, envisagez de plusieurs façons différentes, dans lequel ces entités peuvent apparaître non disponibles pour un système de messagerie durable. En règle générale, nous voyons les entités hello deviennent indisponibles tooapplications que nous écrivons Bonjour suivant de différentes façons :

* Impossible de toosend des messages.
* Impossible de tooreceive des messages.
* Impossible de toomanage entités (créer, récupérer, mettre à jour ou supprimer des entités).
* Service de hello toocontact impossible.

Pour chacun de ces défaillances, différents modes existent qui permettent un travail tooperform toocontinue de l’application à un niveau de fonctionnalité réduite. Par exemple, un système qui peut envoyer des messages mais pas de les recevoir peut encore recevoir des commandes des clients, mais ne peut pas traiter ces commandes. Cette rubrique aborde les problèmes qui peuvent se présenter et explique comment y remédier. Service Bus a introduit un certain nombre de solutions d’atténuation, vous devez adopter, et cette rubrique traite également hello règles régissant hello utilisent ces solutions d’atténuation de participer.

## <a name="reliability-in-service-bus"></a>Fiabilité de Service Bus
Il existe plusieurs façons de problèmes de messages et d’entités toohandle et des instructions gouvernent l’utilisation appropriée de hello de ces solutions d’atténuation. les instructions hello toounderstand, vous devez d’abord comprendre ce que peut échouer dans Service Bus. En raison de la conception toohello des systèmes Azure, tous ces problèmes ont tendance à courte durée de vie de toobe. À un niveau élevé, hello différentes causes d’indisponibilité apparaissent comme suit :

* Limitation d’un système externe dont Service Bus dépend. La limitation se produit à la suite d’interactions avec les ressources de stockage et de calcul.
* Problème d’un système dont Service Bus dépend. Par exemple, une partie donnée du stockage peut rencontrer des problèmes.
* Défaillance de Service Bus dans un sous-système unique Dans ce cas, un nœud de calcul peut entrer dans un état incohérent et qu’il doit être redémarré, à l’origine de toutes les entités son solde de tooload tooother nœuds. Pendant un bref laps de temps, le traitement des messages peut se trouver ralenti.
* Échec de Service Bus dans un centre de données Azure. Il s’agit d’une défaillance grave » » au cours de laquelle hello système est injoignable minutes, voire quelques heures.

> [!NOTE]
> terme de Hello **stockage** peut signifier le stockage Azure et SQL Azure.
> 
> 

Service Bus propose un certain nombre de mesures d’atténuation des problèmes mentionnés ci-dessus. Hello les sections suivantes décrivent chaque problème et leurs solutions d’atténuation respectives.

### <a name="throttling"></a>Limitation
Avec Service Bus, la limitation permet une gestion coopérative de la vitesse des messages. Chaque nœud Service Bus héberge de nombreuses entités. Chacune de ces entités sollicite système hello en termes de processeur, mémoire, stockage et autres facettes. Lorsqu’une de ces facettes détecte une utilisation dépassant les seuils définis, Service Bus peut refuser une demande donnée. Hello appelant reçoit un [ServerBusyException] [ ServerBusyException] et de nouvelles tentatives après 10 secondes.

Pour atténuer le problème, code de hello doit hello erreur de lecture et interrompre toute nouvelle tentative de message de type hello au moins 10 secondes. Étant donné que l’erreur de hello peut se produire sur différents composants de l’application de client hello, il est probable que chacun s’exécute indépendamment logique de nouvelle tentative hello. code de Hello peut réduire la probabilité de hello de limitation en autorisant le partitionnement sur une file d’attente ou une rubrique.

### <a name="issue-for-an-azure-dependency"></a>Problème sur une dépendance Azure
D’autres composants dans Azure peuvent parfois rencontrer des problèmes de service. Par exemple, lorsqu’un système Service Bus est en cours de mise à niveau, ce système peut provisoirement présenter des fonctionnalités réduites. toowork autour de ces types de problèmes, Service Bus régulièrement examine et implémente des solutions d’atténuation. Des effets secondaires de ces mesures de correction peuvent apparaître. Par exemple, toohandle temporaire problèmes de stockage, Service Bus implémente un système qui permet de manière cohérente toowork d’opérations d’envoi message. En raison de la nature toohello d’atténuation de hello, un message envoyé peut occuper tooappear minutes de too15 dans la file d’attente hello affecté ou d’un abonnement et est prêt pour une opération de réception. En règle générale, la plupart des entités ne rencontrent pas ce problème. Toutefois, étant donné nombre hello d’entités dans le Service Bus dans Azure, cette solution d’atténuation est parfois nécessaire pour un petit sous-ensemble de clients de Service Bus.

### <a name="service-bus-failure-on-a-single-subsystem"></a>Défaillance Service Bus dans un sous-système unique
Avec n’importe quelle application, les circonstances peuvent entraîner un composant interne de toobecome Service Bus incohérent. Lorsque le Service Bus détecte, il collecte les données à partir de tooaid d’application hello pour diagnostiquer ce qui est arrivé. Une fois la collecte des données de hello, application hello est redémarré dans une tentative tooreturn tooa un état cohérent. Ce processus se produit assez rapidement et résultats dans une entité toobe non disponible pour les tooa quelques minutes, si classique temps d’inactivité sont beaucoup plus courtes.

Dans ce cas, génère l’application cliente de hello un [System.TimeoutException] [ System.TimeoutException] ou [MessagingException] [ MessagingException] exception. Bus de service contient une atténuation pour ce problème dans l’écran hello de logique de nouvelle tentative automatisé des clients. Une fois hello issue du délai de nouvelle tentative et le message de type hello n’est pas remis, vous pouvez Explorer à l’aide d’autres fonctionnalités telles que [associés des espaces de noms][paired namespaces]. Les espaces de noms associés génèrent d’autres notifications, qui sont abordées dans cet article.

### <a name="failure-of-service-bus-within-an-azure-datacenter"></a>Panne de Service Bus dans un centre de données Azure.
Hello sont généralement dues d’une défaillance dans un centre de données Azure d’échec du déploiement mise à niveau de Service Bus ou un système qui en dépend. Plateforme de hello car a évolué, probabilité hello de ce type de défaillance a diminué. Un centre de données peut également se produire pour les raisons sont hello suivantes :

* Panne électrique (l’alimentation électrique et les générateurs de courant sont interrompus).
* Connectivité (interruption d’Internet entre vos clients et Azure).

Dans les deux cas, une catastrophe naturelle ou humaine a provoqué le problème de hello. toowork contourner ce problème et vous assurer que vous pouvez toujours envoyer des messages, vous pouvez utiliser [associés des espaces de noms] [ paired namespaces] tooenable toobe envoyé tooa deuxième emplacement des messages lors de l’emplacement principal de hello redevient sain. Pour plus d’informations, consultez la section [Meilleures pratiques pour protéger les applications contre les pannes de Service Bus et les sinistres][Best practices for insulating applications against Service Bus outages and disasters].

## <a name="paired-namespaces"></a>Espaces de noms associés
Hello [associés des espaces de noms] [ paired namespaces] fonctionnalité prend en charge les scénarios dans lesquels un déploiement dans un centre de données ou une entité de Service Bus n’est plus disponible. Alors que cet événement se produit rarement, les systèmes distribués toujours doivent être préparées toohandle pire des scénarios. En règle générale, cet événement se produit lorsque certains éléments dont dépend Service Bus rencontrent un problème de courte durée. disponibilité des applications toomaintain pendant la panne, les utilisateurs du Bus de Service peuvent utiliser des deux espaces de noms distincts, de préférence dans des centres de données distincts, toohost leurs entités de messagerie. reste Hello de cette section utilise hello suivant la terminologie :

* Espace de noms principal : hello d’espace de noms avec lequel votre application interagit pour envoyer et recevoir des opérations.
* Espace de noms secondaire : hello d’espace de noms qui agit comme un espace de noms principal toohello de sauvegarde. La logique d’application n’interagit pas avec cet espace de noms.
* Intervalle de basculement : quantité de hello de temps tooaccept normal d’échecs avant application hello bascule de hello espace de noms principal toohello espace de noms secondaire.

Les espaces de noms associés prennent en charge la *disponibilité des fonctions d’envoi*. Disponibilité conserve les messages toosend hello possibilité d’envoi. disponibilité d’envoi toouse, votre application doit répondre aux hello suivant les exigences :

1. Les messages sont reçus uniquement à partir de l’espace de noms principal hello.
2. Tooa de messages envoyés étant donné la file d’attente ou rubrique peut-être arriver dans le désordre.
3. Les messages au sein d’une session peuvent arriver dans le désordre. Ce comportement diffère du comportement normal des sessions. Cela signifie que votre application utilise des messages de groupe de toologically de sessions.
4. État de session est conservé uniquement sur l’espace de noms principal hello.
5. file d’attente principale de Hello permettre se mettre en ligne et commencer à accepter des messages avant de la file d’attente secondaire de hello remet tous les messages en file d’attente principale de hello.

Hello les sections suivantes abordent hello API, comment hello API sont implémentés et montre exemple de code qui utilise la fonctionnalité de hello. Notez que cette fonctionnalité est associée à des coûts.

### <a name="hello-messagingfactorypairnamespaceasync-api"></a>Hello les API MessagingFactory.PairNamespaceAsync
fonctionnalité des espaces de noms appariés Hello inclut hello [PairNamespaceAsync] [ PairNamespaceAsync] méthode sur hello [Microsoft.ServiceBus.Messaging.MessagingFactory] [ Microsoft.ServiceBus.Messaging.MessagingFactory] classe :

```csharp
public Task PairNamespaceAsync(PairedNamespaceOptions options);
```

Lors de la fin de la tâche hello, hello appariement d’espace de noms est également tooact terminé et prêt à pour toute [MessageReceiver][MessageReceiver], [QueueClient] [ QueueClient], ou [TopicClient] [ TopicClient] créé par hello [MessagingFactory] [ MessagingFactory] instance. [Microsoft.ServiceBus.Messaging.PairedNamespaceOptions] [ Microsoft.ServiceBus.Messaging.PairedNamespaceOptions] est la classe de base hello pour hello différents types de correspondance qui sont disponibles avec un [MessagingFactory] [ MessagingFactory] objet. Actuellement, hello uniquement de la classe dérivée est un nommé [SendAvailabilityPairedNamespaceOptions][SendAvailabilityPairedNamespaceOptions], qui implémente les exigences de disponibilité d’envoi hello. [SendAvailabilityPairedNamespaceOptions][SendAvailabilityPairedNamespaceOptions] possède un ensemble de constructeurs qui s’appuient les uns sur les autres. En examinant les constructeur hello avec hello la plupart des paramètres, vous pouvez comprendre comportement hello Hello autres constructeurs.

```csharp
public SendAvailabilityPairedNamespaceOptions(
    NamespaceManager secondaryNamespaceManager,
    MessagingFactory messagingFactory,
    int backlogQueueCount,
    TimeSpan failoverInterval,
    bool enableSyphon)
```

Ces paramètres ont hello suivant significations :

* *secondaryNamespaceManager*: initialisé [NamespaceManager] [ NamespaceManager] de l’instance de l’espace de noms secondaire hello que hello [PairNamespaceAsync] [ PairNamespaceAsync] méthode peut utiliser tooset hello espace de noms secondaire. Gestionnaire d’espace de noms Hello est liste de hello tooobtain utilisés de files d’attente dans l’espace de noms hello et toomake que les files d’attente du backlog hello requis existent. Si ce n’est pas le cas, ces files d’attente sont créées. [NamespaceManager] [ NamespaceManager] requiert hello capacité toocreate un jeton avec hello **gérer** de revendication.
* *messagingFactory*: hello [MessagingFactory] [ MessagingFactory] instance pour l’espace de noms secondaire hello. Hello [MessagingFactory] [ MessagingFactory] objet est toosend utilisé et, si hello [EnableSyphon] [ EnableSyphon] propriété a la valeur trop**true** , recevoir des messages des files d’attente du backlog hello.
* *backlogQueueCount*: nombre de hello de file d’attente toocreate des files d’attente. La valeur doit être au moins à 1. Lors de l’envoi du backlog de messages toohello, une de ces files d’attente est choisie de manière aléatoire. Si vous définissez hello valeur too1, seule file d’attente peut déjà utilisé. Lorsque cela se produit et hello une file d’attente génère des erreurs, client de hello n’est pas en mesure de tootry une autre file d’attente et peut échouer toosend votre message. Nous vous recommandons de définir cette valeur toosome plus grande valeur et par défaut hello valeur too10. Vous pouvez modifier cette tooa supérieur ou inférieur en fonction de la quantité de données votre application envoie par jour. Chaque file d’attente peut contenir jusqu'à Go too5 de messages.
* *failoverInterval*: durée hello au cours de laquelle vous acceptez les échecs sur l’espace de noms principal hello avant de passer d’une entité unique sur l’espace de noms secondaire toohello. Les basculements se produisent sur la base entité par entité. Les entités dans un espace de noms unique résident fréquemment sur différents nœuds au sein de Service Bus. La défaillance d’une entité n’implique pas nécessairement la défaillance d’une autre. Vous pouvez définir cette valeur trop[System.TimeSpan.Zero] [ System.TimeSpan.Zero] toohello toofailover secondaire immédiatement après votre première défaillance non transitoire. Les défaillances qui déclenchent le minuteur de basculement hello sont les [MessagingException] [ MessagingException] les Bonjour [IsTransient] [ IsTransient] propriété est false, ou un [System.TimeoutException][System.TimeoutException]. D’autres exceptions, telles que [UnauthorizedAccessException] [ UnauthorizedAccessException] ne provoquent pas de basculement, car ils indiquent que le client hello est incorrecte. A [ServerBusyException] [ ServerBusyException] n’entraîne pas de basculement, car le modèle correct de hello est toowait 10 secondes, puis renvoyez message de type hello.
* *enableSyphon*: indique que cet appariement doit également transférer les messages hello espace de noms secondaire toohello précédent espace de noms principal. En règle générale, les applications qui envoient des messages doivent définir cette valeur trop**false**; les applications qui reçoivent des messages doivent définir cette valeur trop**true**. raison Hello est que souvent, il existe moins destinataires expéditeurs de messages. En fonction du nombre de hello de destinataires, vous pouvez choisir toohave un droits SIPHON hello de handle d’instance application unique. L’utilisation de nombreux destinataires a un coût pour chaque file d’attente backlog.

toouse hello du code, créez un principal [MessagingFactory] [ MessagingFactory] de l’instance, une base de données secondaire [MessagingFactory] [ MessagingFactory] de l’instance, une base de données secondaire [NamespaceManager] [ NamespaceManager] instance et un [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] instance. appel de Hello peut être aussi simple que suivant de hello :

```csharp
SendAvailabilityPairedNamespaceOptions sendAvailabilityOptions = new SendAvailabilityPairedNamespaceOptions(secondaryNamespaceManager, secondary);
primary.PairNamespaceAsync(sendAvailabilityOptions).Wait();
```

Lorsque hello tâche retournée par hello [PairNamespaceAsync] [ PairNamespaceAsync] méthode se termine, tout est configuré et prêt toouse. Avant de la tâche hello est retournée, ne peut pas avoir tout travail d’arrière-plan hello nécessaire pour hello appariement toowork droite. Par conséquent, vous ne devez pas commencer l’envoi de messages jusqu'à ce que la tâche hello retourne. Si les échecs se sont produits, telles que les informations d’identification incorrectes ou les files d’attente de défaillance toocreate hello du backlog, ces exceptions seront levées une fois la tâche hello terminée. Une fois la tâche hello est retournée, vérifiez que les files d’attente hello ont été trouvés ou créées en examinant hello [BacklogQueueCount] [ BacklogQueueCount] propriété sur votre [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] instance. Pourquoi précédant le code, cette opération apparaît comme suit :

```csharp
if (sendAvailabilityOptions.BacklogQueueCount < 1)
{
    // Handle case where no queues were created.
}
```

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello de la messagerie asynchrone dans le Bus de Service, en savoir plus sur [associés des espaces de noms][paired namespaces].

[ServerBusyException]: /dotnet/api/microsoft.servicebus.messaging.serverbusyexception
[System.TimeoutException]: https://msdn.microsoft.com/library/system.timeoutexception.aspx
[MessagingException]: /dotnet/api/microsoft.servicebus.messaging.messagingexception
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Microsoft.ServiceBus.Messaging.MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[MessageReceiver]: /dotnet/api/microsoft.servicebus.messaging.messagereceiver
[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[TopicClient]: /dotnet/api/microsoft.servicebus.messaging.topicclient
[Microsoft.ServiceBus.Messaging.PairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.pairednamespaceoptions
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[SendAvailabilityPairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions
[NamespaceManager]: /dotnet/api/microsoft.servicebus.namespacemanager
[PairNamespaceAsync]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PairNamespaceAsync_Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_
[EnableSyphon]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_EnableSyphon
[System.TimeSpan.Zero]: https://msdn.microsoft.com/library/system.timespan.zero.aspx
[IsTransient]: /dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient
[UnauthorizedAccessException]: https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx
[BacklogQueueCount]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions?redirectedfrom=MSDN#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_BacklogQueueCount
[paired namespaces]: service-bus-paired-namespaces.md
