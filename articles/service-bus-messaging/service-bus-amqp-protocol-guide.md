---
title: "aaaAMQP 1.0 dans Azure Service Bus et concentrateurs d’événements guide de protocole | Documents Microsoft"
description: "Protocole guide tooexpressions et une description de AMQP 1.0 dans Azure Service Bus et concentrateurs d’événements"
services: service-bus-messaging,event-hubs
documentationcenter: .net
author: clemensv
manager: timlt
editor: 
ms.assetid: d2d3d540-8760-426a-ad10-d5128ce0ae24
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: clemensv;hillaryc;sethm
ms.openlocfilehash: 882ce0fc84af11d9f61bc95dc3e4db0b67b2b020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# Guide du protocole AMQP 1.0 dans Azure Service Bus et Event Hubs

Hello Advanced Message Queueing protocole 1.0 est un protocole de tramage et transfert standardisé pour transférer en toute sécurité en mode asynchrone et fiable des messages entre deux parties. Il est hello principal de messagerie Azure Service Bus et Azure Event Hubs. Les deux services prennent également en charge le protocole HTTPS. Hello SBMP protocole propriétaire qui est également pris en charge est en cours de retrait des fonctionnalités en faveur d’AMQP.

AMQP 1.0 est un résultat hello de collaboration hétérogène qui rassembler des fournisseurs d’intergiciel (middleware), tels que Microsoft et Red Hat, comportant de nombreux utilisateurs intergiciel (middleware) de messagerie telles que JP Morgan Chase représentant le secteur des services financiers hello. forum de normalisation technique Hello pour les spécifications de protocole et l’extension AMQP hello est OASIS, et il a obtenu comme une norme internationale en tant que norme ISO/IEC 19494 formelles d’approbation.

## Objectifs

Cet article résume les concepts de base hello de spécification de messagerie hello AMQP 1.0 avec un petit ensemble de spécifications extension qui sont actuellement en cours de finalisation dans comité technique OASIS AMQP de hello brièvement et explique le fonctionnement d’Azure Service Bus implémente et s’appuie sur ces spécifications.

Hello vise pour tout développeur à l’aide d’une pile de client AMQP 1.0 existante sur n’importe quel toointeract en mesure de toobe plateforme avec Azure Service Bus via AMQP 1.0.

Les piles AMQP 1.0 courantes à usage général, telles que Apache Proton ou AMQP.NET Lite, implémentent déjà tous les mouvements AMQP 1.0 de base. Les mouvements fondamentaux sont parfois encapsulés avec une API de niveau supérieur ; Proton d’Apache offre même deux, hello impératif Messenger API et hello réactive réacteur API.

Bonjour suivant de discussion, nous supposons que gestion hello de connexions, sessions et la gestion des liens et hello de transferts de frame et de contrôle de flux AMQP sont gérées par la pile de hello respectifs (par exemple Apache Proton-C) et ne nécessitent pas beaucoup le cas échéant spécifique attention des développeurs d’applications. Nous supposons due existence hello de quelques API primitives, tels que tooconnect de capacité hello et toocreate une forme de *expéditeur* et *récepteur* objets abstraction, puis comprendre certaines formes de `send()`et `receive()` opérations, respectivement.

Lorsque nous aborderons les fonctionnalités avancées d’Azure Service Bus, telles que la recherche de messages ou la gestion des sessions, celles-ci seront expliquées en termes AMQP, mais également sous la forme d’une pseudo-implémentation en couche au-dessus de cette abstraction d’API supposée.

## Qu’est-ce que le protocole AMQP ?

AMQP est un protocole de tramage et de transfert. Le tramage signifie qu’il fournit la structure des flux de données binaires qui circulent dans les deux directions d’une connexion réseau. structure de Hello fournit délimitation pour différents blocs de données, appelées *frames*, toobe échangées entre les parties hello connecté. fonctionnalités de transfert Hello Assurez-vous que les deux parties communicantes peuvent établir une compréhension commune sur lorsque les frames sont transférés, et lorsque les transferts doivent être considérée comme terminés.

Contrairement aux précédemment expirées brouillon versions produites par groupe de travail AMQP hello qui sont en cours d’utilisation par plusieurs brokers de message, du groupe de travail hello final et standardisé AMQP 1.0 au protocole n’impose pas de présence de hello d’un courtier de messages ou de n’importe quelle topologie particulière pour les entités à l’intérieur d’un courtier de messages.

protocole de Hello peut être utilisé pour la communication de pair à pair symétrique, pour l’interaction avec des brokers de message qui prennent en charge des files d’attente et des entités de publication/abonnement, contrairement à Azure Service Bus. Il peut également être utilisé pour l’interaction avec l’infrastructure de messagerie où les modèles d’interaction hello sont différents des files d’attente standards, comme hello Azure Event Hubs. Un concentrateur d’événements agit comme une file d’attente lorsque les événements sont envoyés tooit mais agit plus comme un service de stockage série lorsque les événements sont lus à partir de celui-ci ; Il est quelque peu semblable un lecteur de bande. client de Hello choisit un décalage dans le flux de données disponibles hello et est ensuite pris en charge tous les événements à partir de ce décalage toohello dernière version disponible.

Hello protocole AMQP 1.0 est conçue toobe extensibles autres spécifications tooenhance ses fonctionnalités. trois spécifications extension Hello, présentées dans ce document pour illustrer ce propos. Pour les communications sur infrastructure HTTPS/WebSockets existante, où la configuration hello native AMQP des ports TCP peut être difficile, une spécification de liaison définit comment toolayer AMQP sur WebSockets. Pour interagir avec l’infrastructure de messagerie hello dans une demande/réponse manière à des fins de gestion ou des fonctionnalités avancée de tooprovide, spécification de la gestion hello AMQP définit des primitives d’interaction de base hello requis. Pour l’intégration de modèle d’autorisation fédérée, hello spécification de sécurité basée sur des revendications AMQP définit comment tooassociate et renouveler des jetons d’autorisation associés aux liens.

## Scénarios AMQP de base

Cette section explique l’utilisation de base hello d’AMQP 1.0 avec Service Bus de Azure, qui inclut la création de connexions, sessions et des liens et le transfert de messages tooand à partir des entités telles que les files d’attente, rubriques et abonnements Service Bus.

Hello plus autorité source toolearn sur le fonctionne du protocole AMQP est la spécification de hello AMQP 1.0, mais la spécification de hello a été écrite de mise en œuvre du guide tooprecisely et non pas le protocole de hello tooteach. Cette section se concentre sur la présentation de toute la terminologie nécessaire à la description de l’utilisation d’AMQP 1.0 par Service Bus. Pour un tooAMQP présentation plus complète, ainsi que d’une description plus détaillée d’AMQP 1.0, vous pouvez consulter [ce cours vidéo][this video course].

### Connexions et sessions

Hello d’appels AMQP communication programmes *conteneurs*; ces contiennent *nœuds*, qui hello communiquent les entités à l’intérieur de ces conteneurs. Une file d’attente peut être un nœud. AMQP permet de multiplexage, une seule connexion peut être utilisée pour plusieurs chemins d’accès de communication entre les nœuds ; par exemple, une application cliente peut simultanément recevoir à partir d’une file d’attente et de file d’attente de tooanother envoi via hello même connexion réseau.

![][1]

connexion de réseau Hello est donc ancrée sur le conteneur de hello. Il est initialisé par le conteneur hello dans le rôle de client hello qui effectue un conteneur de tooa de connexion de socket TCP sortant dans le rôle de récepteur hello, qui écoute et accepte les connexions TCP entrantes. la négociation de connexion Hello inclut la négociation de la version du protocole hello, déclaration ou négocier utilisation hello de sécurité de niveau Transport (TLS/SSL) et une négociation d’authentification/autorisation étendue hello connexion basée sur SASL.

Azure Service Bus requiert l’utilisation hello TLS à tout moment. Il prend en charge les connexions sur le port TCP 5671, selon laquelle la connexion TCP de hello est tout d’abord superposé avec TLS avant d’entrer la négociation de protocole AMQP hello et prend également en charge les connexions sur le port TCP 5672 : hello immédiatement propose une mise à niveau obligatoire de tooTLS de connexion à l’aide du modèle d’AMQP prescrit hello. liaison de AMQP WebSockets Hello crée un tunnel via le port TCP 443 qui est ensuite les 5671 connexions tooAMQP équivalent.

Après avoir configuré la connexion de hello et TLS, Service Bus offre deux options de mécanisme SASL :

* SASL brut est couramment utilisé pour le passage du serveur de tooa d’informations d’identification nom d’utilisateur et mot de passe. Service Bus n’a pas de compte, mais des [règles de sécurité d’accès partagé](service-bus-sas.md) nommées, qui confèrent des droits et sont associées à une clé. nom de Hello d’une règle est utilisé comme nom d’utilisateur hello et clé de hello (texte de codé en base64) est utilisée comme mot de passe hello. droits Hello associés hello choisi règle régissant les opérations de hello autorisées sur la connexion de hello.
* SASL anonyme est utilisé pour le contournement de l’autorisation de SASL lorsque le client de hello souhaite que le modèle de (CBS) toouse hello sécurité basée sur des revendications qui est décrite plus loin. Avec cette option, une connexion cliente peut être établie anonymement pendant une courte période pendant le hello client ne peut interagir avec le point de terminaison CBS hello et procédez de la négociation de CBS hello.

Une fois la connexion de transport hello est établie, les conteneurs hello chacun déclarent taille de trame maximale hello toohandle prêt, et elles après un délai d’inactivité ils allez déconnecter unilatéralement s’il n’existe aucune activité sur une connexion de hello.

Ils déclarent également le nombre de canaux simultanés pris en charge. Un canal est un chemin d’accès de transfert virtuel sortante unidirectionnelle par-dessus la connexion de hello. Une session prend un canal à partir de chaque chemin de communication hello conteneurs interconnectés tooform un bidirectionnelles.

Sessions ont un modèle de contrôle de flux basé sur la fenêtre ; Lorsqu’une session est créée, chaque partie déclare le nombre d’images, il est prêt tooaccept dans sa fenêtre de réception. Étant donné que transférées hello parties exchange frames, frames remplir que fenêtre et des transferts de s’arrêter lorsque la fenêtre hello est plein et jusqu'à ce que la fenêtre hello est réinitialisé ou développée à l’aide de hello *flux performative* (*performative*est hello AMQP terme mouvements au niveau du protocole échangés entre les parties hello deux).

Ce modèle basé sur la fenêtre est à peu près semblable toohello concept de TCP du contrôle de flux basé sur la fenêtre, mais au niveau session hello hello socket. Hello concept du protocole de permettant à plusieurs sessions simultanées existe afin que le trafic de priorité élevée peut être manquer son au-delà d’accélérée trafic normal, comme sur un couloir express route.

Azure Service Bus utilise actuellement une session pour chaque connexion. Hello Service Bus-taille de trame maximale est 262 144 octets (256 Ko) pour le Bus de Service Standard et les concentrateurs d’événements. Elle est de 1 048 576 (1 Mo) pour la version Premium de Service Bus. Service Bus n’impose pas de toute fenêtre de limitation de niveau session particulière, mais les réinitialisations hello fenêtre régulièrement dans le cadre du contrôle de flux au niveau du lien (consultez [hello section suivante](#links)).

Les connexions, les canaux et les sessions sont éphémères. Si la connexion sous-jacente de hello est réduit, les connexions, le tunnel TLS, SASL du contexte d’autorisation et les sessions doivent être rétablies.

### Liens

AMQP transfère les messages via des liens. Un lien est un chemin d’accès de communication créé sur une session qui permet le transfert de messages dans une direction ; négociation de statut de transfert Hello est sur le lien de hello et bidirectionnelles entre les parties hello connecté.

![][2]

Liens peuvent être créés par un conteneur à tout moment et sur une session existante, ce qui rend AMQP différent de nombreux protocoles, y compris HTTP et MQTT, où l’émission de hello de transfert et le chemin d’accès de transfert est un privilège exclusif du tiers hello création connexion du socket Hello.

conteneur qui initie le lien de Hello pose hello opposé conteneur tooaccept un lien, il choisit un rôle d’expéditeur ou récepteur. Par conséquent, conteneur peut lancer la création unidirectionnelle ou chemins d’accès de la communication bidirectionnelle, par hello ce dernier se modélisée en tant que paires de liens.

Des liens sont nommés et associés à des nœuds. Comme indiqué dans le début de hello, les nœuds sont hello communique des entités à l’intérieur d’un conteneur.

Dans Service Bus, un nœud est équivalent tooa file d’attente, une rubrique, un abonnement ou une sous-file d’attente de lettres mortes d’une file d’attente ou d’abonnement. nom du nœud Hello utilisé dans AMQP est par conséquent hello nom relatif d’entité hello au sein de l’espace de noms Service Bus hello. Si une file d’attente est nommée **myqueue**, ce dernier est également son nom de nœud AMQP. Un abonnement à une rubrique suit la convention d’API HTTP hello par en cours de tri dans une collection de ressources « abonnements » et par conséquent, un abonnement **sub** ou une rubrique **mytopic** a du nom de nœud hello AMQP **mytopic/abonnements/sub**.

Hello client se connectant est également requis toouse un nom de nœud local pour la création de liens ; Bus de service n’est pas recommandée sur les noms de nœud et n’interprète pas les. En règle générale, les piles de client AMQP 1.0 utilisent un tooassure de schéma que ces noms de nœud éphémères sont uniques dans la portée de hello du client de hello.

### Transferts

Une fois qu’un lien a été établi, les messages peuvent être transférés via celui-ci. Dans AMQP, un transfert est exécuté avec un mouvement de protocole explicite (hello *transfert* performative) qui déplace un message à partir de l’expéditeur tooreceiver sur un lien. Un transfert est terminé lorsqu’il est « réglée, » ce qui signifie que les deux parties ont établie une compréhension commune des résultats hello de ce transfert.

![][3]

Dans le cas le plus simple hello, l’expéditeur de hello peut choisir les messages toosend « préalable réglées », ce qui signifie que les clients hello n’est pas intéressé par résultat de hello et récepteur de hello ne fournit pas de vos commentaires concernant les opération hello résultat hello. Ce mode est pris en charge par Service Bus à hello au niveau du protocole AMQP, mais pas exposé dans une des API clientes de hello.

Hello régulière cas est que les messages sont envoyés non réglées et récepteur de hello puis indique l’acceptation ou refus à l’aide de hello *disposition* performative. Rejet se produit lorsque le récepteur de hello ne peut pas accepter un message de type hello pour une raison quelconque, et le message de rejet hello contient des informations sur la raison de hello, qui est une structure d’erreur définie par l’AMQP. Si les messages sont rejetés en raison d’erreurs toointernal à l’intérieur du Bus des services, service de hello retourne des informations supplémentaires à l’intérieur de cette structure peut être utilisée pour fournir des diagnostics personnel de toosupport indicateurs si vous utilisez des demandes de prise en charge. Nous aborderons les erreurs plus en détail ultérieurement.

Une forme particulière de rejet est hello *publié* d’état, ce qui signifie que récepteur hello n’a aucun transfert de toohello objection technique, mais également aucun intérêt en réglant ne hello transfert. Que cas existe, par exemple, lorsqu’un message est remis client de Service Bus tooa et client de hello choisit trop « abandonner « message de type hello, car il ne peut pas effectuer le travail hello résultant du traitement du message de type hello ; remise des messages Hello lui-même n’est pas en cause. Une variation de cet état est hello *modifié* état, ce qui permet à message toohello de modifications qu’elles sont publiées. Cet état n’est pas utilisé par Service Bus à l’heure actuelle.

Hello spécification AMQP 1.0 définit une autre disposition état appelé *reçu*, qui aide à récupération du lien toohandle. Récupération du lien permet de reconstituer état hello d’un lien et en attente des remises sur une nouvelle connexion et la session, lorsque les connexion préalable hello et la session ont été perdues.

Service Bus ne prend pas en charge la récupération du lien ; Si le client de hello perd hello connexion tooService Bus avec un message non réglé transférer en attente, ce transfert de message est perdu et hello du client doit se reconnecter, rétablissement de la liaison de hello et essayer des transférer hello.

Par conséquent, Service Bus et concentrateurs d’événements prennent en charge « au moins une fois » transferts où hello expéditeur puisse être assurée pour le message de type hello ayant été stockées et acceptés, mais ne gèrent pas « exactement une fois » transferts à hello niveau AMQP, où le système de hello tentent toorecover Hello lien et continuer la duplication de tooavoid toonegotiate hello remise état hello de transfert de messages.

toocompensate les doublons possibles envoie, Service Bus prend en charge la détection des doublons comme une fonctionnalité facultative sur les files d’attente et rubriques. Les enregistrements de détection des doublons hello ID des messages de tous les messages entrants pendant une période définie par l’utilisateur, puis en mode silencieux supprime avec que tous les messages envoyés hello mêmes message-ID au cours de cette même fenêtre.

### Contrôle de flux

De plus de contrôle de flux au niveau de la session toohello modèle qui décrit précédemment, chaque lien a son propre modèle de flux de contrôle. Contrôle de flux au niveau de la session protège conteneur de hello de ne pas avoir de toohandle trop grand nombre d’images à une seule fois, contrôle de flux au niveau du lien place application hello responsable combien messages toohandle souhaite disposer d’un lien et quand.

![][4]

Sur un lien, transferts ne peuvent se produire lorsque hello expéditeur est suffisant *lien crédit*. Crédit de lien est un ensemble de compteurs en récepteur hello à l’aide de hello *flux* performative, qui est une étendue tooa lien. Lors de l’expéditeur de hello est attribué le crédit de lien, il tente toouse de ce crédit par la remise des messages. Chaque décrémente de remise de message hello crédit restant de lien par 1. Lorsque le crédit de lien de hello est utilisé, les remises arrêter.

Lorsque le Service Bus est dans le rôle de récepteur hello, fournit instantanément l’expéditeur de hello avec crédit de lien propose un grand nombre, afin que les messages peuvent être envoyés immédiatement. Comme lien crédit est utilisé, le Service Bus envoie occasionnellement un *flux* solde du crédit lien toohello performative expéditeur tooupdate hello.

Dans le rôle d’expéditeur hello, Service Bus envoie toouse de messages de crédit lien en attente.

Se traduit par un appel de « réception » au niveau de l’API de hello un *flux* performative est envoyé tooService Bus par client de hello et Service Bus consomme que tout d’abord de crédit en prenant les hello, message de file d’attente de hello, verrouiller, déverrouillé et transférer. Si aucun message n’est immédiatement disponible pour la remise, tout crédit en suspens par n’importe quel lien établi avec qu’entité particulière reste enregistrée dans l’ordre d’arrivée et les messages sont verrouillés et transférées dès qu’elles deviennent disponibles, toouse tout crédit en cours.

verrou de Hello sur un message est libéré lorsque le transfert de hello est réglé dans un des États de Terminal Server hello *accepté*, *rejeté*, ou *publié*. message de type Hello est supprimé de Service Bus lorsque l’état de terminal hello est *accepté*. Il reste dans Service Bus et est remis récepteur suivant de toohello lorsque le transfert de hello atteint un des hello autres États. Service Bus déplace automatiquement le message de type hello en file d’attente de lettres mortes de l’entité hello lorsqu’il atteint le nombre maximal de diffusions de hello autorisé pour l’entité hello en raison des rejets de toorepeated ou de versions.

Même si hello API Service Bus n’exposent pas directement une telle option aujourd'hui, un client de protocole AMQP de niveau inférieur peut utiliser hello crédit de lien modèle tooturn hello de style « pull » une interaction de l’émission d’une unité de crédit pour chaque demande de réception dans un modèle de style « push » en émettant un grand nombre de lien crédits et puis recevoir des messages dès qu’elles sont disponibles sans intervention supplémentaire. Push est pris en charge par le biais hello [MessagingFactory.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PrefetchCount) ou [MessageReceiver.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_PrefetchCount) les paramètres de propriété. Lorsqu’ils sont non nulle, client AMQP l’hello utilise en tant que crédit de lien de hello.

Dans ce contexte, sa, toounderstand important de qui hello horloge l’expiration du verrou hello sur le message de salutation au sein de l’entité de hello hello démarre lorsque hello message provient de l’entité de hello, pas lorsque message de type hello est placé sur le câble de hello. Chaque fois que le client de hello indique la disponibilité de messages de tooreceive en émettant le crédit de lien, est attendu toobe messages activement extraction réseau hello et être prêt toohandle les. Sinon, verrou de message hello a peut-être expiré avant que le message de type hello est remis même. utilisation de Hello credit de liaison de contrôle de flux doit refléter directement toodeal de préparation immédiate hello avec les messages disponibles distribués toohello récepteur.

En résumé, hello sections suivantes fournissent une vue d’ensemble schématique de flux de performative hello lors des interactions de l’API. Chaque section décrit une opération logique différente. Certaines de ces interactions peuvent être « différées », ce qui signifie qu’elles peuvent être effectuées uniquement en cas de besoin. Création d’un expéditeur du message ne peut pas provoquer une interaction réseau jusqu'à ce que le premier message de type hello est envoyé ou demandé.

des flèches de Hello Bonjour tableau suivant indiquent la direction du flux performative hello.

#### Création du destinataire du message

| Client | SERVICE BUS |
| --- | --- |
| --> attach(<br/>name={nom du lien},<br/>handle={gestion numérique},<br/>role=**receiver**,<br/>source={nom de l’entité},<br/>target={id du lien client}<br/>) |Client joint tooentity en tant que récepteur |
| Réponses de service Bus attachement en fin de lien de hello |<-- attach(<br/>name={nom du lien},<br/>handle={gestion numérique},<br/>role=**sender**,<br/>source={nom de l’entité},<br/>target={id du lien client}<br/>) |

#### Création de l’expéditeur du message

| Client | SERVICE BUS |
| --- | --- |
| --> attach(<br/>name={nom du lien},<br/>handle={gestion numérique},<br/>role=**sender**,<br/>source={id du lien client},<br/>target={nom de l’entité}<br/>) |Aucune action |
| Aucune action |<-- attach(<br/>name={nom du lien},<br/>handle={gestion numérique},<br/>role=**receiver**,<br/>source={id du lien client},<br/>target={nom de l’entité}<br/>) |

#### Création de l’expéditeur du message (erreur)

| Client | SERVICE BUS |
| --- | --- |
| --> attach(<br/>name={nom du lien},<br/>handle={gestion numérique},<br/>role=**sender**,<br/>source={id du lien client},<br/>target={nom de l’entité}<br/>) |Aucune action |
| Aucune action |<-- attach(<br/>name={nom du lien},<br/>handle={gestion numérique},<br/>role=**receiver**,<br/>source=null,<br/>target=null<br/>)<br/><br/><-- detach(<br/>handle={gestion numérique},<br/>closed=**true**,<br/>error={infos sur l’erreur}<br/>) |

#### Fermeture de l’expéditeur/du destinataire du message

| Client | SERVICE BUS |
| --- | --- |
| --> detach(<br/>handle={gestion numérique},<br/>closed=**true**<br/>) |Aucune action |
| Aucune action |<-- detach(<br/>handle={gestion numérique},<br/>closed=**true**<br/>) |

#### Envoi (réussite)

| Client | SERVICE BUS |
| --- | --- |
| --> transfer(<br/>delivery-id={gestion numérique},<br/>delivery-tag={gestion binaire},<br/>settled=**false**,,more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |Aucune action |
| Aucune action |<-- disposition(<br/>role=receiver,<br/>first={id d’envoi},<br/>last={id d’envoi},<br/>settled=**true**,<br/>state=**accepted**<br/>) |

#### Envoi (erreur)

| Client | SERVICE BUS |
| --- | --- |
| --> transfer(<br/>delivery-id={gestion numérique},<br/>delivery-tag={gestion binaire},<br/>settled=**false**,,more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |Aucune action |
| Aucune action |<-- disposition(<br/>role=receiver,<br/>first={id d’envoi},<br/>last={id d’envoi},<br/>settled=**true**,<br/>state=**rejected**(<br/>error={infos sur l’erreur}<br/>)<br/>) |

#### Réception

| Client | SERVICE BUS |
| --- | --- |
| --> flow(<br/>link-credit=1<br/>) |Aucune action |
| Aucune action |< transfer(<br/>delivery-id={gestion numérique},<br/>delivery-tag={gestion binaire},<br/>settled=**false**,<br/>more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |
| --> disposition(<br/>role=**receiver**,<br/>first={id d’envoi},<br/>last={id d’envoi},<br/>settled=**true**,<br/>state=**accepted**<br/>) |Aucune action |

#### Réception de plusieurs messages

| Client | SERVICE BUS |
| --- | --- |
| --> flow(<br/>link-credit=3<br/>) |Aucune action |
| Aucune action |< transfer(<br/>delivery-id={gestion numérique},<br/>delivery-tag={gestion binaire},<br/>settled=**false**,<br/>more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |
| Aucune action |< transfer(<br/>delivery-id={gestion numérique+1},<br/>delivery-tag={gestion binaire},<br/>settled=**false**,<br/>more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |
| Aucune action |< transfer(<br/>delivery-id={gestion numérique+2},<br/>delivery-tag={gestion binaire},<br/>settled=**false**,<br/>more=**false**,<br/>state=**null**,<br/>resume=**false**<br/>) |
| --> disposition(<br/>role=receiver,<br/>first={id d’envoi},<br/>last={id d’envoi+2},<br/>settled=**true**,<br/>state=**accepted**<br/>) |Aucune action |

### Messages

Hello sections suivantes expliquent les propriétés à partir des sections de message AMQP standards hello sont utilisées par Service Bus et leur mappage d’ensemble de l’API Service Bus toohello.

#### en-tête

| Nom du champ | Usage | Nom de l’API |
| --- | --- | --- |
| durable |- |- |
| priority |- |- |
| ttl |Temps toolive pour ce message |[TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive) |
| first-acquirer |- |- |
| delivery-count |- |[DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) |

#### properties

| Nom du champ | Usage | Nom de l’API |
| --- | --- | --- |
| message-id |Identifiant défini par l’application, au format libre pour ce message. Utilisation pour la détection des doublons. |[MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) |
| user-id |Identifiant d’utilisateur défini par l’application, non interprété par Service Bus. |Accessible via hello API Service Bus. |
| trop|Identifiant de destination défini par l’application, non interprété par Service Bus. |[To](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_To) |
| subject |Identifiant d’objet de message défini par l’application, non interprété par Service Bus. |[Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) |
| réponse trop|Indicateur reply-path défini par l’application, non interprété par Service Bus. |[ReplyTo](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ReplyTo) |
| correlation-id |Identifiant de corrélation défini par l’application, non interprété par Service Bus. |[CorrelationId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_CorrelationId) |
| content-type |Indicateur de type de contenu défini par l’application pour le corps de hello, ne pas interprété par le Service Bus. |[ContentType](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ContentType) |
| content-encoding |Défini par l’application indicateur l’encodage de contenu pour le corps de hello, ne pas interprété par le Service Bus. |Accessible via hello API Service Bus. |
| absolute-expiry-time |Déclare le hello instantanée absolu message expire. Ignoré en entrée (la durée de vie de l’en-tête est observée), fait autorité en sortie. |[ExpiresAtUtc](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ExpiresAtUtc) |
| creation-time |Déclare à quels hello temps le message a été créé. Pas utilisé par Service Bus |Accessible via hello API Service Bus. |
| group-id |Identifiant défini par l’application pour un ensemble de messages connexes. Utilisé pour les sessions Service Bus. |[SessionId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId) |
| group-sequence |Compteur de numéro d’identification hello séquence relative de message de type hello à l’intérieur d’une session. Ignoré par Service Bus. |Accessible via hello API Service Bus. |
| reply-to-group-id |- |[ReplyToSessionId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ReplyToSessionId) |

## Fonctionnalités avancées de Service Bus

Cette section traite des fonctionnalités avancées d’Azure Service Bus qui reposent sur brouillon extensions tooAMQP, en cours de développement Bonjour comité technique OASIS pour AMQP. Bus de service implémente hello dernières versions de ces projets et adopte les modifications introduites comme les brouillons atteint état standard.

> [!NOTE]
> Les opérations avancées de messagerie Service Bus sont prises en charge via un modèle de demande/réponse. Hello des détails sur ces opérations sont décrites dans le document de hello [AMQP 1.0 dans Service Bus : opérations demande-réponse](service-bus-amqp-request-response.md).
> 
> 

### Gestion du protocole AMQP

Hello spécification de la gestion AMQP est hello premier des extensions de projet hello présentées ici. Cette spécification définit un ensemble de mouvements protocole superposée hello protocole AMQP qui autorisent les interactions de gestion avec hello infrastructure de messagerie via AMQP. spécification de Hello définit les opérations génériques tels que *créer*, *lire*, *mettre à jour*, et *supprimer* pour la gestion des entités à l’intérieur d’un infrastructure de messagerie et un ensemble d’opérations de requête.

Tous les mouvements nécessitent une interaction de demande/réponse entre le client de hello et infrastructure de messagerie hello et spécification de hello définit donc comment toomodel cette interaction modèle par-dessus AMQP : hello se connecte toohello de messagerie infrastructure, initie une session, puis crée une paire de liens. Sur un lien, hello fait Office de l’expéditeur et sur hello autres agit en tant que récepteur, créant ainsi une paire de liens peuvent agir comme un canal bidirectionnel.

| Opération logique | Client | Service Bus |
| --- | --- | --- |
| Création d’un chemin d’accès de réponse à une demande |--> attach(<br/>name={*nom du lien*},<br/>handle={*gestion numérique*},<br/>role=**sender**,<br/>source=**null**,<br/>target=”myentity/$management”<br/>) |Aucune action |
| Création d’un chemin d’accès de réponse à une demande |Aucune action |\<-- attach(<br/>name={*nom du lien*},<br/>handle={*gestion numérique*},<br/>role=**receiver**,<br/>source=null,<br/>target=”myentity”<br/>) |
| Création d’un chemin d’accès de réponse à une demande |--> attach(<br/>name={*nom du lien*},<br/>handle={*gestion numérique*},<br/>role=**receiver**,<br/>source=”myentity/$management”,<br/>target=”myclient$id”<br/>) | |
| Création d’un chemin d’accès de réponse à une demande |Aucune action |\<-- attach(<br/>name={*nom du lien*},<br/>handle={*gestion numérique*},<br/>role=**sender**,<br/>source=”myentity”,<br/>target=”myclient$id”<br/>) |

Absence de cette paire de liens, mise en œuvre de demande/réponse hello est simple : une demande est un message envoyé d’entité tooan au sein de l’infrastructure de messagerie hello qui comprend ce modèle. Dans ce message de demande, hello *réponse* champ hello *propriétés* section a la valeur toohello *cible* identificateur de lien de hello sur la réponse de hello toodeliver. Hello, la gestion des entités traite la demande de hello et fournit une réponse hello sur hello lier dont *cible* hello indiqué correspond à l’identificateur *réponse* identificateur.

modèle de Hello nécessite évidemment que conteneur de client hello et l’identificateur de client généré hello pour la destination de réponse hello sont uniques sur tous les clients et, pour des raisons de sécurité, toopredict également difficile.

les échanges de messages Hello utilisé pour le protocole de gestion hello et pour tous les autres protocoles que hello utilisez même modèle se produisent au niveau de l’application hello ; ils ne définissent pas de nouveaux mouvements d’au niveau du protocole AMQP. Cela est intentionnel afin que les applications puissent tirer immédiatement parti de ces extensions avec les piles compatibles AMQP 1.0.

Bus de service n’implémente pas actuellement une des fonctionnalités de base hello de spécification de la gestion hello, mais le modèle de demande/réponse hello défini par la spécification de la gestion hello est fondamental pour la fonctionnalité de sécurité basée sur des revendications hello et pour presque tous les Hello avancées décrites dans les sections suivantes de hello.

### Autorisation basée sur des revendications

projet de spécification d’autorisation en fonction des revendications AMQP (CBS) Hello s’appuie sur le modèle de demande/réponse de spécification de gestion hello et décrit un modèle généralisé pour comment toouse fédéré avec AMQP, les jetons de sécurité.

modèle de sécurité par défaut Hello de AMQP décrite dans l’introduction de hello est basé sur SASL et s’intègre à la négociation de connexion AMQP hello. À l’aide de SASL a parti hello qu’il fournit un modèle extensible pour lequel un ensemble de mécanismes ont été définies à partir de laquelle tout protocole qui utilise formellement SASL peut bénéficier. Parmi ces mécanismes sont « PLAIN » pour le transfert de noms d’utilisateur et mots de passe, la sécurité de tooTLS au niveau toobind « Externe », absence de hello tooexpress « Anonyme » de l’authentification/autorisation explicite et une grande variété de mécanismes supplémentaires qui permettent le passage des informations d’identification d’authentification et/ou l’autorisation ou de jetons.

L’intégration de SASL au protocole AMQP présente deux inconvénients :

* Toutes les informations d’identification et les jetons sont incluses dans l’étendue toohello connexion. Une infrastructure de messagerie souhaitant tooprovide différenciée le contrôle d’accès sur une base par entité ; par exemple, ce qui permet de porteur hello d’un jeton toosend tooqueue A, mais pas tooqueue B. Contexte d’autorisation hello ancré sur la connexion de hello, il est toouse n’est pas possible une connexion unique et encore utiliser des jetons d’accès différents pour la file d’attente A et de la file d’attente B.
* Les jetons d’accès sont généralement valides uniquement pour une durée limitée. Cette validité nécessite des jetons d’acquérir à nouveau hello utilisateur tooperiodically et fournit une toorefuse de l’émetteur de jeton toohello opportunité émettre un nouveau jeton si hello autorisations d’accès ont été modifiés. Les connexions AMQP peuvent durer longtemps. Hello SASL modèle uniquement fournit une chance tooset un jeton au moment de la connexion, ce qui signifie que hello infrastructure de messagerie soit a client de hello toodisconnect lors de l’expiration du jeton de hello ou doit être risque de hello tooaccept de permettre des communications continues avec un client qui a des droits d’accès ont été révoqués Bonjour intermédiaires.

Hello la spécification AMQP CBS, implémentée par le Service Bus, permet une solution de contournement élégante pour les deux de ces problèmes : il permet à un client tooassociate des jetons d’accès à chaque nœud et tooupdate les jetons avant leur expiration, sans interrompre le flux de messages hello.

CBS définit un nœud de gestion virtuelle nommé *$cbs*, toobe fournie par l’infrastructure de messagerie hello. nœud de gestion Hello accepte les jetons pour le compte de tous les autres nœuds Bonjour infrastructure de messagerie.

mouvement de protocole Hello est un échange de demande/réponse, tel que défini par la spécification de la gestion hello. Que signifie hello client établit une paire de liens avec hello *$cbs* nœud, puis transmet une demande sur hello lien sortant, puis attend la réponse de hello sur hello lien entrant.

message de demande Hello a hello application propriétés suivantes :

| Clé | Facultatif | Type de valeur | Contenu de la valeur |
| --- | --- | --- | --- |
| operation |Non |string |**put-token** |
| type |Non |string |type Hello du jeton hello placé. |
| name |Non |string |jeton de hello toowhich Hello « audience » s’applique. |
| expiration |Oui |timestamp |délai d’expiration Hello du jeton de hello. |

Hello *nom* propriété identifie l’entité hello quels hello jeton doit être associé. Dans le Bus de Service de file d’attente de toohello hello chemin d’accès ou de rubrique/abonnement. Hello *type* propriété identifie le type de jeton hello :

| Type de jeton | Description du jeton | Type de corps | Remarques |
| --- | --- | --- | --- |
| amqp:jwt |JSON Web Token (JWT) |Valeur AMQP (chaîne) |Pas encore disponible. |
| amqp:swt |Clé d’authentification Web simple (SWT) |Valeur AMQP (chaîne) |Pris en charge uniquement pour les clés d’authentification web simples SWT émises par AAD/ACS |
| servicebus.windows.net:sastoken |Jeton SAS Service Bus |Valeur AMQP (chaîne) |- |

Les jetons confèrent des droits. Service Bus connaît trois droits fondamentaux : « Envoyer » autorise l’envoi, « Écouter » autorise la réception, et « Gérer » autorise la manipulation d’entités. Les jetons SWT émis par AAD/ACS incluent explicitement ces droits en tant que revendications. Jetons SAP de Bus de service consultez toorules configuré sur l’espace de noms hello ou de l’entité, et ces règles sont configurées avec des droits. Droits respectifs du jeton hello express hello qui rend donc le jeton de signature hello avec clé hello associée à cette règle. jeton Hello associé à une entité à l’aide de *put-jeton* autorise hello connecté toointeract du client avec l’entité hello par des droits de jeton hello. Un lien sur lequel le client de hello prend sur hello *expéditeur* rôle requiert hello « Envoi » à droite ; sur hello *récepteur* rôle requiert le droit de « Écouter » hello.

message de réponse Hello comporte suivants de hello *-propriétés de l’application* valeurs

| Clé | Facultatif | Type de valeur | Contenu de la valeur |
| --- | --- | --- | --- |
| status-code |Non |int |Code de réponse HTTP **[RFC2616]**. |
| status-description |Oui |string |Description du statut de hello. |

Hello client peut appeler *put-jeton* d’une entité de l’infrastructure de messagerie hello et à plusieurs reprises. les jetons de Hello sont toohello étendue actuel du client et ancrés sur la connexion en cours de hello, serveur hello de signification supprime tous les jetons de retenue lors de la connexion de hello supprime.

implémentation de Service Bus actuelle Hello autorise uniquement CBS conjointement avec hello (méthode) SASL « Anonyme ». Une connexion SSL/TLS doit toujours exister la négociation SASL toohello préalable.

Hello mécanisme anonyme doit donc être pris en charge par hello choisi client AMQP 1.0. Signifie que l’accès anonyme qui hello la négociation de connexion initiale, y compris la création de session initiale de hello se produit sans Service Bus fait de savoir qui consiste à créer des connexions de hello.

Une fois la connexion de hello et la session est établie, l’attachement hello lie toohello *$cbs* nœud et l’envoi de hello *put-jeton* demande sont hello uniquement les opérations autorisées. Un jeton valide doit être défini avec succès à l’aide un *put-jeton* demande pour un nœud d’entité dans les 20 secondes après la connexion de hello a été établie, sinon hello unilatéralement déconnexion par Service Bus.

Hello client est ensuite chargé de suivi d’expiration du jeton. Quand un jeton expire, Service Bus supprime rapidement tous les liens sur l’entité de hello connexion toohello respectifs. tooprevent, hello client peut remplacer un jeton hello pour le nœud de hello avec une autre à tout moment via hello virtuel *$cbs* nœud de gestion avec hello même *put-jeton* de mouvement et sans mise en route Bonjour méthode de charge utile de hello le trafic de ce flux sur différents liens.

## Étapes suivantes

toolearn en savoir plus sur AMQP, visitez hello suivant liens :

* [Vue d’ensemble du protocole AMQP de Service Bus]
* [Prise en charge d’AMQP 1.0 dans les rubriques et files d’attente partitionnées Service Bus]
* [AMQP dans Service Bus pour Windows Server]

[this video course]: https://www.youtube.com/playlist?list=PLmE4bZU0qx-wAP02i0I7PJWvDWoCytEjD
[1]: ./media/service-bus-amqp-protocol-guide/amqp1.png
[2]: ./media/service-bus-amqp-protocol-guide/amqp2.png
[3]: ./media/service-bus-amqp-protocol-guide/amqp3.png
[4]: ./media/service-bus-amqp-protocol-guide/amqp4.png

[Vue d’ensemble du protocole AMQP de Service Bus]: service-bus-amqp-overview.md
[Prise en charge d’AMQP 1.0 dans les rubriques et files d’attente partitionnées Service Bus]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[AMQP dans Service Bus pour Windows Server]: https://msdn.microsoft.com/library/dn574799.aspx
