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
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a><span data-ttu-id="515aa-103">Scénario d’application logique : créer un déclencheur à l’aide d’Azure Functions et d’Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="515aa-103">Scenario: Trigger a logic app with Azure Functions and Azure Service Bus</span></span>

<span data-ttu-id="515aa-104">Lorsque vous avez besoin de toodeploy un écouteur longue ou une tâche, vous pouvez utiliser les fonctions Azure toocreate un déclencheur pour une application logique.</span><span class="sxs-lookup"><span data-stu-id="515aa-104">You can use Azure Functions toocreate a trigger for a logic app when you need toodeploy a long-running listener or task.</span></span> <span data-ttu-id="515aa-105">Par exemple, vous pouvez créer une fonction qui écoute une file d’attente, puis déclenche immédiatement une application logique en tant que déclencheur d’émission.</span><span class="sxs-lookup"><span data-stu-id="515aa-105">For example, you can create a function that listens in on a queue and then immediately fire a logic app as a push trigger.</span></span>

## <a name="build-hello-logic-app"></a><span data-ttu-id="515aa-106">Générez l’application logique de hello</span><span class="sxs-lookup"><span data-stu-id="515aa-106">Build hello logic app</span></span>
<span data-ttu-id="515aa-107">Dans cet exemple, vous disposez d’une fonction en cours d’exécution pour chaque application de la logique qui doit toobe déclenchée.</span><span class="sxs-lookup"><span data-stu-id="515aa-107">In this example, you have a function running for each logic app that needs toobe triggered.</span></span> <span data-ttu-id="515aa-108">Créez d’abord une application logique comportant un déclencheur de demande HTTP.</span><span class="sxs-lookup"><span data-stu-id="515aa-108">First, create a logic app that has an HTTP request trigger.</span></span> <span data-ttu-id="515aa-109">fonction Hello appelle ce point de terminaison chaque fois qu’un message de la file d’attente est reçu.</span><span class="sxs-lookup"><span data-stu-id="515aa-109">hello function calls that endpoint whenever a queue message is received.</span></span>  

1. <span data-ttu-id="515aa-110">Créez une application logique.</span><span class="sxs-lookup"><span data-stu-id="515aa-110">Create a logic app.</span></span>
2. <span data-ttu-id="515aa-111">Sélectionnez hello **manuel - lors de la réception d’une requête HTTP** déclencheur.</span><span class="sxs-lookup"><span data-stu-id="515aa-111">Select hello **Manual - When an HTTP Request is Received** trigger.</span></span>
   <span data-ttu-id="515aa-112">Si vous le souhaitez, vous pouvez spécifier un toouse de schéma JSON avec un message de type hello file d’attente à l’aide d’un outil tel que [jsonschema.net](http://jsonschema.net).</span><span class="sxs-lookup"><span data-stu-id="515aa-112">Optionally, you can specify a JSON schema toouse with hello queue message by using a tool like [jsonschema.net](http://jsonschema.net).</span></span> <span data-ttu-id="515aa-113">Schéma de hello coller dans le déclencheur de hello.</span><span class="sxs-lookup"><span data-stu-id="515aa-113">Paste hello schema in hello trigger.</span></span> <span data-ttu-id="515aa-114">Schémas de comprendre le concepteur hello forme hello des propriétés de données et le flux hello plus facilement à l’aide de flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="515aa-114">Schemas help hello designer understand hello shape of hello data and flow properties more easily through hello workflow.</span></span>
2. <span data-ttu-id="515aa-115">Ajoutez les éventuelles étapes supplémentaires que vous souhaitez toooccur après la réception d’un message de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="515aa-115">Add any additional steps that you want toooccur after a queue message is received.</span></span> <span data-ttu-id="515aa-116">Par exemple, envoyer un courrier électronique via Office 365.</span><span class="sxs-lookup"><span data-stu-id="515aa-116">For example, send an email via Office 365.</span></span>  
3. <span data-ttu-id="515aa-117">Enregistrez hello logique toogenerate hello rappel URL de l’application pour l’application de la logique de hello déclencheur toothis.</span><span class="sxs-lookup"><span data-stu-id="515aa-117">Save hello logic app toogenerate hello callback URL for hello trigger toothis logic app.</span></span> <span data-ttu-id="515aa-118">URL de Hello apparaît sur la carte de déclencheur hello.</span><span class="sxs-lookup"><span data-stu-id="515aa-118">hello URL appears on hello trigger card.</span></span>

![URL de rappel de Hello apparaît sur la carte de déclencheur hello][1]

## <a name="build-hello-function"></a><span data-ttu-id="515aa-120">Créer la fonction hello</span><span class="sxs-lookup"><span data-stu-id="515aa-120">Build hello function</span></span>
<span data-ttu-id="515aa-121">Ensuite, vous devez créer une fonction qui agit en tant que déclencheur de hello et d’écoute de file d’attente toohello.</span><span class="sxs-lookup"><span data-stu-id="515aa-121">Next, you must create a function that acts as hello trigger and listens toohello queue.</span></span>

1. <span data-ttu-id="515aa-122">Bonjour [portal de fonctions d’Azure](https://functions.azure.com/signin), sélectionnez **nouvelle fonction**, puis sélectionnez hello **ServiceBusQueueTrigger - C#** modèle.</span><span class="sxs-lookup"><span data-stu-id="515aa-122">In hello [Azure Functions portal](https://functions.azure.com/signin), select **New Function**, and then select hello **ServiceBusQueueTrigger - C#** template.</span></span>
   
    ![portail Azure Functions][2]
2. <span data-ttu-id="515aa-124">Configurer hello connexion toohello Bus de Service file d’attente, qui utilise hello Azure Service Bus SDK `OnMessageReceive()` écouteur.</span><span class="sxs-lookup"><span data-stu-id="515aa-124">Configure hello connection toohello Service Bus queue, which uses hello Azure Service Bus SDK `OnMessageReceive()` listener.</span></span>
3. <span data-ttu-id="515aa-125">Écrire une fonction de base toocall hello logique application point de terminaison (créé précédemment) à l’aide du message de file d’attente hello en tant que déclencheur.</span><span class="sxs-lookup"><span data-stu-id="515aa-125">Write a basic function toocall hello logic app endpoint (created earlier) by using hello queue message as a trigger.</span></span> <span data-ttu-id="515aa-126">Voici un exemple complet d’une fonction.</span><span class="sxs-lookup"><span data-stu-id="515aa-126">Here's a full example of a function.</span></span> <span data-ttu-id="515aa-127">exemple de Hello utilise un `application/json` type de contenu de message, mais vous pouvez modifier ce type si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="515aa-127">hello example uses an `application/json` message content type, but you can change this type as necessary.</span></span>
   
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

<span data-ttu-id="515aa-128">tootest, ajouter un message de la file d’attente via un outil tel que [Explorateur Service Bus](https://github.com/paolosalvatori/ServiceBusExplorer).</span><span class="sxs-lookup"><span data-stu-id="515aa-128">tootest, add a queue message via a tool like [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span></span> <span data-ttu-id="515aa-129">Consultez hello logique application déclenche immédiatement après que la fonction hello reçoit le message de type hello.</span><span class="sxs-lookup"><span data-stu-id="515aa-129">See hello logic app fire immediately after hello function receives hello message.</span></span>

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
