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
# <a name="send-sms-messages-from-azure-functions-using-hello-twilio-output-binding"></a><span data-ttu-id="4fc46-104">Envoyer des messages SMS à partir des fonctions d’Azure à l’aide de hello liaison de sortie Twilio</span><span class="sxs-lookup"><span data-stu-id="4fc46-104">Send SMS messages from Azure Functions using hello Twilio output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="4fc46-105">Cet article explique comment les liaisons Twilio tooconfigure et l’utilisation avec des fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="4fc46-105">This article explains how tooconfigure and use Twilio bindings with Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="4fc46-106">Prend en charge les fonctions Azure Twilio sortie liaisons tooenable votre texte SMS toosend fonctions des messages avec quelques lignes de code et un [Twilio](https://www.twilio.com/) compte.</span><span class="sxs-lookup"><span data-stu-id="4fc46-106">Azure Functions supports Twilio output bindings tooenable your functions toosend SMS text messages with a few lines of code and a [Twilio](https://www.twilio.com/) account.</span></span> 

## <a name="functionjson-for-hello-twilio-output-binding"></a><span data-ttu-id="4fc46-107">liaison de sortie de Twilio Function.JSON pour hello</span><span class="sxs-lookup"><span data-stu-id="4fc46-107">function.json for hello Twilio output binding</span></span>
<span data-ttu-id="4fc46-108">fichier de function.json Hello fournit hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="4fc46-108">hello function.json file provides hello following properties:</span></span>

* <span data-ttu-id="4fc46-109">`name`: Nom variable utilisée dans le code de fonction pour hello SMS Twilio SMS.</span><span class="sxs-lookup"><span data-stu-id="4fc46-109">`name` : Variable name used in function code for hello Twilio SMS text message.</span></span>
* <span data-ttu-id="4fc46-110">`type`: doit être défini trop*« twilioSms »*.</span><span class="sxs-lookup"><span data-stu-id="4fc46-110">`type` : must be set too*"twilioSms"*.</span></span>
* <span data-ttu-id="4fc46-111">`accountSid`: Cette valeur doit être définie toohello les nom d’un paramètre d’application qui contient le Sid de votre compte Twilio.</span><span class="sxs-lookup"><span data-stu-id="4fc46-111">`accountSid` : This value must be set toohello name of an App Setting that holds your Twilio Account Sid.</span></span>
* <span data-ttu-id="4fc46-112">`authToken`: Cette valeur doit être définie toohello les nom d’un paramètre d’application qui contient votre jeton d’authentification Twilio.</span><span class="sxs-lookup"><span data-stu-id="4fc46-112">`authToken` : This value must be set toohello name of an App Setting that holds your Twilio authentication token.</span></span>
* <span data-ttu-id="4fc46-113">`to`: Cette valeur est définie de numéro de téléphone toohello hello SMS texte est envoyé à.</span><span class="sxs-lookup"><span data-stu-id="4fc46-113">`to` : This value is set toohello phone number that hello SMS text is sent to.</span></span>
* <span data-ttu-id="4fc46-114">`from`: Cette valeur est définie de numéro de téléphone toohello texte SMS de hello est envoyé à partir de.</span><span class="sxs-lookup"><span data-stu-id="4fc46-114">`from` : This value is set toohello phone number that hello SMS text is sent from.</span></span>
* <span data-ttu-id="4fc46-115">`direction`: doit être défini trop*« out »*.</span><span class="sxs-lookup"><span data-stu-id="4fc46-115">`direction` : must be set too*"out"*.</span></span>
* <span data-ttu-id="4fc46-116">`body`: Cette valeur peut être utilisé toohard code hello message texte envoyé si vous n’avez pas besoin tooset dynamiquement dans hello du code de votre fonction.</span><span class="sxs-lookup"><span data-stu-id="4fc46-116">`body` : This value can be used toohard code hello SMS text message if you don't need tooset it dynamically in hello code for your function.</span></span> 

<span data-ttu-id="4fc46-117">Exemple de fichier function.json :</span><span class="sxs-lookup"><span data-stu-id="4fc46-117">Example function.json:</span></span>

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


## <a name="example-c-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="4fc46-118">Exemple de déclencheur de file d’attente C# avec liaison de sortie Twilio</span><span class="sxs-lookup"><span data-stu-id="4fc46-118">Example C# queue trigger with Twilio output binding</span></span>
#### <a name="synchronous"></a><span data-ttu-id="4fc46-119">Synchrone</span><span class="sxs-lookup"><span data-stu-id="4fc46-119">Synchronous</span></span>
<span data-ttu-id="4fc46-120">Ce code exemple synchrone pour un déclencheur de file d’attente de stockage Azure utilise un hors toosend du paramètre client tooa message texte qui a passé une commande.</span><span class="sxs-lookup"><span data-stu-id="4fc46-120">This synchronous example code for an Azure Storage queue trigger uses an out parameter toosend a text message tooa customer who placed an order.</span></span>

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

#### <a name="asynchronous"></a><span data-ttu-id="4fc46-121">Asynchrone</span><span class="sxs-lookup"><span data-stu-id="4fc46-121">Asynchronous</span></span>
<span data-ttu-id="4fc46-122">Ce code exemple asynchrone d’un déclencheur de file d’attente de stockage Azure envoie un client tooa de message texte qui a passé une commande.</span><span class="sxs-lookup"><span data-stu-id="4fc46-122">This asynchronous example code for an Azure Storage queue trigger sends a text message tooa customer who placed an order.</span></span>

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

## <a name="example-nodejs-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="4fc46-123">Exemple de déclencheur de file d’attente Node.js avec liaison de sortie Twilio</span><span class="sxs-lookup"><span data-stu-id="4fc46-123">Example Node.js queue trigger with Twilio output binding</span></span>
<span data-ttu-id="4fc46-124">Cet exemple Node.js envoie un client tooa de message texte qui a passé une commande.</span><span class="sxs-lookup"><span data-stu-id="4fc46-124">This Node.js example sends a text message tooa customer who placed an order.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4fc46-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4fc46-125">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

