---
title: "déclencheur de minuteur fonctions aaaAzure | Documents Microsoft"
description: "Comprendre comment toouse minuteur déclenche dans les fonctions d’Azure."
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
ms.openlocfilehash: 17fca22372dbc55d4684c8c099cc97923a7d3cf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-timer-trigger"></a><span data-ttu-id="873e6-104">Déclencheur de minuteur Azure Functions</span><span class="sxs-lookup"><span data-stu-id="873e6-104">Azure Functions timer trigger</span></span>

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="873e6-105">Cet article explique comment tooconfigure et le code de minuteur déclenche dans les fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="873e6-105">This article explains how tooconfigure and code timer triggers in Azure Functions.</span></span> <span data-ttu-id="873e6-106">Azure Functions offre une liaison de déclencheur de minuteur qui vous permet d’exécuter votre code de fonction selon une planification définie.</span><span class="sxs-lookup"><span data-stu-id="873e6-106">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> 

<span data-ttu-id="873e6-107">déclencheur de minuteur Hello prend en charge plusieurs instances montée en puissance parallèle. Une instance unique d’une fonction de minuteur spécifique est exécutée sur toutes les instances.</span><span class="sxs-lookup"><span data-stu-id="873e6-107">hello timer trigger supports multi-instance scale-out. A single instance of a particular timer function is run across all instances.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a><span data-ttu-id="873e6-108">Déclencheur de minuteur</span><span class="sxs-lookup"><span data-stu-id="873e6-108">Timer trigger</span></span>
<span data-ttu-id="873e6-109">Hello du minuteur déclencheur tooa (fonction) utilise hello objet JSON Bonjour `bindings` tableau de function.json :</span><span class="sxs-lookup"><span data-stu-id="873e6-109">hello timer trigger tooa function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="873e6-110">Hello valeur `schedule` est un [expression CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) qui inclut ces six champs :</span><span class="sxs-lookup"><span data-stu-id="873e6-110">hello value of `schedule` is a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that includes these six fields:</span></span> 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
><span data-ttu-id="873e6-111">La plupart des expressions de cron hello vous trouvez omettre hello `{second}` champ.</span><span class="sxs-lookup"><span data-stu-id="873e6-111">Many of hello cron expressions you find online omit hello `{second}` field.</span></span> <span data-ttu-id="873e6-112">Si vous copiez à partir d’un d’eux, vous devez tooadjust pour hello supplémentaire `{second}` champ.</span><span class="sxs-lookup"><span data-stu-id="873e6-112">If you copy from one of them, you need tooadjust for hello extra `{second}` field.</span></span> <span data-ttu-id="873e6-113">Pour obtenir des exemples spécifiques, consultez la section [Exemples de planification](#examples) plus bas.</span><span class="sxs-lookup"><span data-stu-id="873e6-113">For specific examples, see [Schedule examples](#examples) below.</span></span>

<span data-ttu-id="873e6-114">fuseau horaire de Hello par défaut utilisé avec des expressions CRON hello est le temps universel coordonné (UTC).</span><span class="sxs-lookup"><span data-stu-id="873e6-114">hello default time zone used with hello CRON expressions is Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="873e6-115">toohave votre expression CRON basée sur un autre fuseau horaire, créer un nouveau paramètre d’application pour votre application de la fonction nommée `WEBSITE_TIME_ZONE`.</span><span class="sxs-lookup"><span data-stu-id="873e6-115">toohave your CRON expression based on another time zone, create a new app setting for your function app named `WEBSITE_TIME_ZONE`.</span></span> <span data-ttu-id="873e6-116">Hello valeur toohello le nom du hello souhaité fuseau horaire, comme indiqué dans hello [Index de fuseau horaire Microsoft](https://msdn.microsoft.com/library/ms912391.aspx).</span><span class="sxs-lookup"><span data-stu-id="873e6-116">Set hello value toohello name of hello desired time zone as shown in hello [Microsoft Time Zone Index](https://msdn.microsoft.com/library/ms912391.aspx).</span></span> 

<span data-ttu-id="873e6-117">Par exemple, *l’heure de l’Est* correspond à UTC-05:00.</span><span class="sxs-lookup"><span data-stu-id="873e6-117">For example, *Eastern Standard Time* is UTC-05:00.</span></span> <span data-ttu-id="873e6-118">toohave votre minuterie déclencher incendie à 10:00 AM EST chaque jour, hello Utilisez expression CRON qui tient compte de fuseau horaire UTC suivante :</span><span class="sxs-lookup"><span data-stu-id="873e6-118">toohave your timer trigger fire at 10:00 AM EST every day, use hello following CRON expression that accounts for UTC time zone:</span></span>

```json
"schedule": "0 0 15 * * *",
``` 

<span data-ttu-id="873e6-119">Ou bien, vous pouvez ajouter un nouveau paramètre d’application pour votre application de la fonction nommée `WEBSITE_TIME_ZONE` et la valeur hello trop**l’heure**.</span><span class="sxs-lookup"><span data-stu-id="873e6-119">Alternatively, you could add a new app setting for your function app named `WEBSITE_TIME_ZONE` and set hello value too**Eastern Standard Time**.</span></span>  <span data-ttu-id="873e6-120">Ensuite, hello suivant expression CRON peut être utilisée pour 10:00 AM EST :</span><span class="sxs-lookup"><span data-stu-id="873e6-120">Then hello following CRON expression could be used for 10:00 AM EST:</span></span> 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a><span data-ttu-id="873e6-121">Exemples de planification :</span><span class="sxs-lookup"><span data-stu-id="873e6-121">Schedule examples</span></span>
<span data-ttu-id="873e6-122">Voici quelques exemples d’expressions CRON que vous pouvez utiliser pour hello `schedule` propriété.</span><span class="sxs-lookup"><span data-stu-id="873e6-122">Here are some samples of CRON expressions you can use for hello `schedule` property.</span></span> 

<span data-ttu-id="873e6-123">tootrigger toutes les cinq minutes :</span><span class="sxs-lookup"><span data-stu-id="873e6-123">tootrigger once every five minutes:</span></span>

```json
"schedule": "0 */5 * * * *"
```

<span data-ttu-id="873e6-124">tootrigger qu’une seule fois haut hello de toutes les heures :</span><span class="sxs-lookup"><span data-stu-id="873e6-124">tootrigger once at hello top of every hour:</span></span>

```json
"schedule": "0 0 * * * *",
```

<span data-ttu-id="873e6-125">tootrigger toutes les deux heures :</span><span class="sxs-lookup"><span data-stu-id="873e6-125">tootrigger once every two hours:</span></span>

```json
"schedule": "0 0 */2 * * *",
```

<span data-ttu-id="873e6-126">tootrigger toutes les heures de too5 de 9 : 00 PM :</span><span class="sxs-lookup"><span data-stu-id="873e6-126">tootrigger once every hour from 9 AM too5 PM:</span></span>

```json
"schedule": "0 0 9-17 * * *",
```

<span data-ttu-id="873e6-127">tootrigger à 9 h 30 tous les jours :</span><span class="sxs-lookup"><span data-stu-id="873e6-127">tootrigger At 9:30 AM every day:</span></span>

```json
"schedule": "0 30 9 * * *",
```

<span data-ttu-id="873e6-128">tootrigger à 9 h 30 tous les jours ouvrables :</span><span class="sxs-lookup"><span data-stu-id="873e6-128">tootrigger At 9:30 AM every weekday:</span></span>

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="873e6-129">Utilisation du déclencheur</span><span class="sxs-lookup"><span data-stu-id="873e6-129">Trigger usage</span></span>
<span data-ttu-id="873e6-130">Lorsqu’une fonction de déclenchement du minuteur est appelée, hello [objet timer](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) a été passée dans la fonction hello.</span><span class="sxs-lookup"><span data-stu-id="873e6-130">When a timer trigger function is invoked, hello [timer object](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) is passed into hello function.</span></span> <span data-ttu-id="873e6-131">Bonjour JSON suivant est un exemple de représentation d’objet de minuterie hello.</span><span class="sxs-lookup"><span data-stu-id="873e6-131">hello following JSON is an example representation of hello timer object.</span></span> 

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

## <a name="trigger-sample"></a><span data-ttu-id="873e6-132">Exemple de déclencheur</span><span class="sxs-lookup"><span data-stu-id="873e6-132">Trigger sample</span></span>
<span data-ttu-id="873e6-133">Supposez que vous avez hello suivant déclencheur du minuteur Bonjour `bindings` tableau de function.json :</span><span class="sxs-lookup"><span data-stu-id="873e6-133">Suppose you have hello following timer trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="873e6-134">Voir exemple hello spécifiques au langage qui lit le minuteur de hello toosee de l’objet si elle s’exécute plus tard.</span><span class="sxs-lookup"><span data-stu-id="873e6-134">See hello language-specific sample that reads hello timer object toosee whether it's running late.</span></span>

* [<span data-ttu-id="873e6-135">C#</span><span class="sxs-lookup"><span data-stu-id="873e6-135">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="873e6-136">F#</span><span class="sxs-lookup"><span data-stu-id="873e6-136">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="873e6-137">Node.JS</span><span class="sxs-lookup"><span data-stu-id="873e6-137">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="873e6-138">Exemple de déclencheur en C#</span><span class="sxs-lookup"><span data-stu-id="873e6-138">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-f"></a><span data-ttu-id="873e6-139">Exemple de déclencheur en F#</span><span class="sxs-lookup"><span data-stu-id="873e6-139">Trigger sample in F#</span></span> #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="873e6-140">Exemple de déclencheur en Node.js</span><span class="sxs-lookup"><span data-stu-id="873e6-140">Trigger sample in Node.js</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="873e6-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="873e6-141">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

