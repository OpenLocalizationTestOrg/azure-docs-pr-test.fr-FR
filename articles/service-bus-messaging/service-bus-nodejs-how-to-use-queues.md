---
title: "les files d’attente d’aaaHow toouse Service Bus dans Node.js | Documents Microsoft"
description: "Découvrez comment toouse Service Bus des files d’attente dans Azure à partir d’une application Node.js."
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a87a00f9-9aba-4c49-a0df-f900a8b67b3f
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: c55354b2061c41aba1093cc3f12ce2a1bc37a3cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-nodejs"></a>Comment toouse Service Bus de files d’attente avec Node.js

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Cet article décrit comment toouse Service Bus de files d’attente avec Node.js. exemples de Hello sont écrites en JavaScript et utilisent hello module Node.js Azure. Hello scénarios abordés incluent **création de files d’attente**, **envoyer et recevoir des messages**, et **la suppression de files d’attente**. Pour plus d’informations sur les files d’attente, consultez hello [étapes](#next-steps) section.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a>Création d’une application Node.js
Créez une application Node.js vide. Pour obtenir des instructions sur la façon de toocreate une application Node.js, consultez [créer et déployer un tooan d’application Node.js site Web Azure][Create and deploy a Node.js application tooan Azure Website], ou [Service de cloud computing Node.js] [ Node.js Cloud Service] à l’aide de Windows PowerShell.

## <a name="configure-your-application-toouse-service-bus"></a>Configurer votre toouse application Service Bus
toouse Azure Service Bus, téléchargez et utilisez hello package Node.js Azure. Ce package comprend un ensemble de bibliothèques qui communiquent avec les services de Service Bus REST hello.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Utiliser le Gestionnaire de Package de nœud (NPM) tooobtain hello package
1. Hello d’utilisation **Windows PowerShell pour Node.js** commande fenêtre toonavigate toohello **c:\\nœud\\sbqueues\\WebRole1** dossier dans lequel vous avez créé votre exemple d’application.
2. Type **npm installer azure** dans la fenêtre de commande hello, qui doivent entraîner suivant toohello similaire de sortie :

    ```
    azure@0.7.5 node_modules\azure
        ├── dateformat@1.0.2-1.2.3
        ├── xmlbuilder@0.4.2
        ├── node-uuid@1.2.0
        ├── mime@1.2.9
        ├── underscore@1.4.4
        ├── validator@1.1.1
        ├── tunnel@0.0.2
        ├── wns@0.5.3
        ├── xml2js@0.2.7 (sax@0.5.2)
        └── request@2.21.0 (json-stringify-safe@4.0.0, forever-agent@0.5.0, aws-sign@0.3.0, tunnel-agent@0.3.0, oauth-sign@0.3.0, qs@0.6.5, cookie-jar@0.3.0, node-uuid@1.4.0, http-signature@0.9.11, form-data@0.0.8, hawk@0.13.1)
    ```
3. Vous pouvez exécuter manuellement hello **ls** tooverify de commande qui un **node_modules** dossier a été créé. À l’intérieur de ce hello de recherche du dossier **azure** package qui contient les bibliothèques hello vous devez tooaccess files d’attente Service Bus.

### <a name="import-hello-module"></a>Module d’importation hello
Utilisez le bloc-notes ou un autre éditeur de texte, ajoutez hello suivant en haut de toohello de hello **server.js** fichier de l’application hello :

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a>Configuration d’une connexion Service Bus Azure
module Windows Azure Hello lit variable d’environnement hello `AZURE_SERVICEBUS_CONNECTION_STRING` tooobtain informations requis tooconnect tooService Bus. Si cette variable d’environnement n’est pas définie, vous devez spécifier les informations de compte hello lors de l’appel `createServiceBusService`.

Pour obtenir un exemple de la configuration des variables d’environnement hello dans un fichier de configuration pour un Service Cloud Azure, consultez [Service de Cloud Node.js avec stockage][Node.js Cloud Service with Storage].

Pour obtenir un exemple de la définition de variables d’environnement hello Bonjour [portail Azure] [ Azure portal] pour un site Web Azure, consultez [Node.js d’Application Web avec stockage] [ Node.js Web Application with Storage].

## <a name="create-a-queue"></a>Création d’une file d’attente
Hello **ServiceBusService** objet vous permet de toowork avec les files d’attente Service Bus. Hello de code suivant crée un **ServiceBusService** objet. Ajoutez-le haut hello Hello **server.js** fichier, après hello de tooimport hello instruction module Windows Azure :

```javascript
var serviceBusService = azure.createServiceBusService();
```

En appelant `createQueueIfNotExists` sur hello **ServiceBusService** objet, hello spécifié de file d’attente est retourné (si elle existe) ou une file d’attente avec le nom spécifié de hello est créé. code Hello suivant utilise `createQueueIfNotExists` toocreate ou connectez-vous de file d’attente toohello nommée `myqueue`:

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

Hello `createServiceBusService` méthode prend également en charge des options supplémentaires, qui permettent de paramètres de file d’attente par défaut toooverride comme taille de file d’attente toolive ou une valeur maximale de temps de message. Hello exemple suivant définit hello file d’attente maximale taille too5 Go et heure toolive (TTL) de 1 minute :

```javascript
var queueOptions = {
      MaxSizeInMegabytes: '5120',
      DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createQueueIfNotExists('myqueue', queueOptions, function(error){
    if(!error){
        // Queue exists
    }
});
```

### <a name="filters"></a>Filtres
Les opérations de filtrage facultatif peuvent être appliquées toooperations effectuées à l’aide **ServiceBusService**. Il peut s’agir d’opérations de journalisation, de relance automatique, etc. Les filtres sont des objets qui implémentent une méthode avec la signature de hello :

```javascript
function handle (requestOptions, next)
```

Après son traitement préalable sur les options de demande hello, méthode hello doit appeler `next`, en passant un rappel avec hello après signature :

```javascript
function (returnObject, finalCallback, next)
```

Dans ce rappel et après traitement hello `returnObject` (hello réponse hello demande toohello serveur), le rappel de hello doit appeler `next` si elle existe toocontinue le traitement des autres filtres, ou simplement appeler `finalCallback`, qui se termine à appel de service Hello.

Deux filtres qui implémentent la logique de nouvelle tentative sont incluses avec hello Azure SDK pour Node.js, `ExponentialRetryPolicyFilter` et `LinearRetryPolicyFilter`. Hello de code suivant crée un `ServiceBusService` objet qui utilise hello `ExponentialRetryPolicyFilter`:

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-tooa-queue"></a>Envoyer la file d’attente de messages tooa
toosend une file d’attente Service Bus de messages tooa, votre application appelle hello `sendQueueMessage` méthode sur hello **ServiceBusService** objet. Trop envoyée (et reçues à partir de) Service Bus sont des files d’attente de messages **BrokeredMessage** , et qu’un ensemble de propriétés standard (tels que **étiquette** et **TimeToLive**), un dictionnaire qui est utilisé toohold des propriétés personnalisées spécifiques à l’application et un corps de données d’application arbitraire. Une application peut définir le corps de hello du message de type hello en passant une chaîne en tant que message de type hello. Toutes les propriétés standard requises sont remplies avec les valeurs par défaut.

Hello exemple suivant montre comment toosend une file d’attente toohello test nommé `myqueue` à l’aide de `sendQueueMessage`:

```javascript
var message = {
    body: 'Test message',
    customProperties: {
        testproperty: 'TestValue'
    }};
serviceBusService.sendQueueMessage('myqueue', message, function(error){
    if(!error){
        // message sent
    }
});
```

Les files d’attente Service Bus prend en charge une taille maximale de 256 Ko Bonjour [niveau Standard](service-bus-premium-messaging.md) et 1 Mo Bonjour [niveau Premium](service-bus-premium-messaging.md). en-tête Hello, qui inclut les standard hello et les propriétés de l’application personnalisée, peut avoir une taille maximale de 64 Ko. Il n’existe aucune limite du nombre de hello de messages dans une file d’attente mais hello de taille totale des messages hello détenus par une file d’attente est une extrémité de fin. Cette taille de file d'attente est définie au moment de la création. La limite maximale est de 5 Go. Pour plus d’informations sur les quotas, consultez [Quotas Service Bus][Service Bus quotas].

## <a name="receive-messages-from-a-queue"></a>Réception des messages d'une file d'attente
Les messages sont reçus à partir d’une file d’attente à l’aide de hello `receiveQueueMessage` méthode sur hello **ServiceBusService** objet. Par défaut, les messages sont supprimés de la file d’attente hello lorsqu’elles sont lues ; Toutefois, vous pouvez lire (aperçu) et verrouiller le message de type hello sans le supprimer de la file d’attente hello en définissant le paramètre facultatif hello `isPeekLock` trop**true**.

Hello le comportement par défaut de la lecture et de suppression de message de type hello comme partie de hello opération de réception est le modèle le plus simple hello et convient le mieux pour les scénarios dans lesquels une application peut tolérer ne pas traiter un message dans l’événement hello d’un échec. toounderstand, envisagez un scénario dans les problèmes liés aux consommateurs de hello hello reçoit la demande et puis se bloque avant de le traiter. Comme Service Bus sera ont marqué hello message comme consommé, puis lors de l’application hello redémarre et commence à consommer des messages, elle aura manqué message de type hello qui a été consommée toohello préalable incident.

Si hello `isPeekLock` paramètre est défini trop**true**, hello réception devient une opération en deux étapes, ce qui rend possible toosupport les applications qui ne peut pas tolérer des messages manquants. Lorsque le Service Bus reçoit une demande, il recherche hello suivant message toobe consommé, il verrouille tooprevent autres consommateurs le reçoivent et le retourne toohello application. Une fois l’application hello termine le traitement de message de type hello (ou stocke de manière fiable pour un traitement ultérieur), il termine hello deuxième étape du hello processus de réception en appelant `deleteMessage` (méthode) et en fournissant des toobe de message hello supprimé en tant que paramètre. Hello `deleteMessage` méthode marque le message de type hello comme ayant été consommé et supprime celui-ci de la file d’attente hello.

Hello exemple suivant montre comment tooreceive et processus de messages à l’aide de `receiveQueueMessage`. Hello exemple reçoit d’abord et supprime un message, puis reçoit un message à l’aide de `isPeekLock` défini trop**true**, puis supprime hello à l’aide du message `deleteMessage`:

```javascript
serviceBusService.receiveQueueMessage('myqueue', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
    }
});
serviceBusService.receiveQueueMessage('myqueue', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
            }
        });
    }
});
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Comment toohandle application tombe en panne et messages illisibles
Service Bus fournit toohelp fonctionnalité que surmonter les erreurs dans votre application ou les difficultés du traitement d’un message. Si une application du récepteur ne peut pas tooprocess hello message pour une raison quelconque, elle peut appeler hello `unlockMessage` méthode sur hello **ServiceBusService** objet. Cette opération provoquent Service Bus toounlock le message dans la file d’attente hello et rendre disponible toobe de nouveau reçu, soit hello par même consommation d’application ou par une autre application consommatrice.

Il existe également un délai d’attente d’un message verrouillé dans la file d’attente hello, et si l’échec de l’application hello tooprocess hello message avant hello délai d’attente de verrou expire (par exemple, si de l’application hello se bloque), puis Service Bus déverrouille message de type hello automatiquement et le rendre disponible toobe de nouveau reçu.

Bonjour événement hello application se bloque après le traitement de message de type hello mais avant hello `deleteMessage` méthode est appelée, puis le message de type hello sera redistribué toohello application lors de son redémarrage. Cela est souvent appelé *au moins une fois le traitement*, autrement dit, chaque message est traité au moins une fois, mais dans certain hello situations le même message peut être redistribué. Si le scénario de hello ne peut pas tolérer le traitement dupliqué, les développeurs d’applications doivent ajouter une logique supplémentaire tootheir application toohandle en double remise du message. Cela est souvent obtenue à l’aide de hello **MessageId** propriété de message de type hello, qui reste constante entre les tentatives de remise.

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur les files d’attente, consultez hello suivant des ressources.

* [Files d’attente, rubriques et abonnements][Queues, topics, and subscriptions]
* Référentiel du [Kit de développement logiciel (SDK) Azure pour Node][Azure SDK for Node] sur GitHub
* [Centre pour développeurs Node.js](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application tooan Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md
