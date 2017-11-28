---
title: Liaison Twilio Azure Functions| Microsoft Docs
description: "Découvrez comment utiliser les liaisons Twilio dans Azure Functions."
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
ms.openlocfilehash: 870e47ec7f8ce41ee4acadc7b8ed59298958acbe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="send-sms-messages-from-azure-functions-using-the-twilio-output-binding"></a><span data-ttu-id="0ff30-104">Envoi de messages SMS depuis Azure Functions à l’aide de la liaison de sortie Twilio</span><span class="sxs-lookup"><span data-stu-id="0ff30-104">Send SMS messages from Azure Functions using the Twilio output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="0ff30-105">Cet article vous explique comment configurer et utiliser les liaisons Twilio avec Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="0ff30-105">This article explains how to configure and use Twilio bindings with Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="0ff30-106">Azure Functions prend en charge les liaisons de sortie Twilio, afin de permettre à vos fonctions d’envoyer des SMS avec quelques lignes de codes et un compte [Twilio](https://www.twilio.com/).</span><span class="sxs-lookup"><span data-stu-id="0ff30-106">Azure Functions supports Twilio output bindings to enable your functions to send SMS text messages with a few lines of code and a [Twilio](https://www.twilio.com/) account.</span></span> 

## <a name="functionjson-for-the-twilio-output-binding"></a><span data-ttu-id="0ff30-107">function.json pour la liaison de sortie Twilio</span><span class="sxs-lookup"><span data-stu-id="0ff30-107">function.json for the Twilio output binding</span></span>
<span data-ttu-id="0ff30-108">Le fichier function.json spécifie les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="0ff30-108">The function.json file provides the following properties:</span></span>

* <span data-ttu-id="0ff30-109">`name` : nom de la variable utilisée dans le code de fonction pour le SMS Twilio.</span><span class="sxs-lookup"><span data-stu-id="0ff30-109">`name` : Variable name used in function code for the Twilio SMS text message.</span></span>
* <span data-ttu-id="0ff30-110">`type` : doit être définie sur *"twilioSms"*.</span><span class="sxs-lookup"><span data-stu-id="0ff30-110">`type` : must be set to *"twilioSms"*.</span></span>
* <span data-ttu-id="0ff30-111">`accountSid` : cette valeur doit être définie sur le nom d’un paramètre d’application hébergeant le SID de votre compte Twilio.</span><span class="sxs-lookup"><span data-stu-id="0ff30-111">`accountSid` : This value must be set to the name of an App Setting that holds your Twilio Account Sid.</span></span>
* <span data-ttu-id="0ff30-112">`authToken` : cette valeur doit être définie sur le nom d’un paramètre d’application hébergeant le jeton d’authentification Twilio.</span><span class="sxs-lookup"><span data-stu-id="0ff30-112">`authToken` : This value must be set to the name of an App Setting that holds your Twilio authentication token.</span></span>
* <span data-ttu-id="0ff30-113">`to` : cette valeur est définie sur le numéro de téléphone sur lequel est envoyé le SMS.</span><span class="sxs-lookup"><span data-stu-id="0ff30-113">`to` : This value is set to the phone number that the SMS text is sent to.</span></span>
* <span data-ttu-id="0ff30-114">`from` : cette valeur est définie sur le numéro de téléphone à partir duquel est envoyé le SMS.</span><span class="sxs-lookup"><span data-stu-id="0ff30-114">`from` : This value is set to the phone number that the SMS text is sent from.</span></span>
* <span data-ttu-id="0ff30-115">`direction` : doit être défini sur *out*.</span><span class="sxs-lookup"><span data-stu-id="0ff30-115">`direction` : must be set to *"out"*.</span></span>
* <span data-ttu-id="0ff30-116">`body` : cette valeur peut être utilisée pour coder en dur le SMS, si vous n’avez pas besoin de procéder à une définition dynamique dans le code associé à votre fonction.</span><span class="sxs-lookup"><span data-stu-id="0ff30-116">`body` : This value can be used to hard code the SMS text message if you don't need to set it dynamically in the code for your function.</span></span> 

<span data-ttu-id="0ff30-117">Exemple de fichier function.json :</span><span class="sxs-lookup"><span data-stu-id="0ff30-117">Example function.json:</span></span>

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


## <a name="example-c-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="0ff30-118">Exemple de déclencheur de file d’attente C# avec liaison de sortie Twilio</span><span class="sxs-lookup"><span data-stu-id="0ff30-118">Example C# queue trigger with Twilio output binding</span></span>
#### <a name="synchronous"></a><span data-ttu-id="0ff30-119">Synchrone</span><span class="sxs-lookup"><span data-stu-id="0ff30-119">Synchronous</span></span>
<span data-ttu-id="0ff30-120">Cet exemple de code asynchrone pour un déclencheur de file d’attente Azure Storage utilise un paramètre sortant pour envoyer un SMS à un client qui a passé une commande.</span><span class="sxs-lookup"><span data-stu-id="0ff30-120">This synchronous example code for an Azure Storage queue trigger uses an out parameter to send a text message to a customer who placed an order.</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static void Run(string myQueueItem, out SMSMessage message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a JSON string representing an order that contains the name of a 
    // customer and a mobile number to send text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want to use a hard coded message and number in the binding, you must at least 
    // initialize the SMSMessage variable.
    message = new SMSMessage();

    // A dynamic message can be set instead of the body in the output binding. In this example, we use 
    // the order information to personalize a text message to the mobile number provided for
    // order status updates.
    message.Body = msg;
    message.To = order.mobileNumber;
}
```

#### <a name="asynchronous"></a><span data-ttu-id="0ff30-121">Asynchrone</span><span class="sxs-lookup"><span data-stu-id="0ff30-121">Asynchronous</span></span>
<span data-ttu-id="0ff30-122">Cet exemple de code asynchrone pour un déclencheur de file d’attente Azure Storage envoie un SMS à un client qui a passé une commande.</span><span class="sxs-lookup"><span data-stu-id="0ff30-122">This asynchronous example code for an Azure Storage queue trigger sends a text message to a customer who placed an order.</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static async Task Run(string myQueueItem, IAsyncCollector<SMSMessage> message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a JSON string representing an order that contains the name of a 
    // customer and a mobile number to send text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want to use a hard coded message and number in the binding, you must at least 
    // initialize the SMSMessage variable.
    SMSMessage smsText = new SMSMessage();

    // A dynamic message can be set instead of the body in the output binding. In this example, we use 
    // the order information to personalize a text message to the mobile number provided for
    // order status updates.
    smsText.Body = msg;
    smsText.To = order.mobileNumber;

    await message.AddAsync(smsText);
}
```

## <a name="example-nodejs-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="0ff30-123">Exemple de déclencheur de file d’attente Node.js avec liaison de sortie Twilio</span><span class="sxs-lookup"><span data-stu-id="0ff30-123">Example Node.js queue trigger with Twilio output binding</span></span>
<span data-ttu-id="0ff30-124">Cet exemple Node.js envoie un SMS à un client qui a passé une commande.</span><span class="sxs-lookup"><span data-stu-id="0ff30-124">This Node.js example sends a text message to a customer who placed an order.</span></span>

```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);

    // In this example the queue item is a JSON string representing an order that contains the name of a 
    // customer and a mobile number to send text updates to.
    var msg = "Hello " + myQueueItem.name + ", thank you for your order.";

    // Even if you want to use a hard coded message and number in the binding, you must at least 
    // initialize the message binding.
    context.bindings.message = {};

    // A dynamic message can be set instead of the body in the output binding. In this example, we use 
    // the order information to personalize a text message to the mobile number provided for
    // order status updates.
    context.bindings.message = {
        body : msg,
        to : myQueueItem.mobileNumber
    };

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="0ff30-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0ff30-125">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

