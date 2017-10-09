---
title: exceptions de relais aaaAzure et comment tooresolve les | Documents Microsoft
description: "Obtenir la liste des exceptions de relais d’Azure et des actions suggérées toohelp possibles pour les résoudre."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 5f9dd02c-cce0-43b3-8eb8-744f0c27f38c
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: de417c8e9e43407ef355fd44f6170cf2cdc46d6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-exceptions"></a>Exceptions Azure Relay

Cet article répertorie certaines exceptions peuvent être générées par hello Azure relais API. Cette référence est toochange de sujet, par conséquent, vérifiez de nouveau les mises à jour.

## <a name="exception-categories"></a>Catégories d'exceptions

Hello relais API génèrent des exceptions qui peuvent correspondre à hello suivant des catégories. Également répertoriés sont proposées que vous pouvez prendre toohelp résoudre les exceptions hello.

*   **Erreur de codage utilisateur** : [System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx). 

    **Action générale**: essayez le code de hello toofix avant de continuer.
*   **Erreur d’installation/configuration** : [System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx). 

    **Action générale**: révisez votre configuration. Si nécessaire, modifiez la configuration de hello.
*   **Exceptions temporaires** : [Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception), [Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception). 

    **Action générale**: recommencez l’opération de hello ou informer les utilisateurs.
*   **Autres exceptions** : [System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx). 

    **Action générale**: type d’exception toohello spécifique. Voir tableau hello hello suivant la section. 

## <a name="exception-types"></a>Types d'exceptions

Hello tableau suivant répertorie les types d’exceptions messagerie et leurs causes. Il note également suggérées actions à entreprendre toohelp résoudre les exceptions hello.

| **Type d’exception** | **Description** | **Action suggérée** | **Remarques sur la nouvelle tentative automatique ou immédiate** |
| --- | --- | --- | --- |
| [Délai d'expiration](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |Hello serveur n’a pas répondu toohello a demandé l’opération dans hello spécifié temps, ce qui est contrôlé par [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout). Bonjour serveur peut avoir terminé hello opération demandée. Cela peut se produire en raison de toonetwork ou autres délais d’infrastructure. |Vérifiez l’état du système hello par souci de cohérence et recommencez, si nécessaire. Consultez [TimeoutException](#timeoutexception). |Nouvelle tentative peut vous aider dans certains cas ; Ajoutez toocode logique de nouvelle tentative. |
| [Opération non valide](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |Hello a demandé l’opération utilisateur n’est pas autorisée dans hello serveur ou le service. Message d’exception hello pour plus d’informations, consultez. |Vérifiez le code de hello et la documentation de hello. Vérifiez que hello opération demandée n’est valide. |Une nouvelle tentative ne sera pas bénéfique. |
| [Opération annulée](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |Une tentative est effectuée tooinvoke une opération sur un objet qui a déjà été fermée, l’annulation ou supprimé. Dans de rares cas, la transaction ambiante de hello est déjà supprimée. |Code de hello et assurez-vous qu’il n’appelle pas les opérations sur un objet supprimé. |Une nouvelle tentative ne sera pas bénéfique. |
| [Accès non autorisé](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |Hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) objet n’a pas pu obtenir un jeton, jeton de hello n’est pas valide ou jeton de hello ne contient pas de hello revendications tooperform requis hello opération. |Assurez-vous que ce fournisseur de jetons hello est créé avec les valeurs correctes hello. Vérifiez la configuration de hello Hello service de contrôle d’accès. |Nouvelle tentative peut vous aider dans certains cas ; Ajoutez toocode logique de nouvelle tentative. |
| [Exception d’argument](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [Argument Null](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[Argment hors plage](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |Un ou plusieurs des éléments suivants de hello s’est produite :<br />Un ou plusieurs arguments de type fournis (méthode) toohello ne sont pas valides.<br /> Hello URI fourni trop[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) ou [créer](/dotnet/api/microsoft.servicebus.messaging.messagingfactory.create) contient un ou plusieurs segments de chemin d’accès.<br />schéma d’URI Hello fourni trop[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) ou [créer](/dotnet/api/microsoft.servicebus.messaging.messagingfactory.create) n’est pas valide. <br />valeur de la propriété Hello est supérieure à 32 Ko. |Vérifiez le code d’appel hello et assurez-vous que les arguments hello sont corrects. |Une nouvelle tentative ne sera pas bénéfique. |
| [Serveur occupé](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) |Service n’est pas demande de hello en mesure de tooprocess pour l’instant. |client de Hello, vous pouvez attendre un certain temps, puis recommencez l’opération de hello. |client de Hello peut reprendre après un intervalle spécifique. Si une nouvelle tentative entraîne une exception différente, vérifiez le comportement des nouvelles tentatives hello de cette exception. |
| [Quota dépassé](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |Hello entité de messagerie a atteint sa taille maximale autorisée. |Créer l’espace dans l’entité de hello par la réception de messages à partir de l’entité de hello ou ses files d’attente secondaires. Consultez [QuotaExceededException](#quotaexceededexception). |Nouvelle tentative peut vous aider si les messages ont été supprimés dans hello entre-temps. |
| [Taille des messages dépassée](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) |Une charge utile du message dépasse la limite de 256 Ko hello. Notez que cette limite de 256 Ko hello est hello taille totale du message. Hello taille totale du message peut inclure des propriétés système et toute surcharge Microsoft .NET. |Réduire la taille de hello de charge utile de message hello, puis recommencez l’opération de hello. |Une nouvelle tentative ne sera pas bénéfique. |

## <a name="quotaexceededexception"></a>QuotaExceededException

[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) indique que le quota d’une entité spécifique a été dépassé.

Pour prendre le relais, cette exception encapsule hello [System.ServiceModel.QuotaExceededException](https://msdn.microsoft.com/library/system.servicemodel.quotaexceededexception.aspx), ce qui indique le nombre maximal de ports d’écoute hello a été dépassée pour ce point de terminaison. Cela est indiqué dans hello **MaximumListenersPerEndpoint** valeur de message d’exception hello.

## <a name="timeoutexception"></a>TimeoutException
A [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) indique qu’une opération initiée par l’utilisateur prend plus de temps que le délai d’attente de hello opération. 

Vérifiez la valeur hello hello [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit) propriété. Atteindre cette limite peut également entraîner une exception [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx).

Pour Relay, vous pouvez recevoir des exceptions de délai d’attente lors de la première ouverture d’une connexion d’expéditeur de relais. Deux causes courantes peuvent être à l’origine de cette exception :

*   Hello [OpenTimeout](https://msdn.microsoft.com/library/wcf.opentimeout.aspx) valeur peut s’avérer trop faible (même en une fraction de seconde).
* Un écouteur de relais sur site ne répond pas (ou il peut rencontrer des problèmes de règles de pare-feu qui empêchent les écouteurs d’accepter de nouvelles connexions clientes) et hello [OpenTimeout](https://msdn.microsoft.com/library/wcf.opentimeout.aspx) valeur est inférieure à environ 20 secondes.

Exemple :

```
'System.TimeoutException’: hello operation did not complete within hello allotted timeout of 00:00:10.
hello time allotted toothis operation may have been a portion of a longer timeout.
```

### <a name="common-causes"></a>Causes courantes
Deux causes courantes peuvent être à l’origine de cette erreur :

*   **Configuration incorrecte**
    
    le délai d’attente de Hello opération peut-être être trop petit pour la condition de fonctionnement hello. valeur par défaut de Hello hello opération délai de connexion dans le client hello SDK est de 60 secondes. Vérifiez toosee si hello dans votre code a la valeur toosomething trop petite. Notez que condition hello et l’utilisation de l’UC du réseau de hello peut affecter le temps hello que nécessaire pour une opération toocomplete. Il est judicieux pas tooset hello opération délai d’attente tooa valeur très petite.
*   **Erreur de service temporaire**

    Parfois, hello service de relais peut-être rencontrer des retards de traitement des requêtes. Cela peut se produire, par exemple, pendant les périodes à fort trafic. Si cela se produit, recommencez l’opération après un délai, jusqu'à ce que l’opération de hello a réussi. Si hello même opération continue toofail après plusieurs tentatives, vérifiez hello [site d’état des services Azure](https://azure.microsoft.com/status/) toosee s’il existe connus des interruptions de service.

## <a name="next-steps"></a>Étapes suivantes
* [FAQ Azure Relay](relay-faq.md)
* [Créer un espace de noms Relay](relay-create-namespace-portal.md)
* [Bien démarrer avec Azure Relay et .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Bien démarrer avec Azure Relay et Node](relay-hybrid-connections-node-get-started.md)

