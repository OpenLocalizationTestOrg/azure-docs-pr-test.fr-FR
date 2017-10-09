---
title: liaison de fonctions Twilio aaaAzure | Documents Microsoft
description: "Comprendre comment les liaisons de Twilio toouse avec des fonctions d’Azure."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, calcul dynamique, architecture sans serveur"
ms.assetid: a60263aa-3de9-4e1b-a2bb-0b52e70d559b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/20/2016
ms.author: wesmc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 882853947850e7d6795ca5b2f3fb6b9a83ede182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="send-sms-messages-from-azure-functions-using-hello-twilio-output-binding"></a>Envoyer des messages SMS à partir des fonctions d’Azure à l’aide de hello liaison de sortie Twilio
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Cet article explique comment les liaisons Twilio tooconfigure et l’utilisation avec des fonctions d’Azure. 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Prend en charge les fonctions Azure Twilio sortie liaisons tooenable votre texte SMS toosend fonctions des messages avec quelques lignes de code et un [Twilio](https://www.twilio.com/) compte. 

## <a name="functionjson-for-hello-twilio-output-binding"></a>liaison de sortie de Twilio Function.JSON pour hello
fichier de function.json Hello fournit hello propriétés suivantes :

* `name`: Nom variable utilisée dans le code de fonction pour hello SMS Twilio SMS.
* `type`: doit être défini trop*« twilioSms »*.
* `accountSid`: Cette valeur doit être définie toohello les nom d’un paramètre d’application qui contient le Sid de votre compte Twilio.
* `authToken`: Cette valeur doit être définie toohello les nom d’un paramètre d’application qui contient votre jeton d’authentification Twilio.
* `to`: Cette valeur est définie de numéro de téléphone toohello hello SMS texte est envoyé à.
* `from`: Cette valeur est définie de numéro de téléphone toohello texte SMS de hello est envoyé à partir de.
* `direction`: doit être défini trop*« out »*.
* `body`: Cette valeur peut être utilisé toohard code hello message texte envoyé si vous n’avez pas besoin tooset dynamiquement dans hello du code de votre fonction. 

Exemple de fichier function.json :

```json
{
  "type": "twilioSms",
  "name": "message",
  "accountSid": "TwilioAccountSid",
  "authToken": "TwilioAuthToken",
  "to": "+1704XXXXXXX",
  "from": "+1425XXXXXXX",
  "direction": "out",
  "body": "Azure Functions Testing"
}
```


## <a name="example-c-queue-trigger-with-twilio-output-binding"></a>Exemple de déclencheur de file d’attente C# avec liaison de sortie Twilio
#### <a name="synchronous"></a>Synchrone
Ce code exemple synchrone pour un déclencheur de file d’attente de stockage Azure utilise un hors toosend du paramètre client tooa message texte qui a passé une commande.

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static void Run(string myQueueItem, out SMSMessage message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello SMSMessage variable.
    message = new SMSMessage();

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    message.Body = msg;
    message.too= order.mobileNumber;
}
```

#### <a name="asynchronous"></a>Asynchrone
Ce code exemple asynchrone d’un déclencheur de file d’attente de stockage Azure envoie un client tooa de message texte qui a passé une commande.

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static async Task Run(string myQueueItem, IAsyncCollector<SMSMessage> message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello SMSMessage variable.
    SMSMessage smsText = new SMSMessage();

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    smsText.Body = msg;
    smsText.too= order.mobileNumber;

    await message.AddAsync(smsText);
}
```

## <a name="example-nodejs-queue-trigger-with-twilio-output-binding"></a>Exemple de déclencheur de file d’attente Node.js avec liaison de sortie Twilio
Cet exemple Node.js envoie un client tooa de message texte qui a passé une commande.

```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    var msg = "Hello " + myQueueItem.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello message binding.
    context.bindings.message = {};

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    context.bindings.message = {
        body : msg,
        too: myQueueItem.mobileNumber
    };

    context.done();
};
```

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

