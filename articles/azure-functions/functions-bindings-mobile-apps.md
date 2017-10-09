---
title: liaisons des applications mobiles de fonctions aaaAzure | Documents Microsoft
description: "Comprendre comment les liaisons d’applications mobiles Azure toouse dans les fonctions d’Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, calcul dynamique, architecture sans serveur"
ms.assetid: faad1263-0fa5-41a9-964f-aecbc0be706a
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/31/2016
ms.author: glenga
ms.openlocfilehash: d3679a5d5c66705b32e422ec17e3a1e6d6ac063c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a>Liaisons Azure Mobile Apps Azure Functions
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Cet article explique comment tooconfigure et code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) liaisons dans les fonctions d’Azure. Azure Functions prend en charge des liaisons d’entrée et de sortie pour Mobile Apps.

Hello applications mobiles d’entrée et sortie liaisons vous permettent de [lisent et écrivent des tables de toodata](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) dans votre application mobile.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a>Liaison d’entrée Mobile Apps
Hello liaison d’entrée des applications mobiles charge un enregistrement à partir d’un point de terminaison de table mobile et le passe dans votre fonction. Dans c# et F # fonctions, tout enregistrement toohello de modifications apportées sont automatiquement envoyés arrière toohello table lors de la fonction hello se termine avec succès.

Hello applications mobiles d’entrée tooa fonction utilise hello objet JSON Bonjour `bindings` tableau de function.json :

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of hello record tooretrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

Notez hello suivantes :

* `id`peut être statique, ou il peut être basée sur déclencheur hello qui appelle la fonction hello. Par exemple, si vous utilisez un [déclencheur de la file d’attente]() de votre fonction, puis `"id": "{queueTrigger}"` utilise hello la valeur de chaîne de message de file d’attente hello comme enregistrement ID tooretrieve de hello.
* `connection`doit contenir nom hello d’un paramètre d’application dans votre application de fonction, qui à son tour contient hello les URL de votre application mobile. fonction Hello utilise cette URL tooconstruct hello requis des opérations de reste par rapport à votre application mobile. Vous [créer un paramètre d’application dans votre application de la fonction]() qui contient les URL de votre application mobile (qui ressemble à `http://<appname>.azurewebsites.net`), puis spécifiez le nom de hello du paramètre d’application hello Bonjour `connection` propriété dans votre liaison d’entrée. 
* Vous devez toospecify `apiKey` si vous [implémenter une clé d’API dans le service principal de votre application mobile Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), ou [implémenter une clé d’API dans le service principal de votre application mobile .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key). toodo, vous [créer un paramètre d’application dans votre application de la fonction]() qui contient la clé d’API de hello, puis ajoutez hello `apiKey` propriété dans votre liaison d’entrée par nom de hello du paramètre d’application hello. 
  
  > [!IMPORTANT]
  > Cette clé API ne doit pas être partagée avec vos clients d’application mobile. Il ne doit être distribuées clients tooservice côté en toute sécurité, comme les fonctions d’Azure. 
  > 
  > [!NOTE]
  > Azure Functions stocke vos informations de connexion et les clés API en tant que paramètres d’application, de sorte qu’elles ne soient pas vérifiées dans votre référentiel de contrôle de code source. Ceci protège vos informations sensibles.
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a>Utilisation en entrée
Cette section vous montre comment toouse vos applications mobiles d’entrée de liaison dans votre code de fonction. 

Lors de l’enregistrement hello avec hello spécifié ID de table et d’enregistrement est trouvé, il est passé dans hello nommé [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) paramètre (ou, dans Node.js, il est passé dans hello `context.bindings.<name>` objet). Lors de l’enregistrement de hello n’est pas trouvé, le paramètre hello est `null`. 

Dans les fonctions de c# et F #, toute modification apportée toohello entrée enregistrement (paramètre d’entrée) est automatiquement envoyé arrière toohello table des applications mobiles lors de la fonction hello se termine avec succès. Dans les fonctions de Node.js, utilisez `context.bindings.<name>` tooaccess hello enregistrement d’entrée. Vous ne pouvez pas modifier un enregistrement dans Node.js.

<a name="inputsample"></a>

## <a name="input-sample"></a>Exemple d’entrée
Supposez que vous avez hello suivant function.json, qui extrait un enregistrement de la table de l’application Mobile avec l’id de hello de message de déclenchement de file d’attente hello :

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
        "name": "record",
        "type": "mobileTable",
        "tableName": "MyTable",
        "id" : "{queueTrigger}",
        "connection": "My_MobileApp_Url",
        "apiKey": "My_MobileApp_Key",
        "direction": "in"
    }
],
"disabled": false
}
```

Voir l’exemple hello spécifiques à une langue qui utilise l’enregistrement d’entrée de hello à partir de la liaison de hello. les exemples c# et F # Hello également modifier l’enregistrement hello `text` propriété.

* [C#](#inputcsharp)
* [Node.JS](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a>Exemple d’entrée en C# #

```cs
#r "Newtonsoft.Json"    
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, JObject record)
{
    if (record != null)
    {
        record["Text"] = "This has changed.";
    }    
}
```

<!--
<a name="inputfsharp"></a>
### Input sample in F# ## 

```fsharp
#r "Newtonsoft.Json"    
open Newtonsoft.Json.Linq
let Run(myQueueItem: string, record: JObject) =
  inputDocument?text <- "This has changed."
```
-->

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a>Exemple d’entrée en Node.js

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a>Liaison de sortie Mobile Apps
Utilisez hello Mobile Apps sortie liaison toowrite un enregistrement tooa Mobile Apps table point de terminaison.  

Hello des applications mobiles de sortie pour une fonction utilise hello objet JSON Bonjour `bindings` tableau de function.json :

```json
{
    "name": "<Name of output parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "out"
}
```

Notez hello suivantes :

* `connection`doit contenir nom hello d’un paramètre d’application dans votre application de fonction, qui à son tour contient hello les URL de votre application mobile. fonction Hello utilise cette URL tooconstruct hello requis des opérations de reste par rapport à votre application mobile. Vous [créer un paramètre d’application dans votre application de la fonction]() qui contient les URL de votre application mobile (qui ressemble à `http://<appname>.azurewebsites.net`), puis spécifiez le nom de hello du paramètre d’application hello Bonjour `connection` propriété dans votre liaison d’entrée. 
* Vous devez toospecify `apiKey` si vous [implémenter une clé d’API dans le service principal de votre application mobile Node.js](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), ou [implémenter une clé d’API dans le service principal de votre application mobile .NET](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key). toodo, vous [créer un paramètre d’application dans votre application de la fonction]() qui contient la clé d’API de hello, puis ajoutez hello `apiKey` propriété dans votre liaison d’entrée par nom de hello du paramètre d’application hello. 
  
  > [!IMPORTANT]
  > Cette clé API ne doit pas être partagée avec vos clients d’application mobile. Il ne doit être distribuées clients tooservice côté en toute sécurité, comme les fonctions d’Azure. 
  > 
  > [!NOTE]
  > Azure Functions stocke vos informations de connexion et les clés API en tant que paramètres d’application, de sorte qu’elles ne soient pas vérifiées dans votre référentiel de contrôle de code source. Ceci protège vos informations sensibles.
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a>Utilisation en sortie
Cette section vous montre comment toouse vos applications mobiles de sortie de liaison dans votre code de fonction. 

Dans les fonctions de c#, utilisez un paramètre de sortie nommés de type `out object` tooaccess hello sortie d’enregistrement. Dans les fonctions de Node.js, utilisez `context.bindings.<name>` tooaccess hello sortie d’enregistrement.

<a name="outputsample"></a>

## <a name="output-sample"></a>Exemple de sortie
Supposons que vous avez hello suivant function.json, qui définit un déclencheur de la file d’attente et une sortie d’applications mobiles :

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
    "name": "record",
    "type": "mobileTable",
    "tableName": "MyTable",
    "connection": "My_MobileApp_Url",
    "apiKey": "My_MobileApp_Key",
    "direction": "out"
    }
],
"disabled": false
}
```

Voir exemple hello spécifiques au langage qui crée un enregistrement de point de terminaison de table hello applications mobiles avec le contenu du message de file d’attente hello hello.

* [C#](#outcsharp)
* [Node.JS](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Exemple de sortie en C# #

```cs
public static void Run(string myQueueItem, out object record)
{
    record = new {
        Text = $"I'm running in a C# function! {myQueueItem}"
    };
}
```

<!--
<a name="outfsharp"></a>
### Output sample in F# ## 
```fsharp

```
-->
<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a>Exemple de sortie en Node.js

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

