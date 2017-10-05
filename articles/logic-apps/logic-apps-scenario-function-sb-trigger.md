---
title: "Scénario d’application logique : créer un déclencheur à l’aide d’Azure Functions et d’Azure Service Bus | Microsoft Docs"
description: "Créer une fonction pour déclencher une application logique à l’aide d’Azure Functions et d’Azure Service Bus"
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
ms.openlocfilehash: 088f10bc32dd492f82f0a10a7e5829e76f588758
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="scenario-trigger-a-logic-app-with-azure-functions-and-azure-service-bus"></a><span data-ttu-id="8f553-103">Scénario d’application logique : créer un déclencheur à l’aide d’Azure Functions et d’Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="8f553-103">Scenario: Trigger a logic app with Azure Functions and Azure Service Bus</span></span>

<span data-ttu-id="8f553-104">Vous pouvez utiliser Azure Functions afin de créer un déclencheur pour une application logique lorsque vous avez besoin de déployer un écouteur ou une tâche de longue durée.</span><span class="sxs-lookup"><span data-stu-id="8f553-104">You can use Azure Functions to create a trigger for a logic app when you need to deploy a long-running listener or task.</span></span> <span data-ttu-id="8f553-105">Par exemple, vous pouvez créer une fonction qui écoute une file d’attente, puis déclenche immédiatement une application logique en tant que déclencheur d’émission.</span><span class="sxs-lookup"><span data-stu-id="8f553-105">For example, you can create a function that listens in on a queue and then immediately fire a logic app as a push trigger.</span></span>

## <a name="build-the-logic-app"></a><span data-ttu-id="8f553-106">Création de l'application logique</span><span class="sxs-lookup"><span data-stu-id="8f553-106">Build the logic app</span></span>
<span data-ttu-id="8f553-107">Dans cet exemple, une fonction est en cours d’exécution pour chaque application logique à déclencher.</span><span class="sxs-lookup"><span data-stu-id="8f553-107">In this example, you have a function running for each logic app that needs to be triggered.</span></span> <span data-ttu-id="8f553-108">Créez d’abord une application logique comportant un déclencheur de demande HTTP.</span><span class="sxs-lookup"><span data-stu-id="8f553-108">First, create a logic app that has an HTTP request trigger.</span></span> <span data-ttu-id="8f553-109">La fonction appelle ce point de terminaison chaque fois qu’un message de la file d’attente est reçu.</span><span class="sxs-lookup"><span data-stu-id="8f553-109">The function calls that endpoint whenever a queue message is received.</span></span>  

1. <span data-ttu-id="8f553-110">Créez une application logique.</span><span class="sxs-lookup"><span data-stu-id="8f553-110">Create a logic app.</span></span>
2. <span data-ttu-id="8f553-111">Sélectionnez le déclencheur **Manuel – Lors de la réception d’une demande HTTP**.</span><span class="sxs-lookup"><span data-stu-id="8f553-111">Select the **Manual - When an HTTP Request is Received** trigger.</span></span>
   <span data-ttu-id="8f553-112">Si vous le souhaitez, vous pouvez spécifier un schéma JSON à utiliser avec le message de la file d’attente à l’aide d’un outil tel que [jsonschema.net](http://jsonschema.net).</span><span class="sxs-lookup"><span data-stu-id="8f553-112">Optionally, you can specify a JSON schema to use with the queue message by using a tool like [jsonschema.net](http://jsonschema.net).</span></span> <span data-ttu-id="8f553-113">Collez le schéma dans le déclencheur.</span><span class="sxs-lookup"><span data-stu-id="8f553-113">Paste the schema in the trigger.</span></span> <span data-ttu-id="8f553-114">Les schémas aident le concepteur à comprendre la forme des données et à répercuter plus facilement les propriétés dans le workflow.</span><span class="sxs-lookup"><span data-stu-id="8f553-114">Schemas help the designer understand the shape of the data and flow properties more easily through the workflow.</span></span>
2. <span data-ttu-id="8f553-115">Ajoutez les étapes supplémentaires à exécuter après réception d’un message de la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="8f553-115">Add any additional steps that you want to occur after a queue message is received.</span></span> <span data-ttu-id="8f553-116">Par exemple, envoyer un courrier électronique via Office 365.</span><span class="sxs-lookup"><span data-stu-id="8f553-116">For example, send an email via Office 365.</span></span>  
3. <span data-ttu-id="8f553-117">Enregistrez l’application logique pour générer l’URL de rappel du déclencheur sur cette application logique.</span><span class="sxs-lookup"><span data-stu-id="8f553-117">Save the logic app to generate the callback URL for the trigger to this logic app.</span></span> <span data-ttu-id="8f553-118">L’URL s’affiche sur la carte de déclencheur.</span><span class="sxs-lookup"><span data-stu-id="8f553-118">The URL appears on the trigger card.</span></span>

![L’URL de rappel s’affiche sur la carte de déclencheur][1]

## <a name="build-the-function"></a><span data-ttu-id="8f553-120">Création de la fonction</span><span class="sxs-lookup"><span data-stu-id="8f553-120">Build the function</span></span>
<span data-ttu-id="8f553-121">Vous devez ensuite créer une fonction qui agit comme déclencheur et qui écoute la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="8f553-121">Next, you must create a function that acts as the trigger and listens to the queue.</span></span>

1. <span data-ttu-id="8f553-122">Dans le [portail Azure Functions](https://functions.azure.com/signin), sélectionnez **Nouvelle fonction** puis choisissez le modèle **ServiceBusQueueTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="8f553-122">In the [Azure Functions portal](https://functions.azure.com/signin), select **New Function**, and then select the **ServiceBusQueueTrigger - C#** template.</span></span>
   
    ![portail Azure Functions][2]
2. <span data-ttu-id="8f553-124">Configurez la connexion à la file d’attente Service Bus qui utilise l’écouteur `OnMessageReceive()` du SDK Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="8f553-124">Configure the connection to the Service Bus queue, which uses the Azure Service Bus SDK `OnMessageReceive()` listener.</span></span>
3. <span data-ttu-id="8f553-125">Écrivez une fonction de base pour appeler le point de terminaison de l’application logique (créé précédemment) en utilisant le message de la file d’attente comme déclencheur.</span><span class="sxs-lookup"><span data-stu-id="8f553-125">Write a basic function to call the logic app endpoint (created earlier) by using the queue message as a trigger.</span></span> <span data-ttu-id="8f553-126">Voici un exemple complet d’une fonction.</span><span class="sxs-lookup"><span data-stu-id="8f553-126">Here's a full example of a function.</span></span> <span data-ttu-id="8f553-127">L’exemple utilise un type de contenu de message `application/json`, mais vous pouvez le modifier si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8f553-127">The example uses an `application/json` message content type, but you can change this type as necessary.</span></span>
   
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

<span data-ttu-id="8f553-128">Pour tester, ajoutez un message de la file d’attente via un outil tel que l [’Explorateur Service Bus](https://github.com/paolosalvatori/ServiceBusExplorer).</span><span class="sxs-lookup"><span data-stu-id="8f553-128">To test, add a queue message via a tool like [Service Bus Explorer](https://github.com/paolosalvatori/ServiceBusExplorer).</span></span> <span data-ttu-id="8f553-129">Vous remarquerez que l’application logique se déclenche immédiatement dès que la fonction reçoit le message.</span><span class="sxs-lookup"><span data-stu-id="8f553-129">See the logic app fire immediately after the function receives the message.</span></span>

<!-- Image References -->
[1]: ./media/logic-apps-scenario-function-sb-trigger/manualtrigger.png
[2]: ./media/logic-apps-scenario-function-sb-trigger/newqueuetriggerfunction.png
