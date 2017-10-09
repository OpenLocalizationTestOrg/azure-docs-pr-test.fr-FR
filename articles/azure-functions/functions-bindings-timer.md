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
# <a name="azure-functions-timer-trigger"></a>Déclencheur de minuteur Azure Functions

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Cet article explique comment tooconfigure et le code de minuteur déclenche dans les fonctions d’Azure. Azure Functions offre une liaison de déclencheur de minuteur qui vous permet d’exécuter votre code de fonction selon une planification définie. 

déclencheur de minuteur Hello prend en charge plusieurs instances montée en puissance parallèle. Une instance unique d’une fonction de minuteur spécifique est exécutée sur toutes les instances.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a>Déclencheur de minuteur
Hello du minuteur déclencheur tooa (fonction) utilise hello objet JSON Bonjour `bindings` tableau de function.json :

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

Hello valeur `schedule` est un [expression CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) qui inclut ces six champs : 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
>La plupart des expressions de cron hello vous trouvez omettre hello `{second}` champ. Si vous copiez à partir d’un d’eux, vous devez tooadjust pour hello supplémentaire `{second}` champ. Pour obtenir des exemples spécifiques, consultez la section [Exemples de planification](#examples) plus bas.

fuseau horaire de Hello par défaut utilisé avec des expressions CRON hello est le temps universel coordonné (UTC). toohave votre expression CRON basée sur un autre fuseau horaire, créer un nouveau paramètre d’application pour votre application de la fonction nommée `WEBSITE_TIME_ZONE`. Hello valeur toohello le nom du hello souhaité fuseau horaire, comme indiqué dans hello [Index de fuseau horaire Microsoft](https://msdn.microsoft.com/library/ms912391.aspx). 

Par exemple, *l’heure de l’Est* correspond à UTC-05:00. toohave votre minuterie déclencher incendie à 10:00 AM EST chaque jour, hello Utilisez expression CRON qui tient compte de fuseau horaire UTC suivante :

```json
"schedule": "0 0 15 * * *",
``` 

Ou bien, vous pouvez ajouter un nouveau paramètre d’application pour votre application de la fonction nommée `WEBSITE_TIME_ZONE` et la valeur hello trop**l’heure**.  Ensuite, hello suivant expression CRON peut être utilisée pour 10:00 AM EST : 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a>Exemples de planification :
Voici quelques exemples d’expressions CRON que vous pouvez utiliser pour hello `schedule` propriété. 

tootrigger toutes les cinq minutes :

```json
"schedule": "0 */5 * * * *"
```

tootrigger qu’une seule fois haut hello de toutes les heures :

```json
"schedule": "0 0 * * * *",
```

tootrigger toutes les deux heures :

```json
"schedule": "0 0 */2 * * *",
```

tootrigger toutes les heures de too5 de 9 : 00 PM :

```json
"schedule": "0 0 9-17 * * *",
```

tootrigger à 9 h 30 tous les jours :

```json
"schedule": "0 30 9 * * *",
```

tootrigger à 9 h 30 tous les jours ouvrables :

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a>Utilisation du déclencheur
Lorsqu’une fonction de déclenchement du minuteur est appelée, hello [objet timer](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) a été passée dans la fonction hello. Bonjour JSON suivant est un exemple de représentation d’objet de minuterie hello. 

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

## <a name="trigger-sample"></a>Exemple de déclencheur
Supposez que vous avez hello suivant déclencheur du minuteur Bonjour `bindings` tableau de function.json :

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

Voir exemple hello spécifiques au langage qui lit le minuteur de hello toosee de l’objet si elle s’exécute plus tard.

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.JS](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Exemple de déclencheur en C# #
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

### <a name="trigger-sample-in-f"></a>Exemple de déclencheur en F# #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Exemple de déclencheur en Node.js
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

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

