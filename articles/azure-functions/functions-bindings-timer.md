---
title: "Déclencheur de minuteur Azure Functions| Microsoft Docs"
description: "Découvrez comment utiliser des déclencheurs de minuteur dans Azure Functions."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, calcul dynamique, architecture sans serveur"
ms.assetid: d2f013d1-f458-42ae-baf8-1810138118ac
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: glenga
ms.custom: 
ms.openlocfilehash: 6a97ab8508f889b77d064a5da70e3c726d62900c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-timer-trigger"></a><span data-ttu-id="f30c6-104">Déclencheur de minuteur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="f30c6-104">Azure Functions timer trigger</span></span>

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="f30c6-105">Cet article explique comment configurer et coder des déclencheurs de minuteur dans Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="f30c6-105">This article explains how to configure and code timer triggers in Azure Functions.</span></span> <span data-ttu-id="f30c6-106">Azure Functions offre une liaison de déclencheur de minuteur qui vous permet d’exécuter votre code de fonction selon une planification définie.</span><span class="sxs-lookup"><span data-stu-id="f30c6-106">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> 

<span data-ttu-id="f30c6-107">Le déclencheur du minuteur prend en charge la montée en charge multi-instance. Une instance unique d’une fonction de minuteur spécifique est exécutée sur toutes les instances.</span><span class="sxs-lookup"><span data-stu-id="f30c6-107">The timer trigger supports multi-instance scale-out. A single instance of a particular timer function is run across all instances.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a><span data-ttu-id="f30c6-108">Déclencheur de minuteur</span><span class="sxs-lookup"><span data-stu-id="f30c6-108">Timer trigger</span></span>
<span data-ttu-id="f30c6-109">Le déclencheur de minuteur d’une fonction utilise l’objet JSON suivant dans le tableau `bindings` de function.json :</span><span class="sxs-lookup"><span data-stu-id="f30c6-109">The timer trigger to a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="f30c6-110">La valeur de `schedule` est une [expression CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) qui contient les six champs suivants :</span><span class="sxs-lookup"><span data-stu-id="f30c6-110">The value of `schedule` is a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that includes these six fields:</span></span> 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
><span data-ttu-id="f30c6-111">De nombreuses expressions CRON disponibles en ligne omettent le champ `{second}`.</span><span class="sxs-lookup"><span data-stu-id="f30c6-111">Many of the cron expressions you find online omit the `{second}` field.</span></span> <span data-ttu-id="f30c6-112">Si vous effectuez une copie à partir de l’une d’entre elles, vous devez l’adapter de façon à prendre en compte le champ `{second}` supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="f30c6-112">If you copy from one of them, you need to adjust for the extra `{second}` field.</span></span> <span data-ttu-id="f30c6-113">Pour obtenir des exemples spécifiques, consultez la section [Exemples de planification](#examples) plus bas.</span><span class="sxs-lookup"><span data-stu-id="f30c6-113">For specific examples, see [Schedule examples](#examples) below.</span></span>

<span data-ttu-id="f30c6-114">Le fuseau horaire par défaut utilisé avec les expressions CRON est le Temps universel coordonné (UTC).</span><span class="sxs-lookup"><span data-stu-id="f30c6-114">The default time zone used with the CRON expressions is Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="f30c6-115">Pour baser votre expression CRON sur un autre fuseau horaire, créez un nouveau paramètre d’application nommé `WEBSITE_TIME_ZONE` pour votre application de fonction.</span><span class="sxs-lookup"><span data-stu-id="f30c6-115">To have your CRON expression based on another time zone, create a new app setting for your function app named `WEBSITE_TIME_ZONE`.</span></span> <span data-ttu-id="f30c6-116">Définissez la valeur sur le nom du fuseau horaire souhaité comme indiqué dans l’[index des fuseaux horaires de Microsoft](https://msdn.microsoft.com/library/ms912391.aspx).</span><span class="sxs-lookup"><span data-stu-id="f30c6-116">Set the value to the name of the desired time zone as shown in the [Microsoft Time Zone Index](https://msdn.microsoft.com/library/ms912391.aspx).</span></span> 

<span data-ttu-id="f30c6-117">Par exemple, *l’heure de l’Est* correspond à UTC-05:00.</span><span class="sxs-lookup"><span data-stu-id="f30c6-117">For example, *Eastern Standard Time* is UTC-05:00.</span></span> <span data-ttu-id="f30c6-118">Pour que votre déclencheur de minuteur se déclenche chaque jour à 10 h 00 (heure de l’Est), vous pouvez utiliser l’expression CRON suivante, qui tient compte du fuseau horaire UTC :</span><span class="sxs-lookup"><span data-stu-id="f30c6-118">To have your timer trigger fire at 10:00 AM EST every day, use the following CRON expression that accounts for UTC time zone:</span></span>

```json
"schedule": "0 0 15 * * *",
``` 

<span data-ttu-id="f30c6-119">Sinon, vous pouvez ajouter un nouveau paramètre d’application pour votre application de fonction nommé `WEBSITE_TIME_ZONE` et définir la valeur sur **Est**.</span><span class="sxs-lookup"><span data-stu-id="f30c6-119">Alternatively, you could add a new app setting for your function app named `WEBSITE_TIME_ZONE` and set the value to **Eastern Standard Time**.</span></span>  <span data-ttu-id="f30c6-120">L’expression CRON suivante peut alors être utilisée pour 10h00 EST :</span><span class="sxs-lookup"><span data-stu-id="f30c6-120">Then the following CRON expression could be used for 10:00 AM EST:</span></span> 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a><span data-ttu-id="f30c6-121">Exemples de planification :</span><span class="sxs-lookup"><span data-stu-id="f30c6-121">Schedule examples</span></span>
<span data-ttu-id="f30c6-122">Voici quelques exemples d’expressions CRON que vous pouvez utiliser pour la propriété `schedule`.</span><span class="sxs-lookup"><span data-stu-id="f30c6-122">Here are some samples of CRON expressions you can use for the `schedule` property.</span></span> 

<span data-ttu-id="f30c6-123">Pour déclencher la fonction toutes les cinq minutes :</span><span class="sxs-lookup"><span data-stu-id="f30c6-123">To trigger once every five minutes:</span></span>

```json
"schedule": "0 */5 * * * *"
```

<span data-ttu-id="f30c6-124">Pour déclencher la fonction toutes les heures :</span><span class="sxs-lookup"><span data-stu-id="f30c6-124">To trigger once at the top of every hour:</span></span>

```json
"schedule": "0 0 * * * *",
```

<span data-ttu-id="f30c6-125">Pour déclencher la fonction toutes les deux heures:</span><span class="sxs-lookup"><span data-stu-id="f30c6-125">To trigger once every two hours:</span></span>

```json
"schedule": "0 0 */2 * * *",
```

<span data-ttu-id="f30c6-126">Pour déclencher la fonction toutes les heures entre 9h et 17h :</span><span class="sxs-lookup"><span data-stu-id="f30c6-126">To trigger once every hour from 9 AM to 5 PM:</span></span>

```json
"schedule": "0 0 9-17 * * *",
```

<span data-ttu-id="f30c6-127">Pour déclencher la fonction à 9h30 tous les jours :</span><span class="sxs-lookup"><span data-stu-id="f30c6-127">To trigger At 9:30 AM every day:</span></span>

```json
"schedule": "0 30 9 * * *",
```

<span data-ttu-id="f30c6-128">Pour déclencher la fonction à 9h30 tous les jours de la semaine :</span><span class="sxs-lookup"><span data-stu-id="f30c6-128">To trigger At 9:30 AM every weekday:</span></span>

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="f30c6-129">Utilisation du déclencheur</span><span class="sxs-lookup"><span data-stu-id="f30c6-129">Trigger usage</span></span>
<span data-ttu-id="f30c6-130">Lorsqu’une fonction de déclenchement du minuteur est appelée, [l’objet minuteur](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) est transmis à la fonction.</span><span class="sxs-lookup"><span data-stu-id="f30c6-130">When a timer trigger function is invoked, the [timer object](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) is passed into the function.</span></span> <span data-ttu-id="f30c6-131">Le code JSON suivant est un exemple de représentation de l’objet minuteur.</span><span class="sxs-lookup"><span data-stu-id="f30c6-131">The following JSON is an example representation of the timer object.</span></span> 

```json
{
    "Schedule":{
    },
    "ScheduleStatus": {
        "Last":"2016-10-04T10:15:00.012699+00:00",
        "Next":"2016-10-04T10:20:00+00:00"
    },
    "IsPastDue":false
}
```

<a name="sample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="f30c6-132">Exemple de déclencheur</span><span class="sxs-lookup"><span data-stu-id="f30c6-132">Trigger sample</span></span>
<span data-ttu-id="f30c6-133">Supposez que le tableau `bindings` de function.json contient le déclencheur de minuteur suivant :</span><span class="sxs-lookup"><span data-stu-id="f30c6-133">Suppose you have the following timer trigger in the `bindings` array of function.json:</span></span>

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="f30c6-134">Consultez l’exemple, dans le langage de votre choix, où l’objet minuteur est lu pour déterminer s’il s’exécute avec du retard.</span><span class="sxs-lookup"><span data-stu-id="f30c6-134">See the language-specific sample that reads the timer object to see whether it's running late.</span></span>

* [<span data-ttu-id="f30c6-135">C#</span><span class="sxs-lookup"><span data-stu-id="f30c6-135">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="f30c6-136">F#</span><span class="sxs-lookup"><span data-stu-id="f30c6-136">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="f30c6-137">Node.JS</span><span class="sxs-lookup"><span data-stu-id="f30c6-137">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="f30c6-138">Exemple de déclencheur en C#</span><span class="sxs-lookup"><span data-stu-id="f30c6-138">Trigger sample in C#</span></span> #
```csharp
public static void Run(TimerInfo myTimer, TraceWriter log)
{
    if(myTimer.IsPastDue)
    {
        log.Info("Timer is running late!");
    }
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}" );  
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="f30c6-139">Exemple de déclencheur en F#</span><span class="sxs-lookup"><span data-stu-id="f30c6-139">Trigger sample in F#</span></span> #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="f30c6-140">Exemple de déclencheur en Node.js</span><span class="sxs-lookup"><span data-stu-id="f30c6-140">Trigger sample in Node.js</span></span>
```JavaScript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    if(myTimer.isPastDue)
    {
        context.log('Node.js is running late!');
    }
    context.log('Node.js timer trigger function ran!', timeStamp);   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="f30c6-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f30c6-141">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

