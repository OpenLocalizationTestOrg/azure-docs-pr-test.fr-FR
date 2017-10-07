---
title: "aaaAMQP 1.0 dans les opérations de réponse de demande de Service Bus de Azure | Documents Microsoft"
description: "Liste des opérations basées sur les requêtes-réponses de Microsoft Azure Service Bus."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: e4f26219c53b0c4172747af683fe511d6366ff2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="amqp-10-in-microsoft-azure-service-bus-request-response-based-operations"></a>AMQP 1.0 dans Microsoft Azure Service Bus : opérations basées sur les requêtes-réponses

Cette rubrique définit la liste hello des opérations de demande/réponse de Microsoft Azure Service Bus. Ces informations sont basées sur brouillon hello AMQP Management Version 1.0.  
  
Pour plus d’informations au niveau du câble AMQP 1.0 protocole, qui explique comment le Bus de Service implémente et s’appuie sur hello spécifications OASIS AMQP, consultez hello [AMQP 1.0 dans Azure Service Bus et concentrateurs d’événements guide de protocole](service-bus-amqp-protocol-guide.md).  
  
## <a name="concepts"></a>Concepts  
  
### <a name="entity-description"></a>Description d’entité  

Une description de l’entité fait référence à un Bus des services de tooeither [classe QueueDescription](/dotnet/api/microsoft.servicebus.messaging.queuedescription), [TopicDescription classe](/dotnet/api/microsoft.servicebus.messaging.topicdescription), ou [SubscriptionDescription classe](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription) objet.  
  
### <a name="brokered-message"></a>Message réparti  

Représente un message dans le Bus des services, qui est mappé tooan AMQP message. mappage de Hello est défini dans hello [guide de protocole de Service Bus AMQP](service-bus-amqp-protocol-guide.md).  
  
## <a name="attach-tooentity-management-node"></a>Attacher le nœud de gestion tooentity  

Toutes les opérations de hello décrites dans ce document suivent un modèle demande/réponse, sont incluses dans l’étendue tooan entité et nécessitent l’attachement du nœud de gestion d’entité tooan.  
  
### <a name="create-link-for-sending-requests"></a>Créer le lien pour l’envoi des demandes  

Crée un nœud de gestion toohello lien pour envoyer des demandes.  
  
```  
requestLink = session.attach(     
role: SENDER,   
    target: { address: "<entity address>/$management" },   
    source: { address: ""<my request link unique address>" }   
)  
  
```  
  
### <a name="create-link-for-receiving-responses"></a>Créer le lien pour la réception des réponses  

Crée un lien pour recevoir des réponses à partir du nœud de gestion hello.  
  
```  
responseLink = session.attach(    
role: RECEIVER,   
    source: { address: "<entity address>/$management" }   
    target: { address: "<my response link unique address>" }   
)  
  
```  
  
### <a name="transfer-a-request-message"></a>Transférer un message de demande  

Transfère un message de demande.  
  
```  
requestLink.sendTransfer(  
        Message(  
                properties: {  
                        message-id: <request id>,  
                        reply-to: "<my response link unique address>"  
                },  
                application-properties: {  
                        "operation" -> "<operation>",  
                },  
        )  
```  
  
### <a name="receive-a-response-message"></a>Recevoir un message de réponse  

Reçoit le message de réponse hello à partir du lien de réponse hello.  
  
```  
responseMessage = responseLink.receiveTransfer()  
```  
  
message de réponse Hello est Bonjour suivant du formulaire :
  
```  
Message(  
properties: {     
        correlation-id: <request id>  
    },  
    application-properties: {  
            "statusCode" -> <status code>,  
            "statusDescription" -> <status description>,  
           },         
)  
  
```  
  
### <a name="service-bus-entity-address"></a>Adresse d’entité Service Bus  

Les entités Service Bus doivent être traitées comme suit :  
  
|Type d’entité|Adresse|Exemple|  
|-----------------|-------------|-------------|  
|file d'attente|`<queue_name>`|`“myQueue”`<br /><br /> `“site1/myQueue”`|  
|rubrique|`<topic_name>`|`“myTopic”`<br /><br /> `“site2/page1/myQueue”`|  
|abonnement|`<topic_name>/Subscriptions/<subscription_name>`|`“myTopic/Subscriptions/MySub”`|  
  
## <a name="message-operations"></a>Opérations de message  
  
### <a name="message-renew-lock"></a>Verrouillage du renouvellement du message  

Étend le verrou hello d’un message par heure hello spécifié dans la description de l’entité hello.  
  
#### <a name="request"></a>Demande  

message de demande Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|operation|string|Oui|`com.microsoft:renew-lock`|  
|`com.microsoft:server-timeout`|uint|Non|Délai d’expiration du serveur de l’opération en millisecondes.|  
  
 corps du message de demande Hello doit se composer d’une section amqp-valeur contenant un mappage avec hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|`lock-tokens`|tableau d’uuid|Oui|Toorenew de jetons de verrou de message.|  
  
#### <a name="response"></a>Réponse  

message de réponse Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Oui|Code de réponse HTTP [RFC2616]<br /><br /> 200 : OK-réussite, sinon échec.|  
|statusDescription|string|Non|Description du statut de hello.|  
  
corps du message de réponse Hello doit se composer d’une section amqp-valeur contenant un mappage avec hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|expirations|tableau d’horodatage|Oui|Message verrou jeton nouvelle expiration correspondante toohello demande verrou de jetons.|  
  
### <a name="peek-message"></a>Lire furtivement un message  

Lit furtivement les messages sans les verrouiller.  
  
#### <a name="request"></a>Demande  

message de demande Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|operation|string|Oui|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|Non|Délai d’expiration du serveur de l’opération en millisecondes.|  
  
corps de message de demande Hello doit être un **amqp-valeur** section contenant un **carte** avec hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|`from-sequence-number`|long|Oui|Numéro de séquence du lire toostart.|  
|`message-count`|int|Oui|Nombre maximal de messages toopeek.|  
  
#### <a name="response"></a>Réponse  

message de réponse Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Oui|Code de réponse HTTP [RFC2616]<br /><br /> 200 : OK : a plus de messages<br /><br /> 0xcc : aucun contenu – plus de messages|  
|statusDescription|string|Non|Description du statut de hello.|  
  
corps de message de réponse Hello doit être un **amqp-valeur** section contenant un **carte** avec hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|Cloud vers appareil|liste des mappages|Oui|Liste de messages dans laquelle chaque mappage représente un message.|  
  
carte Hello représentant un message doit contenir hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|message|tableau d’octets|Oui|Message codé en filaire AMPQ 1.0.|  
  
### <a name="schedule-message"></a>Message de planification  

Messages de planification.  
  
#### <a name="request"></a>Demande  

message de demande Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|operation|string|Oui|`com.microsoft:schedule-message`|  
|`com.microsoft:server-timeout`|uint|Non|Délai d’expiration du serveur de l’opération en millisecondes.|  
  
corps de message de demande Hello doit être un **amqp-valeur** section contenant un **carte** avec hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|Cloud vers appareil|liste des mappages|Oui|Liste de messages dans laquelle chaque mappage représente un message.|  
  
carte Hello représentant un message doit contenir hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|message-id|string|Oui|`amqpMessage.Properties.MessageId` comme chaîne|  
|session-id|string|Oui|`amqpMessage.Properties.GroupId as string`|  
|partition-key|string|Oui|`amqpMessage.MessageAnnotations.”x-opt-partition-key"`|  
|message|tableau d’octets|Oui|Message codé en filaire AMPQ 1.0.|  
  
#### <a name="response"></a>Réponse  

message de réponse Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Oui|Code de réponse HTTP [RFC2616]<br /><br /> 200 : OK-réussite, sinon échec.|  
|statusDescription|string|Non|Description du statut de hello.|  
  
corps de message de réponse Hello doit être un **amqp-valeur** section contenant un mappage avec hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|sequence-numbers|tableau de type long|Oui|Numéro de séquence des messages planifiés. Numéro de séquence est toocancel utilisé.|  
  
### <a name="cancel-scheduled-message"></a>Annuler le message planifié  

Annule les messages planifiés.  
  
#### <a name="request"></a>Demande  

message de demande Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|operation|string|Oui|`com.microsoft:cancel-scheduled-message`|  
|`com.microsoft:server-timeout`|uint|Non|Délai d’expiration du serveur de l’opération en millisecondes.|  
  
corps de message de demande Hello doit être un **amqp-valeur** section contenant un **carte** avec hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|sequence-numbers|tableau de type long|Oui|Numéros de séquence de messages planifiés toocancel.|  
  
#### <a name="response"></a>Réponse  

message de réponse Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Oui|Code de réponse HTTP [RFC2616]<br /><br /> 200 : OK-réussite, sinon échec.|  
|statusDescription|string|Non|Description du statut de hello.|  
  
corps de message de réponse Hello doit être un **amqp-valeur** section contenant un mappage avec hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|sequence-numbers|tableau de type long|Oui|Numéro de séquence des messages planifiés. Numéro de séquence est toocancel utilisé.|  
  
## <a name="session-operations"></a>Opérations de session  
  
### <a name="session-renew-lock"></a>Verrouillage de renouvellement de session  

Étend le verrou hello d’un message par heure hello spécifié dans la description de l’entité hello.  
  
#### <a name="request"></a>Demande  

message de demande Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|operation|string|Oui|`com.microsoft:renew-session-lock`|  
|`com.microsoft:server-timeout`|uint|Non|Délai d’expiration du serveur de l’opération en millisecondes.|  
  
corps de message de demande Hello doit être un **amqp-valeur** section contenant un **carte** avec hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|session-id|string|Oui|ID de la session.|  
  
#### <a name="response"></a>Réponse  

message de réponse Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Oui|Code de réponse HTTP [RFC2616]<br /><br /> 200 : OK : a plus de messages<br /><br /> 0xcc : aucun contenu – plus de messages|  
|statusDescription|string|Non|Description du statut de hello.|  
  
corps de message de réponse Hello doit être un **amqp-valeur** section contenant un mappage avec hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|expiration|timestamp|Oui|Nouvelle expiration.|  
  
### <a name="peek-session-message"></a>Message de session de lecture furtive  

Lit furtivement les messages de session sans les verrouiller.  
  
#### <a name="request"></a>Demande  

message de demande Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|operation|string|Oui|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|Non|Délai d’expiration du serveur de l’opération en millisecondes.|  
  
corps de message de demande Hello doit être un **amqp-valeur** section contenant un **carte** avec hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|from-sequence-number|long|Oui|Numéro de séquence du lire toostart.|  
|message-count|int|Oui|Nombre maximal de messages toopeek.|  
|session-id|string|Oui|ID de la session.|  
  
#### <a name="response"></a>Réponse  

message de réponse Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Oui|Code de réponse HTTP [RFC2616]<br /><br /> 200 : OK : a plus de messages<br /><br /> 0xcc : aucun contenu – plus de messages|  
|statusDescription|string|Non|Description du statut de hello.|  
  
corps de message de réponse Hello doit être un **amqp-valeur** section contenant un mappage avec hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|Cloud vers appareil|liste des mappages|Oui|Liste de messages dans laquelle chaque mappage représente un message.|  
  
 carte Hello représentant un message doit contenir hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|message|tableau d’octets|Oui|Message codé en filaire AMPQ 1.0.|  
  
### <a name="set-session-state"></a>Définir l’état d’une session  

Jeux de hello état d’une session.  
  
#### <a name="request"></a>Demande  

message de demande Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|operation|string|Oui|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|uint|Non|Délai d’expiration du serveur de l’opération en millisecondes.|  
  
corps de message de demande Hello doit être un **amqp-valeur** section contenant un **carte** avec hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|session-id|string|Oui|ID de la session.|  
|session-state|tableau d’octets|Oui|Données binaires opaques.|  
  
#### <a name="response"></a>Réponse  

message de réponse Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Oui|Code de réponse HTTP [RFC2616]<br /><br /> 200 : OK-réussite, sinon échec|  
|statusDescription|string|Non|Description du statut de hello.|  
  
### <a name="get-session-state"></a>Obtenir l’état d’une session  

Obtient l’état de hello d’une session.  
  
#### <a name="request"></a>Demande  

message de demande Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|operation|string|Oui|`com.microsoft:get-session-state`|  
|`com.microsoft:server-timeout`|uint|Non|Délai d’expiration du serveur de l’opération en millisecondes.|  
  
corps de message de demande Hello doit être un **amqp-valeur** section contenant un **carte** avec hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|session-id|string|Oui|ID de la session.|  
  
#### <a name="response"></a>Réponse  

message de réponse Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Oui|Code de réponse HTTP [RFC2616]<br /><br /> 200 : OK-réussite, sinon échec|  
|statusDescription|string|Non|Description du statut de hello.|  
  
corps de message de réponse Hello doit être un **amqp-valeur** section contenant un **carte** avec hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|session-state|tableau d’octets|Oui|Données binaires opaques.|  
  
### <a name="enumerate-sessions"></a>Énumérer les sessions  

Énumère les sessions sur une entité de messagerie.  
  
#### <a name="request"></a>Demande  

message de demande Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|operation|string|Oui|`com.microsoft:get-message-sessions`|  
|`com.microsoft:server-timeout`|uint|Non|Délai d’expiration du serveur de l’opération en millisecondes.|  
  
corps de message de demande Hello doit être un **amqp-valeur** section contenant un **carte** avec hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|last-updated-time|timestamp|Oui|Filtrer les sessions uniquement tooinclude mis à jour après un moment donné.|  
|skip|int|Oui|Ignore un certain nombre de sessions.|  
|top|int|Oui|Nombre maximal de sessions.|  
  
#### <a name="response"></a>Réponse  

message de réponse Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Oui|Code de réponse HTTP [RFC2616]<br /><br /> 200 : OK : a plus de messages<br /><br /> 0xcc : aucun contenu – plus de messages|  
|statusDescription|string|Non|Description du statut de hello.|  
  
corps de message de réponse Hello doit être un **amqp-valeur** section contenant un **carte** avec hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|skip|int|Oui|Nombre de sessions ignorées si le code d’état est 200.|  
|sessions-ids|tableau de chaînes|Oui|Tableau d’ID de session si le code d’état est 200.|  
  
## <a name="rule-operations"></a>Opérations relatives aux règles  
  
### <a name="add-rule"></a>Ajout de règle  
  
#### <a name="request"></a>Demande  

message de demande Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|operation|string|Oui|`com.microsoft:add-rule`|  
|`com.microsoft:server-timeout`|uint|Non|Délai d’expiration du serveur de l’opération en millisecondes.|  
  
corps de message de demande Hello doit être un **amqp-valeur** section contenant un **carte** avec hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|rule-name|string|Oui|Nom de règle, à l’exception des noms d’abonnement et de rubrique.|  
|rule-description|map|Oui|Description de la règle comme indiqué dans la section suivante.|  
  
Hello **description de la règle** mappage doit inclure hello suivant entrées, où **sql-filtre** et **filtre de corrélation** s’excluent mutuellement :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|sql-filter|map|Oui|`sql-filter`, comme indiqué dans la section suivante de hello.|  
|correlation-filter|map|Oui|`correlation-filter`, comme indiqué dans la section suivante de hello.|  
|sql-rule-action|map|Oui|`sql-rule-action`, comme indiqué dans la section suivante de hello.|  
  
mappage de filtre sql Hello doit inclure hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|expression|string|Oui|Expression de filtre Sql.|  
  
Hello **filtre de corrélation** mappage doit inclure au moins un des hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|correlation-id|string|Non||  
|message-id|string|Non||  
|to|string|Non||  
|reply-to|string|Non||  
|label|string|Non||  
|session-id|string|Non||  
|reply-to-session-id|string|Non||  
|content-type|string|Non||  
|properties|map|Non|Mappe tooService Bus [BrokeredMessage.Properties](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Properties).|  
  
Hello **sql d’action de règle** mappage doit inclure hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|expression|string|Oui|Expression d’action SQL.|  
  
#### <a name="response"></a>Réponse  

message de réponse Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Oui|Code de réponse HTTP [RFC2616]<br /><br /> 200 : OK-réussite, sinon échec|  
|statusDescription|string|Non|Description du statut de hello.|  
  
### <a name="remove-rule"></a>Supprimer la règle  
  
#### <a name="request"></a>Demande  

message de demande Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|operation|string|Oui|`com.microsoft:remove-rule`|  
|`com.microsoft:server-timeout`|uint|Non|Délai d’expiration du serveur de l’opération en millisecondes.|  
  
corps de message de demande Hello doit être un **amqp-valeur** section contenant un **carte** avec hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|rule-name|string|Oui|Nom de règle, à l’exception des noms d’abonnement et de rubrique.|  
  
#### <a name="response"></a>Réponse  

message de réponse Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Oui|Code de réponse HTTP [RFC2616]<br /><br /> 200 : OK-réussite, sinon échec|  
|statusDescription|string|Non|Description du statut de hello.|  
  
## <a name="deferred-message-operations"></a>Opérations relatives aux messages différés  
  
### <a name="receive-by-sequence-number"></a>Recevoir par numéro de séquence  

Reçoit des messages différés par numéro de séquence.  
  
#### <a name="request"></a>Demande  

message de demande Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|operation|string|Oui|`com.microsoft:receive-by-sequence-number`|  
|`com.microsoft:server-timeout`|uint|Non|Délai d’expiration du serveur de l’opération en millisecondes.|  
  
corps de message de demande Hello doit être un **amqp-valeur** section contenant un **carte** avec hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|sequence-numbers|tableau de type long|Oui|Numéros de séquence.|  
|receiver-settle-mode|ubyte|Oui|Mode de **réglage du récepteur** tel que spécifié dans AMQP core v1.0.|  
  
#### <a name="response"></a>Réponse  

message de réponse Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Oui|Code de réponse HTTP [RFC2616]<br /><br /> 200 : OK-réussite, sinon échec|  
|statusDescription|string|Non|Description du statut de hello.|  
  
corps de message de réponse Hello doit être un **amqp-valeur** section contenant un **carte** avec hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|Cloud vers appareil|liste des mappages|Oui|Liste de messages dans laquelle chaque mappage représente un message.|  
  
carte Hello représentant un message doit contenir hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|lock-token|uuid|Oui|Jeton de verrouillage si `receiver-settle-mode` est 1.|  
|message|tableau d’octets|Oui|Message codé en filaire AMPQ 1.0.|  
  
### <a name="update-disposition-status"></a>Mettre à jour le statut de disposition  

Met à jour d’état de la disposition des messages différés hello.  
  
#### <a name="request"></a>Demande  

message de demande Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|operation|string|Oui|`com.microsoft:update-disposition`|  
|`com.microsoft:server-timeout`|uint|Non|Délai d’expiration du serveur de l’opération en millisecondes.|  
  
corps de message de demande Hello doit être un **amqp-valeur** section contenant un **carte** avec hello suivant entrées :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|disposition-status|string|Oui|Terminé<br /><br /> abandonné<br /><br /> interrompu|  
|lock-tokens|tableau d’uuid|Oui|Statut de disposition de tooupdate de jetons de verrou de message.|  
|deadletter-reason|string|Non|Peut être définie si l’état de la disposition est défini trop**suspendu**.|  
|deadletter-description|string|Non|Peut être définie si l’état de la disposition est défini trop**suspendu**.|  
|properties-to-modify|map|Non|Liste de Service Bus répartie toomodify des propriétés de message.|  
  
#### <a name="response"></a>Réponse  

message de réponse Hello doit inclure hello application propriétés suivantes :  
  
|Clé|Type de valeur|Requis|Contenu de la valeur|  
|---------|----------------|--------------|--------------------|  
|statusCode|int|Oui|Code de réponse HTTP [RFC2616]<br /><br /> 200 : OK-réussite, sinon échec|  
|statusDescription|string|Non|Description du statut de hello.|

## <a name="next-steps"></a>Étapes suivantes

toolearn en savoir plus sur AMQP et Service Bus, visitez hello suivant liens :

* [Vue d’ensemble du protocole AMQP de Service Bus]
* [Prise en charge d’AMQP 1.0 dans les rubriques et files d’attente partitionnées Service Bus]
* [AMQP dans Service Bus pour Windows Server]

[Vue d’ensemble du protocole AMQP de Service Bus]: service-bus-amqp-overview.md
[Prise en charge d’AMQP 1.0 dans les rubriques et files d’attente partitionnées Service Bus]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[AMQP dans Service Bus pour Windows Server]: https://msdn.microsoft.com/library/dn574799.asp