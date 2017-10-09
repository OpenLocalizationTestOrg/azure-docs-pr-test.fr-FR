---
title: "aaaUsing .NET classe bibliothèques avec des fonctions de Azure | Documents Microsoft"
description: "Découvrez comment utilisent les bibliothèques de classes .NET tooauthor pour avec des fonctions d’Azure"
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, calcul dynamique, architecture sans serveur"
ms.assetid: 9f5db0c2-a88e-4fa8-9b59-37a7096fc828
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/09/2017
ms.author: donnam
ms.openlocfilehash: 4e0fd954b554006ba1d8ecc47403a9fb1c67c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-net-class-libraries-with-azure-functions"></a>Utilisation de bibliothèques de classes .NET avec Azure Functions

En outre tooscript fichiers, les fonctions Azure prend en charge la publication d’une bibliothèque de classes en tant qu’implémentation hello pour une ou plusieurs fonctions. Nous vous recommandons d’utiliser hello [Azure fonctions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).

## <a name="prerequisites"></a>Composants requis 

Cet article a hello suivant des conditions préalables :

- [Visual Studio 2017 15.3 (préversion)](https://www.visualstudio.com/vs/preview/) Installer les charges de travail hello **ASP.NET et le développement web** et **le développement Azure**.
- [Outils d’Azure Functions pour Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=AndrewBHall-MSFT.AzureFunctionToolsforVisualStudio2017)

## <a name="functions-class-library-project"></a>Projet de bibliothèque de classes Azure Functions

À partir de Visual Studio, créez un projet Azure Functions. nouveau modèle de projet Hello crée des fichiers de hello *host.json* et *local.settings.json*. Vous pouvez [personnaliser les paramètres d’exécution d’Azure Functions dans host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json). 

fichier de Hello *local.settings.json* stocke les paramètres de l’application, les chaînes de connexion et les paramètres pour les outils de base de fonctions Azure. toolearn en savoir plus sur sa structure, consultez [Code et tester des fonctions Azure localement](functions-run-local.md#local-settings).

### <a name="functionname-attribute"></a>Attribut FunctionName

attribut de Hello [ `FunctionNameAttribute` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/FunctionNameAttribute.cs) marque une méthode comme un point d’entrée de fonction. Il doit être utilisé avec un seul déclencheur et 0 ou plusieurs liaisons d’entrée et de sortie.

### <a name="conversion-toofunctionjson"></a>Conversion toofunction.json

Lors de la génération d’un projet de fonctions d’Azure, il génère un fichier `function.json` dans le répertoire de hello correspondant au nom de fonction hello défini par `[FunctionName]`. Il spécifie le fichier d’assembly de projet toohello points et les liaisons et les déclencheurs.

Cette conversion est effectuée par le package NuGet de hello [Microsoft\.NET\.Sdk\.fonctions](http://www.nuget.org/packages/Microsoft.NET.Sdk.Functions). source de Hello n’est disponible dans le référentiel GitHub de hello [azure\-fonctions\-vs\-générer\-sdk](https://github.com/Azure/azure-functions-vs-build-sdk).

## <a name="triggers-and-bindings"></a>Déclencheurs et liaisons

Hello tableau suivant répertorie les déclencheurs hello et des liaisons qui sont disponibles dans un projet de bibliothèque de classes de fonctions d’Azure. Tous les attributs sont dans l’espace de noms hello `Microsoft.Azure.WebJobs`.

| Liaison | Attribut | Package NuGet |
|------   | ------    | ------        |
| [Déclencheur, entrée, sortie de Stockage Blob](#blob-storage) | [BlobAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | [Stockage d’objets blob] |
| [Liaison d’entrée et de sortie de Cosmos DB](#cosmos-db) | [DocumentDBAttribute] | [Microsoft.Azure.WebJobs.Extensions.DocumentDB] | 
| [Déclencheur et sortie d’Event Hubs](#event-hub) | [EventHubTriggerAttribute], [EventHubAttribute] | [Microsoft.Azure.WebJobs.ServiceBus] |
| [Entrée et sortie de fichier externe](#api-hub) | [ApiHubFileAttribute] | [Microsoft.Azure.WebJobs.Extensions.ApiHub] |
| [Déclencheur HTTP et webhook](#http) | [HttpTriggerAttribute] | [Microsoft.Azure.WebJobs.Extensions.Http] |
| [Entrée et sortie de Mobile Apps](#mobile-apps) | [MobileTableAttribute] | [Microsoft.Azure.WebJobs.Extensions.MobileApps] | 
| [Sortie de Notification Hubs](#nh) | [NotificationHubAttribute] | [Microsoft.Azure.WebJobs.Extensions.NotificationHubs] | 
| [Déclencheur et sortie de Stockage File d’attente](#queue) | [QueueAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | 
| [Sortie de SendGrid](#sendgrid) | [SendGridAttribute] | [Microsoft.Azure.WebJobs.Extensions.SendGrid] | 
| [Déclencheur et sortie de Service Bus](#service-bus) | [ServiceBusAttribute], [ServiceBusAccountAttribute] | [Microsoft.Azure.WebJobs.ServiceBus]
| [Entrée et sortie de Stockage Table](#table) | [TableAttribute], [StorageAccountAttribute] | [Microsoft.Azure.WebJobs] | 
| [Déclencheur de minuteur](#timer) | [TimerTriggerAttribute] | [Microsoft.Azure.WebJobs.Extensions] | 
| [Sortie de Twilio](#twilio) | [TwilioSmsAttribute] | [Microsoft.Azure.WebJobs.Extensions.Twilio] | 

<a name="blob-storage"></a>

### <a name="blob-storage-trigger-input-and-output-bindings"></a>Liaisons de déclencheur, d’entrée, de sortie de Stockage Blob

Azure Functions prend en charge les liaisons de déclencheur, d’entrée et de sortie pour Stockage Blob Azure. Pour plus d’informations sur les expressions et métadonnées de liaison, voir [Liaisons de Stockage Blob Azure Functions](functions-bindings-storage-blob.md).

Un déclencheur d’objet blob est défini avec hello `[BlobTrigger]` attribut. Vous pouvez utiliser les attributs hello `[StorageAccount]` compte de stockage hello toodefine qui est utilisé par une fonction entière ou une classe.

```csharp
[StorageAccount("AzureWebJobsStorage")]
[FunctionName("BlobTriggerCSharp")]        
public static void Run([BlobTrigger("samples-workitems/{name}")] Stream myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

Objet BLOB d’entrée et sortie sont définies à l’aide de hello `[Blob]` d’attribut, ainsi que par un `FileAccess` paramètre indiquant de lecture ou d’écriture. Hello suivant montre comment utiliser un déclencheur de l’objet blob et de liaison de sortie d’objets blob.

```csharp
[FunctionName("ResizeImage")]
[StorageAccount("AzureWebJobsStorage")]
public static void Run(
    [BlobTrigger("sample-images/{name}")] Stream image, 
    [Blob("sample-images-sm/{name}", FileAccess.Write)] Stream imageSmall, 
    [Blob("sample-images-md/{name}", FileAccess.Write)] Stream imageMedium)
{
    var imageBuilder = ImageResizer.ImageBuilder.Current;
    var size = imageDimensionsTable[ImageSize.Small];

    imageBuilder.Build(image, imageSmall,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);

    image.Position = 0;
    size = imageDimensionsTable[ImageSize.Medium];

    imageBuilder.Build(image, imageMedium,
        new ResizeSettings(size.Item1, size.Item2, FitMode.Max, null), false);
}

public enum ImageSize { ExtraSmall, Small, Medium }

private static Dictionary<ImageSize, (int, int)> imageDimensionsTable = new Dictionary<ImageSize, (int, int)>() {
    { ImageSize.ExtraSmall, (320, 200) },
    { ImageSize.Small,      (640, 400) },
    { ImageSize.Medium,     (800, 600) }
};
```        

<a name="cosmos-db"></a>

### <a name="cosmos-db-input-and-output-bindings"></a>Liaisons d’entrée et de sortie Cosmos DB

Azure Functions prend en charge des liaisons d’entrée et de sortie pour Cosmos DB. toolearn savoir plus sur les fonctions hello de liaison de base de données Cosmos hello, consultez [les liaisons de base de données Azure fonctions Cosmos](functions-bindings-documentdb.md).

toobind tooa Cosmos DB document, utilisez les attributs hello `[DocumentDB]` dans le package NuGet de hello [Microsoft.Azure.WebJobs.Extensions.DocumentDB]. Bonjour à l’exemple suivant présente un déclencheur de la file d’attente et une API DocumentDB liaison de sortie :

```csharp
[FunctionName("QueueToDocDB")]        
public static void Run(
    [QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, 
    [DocumentDB("ToDoList", "Items", ConnectionStringSetting = "DocDBConnection")] out dynamic document)
{
    document = new { Text = myQueueItem, id = Guid.NewGuid() };
}

```

<a name="event-hub"></a>

### <a name="event-hubs-trigger-and-output"></a>Déclencheur et sortie d’Event Hubs

Azure Functions prend en charge des liaisons de déclencheur et de sortie pour des Event Hubs. Pour plus d’informations, voir [Liaisons d’Event Hub Azure Functions](functions-bindings-event-hubs.md).

types de Hello `[Microsoft.Azure.WebJobs.ServiceBus.EventHubTriggerAttribute]` et `[Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute]` sont définis dans le package NuGet de hello [Microsoft.Azure.WebJobs.ServiceBus]. 

Hello exemple suivant utilise un déclencheur de concentrateur d’événements :

```csharp
[FunctionName("EventHubTriggerCSharp")]
public static void Run([EventHubTrigger("samples-workitems", Connection = "EventHubConnection")] string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

Hello exemple suivant présente un concentrateur d’événements de sortie, à l’aide de la valeur de retour de méthode hello en tant que sortie de hello :

```csharp
[FunctionName("EventHubOutput")]
[return: EventHub("outputEventHubMessage", Connection = "EventHubConnection")]
public static string Run([TimerTrigger("0 */5 * * * *")] TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    return $"{DateTime.Now}";
}
```

<a name="api-hub"></a>

### <a name="external-file-input-and-output"></a>Entrée et sortie de fichier externe

Azure Functions prend en charge les liaisons de déclencheur, d’entrée et de sortie pour des fichiers externes, tels que Google Drive, Dropbox et OneDrive. toolearn, voir [liaisons du fichier externe de fonctions Azure](functions-bindings-external-file.md). attributs de Hello `[ExternalFileTrigger]` et `[ExternalFile]` sont définis dans le package NuGet de hello [Microsoft.Azure.WebJobs.Extensions.ApiHub].

Hello exemple c# suivant illustre l’entrée et la sortie de liaison d’un fichier externe. copies de code Hello hello le fichier de sortie de fichier d’entrée toohello.

```csharp
[StorageAccount("MyStorageConnection")]
[FunctionName("ExternalFile")]
[return: ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}-Copy", FileAccess.Write)]
public static string Run([QueueTrigger("myqueue-items")] string myQueueItem, 
    [ApiHubFile("MyFileConnection", "samples-workitems/{queueTrigger}", FileAccess.Read)] string myInputFile, 
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    return myInputFile;
}
```

<a name="http"></a>

### <a name="http-and-webhooks"></a>HTTP et webhooks

Hello d’utilisation `HttpTrigger` déclencheur de toodefine HTTP attribut ou webhook. Cet attribut est défini dans le package NuGet de hello [Microsoft.Azure.WebJobs.Extensions.Http]. Vous pouvez personnaliser le niveau d’autorisation de hello, type de webhook, itinéraire et méthodes. Hello exemple suivant définit un déclencheur HTTP avec l’authentification anonyme et _genericJson_ webhook type.

```csharp
[FunctionName("HttpTriggerCSharp")]
public static HttpResponseMessage Run([HttpTrigger(AuthorizationLevel.Anonymous, WebHookType = "genericJson")] HttpRequestMessage req)
{
    return req.CreateResponse(HttpStatusCode.OK);
}
```

<a name="mobile-apps"></a>

### <a name="mobile-apps-input-and-output"></a>Entrée et sortie de Mobile Apps

Azure Functions prend en charge des liaisons d’entrée et de sortie pour Mobile Apps. toolearn, voir [liaisons des applications mobiles de fonctions Azure](functions-bindings-mobile-apps.md). attribut de Hello `[MobileTable]` est défini dans le package NuGet de hello [Microsoft.Azure.WebJobs.Extensions.MobileApps].

exemple Hello illustre une applications mobiles liaison de sortie :

```csharp
[FunctionName("MobileAppsOutput")]        
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem, TraceWriter log)
{
    return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```

<a name="nh"></a>

### <a name="notification-hubs-output"></a>Sortie de Notification Hubs

Azure Functions prend en charge une liaison de sortie pour Notification Hubs. toolearn, voir [liaison de sortie du Hub de Notification de fonctions Azure](functions-bindings-notification-hubs.md). attribut de Hello `[NotificationHub]` est défini dans le package NuGet de hello [Microsoft.Azure.WebJobs.Extensions.NotificationHubs].

<a name="queue"></a>

### <a name="queue-storage-trigger-and-output"></a>Déclencheur et sortie de Stockage File d’attente

Azure Functions prend en charge les liaisons de déclencheur et de sortie pour les files d’attente Azure. Pour plus d’informations, voir [Liaisons de Stockage File d’attente Azure Functions](functions-bindings-storage-queue.md).

Hello suivant montre la fonction de hello toouse type de retour avec une sortie de la file d’attente de liaison, à l’aide de hello `[Queue]` attribut. toodefine un déclencheur de la file d’attente, utilisez hello `[QueueTrigger]` attribut.

```csharp
[StorageAccount("AzureWebJobsStorage")]
public static class QueueFunctions
{
    // HTTP trigger with queue output binding
    [FunctionName("QueueOutput")]
    [return: Queue("myqueue-items")]
    public static string QueueOutput([HttpTrigger] dynamic input,  TraceWriter log)
    {
        log.Info($"C# function processed: {input.Text}");
        return input.Text;
    }

    // Queue trigger
    [FunctionName("QueueTrigger")]
    [StorageAccount("AzureWebJobsStorage")]
    public static void QueueTrigger([QueueTrigger("myqueue-items")] string myQueueItem, TraceWriter log)
    {
        log.Info($"C# function processed: {myQueueItem}");
    }
}

```

<a name="sendgrid"></a>

### <a name="sendgrid-output"></a>Sortie de SendGrid

Azure Functions prend en charge une liaison de sortie SendGrid pour l’envoi de courrier par programmation. toolearn, voir [SendGrid de fonctions Azure liaisons](functions-bindings-sendgrid.md).

attribut de Hello `[SendGrid]` est défini dans le package NuGet de hello [Microsoft.Azure.WebJobs.Extensions.SendGrid].

Hello Voici un exemple d’utilisation d’un déclencheur de la file d’attente Service Bus et un à l’aide de la liaison pour la sortie SendGrid `SendGridMessage`:

```csharp
[FunctionName("SendEmail")]
public static void Run(
    [ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] OutgoingEmail email,
    [SendGrid] out SendGridMessage message)
{
    message = new SendGridMessage();
    message.AddTo(email.To);
    message.AddContent("text/html", email.Body);
    message.SetFrom(new EmailAddress(email.From));
    message.SetSubject(email.Subject);
}

public class OutgoingEmail
{
    public string too{ get; set; }
    public string From { get; set; }
    public string Subject { get; set; }
    public string Body { get; set; }
}
```

<a name="service-bus"></a>

### <a name="service-bus-trigger-and-output"></a>Déclencheur et sortie de Service Bus

Azure Functions prend en charge les liaisons de déclencheur et de sortie pour les files d’attente et les rubriques Service Bus. Pour plus d’informations sur la configuration des liaisons, voir [Liaisons Service Bus Azure Functions](functions-bindings-service-bus.md).

attributs de Hello `[ServiceBusTrigger]` et `[ServiceBus]` sont définis dans le package NuGet de hello [Microsoft.Azure.WebJobs.ServiceBus]. 

Hello Voici un exemple d’un déclencheur de la file d’attente Service Bus :

```csharp
[FunctionName("ServiceBusQueueTriggerCSharp")]                    
public static void Run([ServiceBusTrigger("myqueue", AccessRights.Manage, Connection = "ServiceBusConnection")] string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

Hello Voici un exemple d’une sortie de Bus de Service de liaison, à l’aide du type de retour de méthode hello en tant que sortie de hello :

```csharp
[FunctionName("ServiceBusOutput")]
[return: ServiceBus("myqueue", Connection = "ServiceBusConnection")]
public static string ServiceBusOutput([HttpTrigger] dynamic input, TraceWriter log)
{
    log.Info($"C# function processed: {input.Text}");
    return input.Text;
}
```        

<a name="table"></a>

### <a name="table-storage-input-and-output"></a>Entrée et sortie de Stockage Table

Azure Functions prend en charge les liaisons d’entrée et de sortie pour Stockage de table Azure. toolearn, voir [liaisons de stockage de Table de fonctions Azure](functions-bindings-storage-table.md).

Hello exemple suivant est une classe avec deux fonctions, qui montre la sortie de stockage de table et des liaisons d’entrée. 

```csharp
[StorageAccount("AzureWebJobsStorage")]
public class TableStorage
{
    public class MyPoco
    {
        public string PartitionKey { get; set; }
        public string RowKey { get; set; }
        public string Text { get; set; }
    }

    [FunctionName("TableOutput")]
    [return: Table("MyTable")]
    public static MyPoco TableOutput([HttpTrigger] dynamic input, TraceWriter log)
    {
        log.Info($"C# http trigger function processed: {input.Text}");
        return new MyPoco { PartitionKey = "Http", RowKey = Guid.NewGuid().ToString(), Text = input.Text };
    }

    // use hello metadata parameter "queueTrigger" toobind hello queue payload
    [FunctionName("TableInput")]
    public static void TableInput([QueueTrigger("table-items")] string input, [Table("MyTable", "Http", "{queueTrigger}")] MyPoco poco, TraceWriter log)
    {
        log.Info($"C# function processed: {poco.Text}");
    }
}

```

<a name="timer"></a>

### <a name="timer-trigger"></a>Déclencheur de minuteur

Azure Functions offre une liaison de déclencheur de minuteur qui vous permet d’exécuter votre code de fonction selon une planification définie. toolearn savoir plus sur les fonctions hello de liaison de hello, consultez [planifier l’exécution de code avec les fonctions Azure](functions-bindings-timer.md).

Sur le plan de la consommation de hello, vous pouvez définir des planifications avec un [expression CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression). Si vous utilisez un plan App Service, vous pouvez également utiliser une chaîne TimeSpan. 

Bonjour à l’exemple suivant définit un déclencheur du minuteur qui s’exécute toutes les 5 minutes :

```csharp
[FunctionName("TimerTriggerCSharp")]
public static void Run([TimerTrigger("0 */5 * * * *")]TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
}
```

<a name="twilio"></a>

### <a name="twilio-output"></a>Sortie de Twilio

Prend en charge des fonctions Azure Twilio sortie liaisons tooenable vos fonctions toosend les messages SMS. toolearn, voir [liaison de sortie d’envoi de SMS à partir des fonctions d’Azure à l’aide de hello Twilio](functions-bindings-twilio.md). 

attribut de Hello `[TwilioSms]` est défini dans le package de hello [Microsoft.Azure.WebJobs.Extensions.Twilio].

Hello exemple c# suivant utilise une file d’attente déclencheur et un Twilio de liaison de sortie :

```csharp
[FunctionName("QueueTwilio")]
[return: TwilioSms(AccountSidSetting = "TwilioAccountSid", AuthTokenSetting = "TwilioAuthToken", From = "+1425XXXXXXX" )]
public static SMSMessage Run([QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] JObject order, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {order}");

    var message = new SMSMessage()
    {
        Body = $"Hello {order["name"]}, thanks for your order!",
        too= order["mobileNumber"].ToString()
    };

    return message;
}
```

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’utilisation d’Azure Functions dans un script C#, voir la référence du développeur de script [Azure Functions C\#](functions-reference-csharp.md).

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]


<!-- NuGet packages --> 
[Microsoft.Azure.WebJobs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.DocumentDB]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.MobileApps]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.NotificationHubs]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.NotificationHubs/1.1.0-beta1
[Microsoft.Azure.WebJobs.ServiceBus]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.ServiceBus/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.SendGrid]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.SendGrid/2.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions.Http]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Http/1.0.0-beta1
[Microsoft.Azure.WebJobs.Extensions.BotFramework]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.BotFramework/1.0.15-beta
[Microsoft.Azure.WebJobs.Extensions.ApiHub]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ApiHub/1.0.0-beta4
[Microsoft.Azure.WebJobs.Extensions.Twilio]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Twilio/1.1.0-beta1
[Microsoft.Azure.WebJobs.Extensions]: http://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions/2.1.0-beta1


<!-- Links toosource --> 
[DocumentDBAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs
[EventHubAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs
[EventHubTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubTriggerAttribute.cs
[MobileTableAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs
[NotificationHubAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs 
[ServiceBusAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs
[ServiceBusAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs
[QueueAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs
[StorageAccountAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs
[BlobAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs
[TableAttribute]: https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs
[TwilioSmsAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs
[SendGridAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.SendGrid/SendGridAttribute.cs
[HttpTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/dev/src/WebJobs.Extensions.Http/HttpTriggerAttribute.cs
[ApiHubFileAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.ApiHub/ApiHubFileAttribute.cs
[TimerTriggerAttribute]: https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs
