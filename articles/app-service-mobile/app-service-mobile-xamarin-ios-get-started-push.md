---
title: "Ajouter des notifications Push à votre application Xamarin.iOS à l’aide d’Azure App Service"
description: "Découvrez comment utiliser Azure App Service pour envoyer des notifications Push à votre application Xamarin.iOS."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 2921214a-49f8-45e1-a306-a85ce21defca
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: bf922e49c4c92d0065817a5dd6c7d10a04737304
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinios-app"></a><span data-ttu-id="bb2d6-103">Ajouter des notifications Push à votre application Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="bb2d6-103">Add push notifications to your Xamarin.iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="bb2d6-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="bb2d6-104">Overview</span></span>
<span data-ttu-id="bb2d6-105">Dans ce didacticiel, vous ajoutez des notifications Push au projet [Démarrage rapide Xamarin.iOS](app-service-mobile-xamarin-ios-get-started.md) afin qu'une notification Push soit envoyée chaque fois qu'un enregistrement est inséré.</span><span class="sxs-lookup"><span data-stu-id="bb2d6-105">In this tutorial, you add push notifications to the [Xamarin.iOS quick start](app-service-mobile-xamarin-ios-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="bb2d6-106">Si vous n’utilisez pas le projet de serveur du démarrage rapide téléchargé, vous devrez ajouter le package d’extension de notification Push.</span><span class="sxs-lookup"><span data-stu-id="bb2d6-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="bb2d6-107">Consultez [Fonctionnement avec le Kit de développement logiciel (SDK) du serveur principal .NET pour Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="bb2d6-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb2d6-108">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="bb2d6-108">Prerequisites</span></span>
* <span data-ttu-id="bb2d6-109">Terminez le [didacticiel de démarrage rapide Xamarin.iOS](app-service-mobile-xamarin-ios-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="bb2d6-109">Complete the [Xamarin.iOS quickstart](app-service-mobile-xamarin-ios-get-started.md) tutorial.</span></span>
* <span data-ttu-id="bb2d6-110">Un appareil iOS physique.</span><span class="sxs-lookup"><span data-stu-id="bb2d6-110">A physical iOS device.</span></span> <span data-ttu-id="bb2d6-111">Les notifications Push ne sont pas prises en charge par le simulateur iOS.</span><span class="sxs-lookup"><span data-stu-id="bb2d6-111">Push notifications are not supported by the iOS simulator.</span></span>

## <a name="register-the-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="bb2d6-112">Inscrire l'application pour les notifications push dans le portail de développeurs d'Apple</span><span class="sxs-lookup"><span data-stu-id="bb2d6-112">Register the app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-to-send-push-notifications"></a><span data-ttu-id="bb2d6-113">Configuration de votre application mobile pour l'envoi de notifications push</span><span class="sxs-lookup"><span data-stu-id="bb2d6-113">Configure your Mobile App to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-the-server-project-to-send-push-notifications"></a><span data-ttu-id="bb2d6-114">Mettre à jour le projet de serveur pour l'envoi de notifications Push</span><span class="sxs-lookup"><span data-stu-id="bb2d6-114">Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a><span data-ttu-id="bb2d6-115">Configurer votre projet Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="bb2d6-115">Configure your Xamarin.iOS project</span></span>
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-to-your-app"></a><span data-ttu-id="bb2d6-116">Ajout de notifications Push à votre application</span><span class="sxs-lookup"><span data-stu-id="bb2d6-116">Add push notifications to your app</span></span>
1. <span data-ttu-id="bb2d6-117">Dans **QSTodoService**, ajoutez la propriété suivante pour qu’**AppDelegate** puisse acquérir le client mobile :</span><span class="sxs-lookup"><span data-stu-id="bb2d6-117">In **QSTodoService**, add the following property so that **AppDelegate** can acquire the mobile client:</span></span>
   
            public MobileServiceClient GetClient {
            get
            {
                return client;
            }
            private set
            {
                client = value;
            }
        }
2. <span data-ttu-id="bb2d6-118">Ajoutez l’instruction `using` suivante au début du fichier **AppDelegate.cs** .</span><span class="sxs-lookup"><span data-stu-id="bb2d6-118">Add the following `using` statement to the top of the **AppDelegate.cs** file.</span></span>
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. <span data-ttu-id="bb2d6-119">Dans **AppDelegate**, remplacez l'événement **FinishedLaunching** :</span><span class="sxs-lookup"><span data-stu-id="bb2d6-119">In **AppDelegate**, override the **FinishedLaunching** event:</span></span>
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            // registers for push for iOS8
            var settings = UIUserNotificationSettings.GetSettingsForTypes(
                UIUserNotificationType.Alert
                | UIUserNotificationType.Badge
                | UIUserNotificationType.Sound,
                new NSSet());
   
            UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications();
   
            return true;
        }
4. <span data-ttu-id="bb2d6-120">Dans le même fichier, remplacez l’événement **RegisteredForRemoteNotifications** .</span><span class="sxs-lookup"><span data-stu-id="bb2d6-120">In the same file, override the **RegisteredForRemoteNotifications** event.</span></span> <span data-ttu-id="bb2d6-121">Dans ce code, vous inscrivez une notification de modèle simple qui sera envoyée sur toutes les plateformes prises en charge par le serveur.</span><span class="sxs-lookup"><span data-stu-id="bb2d6-121">In this code you are registering for a simple template notification that will be sent across all supported platforms by the server.</span></span>
   
    <span data-ttu-id="bb2d6-122">Pour plus d’informations sur les modèles avec Notification Hubs, consultez [Modèles](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="bb2d6-122">For more information on templates with Notification Hubs, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>

        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            MobileServiceClient client = QSTodoService.DefaultService.GetClient;

            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyAPNS}
            };

            // Register for push with your mobile app
            var push = client.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }


1. <span data-ttu-id="bb2d6-123">Ensuite, remplacez l’événement **DidReceivedRemoteNotification** :</span><span class="sxs-lookup"><span data-stu-id="bb2d6-123">Then, override the **DidReceivedRemoteNotification** event:</span></span>
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;
   
            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps [new NSString("alert")] as NSString).ToString();
   
            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

<span data-ttu-id="bb2d6-124">L’application est mise à jour et prend en charge les notifications Push.</span><span class="sxs-lookup"><span data-stu-id="bb2d6-124">Your app is now updated to support push notifications.</span></span>

## <span data-ttu-id="bb2d6-125"><a name="test"></a>Tester les notifications push dans votre application</span><span class="sxs-lookup"><span data-stu-id="bb2d6-125"><a name="test"></a>Test push notifications in your app</span></span>
1. <span data-ttu-id="bb2d6-126">Appuyez sur le bouton **Démarrer** pour générer le projet, puis démarrez l’application sur un appareil compatible iOS, et enfin cliquez sur **OK** pour accepter les notifications Push.</span><span class="sxs-lookup"><span data-stu-id="bb2d6-126">Press the **Run** button to build the project and start the app in an iOS capable device, then click **OK** to accept push notifications.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bb2d6-127">Vous devez accepter explicitement les notifications Push de votre application.</span><span class="sxs-lookup"><span data-stu-id="bb2d6-127">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="bb2d6-128">Cette demande s’effectue uniquement lors du premier démarrage de l’application.</span><span class="sxs-lookup"><span data-stu-id="bb2d6-128">This request only occurs the first time that the app runs.</span></span>
   > 
   > 
2. <span data-ttu-id="bb2d6-129">Dans l’application, tapez une tâche, puis cliquez sur l’icône plus (**+**).</span><span class="sxs-lookup"><span data-stu-id="bb2d6-129">In the app, type a task, and then click the plus (**+**) icon.</span></span>
3. <span data-ttu-id="bb2d6-130">Vérifiez que vous avez reçu une notification, puis cliquez sur **OK** pour fermer celle-ci.</span><span class="sxs-lookup"><span data-stu-id="bb2d6-130">Verify that a notification is received, then click **OK** to dismiss the notification.</span></span>
4. <span data-ttu-id="bb2d6-131">Répétez l’étape 2 et fermez immédiatement l’application, puis vérifiez qu’une notification est affichée.</span><span class="sxs-lookup"><span data-stu-id="bb2d6-131">Repeat step 2 and immediately close the app, then verify that a notification is shown.</span></span>

<span data-ttu-id="bb2d6-132">Vous avez terminé ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="bb2d6-132">You have successfully completed this tutorial.</span></span>

<!-- Images. -->

<!-- URLs. -->



