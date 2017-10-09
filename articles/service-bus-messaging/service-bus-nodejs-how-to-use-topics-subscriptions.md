---
title: aaaHow toouse Azure Service Bus rubriques et les abonnements avec Node.js | Documents Microsoft
description: "Découvrez comment toouse Service Bus rubriques et abonnements dans Azure à partir d’une application Node.js."
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b9f5db85-7b6c-4cc7-bd2c-bd3087c99875
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: e8f6e7ad6ed16d844c408337ac9e50f990e3fafd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-nodejs"></a>Comment tooUse Service Bus rubriques et les abonnements avec Node.js

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Ce guide décrit comment toouse Service Bus rubriques et abonnements à partir d’applications Node.js. Hello scénarios abordés incluent **création de rubriques et abonnements**, **création de filtres d’abonnement**, **envoi de messages** tooa rubrique, **réception les messages à partir d’un abonnement**, et **suppression des rubriques et abonnements**. Pour plus d’informations sur les rubriques et les abonnements, consultez hello [étapes](#next-steps) section.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a>Création d’une application Node.js
Créez une application Node.js vide. Pour obtenir des instructions sur la création d’une application Node.js, consultez [créer et déployer un tooan d’application Node.js Site Web Azure], [Service de cloud computing Node.js] [ Node.js Cloud Service] à l’aide de Windows PowerShell, ou un Site Web avec WebMatrix.

## <a name="configure-your-application-toouse-service-bus"></a>Configurer votre toouse application Service Bus
toouse Service Bus, téléchargez hello package Node.js Azure. Ce package comprend un ensemble de bibliothèques qui communiquent avec les services de Service Bus REST hello.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Utiliser le Gestionnaire de Package de nœud (NPM) tooobtain hello package
1. Utiliser une interface de ligne de commande comme **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix), accédez dossier toohello où vous avez créé votre exemple d’application.
2. Type **npm installer azure** dans la fenêtre de commande hello, qui doivent entraîner hello suivant de sortie :

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
3. Vous pouvez exécuter manuellement hello **ls** tooverify de commande qui un **nœud\_modules** dossier a été créé. Dans ce dossier de trouver la **azure** package qui contient les bibliothèques hello vous devez tooaccess rubriques Service Bus.

### <a name="import-hello-module"></a>Module d’importation hello
Utilisez le bloc-notes ou un autre éditeur de texte, ajoutez hello suivant en haut de toohello de hello **server.js** fichier de l’application hello :

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a>Configuration d’une connexion Service Bus
Bonjour Azure module lit les variables d’environnement hello `AZURE_SERVICEBUS_NAMESPACE` et `AZURE_SERVICEBUS_ACCESS_KEY` pour plus d’informations obligatoires tooconnect tooService Bus. Si ces variables d’environnement ne sont pas définies, vous devez spécifier les informations de compte hello lors de l’appel `createServiceBusService`.

Pour obtenir un exemple de la configuration des variables d’environnement hello pour un Service Cloud Azure, consultez [Service de Cloud Node.js avec stockage][Node.js Cloud Service with Storage].

Pour obtenir un exemple de la définition de variables d’environnement hello pour un site Web Azure, consultez [Node.js d’Application Web avec stockage][Node.js Web Application with Storage].

## <a name="create-a-topic"></a>Création d'une rubrique
Hello **ServiceBusService** objet vous permet de toowork aux rubriques. Le code suivant crée un objet **ServiceBusService**. Ajouter au début de hello **server.js** fichier, après le module de hello instruction tooimport hello azure :

```javascript
var serviceBusService = azure.createServiceBusService();
```

En appelant `createTopicIfNotExists` sur hello **ServiceBusService** de l’objet, hello spécifié rubrique sera retournée (si elle existe), ou une rubrique avec le nom spécifié de hello sera créée. code Hello suivant utilise `createTopicIfNotExists` toocreate ou connectez-vous rubrique toohello nommée `MyTopic`:

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

Hello `createServiceBusService` méthode prend également en charge des options supplémentaires, qui vous permettent de paramètres de rubrique toooverride par défaut tels que la durée de vie du message ou de la taille maximale de rubrique. Hello exemple suivant définit too5GB de taille maximale de rubrique hello avec une heure toolive de 1 minute :

```javascript
var topicOptions = {
        MaxSizeInMegabytes: '5120',
        DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createTopicIfNotExists('MyTopic', topicOptions, function(error){
    if(!error){
        // topic was created or exists
    }
});
```

### <a name="filters"></a>Filtres
Les opérations de filtrage facultatif peuvent être appliquées toooperations effectuées à l’aide **ServiceBusService**. Il peut s’agir d’opérations de journalisation, de relance automatique, etc. Les filtres sont des objets qui implémentent une méthode avec la signature de hello :

```javascript
function handle (requestOptions, next)
```

Après avoir effectué sur les options de demande hello de prétraitement, hello appels de méthode `next`, en passant un rappel avec hello après signature :

```javascript
function (returnObject, finalCallback, next)
```

Dans ce rappel et après traitement hello `returnObject` (hello réponse hello demande toohello serveur), rappel de hello doit tooeither appeler ensuite s’il existe des toocontinue du traitement des autres filtres ou appeler `finalCallback` dans le cas contraire, tooend hello appel de service.

Deux filtres qui implémentent la logique de nouvelle tentative sont incluses avec hello Azure SDK pour Node.js, **ExponentialRetryPolicyFilter** et **LinearRetryPolicyFilter**. Hello suivante permet de créer un **ServiceBusService** objet qui utilise hello **ExponentialRetryPolicyFilter**:

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a>Création d’abonnements
Abonnements aux rubriques sont également créés par hello **ServiceBusService** objet. Les abonnements sont nommés et peuvent avoir un filtre facultatif qui limite l’ensemble hello de messages remis de file d’attente virtuelle de l’abonnement toohello.

> [!NOTE]
> Abonnements sont persistantes et continuent jusqu'à ce que soit leur tooexist ou hello rubrique associées, elles sont supprimées. Si votre application contient la logique toocreate un abonnement, il doit tout d’abord vérifier si hello abonnement existe déjà à l’aide de la `getSubscription` (méthode).
>
>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Créer un abonnement avec le filtre par défaut (MatchAll) hello
Hello **MatchAll** filtre est hello par défaut qui est utilisé si aucun filtre n’est spécifiée lors de la création d’un abonnement. Hello lorsque **MatchAll** filtre est utilisé, la rubrique de toohello publié tous les messages sont placés dans la file d’attente virtuelle de l’abonnement. Hello exemple suivant crée un abonnement nommé « AllMessages » et utilise hello par défaut **MatchAll** filtre.

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a>Création d’abonnements avec des filtres
Vous pouvez également créer des filtres qui vous permettent de tooscope lesquelles messages envoyés tooa rubrique doit apparaître dans un abonnement à une rubrique spécifique.

Bonjour type de filtre pris en charge par les abonnements plus souple est la **SqlFilter**, qui implémente un sous-ensemble de SQL92. Filtres SQL fonctionnent sur les propriétés hello de messages hello qui sont publiées toohello rubrique. Pour plus d’informations sur les expressions hello qui peuvent être utilisées avec un filtre SQL, consultez hello [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] syntaxe.

Filtres peuvent être ajoutés tooa abonnement à l’aide de hello `createRule` méthode Hello **ServiceBusService** objet. Cette méthode vous permet de vous permet d’ajouter de nouveaux filtres tooan abonnement.

> [!NOTE]
> Étant donné que le filtre par défaut de hello est appliqué automatiquement tooall nouveaux abonnements, vous devez d’abord supprimer filtre par défaut de hello ou **MatchAll** remplace tous les autres filtres que vous pouvez spécifier. Vous pouvez supprimer la règle par défaut de hello à l’aide de hello `deleteRule` méthode de la **ServiceBusService** objet.
>
>

Hello exemple suivant crée un abonnement nommé `HighMessages` avec un **SqlFilter** qui sélectionne uniquement les messages qui ont personnalisé `messagenumber` propriété supérieure à 3 :

```javascript
serviceBusService.createSubscription('MyTopic', 'HighMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'HighMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber > 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'HighMessages',
            'HighMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

De même, hello exemple suivant crée un abonnement nommé `LowMessages` avec un **SqlFilter** qui sélectionne uniquement les messages qui ont un `messagenumber` propriété inférieur ou égal too3 :

```javascript
serviceBusService.createSubscription('MyTopic', 'LowMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'LowMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber <= 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'LowMessages',
            'LowMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

Lorsqu’un message est envoyé maintenant trop`MyTopic`, elle est envoyée à l’abonné de récepteurs toohello `AllMessages` abonnement à une rubrique et remis de manière sélective tooreceivers abonné toohello `HighMessages` et `LowMessages` abonnements à la rubrique (en fonction de contenu du message hello).

## <a name="how-toosend-messages-tooa-topic"></a>Comment les messages toosend tooa rubrique
toosend une rubrique de Service Bus message tooa, votre application doit utiliser le `sendTopicMessage` méthode Hello **ServiceBusService** objet.
Les messages envoyés sont des rubriques du Bus tooService **BrokeredMessage** objets.
**BrokeredMessage** objets comportent un ensemble de propriétés standard (tels que `Label` et `TimeToLive`), un dictionnaire qui est utilisé toohold des propriétés personnalisées spécifiques à l’application et un corps de données de chaîne. Une application peut définir le corps de hello du message de type hello en passant une valeur de chaîne Hello `sendTopicMessage` et toute requise propriétés standard seront remplies par les valeurs par défaut.

Hello exemple suivant montre comment toosend cinq messages de test à `MyTopic`. Notez que hello `messagenumber` varie en fonction de valeur de la propriété de chaque message sur l’itération hello de boucle de hello (Cela permet de déterminer les abonnements reçoivent) :

```javascript
var message = {
    body: '',
    customProperties: {
        messagenumber: 0
    }
}

for (i = 0;i < 5;i++) {
    message.customProperties.messagenumber=i;
    message.body='This is Message #'+i;
    serviceBusService.sendTopicMessage(topic, message, function(error) {
      if (error) {
        console.log(error);
      }
    });
}
```

Rubriques Service Bus prend en charge une taille maximale de 256 Ko Bonjour [niveau Standard](service-bus-premium-messaging.md) et 1 Mo Bonjour [niveau Premium](service-bus-premium-messaging.md). en-tête Hello, qui inclut les standard hello et les propriétés de l’application personnalisée, peut avoir une taille maximale de 64 Ko. Il n’existe aucune limite sur le nombre de hello de messages conservés dans une rubrique mais hello de taille totale des messages hello détenus par une rubrique est une extrémité de fin. Cette taille de rubrique est définie au moment de la création. La limite maximale est de 5 Go.

## <a name="receive-messages-from-a-subscription"></a>Réception des messages d’un abonnement
Les messages sont reçus à partir d’un abonnement à l’aide de la `receiveSubscriptionMessage` méthode sur hello **ServiceBusService** objet. Par défaut, les messages sont supprimés de l’abonnement de hello lorsqu’elles sont lues ; Toutefois, vous pouvez lire (aperçu) et verrouiller le message de type hello sans la supprimer de l’abonnement de hello en définissant le paramètre facultatif hello `isPeekLock` trop**true**.

Hello par défaut de lecture et de suppression de message de type hello comme partie de l’opération de réception est le modèle le plus simple hello et fonctionne mieux pour les scénarios dans lesquels une application peut tolérer ne pas traiter un message dans l’événement hello d’un échec. toounderstand, envisagez un scénario dans lequel la hello problèmes consommateur reçoit la demande et puis se bloque avant de le traiter. Comme Service Bus sera ont marqué hello message comme consommé, puis lors de l’application hello redémarre et commence à consommer des messages, elle aura manqué message de type hello qui a été consommée toohello préalable incident.

Si hello `isPeekLock` paramètre est défini trop**true**, hello réception devient une opération en deux étapes, ce qui rend possible toosupport les applications qui ne peut pas tolérer des messages manquants. Lorsque le Service Bus reçoit une demande, il recherche hello suivant message toobe consommé, il verrouille tooprevent autres consommateurs le reçoivent et le retourne toohello application.
Une fois l’application hello termine le traitement de message de type hello (ou stocke de manière fiable pour un traitement ultérieur), il exécute hello deuxième étape du processus de réception en appelant **deleteMessage** méthode et en fournissant le message toobe supprimé en tant que paramètre. Hello **deleteMessage** méthode marquer le message de type hello comme ayant été consommé et le supprimer de l’abonnement de hello.

Hello exemple suivant montre comment les messages peuvent être reçus et traités à l’aide de `receiveSubscriptionMessage`. Hello exemple reçoit d’abord et supprime un message de salutation 'LowMessages' abonnement, puis reçoit un message à l’aide de hello 'HighMessages' abonnement `isPeekLock` définir tootrue. Il supprime ensuite à l’aide du message hello `deleteMessage`:

```javascript
serviceBusService.receiveSubscriptionMessage('MyTopic', 'LowMessages', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
        console.log(receivedMessage);
    }
});
serviceBusService.receiveSubscriptionMessage('MyTopic', 'HighMessages', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        console.log(lockedMessage);
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
                console.log('message has been deleted.');
            }
        }
    }
});
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Comment toohandle application tombe en panne et messages illisibles
Service Bus fournit toohelp fonctionnalité que surmonter les erreurs dans votre application ou les difficultés du traitement d’un message. Si une application du récepteur ne peut pas tooprocess hello message pour une raison quelconque, elle peut appeler hello `unlockMessage` méthode sur le **ServiceBusService** objet. Cette opération provoquent Service Bus toounlock du message au sein de l’abonnement de hello et rendre disponible toobe de nouveau reçu, soit hello par même consommation d’application ou par une autre application consommatrice.

Il existe également un délai d’attente d’un message verrouillé dans l’abonnement, et en cas d’un message de type hello tooprocess avant application hello hello expiration délai de verrouillage (par exemple, si de l’application hello se bloque), puis le Service Bus déverrouille le message de type hello automatiquement et le rend disponible toobe de nouveau reçu.

Bonjour événement hello application se bloque après le traitement de message de type hello mais avant hello `deleteMessage` méthode est appelée, puis le message de type hello sera redistribué toohello application lors de son redémarrage. Cela est souvent appelé *au moins une fois le traitement*, autrement dit, chaque message est traité au moins une fois, mais dans certain hello situations le même message peut être redistribué. Si le scénario de hello ne peut pas tolérer le traitement dupliqué, les développeurs d’applications doivent ajouter une logique supplémentaire tootheir application toohandle en double remise du message. Cela est souvent obtenue grâce à la **MessageId** propriété de message de type hello, qui reste constante entre les tentatives de remise.

## <a name="delete-topics-and-subscriptions"></a>Suppression de rubriques et d'abonnements
Rubriques et les abonnements sont persistants et doivent être explicitement supprimés via hello [portail Azure] [ Azure portal] ou par programme.
Hello exemple suivant montre comment la rubrique de hello toodelete nommé `MyTopic`:

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

Suppression d’une rubrique supprime également tous les abonnements qui sont inscrits auprès de rubrique de hello. Les abonnements peuvent aussi être supprimés de manière indépendante. L’exemple suivant montre comment toodelete un abonnement nommé `HighMessages` de hello `MyTopic` rubrique :

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello des rubriques Service Bus, suivez ces liens de toolearn plus.

* Consultez [Files d’attente, rubriques et abonnements][Queues, topics, and subscriptions].
* Référence d’API pour [SqlFilter][SqlFilter].
* Visitez hello [Azure SDK pour le nœud] [ Azure SDK for Node] référentiel sur GitHub.

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[créer et déployer un tooan d’application Node.js Site Web Azure]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
