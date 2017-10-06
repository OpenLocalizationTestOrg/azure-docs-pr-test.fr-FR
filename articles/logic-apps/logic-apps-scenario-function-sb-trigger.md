---
title: "aaaScenario - applications de la logique de déclencheur avec les fonctions d’Azure et d’Azure Service Bus | Documents Microsoft"
description: "Créer une fonction tootrigger une application logique à l’aide des fonctions d’Azure et d’Azure Service Bus"
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 19cbd921-7071-4221-ab86-b44d0fc0ecef
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/23/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: a7b78ebcfe492eee2e08ceeae6b9c5f8ed4717bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a>Scénario d’application logique : créer un déclencheur à l’aide d’Azure Functions et d’Azure Service Bus

Lorsque vous avez besoin de toodeploy un écouteur longue ou une tâche, vous pouvez utiliser les fonctions Azure toocreate un déclencheur pour une application logique. Par exemple, vous pouvez créer une fonction qui écoute une file d’attente, puis déclenche immédiatement une application logique en tant que déclencheur d’émission.

## <a name="build-hello-logic-app"></a>Générez l’application logique de hello
Dans cet exemple, vous disposez d’une fonction en cours d’exécution pour chaque application de la logique qui doit toobe déclenchée. Créez d’abord une application logique comportant un déclencheur de demande HTTP. fonction Hello appelle ce point de terminaison chaque fois qu’un message de la file d’attente est reçu.  

1. Créez une application logique.
2. Sélectionnez hello **manuel - lors de la réception d’une requête HTTP** déclencheur.
   Si vous le souhaitez, vous pouvez spécifier un toouse de schéma JSON avec un message de type hello file d’attente à l’aide d’un outil tel que [jsonschema.net](http://jsonschema.net). Schéma de hello coller dans le déclencheur de hello. Schémas de comprendre le concepteur hello forme hello des propriétés de données et le flux hello plus facilement à l’aide de flux de travail hello.
2. Ajoutez les éventuelles étapes supplémentaires que vous souhaitez toooccur après la réception d’un message de la file d’attente. Par exemple, envoyer un courrier électronique via Office 365.  
3. Enregistrez hello logique toogenerate hello rappel URL de l’application pour l’application de la logique de hello déclencheur toothis. URL de Hello apparaît sur la carte de déclencheur hello.

![URL de rappel de Hello apparaît sur la carte de déclencheur hello][1]

## <a name="build-hello-function"></a>Créer la fonction hello
Ensuite, vous devez créer une fonction qui agit en tant que déclencheur de hello et d’écoute de file d’attente toohello.

1. Bonjour [portal de fonctions d’Azure](https://functions.azure.com/signin), sélectionnez **nouvelle fonction**, puis sélectionnez hello **ServiceBusQueueTrigger - C#** modèle.
   
    ![portail Azure Functions][2]
2. Configurer hello connexion toohello Bus de Service file d’attente, qui utilise hello Azure Service Bus SDK `OnMessageReceive()` écouteur.
3. Écrire une fonction de base toocall hello logique application point de terminaison (créé précédemment) à l’aide du message de file d’attente hello en tant que déclencheur. Voici un exemple complet d’une fonction. exemple de Hello utilise un `application/json` type de contenu de message, mais vous pouvez modifier ce type si nécessaire.
   
   ```
   using System;
   using System.Threading.Tasks;
   using System.Net.Http;
   using System.Text;
   
   private static string logicAppUri = @"https://prod-05.westus.logic.azure.com:443/.........";
   
   public static void Run(string myQueueItem, TraceWriter log)
   {
   
       log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
       using (var client = new HttpClient())
       {
           var response = client.PostAsync(logicAppUri, new StringContent(myQueueItem, Encoding.UTF8, "application/json")).Result;
       }
   }
   ```

tootest, ajouter un message de la file d’attente via un outil tel que [Explorateur Service Bus](https://github.com/paolosalvatori/ServiceBusExplorer). Consultez hello logique application déclenche immédiatement après que la fonction hello reçoit le message de type hello.

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
