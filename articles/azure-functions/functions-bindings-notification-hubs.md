---
title: Liaison Notification Hubs Azure Functions| Microsoft Docs
description: "Découvrez comment utiliser les liaisons Azure Notification Hubs dans Azure Functions."
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
ms.openlocfilehash: fa3d37b963c1bb6b58127b9180cd657d7b1dabcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-notification-hub-output-binding"></a><span data-ttu-id="46de4-104">Liaison de sortie Notification Hubs Azure Functions</span><span class="sxs-lookup"><span data-stu-id="46de4-104">Azure Functions Notification Hub output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="46de4-105">Cet article explique comment configurer et coder des liaisons Notification Hubs dans Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="46de4-105">This article explains how to configure and code Azure Notification Hub bindings in Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="46de4-106">Vos fonctions peuvent envoyer des notifications Push à l’aide d’un Azure Notification Hub configuré avec quelques lignes de code.</span><span class="sxs-lookup"><span data-stu-id="46de4-106">Your functions can send push notifications using a configured Azure Notification Hub with a few lines of code.</span></span> <span data-ttu-id="46de4-107">Toutefois, l’Azure Notification Hub doit être configuré pour l’infrastructure Platform Notification System (PNS) que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="46de4-107">However, the Azure Notification Hub must be configured for the Platform Notifications Services (PNS) you want to use.</span></span> <span data-ttu-id="46de4-108">Pour plus d’informations sur la configuration d’un Azure Notification Hub et sur le développement d’applications clientes qui s’inscrivent pour recevoir des notifications, voir [Prise en main de Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) en cliquant sur votre plateforme cliente cible au début de l’article.</span><span class="sxs-lookup"><span data-stu-id="46de4-108">For more information on configuring an Azure Notification Hub and developing a client applications that register to receive notifications, see [Getting started with Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) and click your target client platform at the top.</span></span>

<span data-ttu-id="46de4-109">Les notifications que vous envoyez peuvent être des notifications natives ou des notifications de modèle.</span><span class="sxs-lookup"><span data-stu-id="46de4-109">The notifications you send can be native notifications or template notifications.</span></span> <span data-ttu-id="46de4-110">Les notifications natives ciblent une plateforme de notification spécifique telle que configurée dans la propriété `platform` de la liaison de sortie.</span><span class="sxs-lookup"><span data-stu-id="46de4-110">Native notifications target a specific notification platform as configured in the `platform` property of the output binding.</span></span> <span data-ttu-id="46de4-111">Un modèle de notification peut servir à plusieurs plateformes cibles.</span><span class="sxs-lookup"><span data-stu-id="46de4-111">A template notification can be used to target multiple platforms.</span></span>   

## <a name="notification-hub-output-binding-properties"></a><span data-ttu-id="46de4-112">Propriété de liaison de sortie du hub de notification</span><span class="sxs-lookup"><span data-stu-id="46de4-112">Notification hub output binding properties</span></span>
<span data-ttu-id="46de4-113">Le fichier function.json spécifie les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="46de4-113">The function.json file provides the following properties:</span></span>

* <span data-ttu-id="46de4-114">`name` : nom de variable utilisé dans le code de fonction pour le message du hub de notification.</span><span class="sxs-lookup"><span data-stu-id="46de4-114">`name` : Variable name used in function code for the notification hub message.</span></span>
* <span data-ttu-id="46de4-115">`type` : doit être défini sur *"notificationHub"*.</span><span class="sxs-lookup"><span data-stu-id="46de4-115">`type` : must be set to *"notificationHub"*.</span></span>
* <span data-ttu-id="46de4-116">`tagExpression` : expressions de balise vous permettant de demander que les notifications soient remises à un ensemble d’appareils qui se sont inscrits pour la réception de notifications correspondant à l’expression de balise.</span><span class="sxs-lookup"><span data-stu-id="46de4-116">`tagExpression` : Tag expressions allow you to specify that notifications be delivered to a set of devices who have registered to receive notifications that match the tag expression.</span></span>  <span data-ttu-id="46de4-117">Pour plus d’informations, voir [Routage et expressions de balise](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="46de4-117">For more information, see [Routing and tag expressions](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span></span>
* <span data-ttu-id="46de4-118">`hubName` : nom de la ressource de hub de notification dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="46de4-118">`hubName` : Name of the notification hub resource in the Azure portal.</span></span>
* <span data-ttu-id="46de4-119">`connection` : cette chaîne de connexion doit correspondre à une chaîne de connexion **Paramètre d’application** définie sur la valeur *DefaultFullSharedAccessSignature* de votre hub de notification.</span><span class="sxs-lookup"><span data-stu-id="46de4-119">`connection` : This connection string must be an **Application Setting** connection string set to the *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
* <span data-ttu-id="46de4-120">`direction` : doit être défini sur *out*.</span><span class="sxs-lookup"><span data-stu-id="46de4-120">`direction` : must be set to *"out"*.</span></span> 
* <span data-ttu-id="46de4-121">`platform` : la propriété de la plateforme indique la plateforme de notification ciblée par votre notification.</span><span class="sxs-lookup"><span data-stu-id="46de4-121">`platform` : The platform property indicates the notification platform your notification targets.</span></span> <span data-ttu-id="46de4-122">Il doit s’agir de l’une des valeurs suivantes : </span><span class="sxs-lookup"><span data-stu-id="46de4-122">Must be one of the following values:</span></span>
  * <span data-ttu-id="46de4-123">Par défaut, si la propriété de la plateforme est omise dans la liaison de sortie, les notifications de modèle peuvent être utilisées pour cibler n’importe quelle plateforme configurée sur Azure Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="46de4-123">By default, if the platform property is omitted from the output binding, template notifications can be used to target any platform configured on the Azure Notification Hub.</span></span> <span data-ttu-id="46de4-124">Pour en savoir plus sur l’utilisation de modèles en général pour envoyer entre des notifications entre plusieurs plateformes avec un Azure Notification Hub, consultez la rubrique [Modèles](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="46de4-124">For more information on using templates in general to send cross platform notifications with an Azure Notification Hub, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>
  * <span data-ttu-id="46de4-125">`apns` : Apple Push Notification Service (APNS)</span><span class="sxs-lookup"><span data-stu-id="46de4-125">`apns` : Apple Push Notification Service.</span></span> <span data-ttu-id="46de4-126">Pour en savoir plus sur la configuration du hub de notification pour APNS et la réception de notifications dans une application cliente, consultez [Envoi de notifications Push vers iOS avec Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="46de4-126">For more information on configuring the notification hub for APNS and receiving the notification in a client app, see [Sending push notifications to iOS with Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span></span> 
  * <span data-ttu-id="46de4-127">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span><span class="sxs-lookup"><span data-stu-id="46de4-127">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span></span> <span data-ttu-id="46de4-128">Pour en savoir plus sur la configuration du hub de notification pour ADM et la réception de notifications dans une application Kindle, consultez [Prise en main de Notification Hubs pour les applications Kindle](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="46de4-128">For more information on configuring the notification hub for ADM and receiving the notification in a Kindle app, see [Getting Started with Notification Hubs for Kindle apps](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span></span> 
  * <span data-ttu-id="46de4-129">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="46de4-129">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span></span> <span data-ttu-id="46de4-130">Firebase Cloud Messaging, qui est la nouvelle version de GCM, est également pris en charge.</span><span class="sxs-lookup"><span data-stu-id="46de4-130">Firebase Cloud Messaging, which is the new version of GCM, is also supported.</span></span> <span data-ttu-id="46de4-131">Pour en savoir plus sur la configuration du hub de notification pour GCM/FCM et la réception de notifications dans une application cliente Android, consultez [Envoi de notifications Push vers Android avec Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="46de4-131">For more information on configuring the notification hub for GCM/FCM and receiving the notification in an Android client app, see [Sending push notifications to Android with Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span></span>
  * <span data-ttu-id="46de4-132">`wns` : [services de notification push Windows](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) ciblant les plateformes Windows.</span><span class="sxs-lookup"><span data-stu-id="46de4-132">`wns` : [Windows Push Notification Services](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) targeting Windows platforms.</span></span> <span data-ttu-id="46de4-133">Windows Phone 8.1 et les versions ultérieures sont est également prises en charge par WNS.</span><span class="sxs-lookup"><span data-stu-id="46de4-133">Windows Phone 8.1 and later is also supported by WNS.</span></span> <span data-ttu-id="46de4-134">Pour en savoir plus sur la configuration du hub de notification pour WNS et la réception de notifications dans une application Universal Windows Platform (UWP), consultez [Prise en main de Notification Hubs pour les applications de plateforme Windows universelle](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="46de4-134">For more information on configuring the notification hub for WNS and receiving the notification in a Universal Windows Platform (UWP) app, see [Getting started with Notification Hubs for Windows Universal Platform Apps](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span></span>
  * <span data-ttu-id="46de4-135">`mpns` : [service de notifications Push Microsoft](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span><span class="sxs-lookup"><span data-stu-id="46de4-135">`mpns` : [Microsoft Push Notification Service](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span></span> <span data-ttu-id="46de4-136">Cette plateforme prend en charge Windows Phone 8 et les plateformes antérieures de Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="46de4-136">This platform supports Windows Phone 8 and earlier Windows Phone platforms.</span></span> <span data-ttu-id="46de4-137">Pour en savoir plus sur la configuration du hub de notification pour MPNS et la réception de notifications dans une application Windows Phone, consultez [Envoi de notifications Push avec Azure Notification Hubs sur Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span><span class="sxs-lookup"><span data-stu-id="46de4-137">For more information on configuring the notification hub for MPNS and receiving the notification in a Windows Phone app, see [Sending push notifications with Azure Notification Hubs on Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span></span>

<span data-ttu-id="46de4-138">Exemple de fichier function.json :</span><span class="sxs-lookup"><span data-stu-id="46de4-138">Example function.json:</span></span>

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

## <a name="notification-hub-connection-string-setup"></a><span data-ttu-id="46de4-139">Configuration de la chaîne de connexion du hub de notification</span><span class="sxs-lookup"><span data-stu-id="46de4-139">Notification hub connection string setup</span></span>
<span data-ttu-id="46de4-140">Pour utiliser une liaison de sortie de hub de notification, vous devez configurer la chaîne de connexion pour le hub.</span><span class="sxs-lookup"><span data-stu-id="46de4-140">To use a Notification hub output binding, you must configure the connection string for the hub.</span></span> <span data-ttu-id="46de4-141">Vous pouvez effectuer cette opération dans l’onglet *Intégrer*. Pour cela, sélectionnez votre hub de notification ou d’en créer un.</span><span class="sxs-lookup"><span data-stu-id="46de4-141">This can be done on the *Integrate* tab by selecting your notification hub or creating a new one.</span></span> 

<span data-ttu-id="46de4-142">Vous pouvez également ajouter manuellement une chaîne de connexion pour un hub existant en ajoutant cette chaîne pour *DefaultFullSharedAccessSignature* à votre hub de notification.</span><span class="sxs-lookup"><span data-stu-id="46de4-142">You can also manually add a connection string for an existing hub by adding a connection string for the *DefaultFullSharedAccessSignature* to your notification hub.</span></span> <span data-ttu-id="46de4-143">Cette chaîne de connexion fournit l’autorisation d’accès de votre fonction pour l’envoi des messages de notification.</span><span class="sxs-lookup"><span data-stu-id="46de4-143">This connection string provides your function access permission to send notification messages.</span></span> <span data-ttu-id="46de4-144">La valeur de la chaîne de connexion *DefaultFullSharedAccessSignature* est accessible à partir du bouton **clés** dans le panneau principal de votre ressource Notification Hub, dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="46de4-144">The *DefaultFullSharedAccessSignature* connection string value can be accessed from the **keys** button in the main blade of your notification hub resource in the Azure portal.</span></span> <span data-ttu-id="46de4-145">Pour ajouter manuellement une chaîne de connexion pour votre hub, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="46de4-145">To manually add a connection string for your hub, use the following steps:</span></span> 

1. <span data-ttu-id="46de4-146">Dans le panneau **Function App** du portail Azure, cliquez sur **Paramètres Function App > Accéder aux paramètres App Service**.</span><span class="sxs-lookup"><span data-stu-id="46de4-146">On the **Function app** blade of the Azure portal, click **Function App Settings > Go to App Service settings**.</span></span>
2. <span data-ttu-id="46de4-147">Dans le panneau **Paramètres**, cliquez sur **Paramètres de l’application**.</span><span class="sxs-lookup"><span data-stu-id="46de4-147">In the **Settings** blade, click **Application Settings**.</span></span>
3. <span data-ttu-id="46de4-148">Faites défiler les éléments vers le bas jusqu’à la section **Paramètres de l’application**, puis ajoutez une entrée nommée pour la valeur *DefaultFullSharedAccessSignature* pour votre hub de notification.</span><span class="sxs-lookup"><span data-stu-id="46de4-148">Scroll down to the **App settings** section, and add a named entry for *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
4. <span data-ttu-id="46de4-149">Référencez votre nom de chaîne de paramètre de l’application dans les liaisons de sortie.</span><span class="sxs-lookup"><span data-stu-id="46de4-149">Reference your App setting string name in the output bindings.</span></span> <span data-ttu-id="46de4-150">Cette chaîne sera semblable à **MyHubConnectionString** utilisé dans l’exemple ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="46de4-150">Similar to **MyHubConnectionString** used in the example above.</span></span>

## <a name="apns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="46de4-151">Notifications natives APNS avec déclencheurs de file d’attente C#</span><span class="sxs-lookup"><span data-stu-id="46de4-151">APNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="46de4-152">Cet exemple indique comment utiliser les types définis dans la [bibliothèque Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) pour envoyer une notification APNS native.</span><span class="sxs-lookup"><span data-stu-id="46de4-152">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native APNS notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The JSON format for a native APNS notification is ...
    // { "aps": { "alert": "notification message" }}  

    log.Info($"Sending APNS notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string apnsNotificationPayload = "{\"aps\": {\"alert\": \"A new user wants to be added (" + 
                                        user.name + ")\" }}";
    log.Info($"{apnsNotificationPayload}");
    await notification.AddAsync(new AppleNotification(apnsNotificationPayload));        
}
```

## <a name="gcm-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="46de4-153">Notifications natives GCM avec déclencheurs de file d’attente C#</span><span class="sxs-lookup"><span data-stu-id="46de4-153">GCM native notifications with C# queue triggers</span></span>
<span data-ttu-id="46de4-154">Cet exemple indique comment utiliser les types définis dans la [bibliothèque Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) pour envoyer une notification GCM native.</span><span class="sxs-lookup"><span data-stu-id="46de4-154">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native GCM notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The JSON format for a native GCM notification is ...
    // { "data": { "message": "notification message" }}  

    log.Info($"Sending GCM notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string gcmNotificationPayload = "{\"data\": {\"message\": \"A new user wants to be added (" + 
                                        user.name + ")\" }}";
    log.Info($"{gcmNotificationPayload}");
    await notification.AddAsync(new GcmNotification(gcmNotificationPayload));        
}
```

## <a name="wns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="46de4-155">Notifications natives WNS avec déclencheurs de file d’attente C#</span><span class="sxs-lookup"><span data-stu-id="46de4-155">WNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="46de4-156">Cet exemple indique comment utiliser les types définis dans la [bibliothèque Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) pour envoyer une notification toast WNS native.</span><span class="sxs-lookup"><span data-stu-id="46de4-156">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native WNS toast notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The XML format for a native WNS toast notification is ...
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
                                            "A new user wants to be added (" + user.name + ")" + 
                                        "</text>" +
                                    "</binding></visual></toast>";

    log.Info($"{wnsNotificationPayload}");
    await notification.AddAsync(new WindowsNotification(wnsNotificationPayload));        
}
```

## <a name="template-example-for-nodejs-timer-triggers"></a><span data-ttu-id="46de4-157">Exemple de modèle pour les déclencheurs de minuteur Node.js</span><span class="sxs-lookup"><span data-stu-id="46de4-157">Template example for Node.js timer triggers</span></span>
<span data-ttu-id="46de4-158">Cet exemple envoie une notification pour une [inscription de modèles](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) contenant `location` et `message`.</span><span class="sxs-lookup"><span data-stu-id="46de4-158">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

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

## <a name="template-example-for-f-timer-triggers"></a><span data-ttu-id="46de4-159">Exemple de modèle pour les déclencheurs de minuteur F#</span><span class="sxs-lookup"><span data-stu-id="46de4-159">Template example for F# timer triggers</span></span>
<span data-ttu-id="46de4-160">Cet exemple envoie une notification pour une [inscription de modèles](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) contenant `location` et `message`.</span><span class="sxs-lookup"><span data-stu-id="46de4-160">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a><span data-ttu-id="46de4-161">Exemple de modèle utilisant un paramètre de sortie</span><span class="sxs-lookup"><span data-stu-id="46de4-161">Template example using an out parameter</span></span>
<span data-ttu-id="46de4-162">Cet exemple envoie une notification pour une [inscription de modèles](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) contenant un emplacement réservé `message` dans le modèle.</span><span class="sxs-lookup"><span data-stu-id="46de4-162">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in the template.</span></span>

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

## <a name="template-example-with-asynchronous-function"></a><span data-ttu-id="46de4-163">Exemple de modèle avec fonction asynchrone</span><span class="sxs-lookup"><span data-stu-id="46de4-163">Template example with asynchronous function</span></span>
<span data-ttu-id="46de4-164">Si vous utilisez du code asynchrone, les paramètres de sortie ne sont pas autorisés.</span><span class="sxs-lookup"><span data-stu-id="46de4-164">If you are using asynchronous code, out parameters are not allowed.</span></span> <span data-ttu-id="46de4-165">Dans ce cas, utilisez `IAsyncCollector` pour renvoyer votre notification modèle.</span><span class="sxs-lookup"><span data-stu-id="46de4-165">In this case use `IAsyncCollector` to return your template notification.</span></span> <span data-ttu-id="46de4-166">Le code suivant est un exemple de code asynchrone ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="46de4-166">The following code is an asynchronous example of the code above.</span></span> 

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static async Task Run(string myQueueItem, IAsyncCollector<IDictionary<string,string>> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    log.Info($"Sending Template Notification to Notification Hub");
    await notification.AddAsync(GetTemplateProperties(myQueueItem));    
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["user"] = "A new user wants to be added : " + message;
    return templateProperties;
}
```

## <a name="template-example-using-json"></a><span data-ttu-id="46de4-167">Exemple de modèle utilisant JSON</span><span class="sxs-lookup"><span data-stu-id="46de4-167">Template example using JSON</span></span>
<span data-ttu-id="46de4-168">Cet exemple envoie une notification pour une [inscription de modèles](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) contenant un emplacement réservé `message` dans le modèle à l’aide d’une chaîne JSON valide.</span><span class="sxs-lookup"><span data-stu-id="46de4-168">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in the template using a valid JSON string.</span></span>

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a><span data-ttu-id="46de4-169">Exemple de modèle utilisant des types de bibliothèques de Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="46de4-169">Template example using Notification Hubs library types</span></span>
<span data-ttu-id="46de4-170">Cet exemple indique comment utiliser le type défini dans la [bibliothèque Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="46de4-170">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="46de4-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="46de4-171">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

