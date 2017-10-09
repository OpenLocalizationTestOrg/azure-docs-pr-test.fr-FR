---
title: liaison de Hub de Notification de fonctions aaaAzure | Documents Microsoft
description: "Comprendre la liaison du Hub de Notification Azure toouse dans les fonctions d’Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "azure functions, fonctions, traitement des événements, calcul dynamique, architecture sans serveur"
ms.assetid: 0ff0c949-20bf-430b-8dd5-d72b7b6ee6f7
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/27/2016
ms.author: glenga
ms.openlocfilehash: d192424a8ec701d02f8bcb4aa4c1d189b20537a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-notification-hub-output-binding"></a>Liaison de sortie Notification Hubs Azure Functions
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Cet article explique comment les liaisons de Hub de Notification Azure tooconfigure et de code dans les fonctions d’Azure. 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Vos fonctions peuvent envoyer des notifications Push à l’aide d’un Azure Notification Hub configuré avec quelques lignes de code. Toutefois, hello Hub de Notification Azure doit être configuré pour hello souhaité toouse plateforme Notifications Services (PNS). Pour plus d’informations sur la configuration d’un concentrateur de Notification Azure et de développement d’applications clientes qui inscrivent tooreceive notifications, consultez [prise en main de concentrateurs de Notification](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) et cliquez sur la plate-forme du client cible au hello Retour au début.

vous envoyez des notifications de Hello peuvent être notifications natives ou des notifications de modèle. Notifications natives ciblent une plateforme de notification spécifique tel que configuré dans hello `platform` liaison de sortie de la propriété de hello. Une notification de modèle peut être utilisé tootarget plusieurs plateformes.   

## <a name="notification-hub-output-binding-properties"></a>Propriété de liaison de sortie du hub de notification
fichier de function.json Hello fournit hello propriétés suivantes :

* `name`: Nom variable utilisée dans le code de la fonction hello message de notification hub.
* `type`: doit être défini trop*« notificationHub »*.
* `tagExpression`: Expressions de balise autorisent toospecify que les notifications remises ensemble tooa de périphériques qui ont enregistré les notifications tooreceive qui correspond à l’expression de balise hello.  Pour plus d’informations, voir [Routage et expressions de balise](../notification-hubs/notification-hubs-tags-segment-push-message.md).
* `hubName`: Nom de ressource de concentrateur de notification hello Bonjour portail Azure.
* `connection`: Cette chaîne de connexion doit être un **paramètre d’Application** chaîne de connexion définie toohello *DefaultFullSharedAccessSignature* valeur votre hub de notification.
* `direction`: doit être défini trop*« out »*. 
* `platform`: propriété de plateforme hello indique plateforme de notification hello votre cible de notification. Doit être une des valeurs suivantes de hello :
  * Par défaut, si la propriété de plateforme hello est omise de la sortie hello de liaison, les notifications de modèle peuvent être utilisé tootarget n’importe quelle plateforme configurée sur hello Hub de Notification Azure. Pour plus d’informations sur l’utilisation de modèles en général toosend cross-platform des notifications avec un Hub de Notification Azure, consultez [modèles](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).
  * `apns` : Apple Push Notification Service (APNS) Pour plus d’informations sur la configuration de concentrateur de notification hello pour APNS et de réception des notifications de hello dans une application cliente, consultez [envoi tooiOS de notifications push avec Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md) 
  * `adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging). Pour plus d’informations sur la configuration du hub de notification hello pour ADM et réception des notifications de hello dans une application Kindle, consultez [prise en main de concentrateurs de Notification pour les applications Kindle](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md) 
  * `gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/). Messagerie Cloud firebase, qui est la nouvelle version de hello de GCM, est également pris en charge. Pour plus d’informations sur la configuration du hub de notification hello pour GCM/FCM et réception des notifications de hello dans une application cliente Android, consultez [envoi tooAndroid de notifications push avec Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)
  * `wns` : [services de notification push Windows](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) ciblant les plateformes Windows. Windows Phone 8.1 et les versions ultérieures sont est également prises en charge par WNS. Pour plus d’informations sur la configuration du hub de notification hello pour WNS et réception des notifications de hello dans une application de plateforme Windows universelle (UWP), consultez [mise en route avec Notification Hubs pour les applications Windows universelles plateforme](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)
  * `mpns` : [service de notifications Push Microsoft](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx). Cette plateforme prend en charge Windows Phone 8 et les plateformes antérieures de Windows Phone. Pour plus d’informations sur la configuration du hub de notification hello pour MPNS et réception des notifications de hello dans une application Windows Phone, consultez [envoi des notifications push avec Azure Notification Hubs sur Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)

Exemple de fichier function.json :

```json
{
  "bindings": [
    {
      "name": "notification",
      "type": "notificationHub",
      "tagExpression": "",
      "hubName": "my-notification-hub",
      "connection": "MyHubConnectionString",
      "platform": "gcm",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

## <a name="notification-hub-connection-string-setup"></a>Configuration de la chaîne de connexion du hub de notification
liaison de sortie toouse un concentrateur de Notification, vous devez configurer la chaîne de connexion hello pour le hub de hello. Cela peut être effectuée sur hello *intégrer* onglet en sélectionnant votre concentrateur de notification ou en créer un nouveau. 

Vous pouvez également ajouter manuellement une chaîne de connexion pour un concentrateur existant en ajoutant une chaîne de connexion pour hello *DefaultFullSharedAccessSignature* hub de notification tooyour. Cette chaîne de connexion fournit des messages de notification toosend autorisation votre accès à la fonction. Hello *DefaultFullSharedAccessSignature* valeur de chaîne de connexion est accessible à partir de hello **clés** bouton dans le panneau principal de hello de votre ressource de concentrateur de notification Bonjour portail Azure. toomanually ajouter une chaîne de connexion pour votre concentrateur, hello utilisation comme suit : 

1. Sur hello **fonction application** Panneau de hello portail Azure, cliquez sur **paramètres de fonction de l’application > Aller paramètres du Service tooApp**.
2. Bonjour **paramètres** panneau, cliquez sur **paramètres de l’Application**.
3. Faites défiler vers le bas toohello **paramètres de l’application** section et ajouter une entrée nommée pour *DefaultFullSharedAccessSignature* valeur votre hub de notification.
4. Faire référence à votre application, nom de chaîne du paramètre Bonjour liaisons de sortie. Similaire trop**MyHubConnectionString** utilisé dans l’exemple hello ci-dessus.

## <a name="apns-native-notifications-with-c-queue-triggers"></a>Notifications natives APNS avec déclencheurs de file d’attente C#
Cet exemple montre comment les types de toouse défini dans hello [Microsoft Azure Notification Hubs bibliothèque](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend une notification APNS native. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello JSON format for a native APNS notification is ...
    // { "aps": { "alert": "notification message" }}  

    log.Info($"Sending APNS notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string apnsNotificationPayload = "{\"aps\": {\"alert\": \"A new user wants toobe added (" + 
                                        user.name + ")\" }}";
    log.Info($"{apnsNotificationPayload}");
    await notification.AddAsync(new AppleNotification(apnsNotificationPayload));        
}
```

## <a name="gcm-native-notifications-with-c-queue-triggers"></a>Notifications natives GCM avec déclencheurs de file d’attente C#
Cet exemple montre comment les types de toouse défini dans hello [Microsoft Azure Notification Hubs bibliothèque](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend une notification GCM native. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello JSON format for a native GCM notification is ...
    // { "data": { "message": "notification message" }}  

    log.Info($"Sending GCM notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string gcmNotificationPayload = "{\"data\": {\"message\": \"A new user wants toobe added (" + 
                                        user.name + ")\" }}";
    log.Info($"{gcmNotificationPayload}");
    await notification.AddAsync(new GcmNotification(gcmNotificationPayload));        
}
```

## <a name="wns-native-notifications-with-c-queue-triggers"></a>Notifications natives WNS avec déclencheurs de file d’attente C#
Cet exemple montre comment les types de toouse défini dans hello [Microsoft Azure Notification Hubs bibliothèque](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend un WNS native de notification toast. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello XML format for a native WNS toast notification is ...
    // <?xml version="1.0" encoding="utf-8"?>
    // <toast>
    //      <visual>
    //     <binding template="ToastText01">
    //       <text id="1">notification message</text>
    //     </binding>
    //   </visual>
    // </toast>

    log.Info($"Sending WNS toast notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string wnsNotificationPayload = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                                    "<toast><visual><binding template=\"ToastText01\">" +
                                        "<text id=\"1\">" + 
                                            "A new user wants toobe added (" + user.name + ")" + 
                                        "</text>" +
                                    "</binding></visual></toast>";

    log.Info($"{wnsNotificationPayload}");
    await notification.AddAsync(new WindowsNotification(wnsNotificationPayload));        
}
```

## <a name="template-example-for-nodejs-timer-triggers"></a>Exemple de modèle pour les déclencheurs de minuteur Node.js
Cet exemple envoie une notification pour une [inscription de modèles](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) contenant `location` et `message`.

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    if(myTimer.isPastDue)
    {
        context.log('Node.js is running late!');
    }
    context.log('Node.js timer trigger function ran!', timeStamp);  
    context.bindings.notification = {
        location: "Redmond",
        message: "Hello from Node!"
    };
    context.done();
};
```

## <a name="template-example-for-f-timer-triggers"></a>Exemple de modèle pour les déclencheurs de minuteur F#
Cet exemple envoie une notification pour une [inscription de modèles](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) contenant `location` et `message`.

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a>Exemple de modèle utilisant un paramètre de sortie
Cet exemple envoie une notification un [inscription de modèle](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) qui contient un `message` espace réservé dans le modèle de hello.

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static void Run(string myQueueItem,  out IDictionary<string, string> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = GetTemplateProperties(myQueueItem);
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return templateProperties;
}
```

## <a name="template-example-with-asynchronous-function"></a>Exemple de modèle avec fonction asynchrone
Si vous utilisez du code asynchrone, les paramètres de sortie ne sont pas autorisés. Dans ce cas utiliser `IAsyncCollector` tooreturn votre notification de modèle. Hello de code suivant est un exemple asynchrone de code hello ci-dessus. 

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static async Task Run(string myQueueItem, IAsyncCollector<IDictionary<string,string>> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    log.Info($"Sending Template Notification tooNotification Hub");
    await notification.AddAsync(GetTemplateProperties(myQueueItem));    
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["user"] = "A new user wants toobe added : " + message;
    return templateProperties;
}
```

## <a name="template-example-using-json"></a>Exemple de modèle utilisant JSON
Cet exemple envoie une notification un [inscription de modèle](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) qui contient un `message` espace réservé dans le modèle hello à l’aide d’une chaîne JSON valide.

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a>Exemple de modèle utilisant des types de bibliothèques de Notification Hubs
Cet exemple montre comment les types de toouse défini dans hello [Microsoft Azure Notification Hubs bibliothèque](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/). 

```cs
#r "Microsoft.Azure.NotificationHubs"

using System;
using System.Threading.Tasks;
using Microsoft.Azure.NotificationHubs;

public static void Run(string myQueueItem,  out Notification notification, TraceWriter log)
{
   log.Info($"C# Queue trigger function processed: {myQueueItem}");
   notification = GetTemplateNotification(myQueueItem);
}

private static TemplateNotification GetTemplateNotification(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return new TemplateNotification(templateProperties);
}
```

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

