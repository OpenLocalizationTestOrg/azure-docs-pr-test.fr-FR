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
# <a name="azure-functions-notification-hub-output-binding"></a><span data-ttu-id="fca68-104">Liaison de sortie Notification Hubs Azure Functions</span><span class="sxs-lookup"><span data-stu-id="fca68-104">Azure Functions Notification Hub output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="fca68-105">Cet article explique comment les liaisons de Hub de Notification Azure tooconfigure et de code dans les fonctions d’Azure.</span><span class="sxs-lookup"><span data-stu-id="fca68-105">This article explains how tooconfigure and code Azure Notification Hub bindings in Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="fca68-106">Vos fonctions peuvent envoyer des notifications Push à l’aide d’un Azure Notification Hub configuré avec quelques lignes de code.</span><span class="sxs-lookup"><span data-stu-id="fca68-106">Your functions can send push notifications using a configured Azure Notification Hub with a few lines of code.</span></span> <span data-ttu-id="fca68-107">Toutefois, hello Hub de Notification Azure doit être configuré pour hello souhaité toouse plateforme Notifications Services (PNS).</span><span class="sxs-lookup"><span data-stu-id="fca68-107">However, hello Azure Notification Hub must be configured for hello Platform Notifications Services (PNS) you want toouse.</span></span> <span data-ttu-id="fca68-108">Pour plus d’informations sur la configuration d’un concentrateur de Notification Azure et de développement d’applications clientes qui inscrivent tooreceive notifications, consultez [prise en main de concentrateurs de Notification](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) et cliquez sur la plate-forme du client cible au hello Retour au début.</span><span class="sxs-lookup"><span data-stu-id="fca68-108">For more information on configuring an Azure Notification Hub and developing a client applications that register tooreceive notifications, see [Getting started with Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) and click your target client platform at hello top.</span></span>

<span data-ttu-id="fca68-109">vous envoyez des notifications de Hello peuvent être notifications natives ou des notifications de modèle.</span><span class="sxs-lookup"><span data-stu-id="fca68-109">hello notifications you send can be native notifications or template notifications.</span></span> <span data-ttu-id="fca68-110">Notifications natives ciblent une plateforme de notification spécifique tel que configuré dans hello `platform` liaison de sortie de la propriété de hello.</span><span class="sxs-lookup"><span data-stu-id="fca68-110">Native notifications target a specific notification platform as configured in hello `platform` property of hello output binding.</span></span> <span data-ttu-id="fca68-111">Une notification de modèle peut être utilisé tootarget plusieurs plateformes.</span><span class="sxs-lookup"><span data-stu-id="fca68-111">A template notification can be used tootarget multiple platforms.</span></span>   

## <a name="notification-hub-output-binding-properties"></a><span data-ttu-id="fca68-112">Propriété de liaison de sortie du hub de notification</span><span class="sxs-lookup"><span data-stu-id="fca68-112">Notification hub output binding properties</span></span>
<span data-ttu-id="fca68-113">fichier de function.json Hello fournit hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="fca68-113">hello function.json file provides hello following properties:</span></span>

* <span data-ttu-id="fca68-114">`name`: Nom variable utilisée dans le code de la fonction hello message de notification hub.</span><span class="sxs-lookup"><span data-stu-id="fca68-114">`name` : Variable name used in function code for hello notification hub message.</span></span>
* <span data-ttu-id="fca68-115">`type`: doit être défini trop*« notificationHub »*.</span><span class="sxs-lookup"><span data-stu-id="fca68-115">`type` : must be set too*"notificationHub"*.</span></span>
* <span data-ttu-id="fca68-116">`tagExpression`: Expressions de balise autorisent toospecify que les notifications remises ensemble tooa de périphériques qui ont enregistré les notifications tooreceive qui correspond à l’expression de balise hello.</span><span class="sxs-lookup"><span data-stu-id="fca68-116">`tagExpression` : Tag expressions allow you toospecify that notifications be delivered tooa set of devices who have registered tooreceive notifications that match hello tag expression.</span></span>  <span data-ttu-id="fca68-117">Pour plus d’informations, voir [Routage et expressions de balise](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="fca68-117">For more information, see [Routing and tag expressions](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span></span>
* <span data-ttu-id="fca68-118">`hubName`: Nom de ressource de concentrateur de notification hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fca68-118">`hubName` : Name of hello notification hub resource in hello Azure portal.</span></span>
* <span data-ttu-id="fca68-119">`connection`: Cette chaîne de connexion doit être un **paramètre d’Application** chaîne de connexion définie toohello *DefaultFullSharedAccessSignature* valeur votre hub de notification.</span><span class="sxs-lookup"><span data-stu-id="fca68-119">`connection` : This connection string must be an **Application Setting** connection string set toohello *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
* <span data-ttu-id="fca68-120">`direction`: doit être défini trop*« out »*.</span><span class="sxs-lookup"><span data-stu-id="fca68-120">`direction` : must be set too*"out"*.</span></span> 
* <span data-ttu-id="fca68-121">`platform`: propriété de plateforme hello indique plateforme de notification hello votre cible de notification.</span><span class="sxs-lookup"><span data-stu-id="fca68-121">`platform` : hello platform property indicates hello notification platform your notification targets.</span></span> <span data-ttu-id="fca68-122">Doit être une des valeurs suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="fca68-122">Must be one of hello following values:</span></span>
  * <span data-ttu-id="fca68-123">Par défaut, si la propriété de plateforme hello est omise de la sortie hello de liaison, les notifications de modèle peuvent être utilisé tootarget n’importe quelle plateforme configurée sur hello Hub de Notification Azure.</span><span class="sxs-lookup"><span data-stu-id="fca68-123">By default, if hello platform property is omitted from hello output binding, template notifications can be used tootarget any platform configured on hello Azure Notification Hub.</span></span> <span data-ttu-id="fca68-124">Pour plus d’informations sur l’utilisation de modèles en général toosend cross-platform des notifications avec un Hub de Notification Azure, consultez [modèles](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="fca68-124">For more information on using templates in general toosend cross platform notifications with an Azure Notification Hub, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>
  * <span data-ttu-id="fca68-125">`apns` : Apple Push Notification Service (APNS)</span><span class="sxs-lookup"><span data-stu-id="fca68-125">`apns` : Apple Push Notification Service.</span></span> <span data-ttu-id="fca68-126">Pour plus d’informations sur la configuration de concentrateur de notification hello pour APNS et de réception des notifications de hello dans une application cliente, consultez [envoi tooiOS de notifications push avec Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="fca68-126">For more information on configuring hello notification hub for APNS and receiving hello notification in a client app, see [Sending push notifications tooiOS with Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span></span> 
  * <span data-ttu-id="fca68-127">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span><span class="sxs-lookup"><span data-stu-id="fca68-127">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span></span> <span data-ttu-id="fca68-128">Pour plus d’informations sur la configuration du hub de notification hello pour ADM et réception des notifications de hello dans une application Kindle, consultez [prise en main de concentrateurs de Notification pour les applications Kindle](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="fca68-128">For more information on configuring hello notification hub for ADM and receiving hello notification in a Kindle app, see [Getting Started with Notification Hubs for Kindle apps](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span></span> 
  * <span data-ttu-id="fca68-129">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="fca68-129">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span></span> <span data-ttu-id="fca68-130">Messagerie Cloud firebase, qui est la nouvelle version de hello de GCM, est également pris en charge.</span><span class="sxs-lookup"><span data-stu-id="fca68-130">Firebase Cloud Messaging, which is hello new version of GCM, is also supported.</span></span> <span data-ttu-id="fca68-131">Pour plus d’informations sur la configuration du hub de notification hello pour GCM/FCM et réception des notifications de hello dans une application cliente Android, consultez [envoi tooAndroid de notifications push avec Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="fca68-131">For more information on configuring hello notification hub for GCM/FCM and receiving hello notification in an Android client app, see [Sending push notifications tooAndroid with Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span></span>
  * <span data-ttu-id="fca68-132">`wns` : [services de notification push Windows](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) ciblant les plateformes Windows.</span><span class="sxs-lookup"><span data-stu-id="fca68-132">`wns` : [Windows Push Notification Services](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) targeting Windows platforms.</span></span> <span data-ttu-id="fca68-133">Windows Phone 8.1 et les versions ultérieures sont est également prises en charge par WNS.</span><span class="sxs-lookup"><span data-stu-id="fca68-133">Windows Phone 8.1 and later is also supported by WNS.</span></span> <span data-ttu-id="fca68-134">Pour plus d’informations sur la configuration du hub de notification hello pour WNS et réception des notifications de hello dans une application de plateforme Windows universelle (UWP), consultez [mise en route avec Notification Hubs pour les applications Windows universelles plateforme](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="fca68-134">For more information on configuring hello notification hub for WNS and receiving hello notification in a Universal Windows Platform (UWP) app, see [Getting started with Notification Hubs for Windows Universal Platform Apps](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span></span>
  * <span data-ttu-id="fca68-135">`mpns` : [service de notifications Push Microsoft](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span><span class="sxs-lookup"><span data-stu-id="fca68-135">`mpns` : [Microsoft Push Notification Service](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span></span> <span data-ttu-id="fca68-136">Cette plateforme prend en charge Windows Phone 8 et les plateformes antérieures de Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="fca68-136">This platform supports Windows Phone 8 and earlier Windows Phone platforms.</span></span> <span data-ttu-id="fca68-137">Pour plus d’informations sur la configuration du hub de notification hello pour MPNS et réception des notifications de hello dans une application Windows Phone, consultez [envoi des notifications push avec Azure Notification Hubs sur Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span><span class="sxs-lookup"><span data-stu-id="fca68-137">For more information on configuring hello notification hub for MPNS and receiving hello notification in a Windows Phone app, see [Sending push notifications with Azure Notification Hubs on Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span></span>

<span data-ttu-id="fca68-138">Exemple de fichier function.json :</span><span class="sxs-lookup"><span data-stu-id="fca68-138">Example function.json:</span></span>

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

## <a name="notification-hub-connection-string-setup"></a><span data-ttu-id="fca68-139">Configuration de la chaîne de connexion du hub de notification</span><span class="sxs-lookup"><span data-stu-id="fca68-139">Notification hub connection string setup</span></span>
<span data-ttu-id="fca68-140">liaison de sortie toouse un concentrateur de Notification, vous devez configurer la chaîne de connexion hello pour le hub de hello.</span><span class="sxs-lookup"><span data-stu-id="fca68-140">toouse a Notification hub output binding, you must configure hello connection string for hello hub.</span></span> <span data-ttu-id="fca68-141">Cela peut être effectuée sur hello *intégrer* onglet en sélectionnant votre concentrateur de notification ou en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="fca68-141">This can be done on hello *Integrate* tab by selecting your notification hub or creating a new one.</span></span> 

<span data-ttu-id="fca68-142">Vous pouvez également ajouter manuellement une chaîne de connexion pour un concentrateur existant en ajoutant une chaîne de connexion pour hello *DefaultFullSharedAccessSignature* hub de notification tooyour.</span><span class="sxs-lookup"><span data-stu-id="fca68-142">You can also manually add a connection string for an existing hub by adding a connection string for hello *DefaultFullSharedAccessSignature* tooyour notification hub.</span></span> <span data-ttu-id="fca68-143">Cette chaîne de connexion fournit des messages de notification toosend autorisation votre accès à la fonction.</span><span class="sxs-lookup"><span data-stu-id="fca68-143">This connection string provides your function access permission toosend notification messages.</span></span> <span data-ttu-id="fca68-144">Hello *DefaultFullSharedAccessSignature* valeur de chaîne de connexion est accessible à partir de hello **clés** bouton dans le panneau principal de hello de votre ressource de concentrateur de notification Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fca68-144">hello *DefaultFullSharedAccessSignature* connection string value can be accessed from hello **keys** button in hello main blade of your notification hub resource in hello Azure portal.</span></span> <span data-ttu-id="fca68-145">toomanually ajouter une chaîne de connexion pour votre concentrateur, hello utilisation comme suit :</span><span class="sxs-lookup"><span data-stu-id="fca68-145">toomanually add a connection string for your hub, use hello following steps:</span></span> 

1. <span data-ttu-id="fca68-146">Sur hello **fonction application** Panneau de hello portail Azure, cliquez sur **paramètres de fonction de l’application > Aller paramètres du Service tooApp**.</span><span class="sxs-lookup"><span data-stu-id="fca68-146">On hello **Function app** blade of hello Azure portal, click **Function App Settings > Go tooApp Service settings**.</span></span>
2. <span data-ttu-id="fca68-147">Bonjour **paramètres** panneau, cliquez sur **paramètres de l’Application**.</span><span class="sxs-lookup"><span data-stu-id="fca68-147">In hello **Settings** blade, click **Application Settings**.</span></span>
3. <span data-ttu-id="fca68-148">Faites défiler vers le bas toohello **paramètres de l’application** section et ajouter une entrée nommée pour *DefaultFullSharedAccessSignature* valeur votre hub de notification.</span><span class="sxs-lookup"><span data-stu-id="fca68-148">Scroll down toohello **App settings** section, and add a named entry for *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
4. <span data-ttu-id="fca68-149">Faire référence à votre application, nom de chaîne du paramètre Bonjour liaisons de sortie.</span><span class="sxs-lookup"><span data-stu-id="fca68-149">Reference your App setting string name in hello output bindings.</span></span> <span data-ttu-id="fca68-150">Similaire trop**MyHubConnectionString** utilisé dans l’exemple hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="fca68-150">Similar too**MyHubConnectionString** used in hello example above.</span></span>

## <a name="apns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="fca68-151">Notifications natives APNS avec déclencheurs de file d’attente C#</span><span class="sxs-lookup"><span data-stu-id="fca68-151">APNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="fca68-152">Cet exemple montre comment les types de toouse défini dans hello [Microsoft Azure Notification Hubs bibliothèque](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend une notification APNS native.</span><span class="sxs-lookup"><span data-stu-id="fca68-152">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend a native APNS notification.</span></span> 

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

## <a name="gcm-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="fca68-153">Notifications natives GCM avec déclencheurs de file d’attente C#</span><span class="sxs-lookup"><span data-stu-id="fca68-153">GCM native notifications with C# queue triggers</span></span>
<span data-ttu-id="fca68-154">Cet exemple montre comment les types de toouse défini dans hello [Microsoft Azure Notification Hubs bibliothèque](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend une notification GCM native.</span><span class="sxs-lookup"><span data-stu-id="fca68-154">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend a native GCM notification.</span></span> 

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

## <a name="wns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="fca68-155">Notifications natives WNS avec déclencheurs de file d’attente C#</span><span class="sxs-lookup"><span data-stu-id="fca68-155">WNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="fca68-156">Cet exemple montre comment les types de toouse défini dans hello [Microsoft Azure Notification Hubs bibliothèque](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend un WNS native de notification toast.</span><span class="sxs-lookup"><span data-stu-id="fca68-156">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend a native WNS toast notification.</span></span> 

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

## <a name="template-example-for-nodejs-timer-triggers"></a><span data-ttu-id="fca68-157">Exemple de modèle pour les déclencheurs de minuteur Node.js</span><span class="sxs-lookup"><span data-stu-id="fca68-157">Template example for Node.js timer triggers</span></span>
<span data-ttu-id="fca68-158">Cet exemple envoie une notification pour une [inscription de modèles](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) contenant `location` et `message`.</span><span class="sxs-lookup"><span data-stu-id="fca68-158">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

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

## <a name="template-example-for-f-timer-triggers"></a><span data-ttu-id="fca68-159">Exemple de modèle pour les déclencheurs de minuteur F#</span><span class="sxs-lookup"><span data-stu-id="fca68-159">Template example for F# timer triggers</span></span>
<span data-ttu-id="fca68-160">Cet exemple envoie une notification pour une [inscription de modèles](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) contenant `location` et `message`.</span><span class="sxs-lookup"><span data-stu-id="fca68-160">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a><span data-ttu-id="fca68-161">Exemple de modèle utilisant un paramètre de sortie</span><span class="sxs-lookup"><span data-stu-id="fca68-161">Template example using an out parameter</span></span>
<span data-ttu-id="fca68-162">Cet exemple envoie une notification un [inscription de modèle](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) qui contient un `message` espace réservé dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="fca68-162">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in hello template.</span></span>

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

## <a name="template-example-with-asynchronous-function"></a><span data-ttu-id="fca68-163">Exemple de modèle avec fonction asynchrone</span><span class="sxs-lookup"><span data-stu-id="fca68-163">Template example with asynchronous function</span></span>
<span data-ttu-id="fca68-164">Si vous utilisez du code asynchrone, les paramètres de sortie ne sont pas autorisés.</span><span class="sxs-lookup"><span data-stu-id="fca68-164">If you are using asynchronous code, out parameters are not allowed.</span></span> <span data-ttu-id="fca68-165">Dans ce cas utiliser `IAsyncCollector` tooreturn votre notification de modèle.</span><span class="sxs-lookup"><span data-stu-id="fca68-165">In this case use `IAsyncCollector` tooreturn your template notification.</span></span> <span data-ttu-id="fca68-166">Hello de code suivant est un exemple asynchrone de code hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="fca68-166">hello following code is an asynchronous example of hello code above.</span></span> 

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

## <a name="template-example-using-json"></a><span data-ttu-id="fca68-167">Exemple de modèle utilisant JSON</span><span class="sxs-lookup"><span data-stu-id="fca68-167">Template example using JSON</span></span>
<span data-ttu-id="fca68-168">Cet exemple envoie une notification un [inscription de modèle](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) qui contient un `message` espace réservé dans le modèle hello à l’aide d’une chaîne JSON valide.</span><span class="sxs-lookup"><span data-stu-id="fca68-168">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in hello template using a valid JSON string.</span></span>

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a><span data-ttu-id="fca68-169">Exemple de modèle utilisant des types de bibliothèques de Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="fca68-169">Template example using Notification Hubs library types</span></span>
<span data-ttu-id="fca68-170">Cet exemple montre comment les types de toouse défini dans hello [Microsoft Azure Notification Hubs bibliothèque](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="fca68-170">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="fca68-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fca68-171">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

